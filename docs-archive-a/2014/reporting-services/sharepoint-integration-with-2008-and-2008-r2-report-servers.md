---
title: SharePoint 與2008和 2008 R2 報表伺服器的整合 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d9f51c37-b071-45d0-baec-f82fa6db366f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0b12429a520a674f4bc3ec7626bb3885fc33c814
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687421"
---
# <a name="sharepoint-integration-with-2008-and-2008-r2--report-servers"></a>與 2008 及 2008 R2 報表伺服器的 SharePoint 整合
   的  版本引進了一種架構，其中 SharePoint 模式現在是以 SharePoint 共用服務為基礎。 新功能的管理是在 SharePoint 管理中心的 [**管理服務**] 和 [**管理員服務應用程式**] 頁面上完成。 Sharepoint [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2010 產品的增益集仍然支援 Sharepoint 整合的先前架構， [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 因此您可以將 sharepoint 2010 與舊版的報表伺服器整合。  
  
 您可在下列位置找到用來管理舊有架構的 SharePoint 管理中心頁面：  
  
1.  從 SharePoint 管理中心，按一下 **[一般應用程式設定**]。  
  
2.  ** (2008 和 2008 R2 的群組 SQL Server Reporting Services) **包含舊版架構的連結和管理頁面  
  
## <a name="server-integration-architecture"></a>伺服器整合架構  
 將報表伺服器與 SharePoint 產品的執行個體整合時，項目和屬性會儲存在 SharePoint 內容資料庫中。 這可以為將會影響內容的儲存、安全性和存取方式的伺服器技術之間，提供更深層級的整合。  
  
 將報表項目和屬性儲存在 SharePoint 內容資料庫中，可以讓您進行下列作業：瀏覽 SharePoint 程式庫以取得報表伺服器內容類型、使用與 SharePoint 網站上所主控之其他商務文件存取控制相同的權限層級和驗證提供者來保護項目的安全性、使用共同作業和文件管理功能來簽入及簽出報表以進行修改、使用警示以便在項目變更時獲得通知，以及在應用程式內的網頁和網站上內嵌或自訂報表檢視器 Web 組件。 如果您在 SharePoint 站台內有足夠的權限，您也可以從共用資料來源產生報表模型，並使用報表產生器來建立報表。  
  
 報表伺服器會繼續提供所有的資料處理、轉譯和傳遞， 也支援快照和報表記錄所有已排程的報表處理。 當您從 SharePoint 網站開啟報表時，報表伺服器端點會連接到報表伺服器、建立工作階段、準備報表處理作業、擷取資料、將報表合併至報表配置中，然後在報表檢視器 Web 組件中加以顯示。 當報表為開啟狀態時，您可以將其匯出為不同的應用程式格式，或藉由鑽研基礎數字或按選相關的報表，與資料進行互動。 匯出和報表互動作業都是在報表伺服器上執行。  
  
 報表伺服器會與 SharePoint 同步處理作業和資料，並追蹤所處理之檔案的相關資訊。 當您修改任何報表伺服器項目的屬性或設定時，變更會儲存在 SharePoint 資料庫中，然後再複製到可以為報表伺服器提供內部儲存的報表伺服器資料庫。  
  
## <a name="related-content"></a>相關內容  
 [在 SharePoint 中啟用報表伺服器和 Power View 整合功能](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)  
 描述如何啟動與舊版報表伺服器整合所需的報表伺服器功能。  
  
  
