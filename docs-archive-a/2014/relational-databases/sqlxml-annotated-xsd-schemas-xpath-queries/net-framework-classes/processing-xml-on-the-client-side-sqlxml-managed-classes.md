---
title: 在用戶端上處理 XML (SQLXML Managed 類別) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- processing XML on client side [SQLXML]
- client-side XML formatting
- Managed Classes [SQLXML], client-side XML formatting
- SQLXML Managed Classes, client-side XML formatting
- ClientSideXml property
ms.assetid: 5e7ecf18-66fc-49ff-bc50-83635cd7ac0b
author: rothja
ms.author: jroth
ms.openlocfilehash: fb90f7c5c823c750b64f47d0c9df9551b9f857b5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585247"
---
# <a name="processing-xml-on-the-client-side-sqlxml-managed-classes"></a>在用戶端上處理 XML (SQLXML Managed 類別)
  這個範例說明如何使用 ClientSideXml 屬性。 應用程式會在伺服器上執行預存程序。 預存程序的結果 (兩個資料行的資料列集) 會在用戶端上進行處理以產生 XML 文件。  
  
 下列 GetContacts 預存程式會傳回 AdventureWorks 資料庫之 Person 資料表中員工的**FirstName**和**LastName** 。  
  
```  
USE AdventureWorks  
CREATE PROCEDURE GetContacts @LastName varchar(20)  
AS  
SELECT FirstName, LastName  
FROM   Person.Contact  
WHERE LastName = @LastName  
Go  
```  
  
 這個 c # 應用程式會執行預存程式，並在指定 CommandText 值時指定 FOR XML AUTO 選項。 在應用程式中，SqlXmlCommand 物件的 ClientSideXml 屬性會設定為 true。 這可讓您執行預先存在的預存程序以傳回資料列集，並在用戶端上，將 XML 轉換套用到該資料列集。  
  
> [!NOTE]  
>  在程式碼中，您必須於連接字串內提供 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
    static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testParams()  
      {  
         //Stream strm;  
         SqlXmlParameter p;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.ClientSideXml = true;  
         cmd.CommandText = "EXEC GetContacts ? FOR XML NESTED";  
         p = cmd.CreateParameter();  
         p.Value = "Achong";  
         using (Stream strm = cmd.ExecuteStream())   
         {  
            using (StreamReader sr = new StreamReader(strm))  
                  {  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         return 0;  
      }  
  
public static int Main(String[] args)  
{  
    testParams();  
    return 0;  
}  
}  
```  
  
 若要測試此範例，您必須先在電腦上安裝 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework。  
  
### <a name="to-test-the-application"></a>若要測試應用程式  
  
1.  建立預存程序。  
  
2.  將此範例中提供的 C# 程式碼 (DocSample.cs) 儲存到資料夾中。 編輯該程式碼來指定適當的登入和密碼資訊。  
  
3.  編譯程式碼。 若要在命令提示字元下編譯程式碼，請使用：  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     這樣會建立可執行檔 (DocSample.exe)。  
  
4.  在命令提示字元中，執行 DocSample.exe。  
  
  
