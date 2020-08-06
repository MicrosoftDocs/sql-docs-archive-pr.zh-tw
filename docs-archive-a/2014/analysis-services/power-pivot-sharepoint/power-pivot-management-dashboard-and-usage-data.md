---
title: PowerPivot 管理儀表板和使用量資料 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 541c8b1f-c6c2-423d-a97d-65c379967e0c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 581ed571661d54b1cfe9a63224b05f4f8b0267e3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596326"
---
# <a name="powerpivot-management-dashboard-and-usage-data"></a>PowerPivot 管理儀表板和使用量資料
  PowerPivot 管理儀表板是 SharePoint 管理中心內預先定義之報表和網頁組件的集合，可讓您管理 SQL Server PowerPivot for SharePoint 部署。 管理儀表板會提供伺服器健全狀況、活頁簿活動和資料重新整理的相關資訊。 儀表板會使用 SharePoint 使用量資料收集的資料。  
  
 [先決條件](#prereq)  
  
 [儀表板區段的總覽](#items)  
  
 [開啟 PowerPivot 管理儀表板](#open)  
  
 [儀表板中的來源資料](#sourcedata)  
  
 [編輯 PowerPivot 儀表板](#edit)  
  
 [建立 PowerPivot 管理儀表板中的自訂報表](#reports)  
  
##  <a name="prerequisites"></a><a name="prereq"></a> 必要條件  
 您必須是服務管理員，才能開啟所管理 PowerPivot 服務應用程式的 PowerPivot 管理儀表板。  
  
##  <a name="overview-of-the-sections-of-the-dashboard"></a><a name="items"></a> 儀表板中各區段的概觀  
 PowerPivot 管理儀表板包含 Web 組件和向下鑽研至特定資訊類別的內嵌報表。 下列清單描述的是儀表板的每個部分：  
  
|儀表板|描述|  
|---------------|-----------------|  
|基礎結構 - 伺服器健全狀況|顯示隨時間經過的 CPU 使用量、記憶體消耗量和查詢回應時間趨勢，以便評估系統資源是已接近最大容量，或利用率極低。|  
|[動作]|包含管理中心內其他頁面的連結，包括目前的服務應用程式、服務應用程式的清單以及使用量記錄。|  
|活頁簿活動 - 圖表|報告資料存取頻率。 您可以了解每日或每週發生 PowerPivot 資料來源連接的頻率。|  
|活頁簿活動 - 清單|報告資料存取頻率。 您可以了解每日或每週發生 PowerPivot 資料來源連接的頻率。|  
|資料重新整理 - 最近的活動|報告資料重新整理的狀態，包括無法執行的工作。 此報告會提供應用程式層級的資料重新整理作業綜合檢視。 管理員一眼就能看清為整個 PowerPivot 服務應用程式所定義的資料重新整理工作數。|  
|資料重新整理 - 最近的失敗|列出未順利完成資料重新整理的 PowerPivot 活頁簿。|  
|報表|包含您可以在 Excel 中開啟的報表連結。|  
  
##  <a name="open-powerpivot-management-dashboard"></a><a name="open"></a>開啟 PowerPivot 管理儀表板  
 儀表板一次只為一個 PowerPivot 服務應用程式顯示資訊。 您可以從兩個不同的位置開啟管理儀表板。  
  
### <a name="open-the-dashboard-from-general-application-settings"></a>從一般應用程式設定開啟儀表板  
  
1.  在 [管理中心] 的 **[一般應用程式設定]** 群組中，按一下 **[PowerPivot 管理儀表板]**。  
  
2.  在主頁面上選取您要檢視作業資料的 PowerPivot 服務應用程式。  
  
### <a name="open-the-dashboard-from-a-powerpivot-service-application"></a>從 PowerPivot 服務應用程式開啟儀表板  
  
1.  在 [管理中心] 的 [**應用程式管理**] 中，按一下 [**管理服務應用程式**]。  
  
2.  按一下 PowerPivot 服務應用程式的名稱。 PowerPivot 管理儀表板就會顯示目前服務應用程式的作業資料。  
  
### <a name="change-the-current-service-application"></a>變更目前的服務應用程式。  
 若要在管理儀表板中變更目前的 PowerPivot 服務應用程式：  
  
1.  在 PowerPivot 管理儀表板的頂端，記下目前服務應用程式的名稱，例如 [**預設的 PowerPivot 服務應用程式**]。  
  
2.  在 **[動作]** 儀表板中，按一下 **[列示服務應用程式]**。  
  
3.  按一下您想要查看管理儀表板報表之 PowerPivot 服務應用程式的名稱。  
  
##  <a name="source-data-in-dashboards"></a><a name="sourcedata"></a> 儀表板中的來源資料  
 儀表板、報表和網頁組件會顯示內部資料模型的資料，而該模型會從系統和 PowerPivot 應用程式資料庫中提取資料。 內部資料模型內嵌在管理中心網站所裝載 PowerPivot 活頁簿中。 資料模型的結構是固定的。 雖然您可以使用 PowertPivot 活頁簿做為資料來源建立新報表，但是不得以任何方式修改結構而中斷了使用該來源的預先定義報表。  
  
 如需有關如何收集資料的詳細資訊，請參閱下列主題：  
  
-   [PowerPivot 使用量資料收集](power-pivot-usage-data-collection.md)  
  
-   [設定 &#40;PowerPivot for SharePoint 的使用量資料收集](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
 若要擷取 PowerPivot 伺服器系統的相關資料，請確認已針對每個 PowerPivot 服務應用程式啟用事件訊息、資料重新整理記錄和其他使用量記錄。 一般伺服器作業期間所蒐集的伺服器與使用量資料就是來源資料，最後會送入內部資料模型中。 **注意** ：如果關閉事件或使用量記錄，綜合報表會不完整或發生錯誤。  
  
##  <a name="edit-powerpivot-dashboard"></a><a name="edit"></a>編輯 PowerPivot 儀表板  
 如果您擁有開發或自訂儀表板的專業技術，可以編輯儀表板以包含新的網頁組件。 您也可以編輯包含於儀表板中的網頁組件屬性。  
  
##  <a name="create-custom-reports-for-powerpivot-management-dashboard"></a><a name="reports"></a>建立 PowerPivot 管理儀表板的自訂報表  
 基於報表用途，PowerPivot 使用量資料與記錄會保留在與儀表板一起建立和設定的內部 PowerPivot 活頁簿中。 如果預設報表沒有提供您所需要的資訊，可以在 Excel 中，根據活頁簿建立自訂報表。 如果您稍後升級或解除安裝 PowerPivot 方案檔，您所建立的活頁簿和所有自訂報表都會保留下來。 這些活頁簿和報表會儲存在管理中心網站內的 PowerPivot 管理庫中。 預設看不到這個管理庫，但是您可以使用 [網站動作] 底下的 [檢視所有網站內容] 動作檢視此管理庫。  
  
 為了協助您開始使用自訂報表，PowerPivot 管理儀表板會提供 Office 資料連線 (.odc) 檔案以連線到來源活頁簿。 例如，您可以在 Excel 中使用 .odc 檔案來建立其他報表。  
  
> [!NOTE]  
>  當您嘗試在 Excel 中使用 .odc 檔案時，請編輯該檔案以防止下列錯誤：「初始化資料來源失敗」。 自動產生的 .odc 檔案包含 MSOLAP OLE DB 提供者不支援的參數。 下列指示提供移除參數的因應措施。  
  
 您必須是伺服陣列或服務管理員，才能根據管理中心的 PowerPivot 活頁簿建立報表。  
  
1.  開啟 PowerPivot 管理儀表板。  
  
2.  捲動到頁面底部的 **[報表]** 區段。  
  
3.  按一下 **[PowerPivot 管理資料]**。  
  
4.  將 .odc 檔案儲存至本機資料夾。  
  
5.  在文字編輯器中開啟 .odc 檔。  
  
6.  在 `<odc:ConnectionString>` 元素中，捲動至行尾並移除 `Embedded Data=False`，然後移除 `Edit Mode=0`。 如果字串中的最後一個字元是分號，請將它移除。  
  
7.  儲存檔案。 其餘步驟取決於您所使用的 PowerPivot 與 Excel 版本。  
  
8.  1.  啟動 Excel 2013。  
  
    2.  在 **[PowerPivot]** 功能區中，按一下 **[管理]**。  
  
    3.  按一下 **[取得外部資料]** ，然後按一下 **[現有連接]**。  
  
    4.  如果您看到 .ODC 檔案，請按一下該檔案。 如果您看不到 .ODC 檔案，請按一下 **[瀏覽其他]** ，然後在檔案路徑中，指定 .odc 檔案。  
  
    5.  按一下 [**開啟**]  
  
    6.  按一下 **[測試連接]** 確認連接是否成功。  
  
    7.  輸入連接的名稱，然後按 **[下一步]**。  
  
    8.  在 [指定 MDX 查詢] 中，按一下 [**設計**] 開啟 MDX 查詢設計工具，以組合您要使用的資料，**如果您看到錯誤訊息**「編輯模式屬性名稱的格式不正確。」，請確認您已編輯。ODC 檔案。  
  
    9. 按一下 **[確定]** ，然後按一下 **[完成]**。  
  
    10. 建立樞紐分析表或樞紐分析圖報表，將 Excel 中的資料視覺化。  
  
9. 1.  啟動 Excel 2010。  
  
    2.  按一下 [PowerPivot] 功能區上的 **[啟動 PowerPivot 視窗]**。  
  
    3.  在 PowerPivot 視窗的 [設計] 功能區中，按一下 **[現有連接]**。  
  
    4.  按一下 **[瀏覽其他]**。  
  
    5.  在檔案路徑中，指定 .odc 檔。  
  
    6.  按一下 **[開啟]** 。 「資料表匯入精靈」隨即使用包含使用方式資料之 PowerPivot 活頁簿的連接字串啟動。  
  
    7.  按一下 **[測試連接]** 確認您是否擁有存取權。  
  
    8.  為連接輸入易記的名稱，然後按 **[下一步]**。  
  
    9. 在 [指定 MDX 查詢] 中，按一下 **[設計]** 開啟 MDX 查詢設計工具以組合您要使用的資料，然後建立樞紐分析表或樞紐分析圖報表，將 Excel 中的資料視覺化。  
  
## <a name="see-also"></a>另請參閱  
 [PowerPivot 資料重新整理與 SharePoint 2010](../powerpivot-data-refresh-with-sharepoint-2010.md)   
 [設定 &#40;PowerPivot for SharePoint 的使用量資料收集](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
