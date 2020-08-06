---
title: 開始報表產生器 (報表產生器) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 28c046f5f46e1633cb108bf2d7f1803d6adc702b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598238"
---
# <a name="start-report-builder-report-builder"></a>啟動報表產生器 (報表產生器)
  [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]包含獨立和 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 版本的報表產生器。 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 版本可以搭配在原生模式或 SharePoint 整合模式下安裝的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用。  
  
> [!NOTE]  
>  報表產生器無法安裝在 Itanium 64 型電腦上。 這同樣適用於 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 和單機版本的報表產生器。  
  
 如果開啟之 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 版本的報表產生器為舊版的報表產生器，請連絡可以更新報表管理員和 SharePoint 網站的管理員來使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的報表產生器。  
  
 您也可以在已發行至 SharePoint 的 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 活頁簿上使用 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 版本的報表產生器建立報表。 如需搭配使用報表產生器的詳細資訊 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ，請參閱在 technet.microsoft.com 上[使用 PowerPivot 資料建立 Reporting Services 報表](https://go.microsoft.com/fwlink/?LinkId=185238)。  
  
 若要從本機電腦上的 [**開始**] 功能表獨立啟動報表產生器，您或系統管理員必須先在電腦上安裝報表產生器，才能使用此工具。 安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 時不會安裝單機版本；您必須另外進行下載與安裝。 若要下載報表產生器，請參閱[Microsoft® SQL Server®2012報表產生器](https://go.microsoft.com/fwlink/?LinkId=401502)。  
  
### <a name="to-start-report-builder-clickonce-from-report-manager"></a>若要從報表管理員啟動報表產生器 ClickOnce  
  
1.  在網頁瀏覽器的網址列中，輸入報表伺服器的 URL。 根據預設，URL 為 HTTP:// \<*servername*> /reports。 報表管理員隨即開啟。  
  
2.  按一下 **[報表產生器]**。  
  
     報表產生器隨即開啟，而且您可以在報表伺服器上建立報表或開啟報表。  
  
### <a name="to-start-report-builder-clickonce-using-a-url"></a>若要使用 URL 來啟動報表產生器 ClickOnce  
  
1.  在網頁瀏覽器中，於網址列中輸入下列 URL：  
  
     HTTP:// \<servername> /reportserver/reportbuilder/ReportBuilder_3_0_0_0. 應用程式  
  
2.  按 ENTER 鍵。  
  
     報表產生器隨即開啟，而且您可以在報表伺服器上建立報表或開啟報表。  
  
### <a name="to-start-report-builder-clickonce-in-sharepoint-integrated-mode"></a>以 SharePoint 整合模式啟動報表產生器 ClickOnce  
  
1.  巡覽至包含您需要之文件庫的 SharePoint 網站。  
  
2.  開啟文件庫。  
  
3.  按一下 [文件]****。  
  
4.  在 [新增文件]**** 功能表上，按一下 [報表產生器報表]****。  
  
     報表產生器隨即開啟，而且您可以在報表伺服器上建立報表或開啟報表。  
  
     **注意**如果 [**新增檔**] 功能表未列出 [**報表產生器報表**]、[**報表產生器模型**] 和 [**報表資料來源**] 選項，則必須將其內容類型加入至 SharePoint 文件庫。 如需詳細資訊，請參閱 msdn.microsoft.com 上的《線上叢書》中的[將報表伺服器內容類型加入至程式庫 &#40;Reporting Services SharePoint 整合模式中的&#41;](../add-reporting-services-content-types-to-a-sharepoint-library.md) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](https://go.microsoft.com/fwlink/?LinkId=154888) 。  
  
### <a name="to-start-report-builder-stand-alone-from-the-start-menu"></a>若要從開始功能表獨立啟動報表產生器  
  
1.  在 [開始] 功能表上，按一下 [**所有程式**]，然後按一下 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] **報表產生器**]。  
  
2.  按一下 [報表產生器] **** 。  
  
     報表產生器隨即開啟，而且您可以建立或開啟報表。  
  
3.  若要建立新的報表，請按一下報表產生器左上角的 SQL Server 圖示，然後按一下 [新增]。  
  
4.  若要開啟儲存於您本機電腦或報表伺服器上的現有報表，請按一下左上角的 SQL Server 圖示，然後按一下 [開啟]。  
  
     如果您在現有伺服器清單中看不到報表伺服器，請關閉 [**開啟報表**] 對話方塊，然後按一下報表產生器底部的 [**連接**]，以連接到伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 中的報表產生器](report-builder-in-sql-server-2016.md)  
  
  
