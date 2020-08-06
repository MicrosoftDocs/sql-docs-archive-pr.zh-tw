---
title: 自訂組件中的判斷提示權限 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- secure calls [Reporting Services]
- custom assemblies [Reporting Services], permissions
- permission sets [Reporting Services]
- asserting permissions
- permissions [Reporting Services], custom assemblies
- limited permission sets
- security configuration files [Reporting Services]
ms.assetid: 3afb9631-f15e-405e-990b-ee102828f298
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cba3c0b74712b6b4d0f6b5c58925cfd562f0df77
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584286"
---
# <a name="asserting-permissions-in-custom-assemblies"></a>自訂組件中的判斷提示權限
  根據預設，自訂組譯碼會使用有限的 **Execution** 權限集合執行。 在某些情況下，您可能希望實作自訂組件，以安全地呼叫在安全性系統中受保護的資源 (例如檔案或是登錄)。 若要完成這個動作，您必須執行下列項目：  
  
1.  識別您程式碼所需的完整權限，以進行安全的呼叫。 如果這個方法是程式庫的一部分 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ，這項資訊應該包含在方法檔中。  
  
2.  修改報表伺服器原則組態檔，以授與自訂組件所需的權限。 如需安全性原則設定檔的詳細資訊，請參閱[使用 Reporting Services 安全性原則檔](../extensions/secure-development/using-reporting-services-security-policy-files.md)。  
  
3.  判斷提示所需的權限，做為進行安全呼叫的方法之一部分。 這是必要的動作，因為報表伺服器所呼叫的自訂組譯碼是報表運算式主機組件的一部分，報表運算式主機組件預設會以 **Execution** 權限執行。 **Execution** 權限集合允許執行程式碼，但不允許使用受保護的資源。  
  
4.  如果使用強式名稱簽署自訂組件，請將它標示為 **AllowPartiallyTrustedCallersAttribute**。 這是必要的動作，因為自訂組件是從報表運算式中呼叫，而報表運算式是報表運算式主機組件的一部分，所以預設不會授與 **FullTrust**，因此它屬於「部分信任的」呼叫端。 如需詳細資訊，請參閱[使用強式名稱自訂組件](using-strong-named-custom-assemblies.md)。  
  
## <a name="implementing-a-secure-call"></a>實作安全呼叫  
 您可以修改原則組態檔，以授與組件特定權限。 例如，如果您正在撰寫用來進行貨幣轉換的自訂組件，可能需要從檔案讀取目前的貨幣匯率。 若要擷取匯率資訊，您需要將額外的安全性權限 **FileIOPermission** 新增至組件的權限集合。 您可以在原則組態檔中建立下列其他項目：  
  
```  
<PermissionSet class="NamedPermissionSet"  
   version="1"  
   Name="CurrencyRatesFilePermissionSet"  
   Description="A special permission set that grants read access to my currency rates file.">  
      <IPermission class="FileIOPermission"  
         version="1"  
         Read="C:\CurrencyRates.xml"/>  
      <IPermission class="SecurityPermission"  
         version="1"  
         Flags="Execution, Assertion"/>  
</PermissionSet>  
```  
  
 然後，您可以加入參考該權限集合的程式碼群組：  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="CurrencyRatesFilePermissionSet"  
   Name="MyNewCodeGroup"  
   Description="A special code group for my custom assembly.">  
   <IMembershipCondition class="UrlMembershipCondition"  
      version="1"  
      Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\MSSQL\Reporting Services\ReportServer\bin\CurrencyConversion.dll"/>  
</CodeGroup>  
```  
  
 為了讓您的程式碼取得適當的權限，必須在自訂組件程式碼中判斷提示權限。 例如，如果您想要將唯讀存取權加入 XML 檔案 C:\CurrencyRates.xml 中，必須將下列程式碼加入您的方法：  
  
```  
// C#  
FileIOPermission permission = new FileIOPermission(FileIOPermissionAccess.Read, @"C:\CurrencyRates.xml");  
try  
{  
   permission.Assert();  
   // Load the XML currency rates file  
   XmlDocument doc = new XmlDocument();  
   doc.Load(@"C:\CurrencyRates.xml");  
...  
```  
  
 您也可以加入判斷提示，將其做為方法屬性：  
  
```  
[FileIOPermissionAttribute(SecurityAction.Assert, Read=@"C:\CurrencyRates.xml")]  
```  
  
 如需詳細資訊，請參閱＜.NET Framework 開發人員指南＞中的＜.NET Framework 安全性＞。  
  
## <a name="see-also"></a>另請參閱  
 [將自訂組件與報表搭配使用](using-custom-assemblies-with-reports.md)  
  
  
