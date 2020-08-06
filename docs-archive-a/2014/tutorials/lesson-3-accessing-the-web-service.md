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
# <a name="lesson-3-accessing-the-web-service"></a><span data-ttu-id="945ef-102">第 3 課：存取 Web 服務</span><span class="sxs-lookup"><span data-stu-id="945ef-102">Lesson 3: Accessing the Web Service</span></span>
  <span data-ttu-id="945ef-103">將報表伺服器 Web 服務的參考加入專案後，下一步就是建立 Web 服務之 Proxy 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="945ef-103">After you add a reference for the Report Server Web service to your project, the next step is to create an instance of the Web service's proxy class.</span></span> <span data-ttu-id="945ef-104">然後您可以藉由呼叫 Proxy 類別中的方法來存取 Web 服務的方法。</span><span class="sxs-lookup"><span data-stu-id="945ef-104">You can then access the methods of the Web service by calling the methods in the proxy class.</span></span> <span data-ttu-id="945ef-105">當您的應用程式呼叫這些方法時， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 產生的 Proxy 類別程式碼會處理應用程式與 Web 服務之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="945ef-105">When your application calls these methods, the proxy class code generated by [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] handles the communications between your application and the Web service.</span></span>  
  
 <span data-ttu-id="945ef-106">首先，您要建立 Web 服務之 Proxy 類別的執行個體 <xref:ReportService2010.ReportingService2010>。</span><span class="sxs-lookup"><span data-stu-id="945ef-106">First, you will create an instance of the Web service's proxy class, <xref:ReportService2010.ReportingService2010>.</span></span> <span data-ttu-id="945ef-107">下一步，您要使用 Proxy 類別來呼叫 Web 服務的 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="945ef-107">Next, you will make a call to the Web service's <xref:ReportService2010.ReportingService2010.GetProperties%2A> method using the proxy class.</span></span> <span data-ttu-id="945ef-108">您要使用此呼叫來擷取範例報表「公司銷售」的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="945ef-108">You will use the call to retrieve the name and description of one of the sample reports, Company Sales.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="945ef-109">當您存取在 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services 上執行的 Web 服務時，必須將 "$SQLExpress" 附加至 "ReportServer" 路徑。</span><span class="sxs-lookup"><span data-stu-id="945ef-109">When accessing a Web service running on [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services, you must append "$SQLExpress" to the "ReportServer" path.</span></span> <span data-ttu-id="945ef-110">例如：</span><span class="sxs-lookup"><span data-stu-id="945ef-110">For example:</span></span>  
>   
>  `http://<Server Name>/reportserver$sqlexpress/reportservice2010.asmx"`  
  
### <a name="to-access-the-web-service"></a><span data-ttu-id="945ef-111">若要存取 Web 服務</span><span class="sxs-lookup"><span data-stu-id="945ef-111">To access the Web service</span></span>  
  
1.  <span data-ttu-id="945ef-112">您必須先將 `using` ([!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 中的 `Imports`) 指示詞加入至程式碼檔案，藉以將命名空間加入至 Program.cs 檔案 ([!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 中的 Module1.vb)。</span><span class="sxs-lookup"><span data-stu-id="945ef-112">You must first add the namespace to the Program.cs file (Module1.vb in [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) by adding a `using` (`Imports` in [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) directive to the code file.</span></span> <span data-ttu-id="945ef-113">如果您使用這個指示詞，就不需要完全符合命名空間的類型。</span><span class="sxs-lookup"><span data-stu-id="945ef-113">If you use this directive, you do not need to fully qualify the types in the namespace.</span></span>  
  
2.  <span data-ttu-id="945ef-114">若要完成這個步驟，請在您的程式碼檔案開頭中加入以下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="945ef-114">To do this, add the following code to the beginning of your code file:</span></span>  
  
    ```vb  
    Imports System  
    Imports GetPropertiesSample.ReportService2010  
    ```  
  
    ```csharp  
    using System;  
    using GetPropertiesSample.ReportService2010;  
    ```  
  
3.  <span data-ttu-id="945ef-115">當您在程式碼檔案中輸入命名空間指示詞之後，請在主控台應用程式的主要方法中輸入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="945ef-115">Once you have entered the namespace directive to your code file, enter the following code in the Main method of your console application.</span></span> <span data-ttu-id="945ef-116">在設定 Web 服務執行個體的 **Url** 屬性時，請務必變更伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="945ef-116">Make sure to change the name of your server when setting the **Url** property of the web service instance:</span></span>  
  
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
  
4.  <span data-ttu-id="945ef-117">儲存方案。</span><span class="sxs-lookup"><span data-stu-id="945ef-117">Save the solution.</span></span>  
  
 <span data-ttu-id="945ef-118">逐步解說範例程式碼會使用 Web 服務的 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法來擷取範例報表 Company Sales 2012 的屬性。</span><span class="sxs-lookup"><span data-stu-id="945ef-118">The walkthrough sample code uses the <xref:ReportService2010.ReportingService2010.GetProperties%2A> method of the Web service to retrieve properties of the sample report, Company Sales 2012.</span></span> <span data-ttu-id="945ef-119"><xref:ReportService2010.ReportingService2010.GetProperties%2A>方法接受兩個引數：您要取得其屬性資訊的報表名稱，以及包含您想要取得其值之屬性名稱的**property []** 物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="945ef-119">The <xref:ReportService2010.ReportingService2010.GetProperties%2A> method takes two arguments: the name of the report for which you want to retrieve property information and an array of **Property[]** objects that contains the names of properties whose values you want to retrieve.</span></span> <span data-ttu-id="945ef-120">方法也會傳回**Property []** 物件的陣列，其中包含 properties 引數中指定之屬性的名稱和值。</span><span class="sxs-lookup"><span data-stu-id="945ef-120">The method also returns an array of **Property[]** objects that contains the names and values of the properties specified in the properties argument.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="945ef-121">如果您為 properties 引數提供空的**Property []** 陣列，則會傳回所有可用的屬性。</span><span class="sxs-lookup"><span data-stu-id="945ef-121">If you supply an empty **Property[]** array for the properties argument, all available properties are returned.</span></span>  
  
 <span data-ttu-id="945ef-122">在先前範例中，程式碼使用 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法來傳回範例報表 Company Sales 2012 的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="945ef-122">In the previous sample, the code uses the <xref:ReportService2010.ReportingService2010.GetProperties%2A> method to return the name and description of the sample report, Company Sales 2012.</span></span> <span data-ttu-id="945ef-123">然後程式碼會使用 `foreach` 迴圈，將屬性和值寫入主控台。</span><span class="sxs-lookup"><span data-stu-id="945ef-123">The code then uses a `foreach` loop to write the properties and values to the console.</span></span>  
  
 <span data-ttu-id="945ef-124">如需有關建立和使用報表伺服器 Web 服務之 Proxy 類別的詳細資訊，請參閱＜ [Creating the Web Service Proxy](../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md)＞。</span><span class="sxs-lookup"><span data-stu-id="945ef-124">For more information about creating and using a proxy class for the Report Server Web service, see [Creating the Web Service Proxy](../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="945ef-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="945ef-125">See Also</span></span>  
 <span data-ttu-id="945ef-126">[第4課：執行應用程式 &#40;VB-VC&#35;&#41;](../../2014/tutorials/lesson-4-running-the-application-vb-vcsharp.md) </span><span class="sxs-lookup"><span data-stu-id="945ef-126">[Lesson 4: Running the Application &#40;VB-VC&#35;&#41;](../../2014/tutorials/lesson-4-running-the-application-vb-vcsharp.md) </span></span>  
 [<span data-ttu-id="945ef-127">使用 Visual Basic 或 Visual C&#35; &#40;SSRS 教學課程來存取報表伺服器 Web 服務&#41;</span><span class="sxs-lookup"><span data-stu-id="945ef-127">Accessing the Report Server Web Service Using Visual Basic or Visual C&#35; &#40;SSRS Tutorial&#41;</span></span>](../../2014/tutorials/access-report-server-web-service-vb-vcsharp-ssrs-tutorial.md)  
  
  