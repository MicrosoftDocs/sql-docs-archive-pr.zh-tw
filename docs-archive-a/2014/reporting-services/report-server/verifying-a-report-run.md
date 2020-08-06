---
title: 驗證報表執行 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- auditing [Reporting Services]
- verifying report execution
- logs [Reporting Services], verifying report run
- report execution data [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services], verifying execution
- checking report execution
ms.assetid: 18a98f2f-6b40-454e-9b37-568ed1a96458
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c11c57f7c5f67b2557f5637ad10658abc9f80606
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595616"
---
# <a name="verifying-a-report-run"></a>驗證報表執行
  若要檢視有關報表處理的狀態資訊，您可以使用記錄檔或參考報表管理員中與報表同時顯示的狀態資訊。  
  
## <a name="sources-of-report-execution-data"></a>報表執行資料的來源  
 報表執行記錄提供有關報表執行的詳細資訊，包括報表的名稱、執行報表的使用者名稱、報表執行時間，以及用於散發報表的傳遞延伸模組。 若要檢視與分析此資料，您可以複製報表執行記錄至資料庫資料表，以便於查詢和報告。  
  
 記錄檔包含許多有關報表執行與其他伺服器活動的項目。 因為記錄檔包含的資料很多，所以如果您只想確認報表上次執行的時間，就可以使用報表管理員。 如果您需要其他資訊，就必須檢視記錄檔。  
  
> [!NOTE]  
>  報表管理員不會顯示在需要時執行之報表的處理時間。  
  
 下表描述如何檢視不同類型報表的處理日期和時間。  
  
|報表類型|日期和時間資訊的記錄位置|若要檢視資訊，請執行下列步驟|  
|-----------------------------|-----------------------------------------------|-----------------------------------------------|  
|以報表快照集形式執行的報表。|在 [內容] 頁面上。 如需詳細資訊，請參閱[內容頁面 &#40;報表管理員&#41;](../contents-page-report-manager.md)。|1) 尋找包含報表的資料夾。<br />2) 在 [詳細資料] 檢視中設定資料夾。<br />3) 3) 記下 [**執行時**] 資料行中的日期和時間。|  
|報表記錄中的快照集。|在 [記錄屬性] 頁面上。 如需詳細資訊，請參閱[快照集選項屬性頁 &#40;報表管理員&#41;](../snapshot-options-properties-page-report-manager.md)。|1) 開啟報表。<br />2) 按一下 [屬性]  頁面。<br />3) 按一下 [記錄]  索引標籤。<br />4) 記下 [執行時]  資料行中的日期和時間。|  
|快取報表。|在用於建立與重新整理快取報表的排程中。|1) 開啟報表。<br />2) 按一下 [屬性]  頁面。<br />3) 按一下 [執行]  索引標籤。<br />4) 開啟排程。|  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 記錄檔和來源](../report-server/reporting-services-log-files-and-sources.md)   
 [設定報表處理屬性](set-report-processing-properties.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)  
  
  
