---
title: 第3課：存取 Web 服務 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c3e4c198-ab35-4548-9471-1b4e6b6e5dfd
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c69e0dbe9eef987a764686bdf84e68bd8c530628
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87702205"
---
# <a name="lesson-3-accessing-the-web-service"></a>第 3 課：存取 Web 服務
  將報表伺服器 Web 服務的參考加入專案後，下一步就是建立 Web 服務之 Proxy 類別的執行個體。 然後您可以藉由呼叫 Proxy 類別中的方法來存取 Web 服務的方法。 當您的應用程式呼叫這些方法時， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 產生的 Proxy 類別程式碼會處理應用程式與 Web 服務之間的通訊。  
  
 首先，您要建立 Web 服務之 Proxy 類別的執行個體 <xref:ReportService2010.ReportingService2010>。 下一步，您要使用 Proxy 類別來呼叫 Web 服務的 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法。 您要使用此呼叫來擷取範例報表「公司銷售」的名稱和描述。  
  
> [!NOTE]  
>  當您存取在 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services 上執行的 Web 服務時，必須將 "$SQLExpress" 附加至 "ReportServer" 路徑。 例如：  
>   
>  `http://<Server Name>/reportserver$sqlexpress/reportservice2010.asmx"`  
  
### <a name="to-access-the-web-service"></a>若要存取 Web 服務  
  
1.  您必須先將 `using` ([!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 中的 `Imports`) 指示詞加入至程式碼檔案，藉以將命名空間加入至 Program.cs 檔案 ([!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 中的 Module1.vb)。 如果您使用這個指示詞，就不需要完全符合命名空間的類型。  
  
2.  若要完成這個步驟，請在您的程式碼檔案開頭中加入以下的程式碼：  
  
    ```vb  
    Imports System  
    Imports GetPropertiesSample.ReportService2010  
    ```  
  
    ```csharp  
    using System;  
    using GetPropertiesSample.ReportService2010;  
    ```  
  
3.  當您在程式碼檔案中輸入命名空間指示詞之後，請在主控台應用程式的主要方法中輸入下列程式碼。 在設定 Web 服務執行個體的 **Url** 屬性時，請務必變更伺服器的名稱。  
  
    ```vb  
    Sub Main()  
       Dim rs As New ReportingService2010  
       rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
       rs.Url = "http://<Server Name>/reportserver/reportservice2010.asmx"  
  
       Dim name As New [Property]  
       name.Name = "Name"  
  
       Dim description As New [Property]  
       description.Name = "Description"  
  
       Dim properties(1) As [Property]  
       properties(0) = name  
       properties(1) = description  
  
       Try  
          Dim returnProperties As [Property]() = rs.GetProperties( _  
             "/AdventureWorks 2012 Sample Reports/Company Sales 2012", properties)  
  
          Dim p As [Property]  
          For Each p In returnProperties  
              Console.WriteLine((p.Name + ": " + p.Value))  
          Next p  
  
       Catch e As Exception  
          Console.WriteLine(e.Message)  
       End Try  
    End Sub  
    ```  
  
    ```csharp  
    static void Main(string[] args)  
    {  
       ReportingService2010 rs = new ReportingService2010();  
       rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
       rs.Url = "http://<Server Name>/reportserver/reportservice2010.asmx";  
  
       Property name = new Property();  
       name.Name = "Name";  
  
       Property description = new Property();  
       description.Name = "Description";  
  
       Property[] properties = new Property[2];  
       properties[0] = name;  
       properties[1] = description;  
  
       try  
       {  
          Property[] returnProperties = rs.GetProperties(  
          "/AdventureWorks 2012 Sample Reports/Company Sales 2012",properties);  
  
          foreach (Property p in returnProperties)  
          {  
             Console.WriteLine(p.Name + ": " + p.Value);  
          }  
       }  
  
       catch (Exception e)  
       {  
          Console.WriteLine(e.Message);  
       }  
    }  
    ```  
  
4.  儲存方案。  
  
 逐步解說範例程式碼會使用 Web 服務的 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法來擷取範例報表 Company Sales 2012 的屬性。 <xref:ReportService2010.ReportingService2010.GetProperties%2A>方法接受兩個引數：您要取得其屬性資訊的報表名稱，以及包含您想要取得其值之屬性名稱的**property []** 物件的陣列。 方法也會傳回**Property []** 物件的陣列，其中包含 properties 引數中指定之屬性的名稱和值。  
  
> [!NOTE]  
>  如果您為 properties 引數提供空的**Property []** 陣列，則會傳回所有可用的屬性。  
  
 在先前範例中，程式碼使用 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法來傳回範例報表 Company Sales 2012 的名稱和描述。 然後程式碼會使用 `foreach` 迴圈，將屬性和值寫入主控台。  
  
 如需有關建立和使用報表伺服器 Web 服務之 Proxy 類別的詳細資訊，請參閱＜ [Creating the Web Service Proxy](../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [第4課：執行應用程式 &#40;VB-VC&#35;&#41;](../../2014/tutorials/lesson-4-running-the-application-vb-vcsharp.md)   
 [使用 Visual Basic 或 Visual C&#35; &#40;SSRS 教學課程來存取報表伺服器 Web 服務&#41;](../../2014/tutorials/access-report-server-web-service-vb-vcsharp-ssrs-tutorial.md)  
  
  
