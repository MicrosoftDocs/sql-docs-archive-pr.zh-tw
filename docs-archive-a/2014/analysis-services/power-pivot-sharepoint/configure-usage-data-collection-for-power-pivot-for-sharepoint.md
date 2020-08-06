---
title: 設定 (PowerPivot for SharePoint 的使用量資料收集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 955ca6d6-9d5b-47a4-a87c-59bd23f1bf74
author: minewiskan
ms.author: owend
ms.openlocfilehash: 90a071cf8380d1a951fcc413d659a22e7e420853
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598590"
---
# <a name="configure-usage-data-collection-for-powerpivot-for-sharepoint"></a>設定使用量資料收集的對象 (PowerPivot for SharePoint
  使用量資料收集是伺服陣列層級的 SharePoint 功能。 PowerPivot for SharePoint 會使用並擴充此系統來支援 PowerPivot 管理儀表板中的報表，以便顯示 PowerPivot 資料與服務的使用方式。 根據您安裝 SharePoint 的方式而定，可能會關閉伺服陣列的使用量資料收集。 伺服陣列管理員必須啟用使用量記錄，以建立會顯示在 PowerPivot 管理儀表板中的使用量資料。  
  
 如需有關 PowerPivot 管理儀表板中使用量資料的詳細資訊，請參閱＜ [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md)＞。  
  
 **本主題內容：**  
  
 [啟用使用量資料收集，並選擇觸發資料收集的事件](#events)  
  
 [設定記錄檔位置](#configdb)  
  
 [設定用於使用量資料收集的計時器工作](#jobs)  
  
 [限制儲存使用量資料記錄的時間長度](#confighist)  
  
 [針對報告目的而定義快速、中等及緩慢的查詢回應類別目錄](#qrh)  
  
 [指定向使用量資料收集系統報告查詢統計資料的頻率](#ttr)  
  
 [開啟 [PowerPivot 服務應用程式] 頁面以存取組態設定](#openconfig)  
  
 [PowerPivot 使用量資料收集的預設組態](#defaultconfig)  
  
> [!IMPORTANT]  
>  使用量資料讓您可深入了解使用者如何存取資料和資源，但它並不保證伺服器作業和使用者存取的資料為可靠且持續性的。 例如，如果重新啟動伺服器，則事件使用量資料將會遺失並且無法復原。 同樣地，如果暫存記錄檔到達大小上限，在清除檔案之前將不會加入任何新資料。 如果您需要稽核功能，請考慮使用 SharePoint 所提供的工作流程與內容類型功能，來為您的伺服陣列建立稽核子系統。 如需詳細資訊，請在網站上尋找產品與社群文件集。  
  
##  <a name="enable-usage-data-collection-and-choose-events-that-trigger-data-collection"></a><a name="events"></a>啟用使用量資料收集，並選擇觸發資料收集的事件  
 在 SharePoint 管理中心內設定使用量資料收集。  
  
1.  在管理中心，按一下 **[監視]**。  
  
2.  在 **[報表]** 區段中，按一下 **[設定 Usage and Health Data Collection]**。  
  
3.  選取 **[啟用使用狀況資料收集]**。  
  
4.  在 **[要記錄的事件]** 區段中，選取或清除核取方塊以啟用或停用下列 Analysis Services 事件：  
  
    |Event - 事件|描述|  
    |-----------|-----------------|  
    |**PowerPivot 連接**|PowerPivot 連接事件是用來監視以使用者身分建立的 PowerPivot 伺服器連接。|  
    |**PowerPivot 載入資料使用量**|PowerPivot 載入資料使用量是用來監視將 PowerPivot 資料載入伺服器記憶體的要求。 從內容資料庫或從快取載入的 PowerPivot 資料檔會產生載入事件。|  
    |**PowerPivot 卸載資料使用量**|PowerPivot 卸載資料使用量是用來監視在一段時間閒置後，卸載 PowerPivot 資料來源的要求。 將 PowerPivot 資料來源快取到磁碟將會報告成卸載事件。|  
    |**PowerPivot 查詢使用量**|PowerPivot 查詢使用量是用來監視在 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 執行個體中載入之資料的查詢處理時間。|  
  
    > [!NOTE]  
    >  伺服器健全狀況和資料重新整理作業也會產生使用量資料，但是沒有任何事件與這些處理序相關聯。  
  
5.  您也可以更新記錄檔位置。 如需詳細資訊，請參閱下一節。  
  
6.  按一下 [確定]  以儲存變更。  
  
7.  您可以選擇性地指定是否記錄所有的訊息或只記錄錯誤。 如需如何節流事件訊息的詳細資訊，請參閱[設定及查看 SharePoint 記錄檔和診斷記錄 &#40;PowerPivot for SharePoint&#41;](configure-and-view-sharepoint-and-diagnostic-logging.md)。  
  
##  <a name="set-log-file-location"></a><a name="configdb"></a>設定記錄檔位置  
 PowerPivot 使用量資料一開始會儲存在本機伺服器的使用量記錄檔中，然後再定期移至 PowerPivot 服務應用程式資料庫。 記錄檔位置是在管理中心內設定的。 預設位置為：  
  
 `C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\logs`  
  
 若要檢視或變更這些屬性，請使用 **[Usage and Health data collection]** 頁面。  
  
1.  在管理中心的首頁上，按一下 **[監視]**。  
  
2.  在 [監視] 區段中，按一下 **[設定使用量和健全資料收集]**。  
  
3.  在 [使用量資料收集設定] 中，檢視或修改檔案位置、名稱或檔案大小上限。 如果您指定的檔案大小太低，檔案大小將會達到上限，而且在將其內容移到中央的使用量資料收集資料庫之前，將不會再加入新的項目。  
  
##  <a name="configure-the-timer-jobs-used-in-usage-data-collection"></a><a name="jobs"></a>設定用於使用量資料收集的計時器工作  
 PowerPivot 伺服器健全狀況與使用量資料會透過兩個計時器工作，移到使用量資料收集系統中的不同位置：  
  
-   「Microsoft SharePoint Foundation 使用量資料匯入」計時器工作會將 PowerPivot 使用量移至 PowerPivot 服務應用程式資料庫。  
  
-   「PowerPivot 管理儀表板處理」計時器工作會將資料加入至 PowerPivot 活頁簿，這是內建系統管理報表的資料來源。  
  
 如果您需要更頻繁地重新整理出現在 PowerPivot 管理儀表板中的系統管理報表，請按照以下的步驟進行。  
  
1.  在管理中心，按一下 **[監視]**。  
  
2.  按一下 **[檢閱工作定義]** 在 **[計時器工作]** 區段中。  
  
3.  按一下 **[Microsoft SharePoint Foundation 使用量資料匯入]**。  
  
4.  按一下 [**立即執行**]。 如果 **[立即執行]** 按鈕已停用，請按一下 **[啟用]** ，然後按一下 **[立即執行]**。  
  
5.  在 [工作定義] 清單中，按一下 **[PowerPivot 資料管理儀表板處理計時器工作]**。  
  
6.  按一下 [**立即執行**]。  
  
7.  檢查報表以檢視重新整理資料。 如需詳細資訊，請參閱＜ [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md)＞。  
  
##  <a name="limit-how-long-usage-data-history-is-stored"></a><a name="confighist"></a>限制儲存使用量資料歷程記錄的時間長度  
 事件 (連接、載入、卸載及視需要的查詢處理) 及資料重新整理 (已排程的資料處理) 都會儲存使用量資料記錄。 雖然使用量資料是透過 SharePoint 使用量資料收集系統來收集，但是會將報表資料移到 PowerPivot 應用程式資料庫及報表資料庫，以獲得較長期的儲存。 使用量資料記錄設定會控制使用量資料在 PowerPivot 應用程式資料庫中保留的時間長度。 相同的限制會同樣地套用至相同 PowerPivot 服務應用程式資料庫中所有類型之儲存的使用量資料。  
  
1.  [開啟 PowerPivot 服務應用程式頁面](#openconfig)。  
  
2.  在 **[使用量資料收集]** 區段的 **[使用量資料記錄]** 中，輸入要為每個活頁簿記錄資料重新整理活動的天數。  
  
    -   預設值為 365 天。  
  
    -   0 指定無限制的儲存體，在此會無限期地保留使用量資料。  
  
    -   或者，您也可以指定介於 1 到 5000 之間的範圍。  
  
     將保留週期減少到較小的天數，將會刪除任何超過新限制的資料。 例如，將值從 365 變更到 30，會導致將發生在 30 天前的所有歷程記錄資訊之使用量資料刪除。 只有最近 30 天的資料才會保留。  
  
     下一個事件發生時，就會實際刪除資料。 只有在系統處理事件時，才會檢查使用量資料記錄的限制。  
  
3.  按一下 [確定]  。  
  
 如需如何收集和儲存使用量資料的詳細資訊，請參閱[PowerPivot 使用量資料收集](power-pivot-usage-data-collection.md)。  
  
##  <a name="define-fast-medium-and-slow-query-response-categories-for-reporting-purposes"></a><a name="qrh"></a>定義快速、中等和緩慢的查詢回應類別以供報告之用  
 查詢處理效能是針對預先定義的類別目錄來計算，這些類別目錄會按照完成的時間長度來定義要求-回應循環。 預先定義的類別目錄包括：「簡單式」、「快速」、「預期」、「長時間執行」及「已超過」。 PowerPivot 伺服器的每個要求都會根據完成的時間歸類到其中一個類別目錄。  
  
 查詢回應資訊是用於活動報表。 在報表中，每個類別目錄都會以不同的方式來使用，以便能更妥善地顯示 PowerPivot 系統的效能趨勢。 例如，會完全排除簡單式要求，因為這樣做，可移除資料中的雜訊，並且可使用其餘的類別來顯示更有意義的趨勢。 相反地，「長時間執行」或「已超過」要求統計資料會在報表中特別突出，以利系統管理員或活頁簿擁有者可以立即採取更正動作。  
  
 雖然您無法加入或刪除類別目錄，但是可以定義上限和下限，以決定某個類別目錄的停止處及下一個類別目錄的開始處。 如果您的組織使用服務等級協定 (SLA) 來定義伺服器可用性與效能的可接受層級，則可以微調這些類別，以反映您所建立的 SLA。  
  
1.  [開啟 PowerPivot 服務應用程式頁面](#openconfig)。  
  
2.  在 [使用量資料收集]**** 區段中的 [簡單式回應時間上限]**** 中，輸入以毫秒為單位的值，以設定完成簡單式回應時間的上限。 歸類為此類別目錄的要求通常包括伺服器 Ping、工作階段初始化及中繼資料查詢。 預設值為 500 毫秒 (或半秒)。  
  
3.  在 [快速要求上限] 中，輸入以毫秒為單位的值，以設定完成快速回應時間的上限。 歸類到此類別目錄的要求，包含非常小的資料集查詢或大型資料集的中繼資料伺服器。 預設值為 1000 毫秒 (或 1 秒)。  
  
4.  在 [預期回應時間上限]**** 中，輸入以毫秒為單位的值，以設定完成預期或平均時間範圍中回應時間的上限。 歸類到此類別的要求包括將資料載入檢視器。 預設值為 3000 毫秒 (或 3 秒)。  
  
5.  在 [長回應時間上限]**** 中，輸入以毫秒為單位的值，以設定完成長時間執行回應時間的上限。 歸類到此類別目錄的要求會比預期的執行時間還長，但仍在可接受的範圍內。 預設值為 10000 毫秒 (或 10 秒)。  
  
     任何超過此限制的要求都會被分類為 *「已超過」*。 *「已超過」* 沒有可設定的臨界值。 它會從您在 [長時間要求上限] 指定的上限來推斷。 歸類為「已超過」類別的要求，執行的時間超過您已定義的 SLA 所允許的時間。  
  
6.  按一下 [確定]  。  
  
##  <a name="specify-how-often-query-statistics-are-reported-to-the-usage-data-collection-system"></a><a name="ttr"></a>指定向使用量資料收集系統報告查詢統計資料的頻率  
 報告時間間隔指定向使用量資料收集系統報告查詢統計資料的頻率。 查詢統計資料會累積在處理序中，並定期報告為單一事件。 您可以調整間隔，以增加或減少寫入記錄檔的頻率。  
  
1.  [開啟 PowerPivot 服務應用程式頁面](#openconfig)。  
  
2.  在 [使用量資料收集]**** 區段的 [查詢報告間隔]**** 中，輸入在伺服器將向使用量資料收集系統，將所有類別目錄 (「簡單式」、「快速」、「預期」、「長時間執行」及「已超過」) 的查詢統計資料報告為單一事件之後的秒數。  
  
    -   範圍是 1 到任何的正整數。  
  
    -   預設值為 300 秒 (或 5 分鐘)。 這個值建議用於執行各種應用程式及服務的動態伺服陣列環境。  
  
     如果您將此值引發成更大的數字，則可能會在可以報告它之前，即遺失統計資料。 例如，服務重新啟動將會導致查詢統計資料遺失。 相反地，如果內建的活動報表顯示資料不足，請考慮減少間隔，以便更頻繁地取得報告時間事件。  
  
3.  按一下 [確定]  。  
  
##  <a name="open-the-powerpivot-service-application-page-to-access-configuration-settings"></a><a name="openconfig"></a>開啟 [PowerPivot 服務應用程式] 頁面以存取設定  
 您必須是伺服陣列或服務系統管理員，才能修改服務應用程式設定。 如果在伺服陣列中定義了多個 PowerPivot 服務應用程式，則必須個別修改每個服務應用程式。  
  
1.  在 [SharePoint 管理中心] 的 **[應用程式管理]** 中，按一下 **[管理服務應用程式]**。  
  
2.  尋找 PowerPivot 服務應用程式。 您可以依其類型來識別服務應用程式。 PowerPivot 服務應用程式類型為 **[PowerPivot 服務應用程式]**。  
  
3.  按一下 PowerPivot 服務應用程式名稱。 PowerPivot 管理儀表板隨即開啟。  
  
4.  在 **[動作]** 中，按一下 **[設定服務應用程式設定]**。 [PowerPivot 服務應用程式設定] 頁面隨即開啟。  
  
##  <a name="the-default-configuration-for-powerpivot-usage-data-collection"></a><a name="defaultconfig"></a>PowerPivot 使用量資料收集的預設設定  
 PowerPivot 服務作業的使用量資料收集可以用預設值來啟用，以便在支援 Analysis Services 整合功能的應用程式中可以立即使用它。 預設值包括會觸發使用量資料收集的事件，對儲存使用量資料之時間長度的限制，以及分類查詢回應時間的臨界值。  
  
 下表顯示使用量資料收集組態的預設值。  
  
|設定|預設值|類型|有效範圍|  
|-------------|-------------------|----------|-----------------|  
|**Analysis Services 使用量事件** (連接、載入、卸載、要求)|\<enabled>|Boolean|啟用或停用這些值。|  
|**查詢報告間隔**|300 (以秒為單位)|整數|1 到任何正整數。 預設值是 5 分鐘。|  
|**[使用量資料記錄]**|365 (以天為單位)|整數|0 表示無限制，但是您也可以設定歷程記錄資料到期的上限，並設成可自動刪除資料。 有限的保留週期有效值為 1 到 5000 (以天為單位)。|  
|簡單式回應時間上限|500 (以毫秒為單位)|整數|設定會定義簡單式要求-回應交換的上限。 任何介於 0 到 500 毫秒之間完成的要求都是簡單式要求，報告用途會加以忽略。|  
|快速回應時間上限|1000 (以毫秒為單位)|整數|設定會定義快速要求-回應交換的上限。|  
|預期回應時間上限|3000 (以毫秒為單位)|整數|設定會定義預期要求-回應交換的上限。|  
|長時間執行回應的上限|10000 (以毫秒為單位)|整數|設定會定義長時間執行要求-回應交換的上限。 任何超過此上限的要求，都會歸類到沒有上限臨界值的「已超過」類別目錄。|  
  
## <a name="see-also"></a>另請參閱  
 [設定參考 &#40;PowerPivot for SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [PowerPivot 使用量資料收集](power-pivot-usage-data-collection.md)  
  
  
