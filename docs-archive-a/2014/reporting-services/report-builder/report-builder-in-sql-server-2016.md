---
title: SQL Server 2014 中的報表產生器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10428"
helpviewer_keywords:
- overview of Report Builder
- getting started
ms.assetid: 55bf4f9c-d037-412f-ae57-3fc39ce32fa5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b2fb8994272eb24594239551d623021f7b87694c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592490"
---
# <a name="report-builder-in-sql-server-2014"></a>SQL Server 2014 中的報表產生器
  報表產生器是一個報表撰寫環境，適合喜歡在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Office 環境中工作的商務使用者使用。 當您設計報表時，可以指定要取得資料的位置、要取得的資料，以及要顯示資料的方式。 當您執行報表時，報表處理器會採用已指定的所有資訊、擷取資料，然後將它與報表配置結合，以便產生報表。 您可以在報表產生器中預覽報表，也可以將報表發行至報表伺服器或處於 SharePoint 整合模式的報表伺服器，讓其他人執行報表。  
  
 下圖中的報表提供一個矩陣，內含資料列和資料行群組、走勢圖、指標以及位於邊角資料格的摘要圓形圖，並附有一份地圖，地圖中具有兩組以色彩和圓形大小呈現的地理資料。  
  
 ![rs_GettingStartedReport](../media/rs-gettingstartedreport.gif "rs_GettingStartedReport")  
  
##  <a name="jump-start-report-creation"></a><a name="JumpStartReptCreation"></a>快速入門報表建立  
  
-   啟動您小組中其他人所建立的**報表 withreport 元件**。 報表組件是已個別發行至報表伺服器或與報表伺服器整合之 SharePoint 網站上的報表項目。 報表組件可以在其他報表中重複使用。 諸如資料表、矩陣、圖表和影像等報表項目都可以發行為報表組件。  
  
-   從小組中其他人所建立的**共用資料集開始**。 共用資料集是以儲存到報表伺服器或與報表伺服器整合之 SharePoint 網站上之共用資料來源做為基礎的查詢。  
  
-   **開始使用 [資料表精靈]、[矩陣精靈] 或 [圖表精靈]** 。 您可以選擇資料來源連接、拖放欄位以建立資料集查詢、選取配置和樣式，以及自訂報表。  
  
-   **開始使用 [地圖精靈]** ，以建立根據地理或幾何背景顯示彙總資料的報表。 地圖資料可能是來自 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢或環境系統研究協會 (Environmental Systems Research Institute, Inc.) 的空間資料。(ESRI) 形狀檔。 您也可以加入 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Bing 地圖底圖背景。  
  

  
##  <a name="design-your-report"></a><a name="DesignRept"></a>設計您的報表  
  
-   **建立含有資料表、矩陣、圖表和自由形式報表配置的報表。** 針對以資料行為基礎的資料建立資料表報表，針對摘要資料建立矩陣報表 (例如交叉分析或樞紐分析表報表)，針對圖形化資料建立圖表報表，以及針對其他任何內容建立任意格式的報表。 報表可以內嵌其他報表和圖表，連同動態 Web 應用程式的清單、圖形和控制項。  
  
-   **來自各種資料來源的報表。** 使用具有 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 管理的資料提供者、OLE DB 提供者或 ODBC 資料來源之任何資料來源類型中的資料建立報表。 您可以建立使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、Oracle、Hyperion 及其他資料庫中關聯式和多維度資料的報表。 您可以使用 XML 資料處理延伸模組，從任何 XML 資料來源擷取資料。 您可以使用資料表值函數來設計自訂資料來源。  
  
-   **修改現有的報表。** 藉由使用報表產生器，您可以自訂及更新在報表設計師中建立的報表 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 。  
  
-   藉由篩選、分組和排序資料，或是加入公式或運算式來**修改您的資料**。  
  
-   **加入圖表、量測計、走勢圖和指標** ，以視覺化格式摘要列出資料，並且一次展示大量的彙總資訊。  
  
-   **新增互動式功能**，例如文件引導模式、顯示/隱藏按鈕，以及子報表和鑽研報表的鑽研連結。 使用參數和篩選來篩選自訂檢視的資料。  
  
-   **內嵌或參考影像**與其他資源，包括外部內容。  
  

  
##  <a name="manage-your-report"></a><a name="ManageRpt"></a>管理您的報表  
  
-   **儲存報表的定義**至您的電腦或報表伺服器，以便您進行管理並與其他人共用。  
  
-   當您開啟報表時，或在您開啟報表之後，**選擇呈現格式**。 您可以選取 Web 導向、頁面導向和傳統型應用程式格式。 格式包括 HTML、MHTML、PDF、XML、CSV、TIFF、Word 及 Excel。  
  
-   **設定訂閱。** 當您將報表發行至報表伺服器或處於 SharePoint 整合模式的報表伺服器之後，就可以將報表設定成在特定時間執行、建立報表記錄，以及設定電子郵件訂閱。  
  
-   使用 Reporting Services Atom 轉譯延伸模組，從報表**產生資料摘要** 。  
  
> [!NOTE]  
>  報表伺服器管理員會在報表伺服器或處於 SharePoint 整合模式的報表伺服器上管理已發行的報表。 報表伺服器管理員可以定義安全性、設定屬性以及排程作業，例如報表記錄和電子郵件報表傳遞。 他們可以建立共用排程和共用資料來源，讓它們可供一般使用。 管理員也會管理所有報表伺服器資料夾。 執行管理工作的能力需視使用者權限而定。  
  

  
##  <a name="in-this-section"></a><a name="InThisSection"></a> 本節內容  
 [SQL Server 2014 報表產生器的新功能](../what-s-new-in-report-builder-for-sql-server-2014.md)  
 描述此版本報表產生器的新功能，包括地圖。  
  
 [教學課程：離線建立快速圖表報表](tutorial-create-a-quick-chart-report-offline-report-builder.md)  
 介紹報表產生器以及可協助您建立報表的精靈。 此教學課程會提供一組資料供您使用，所以您不需要連接至資料來源以便開始作業。  
  
 [規劃報表 &#40;報表產生器&#41;](../report-design/planning-a-report-report-builder.md)  
 提供有關開始建立報表之前應該考量之事項的資訊。  
  
 [報表撰寫概念 &#40;報表產生器及 SSRS&#41;](../report-design/report-authoring-concepts-report-builder-and-ssrs.md)  
 定義整個報表產生器文件集中使用的重要概念。  
  
 [報表設計檢視 &#40;報表產生器&#41;](report-design-view-report-builder.md)  
 說明報表設計檢視的不同窗格和區域。  
  
 [共用資料集設計檢視 &#40;報表產生器&#41;](shared-dataset-design-view-report-builder.md)  
 說明共用資料集設計檢視的不同窗格和區域。  
  
 [鍵盤快速鍵 &#40;報表產生器&#41;](keyboard-shortcuts-report-builder.md)  
 概述報表產生器中可用於導覽及設計報表的快速鍵。  
  
 [開始報表產生器 &#40;報表產生器&#41;](start-report-builder.md)  
 說明如何啟動兩種不同版本的報表產生器：單機版和 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 版。  
  
  
