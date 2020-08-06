---
title: 設定報表的執行屬性 (報表管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- reports [Reporting Services], properties
- reports [Reporting Services], execution options
ms.assetid: 73cc8dcc-ef80-40d7-9739-d33bba0eb28a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 51cd7b5db225b39f5a061ed750b2ef5cdd265b9a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607257"
---
# <a name="configure-execution-properties-for-a-report--report-manager"></a>設定報表的執行屬性 (報表管理員)
  您可以設定報表處理選項，以便指定擷取報表資料的時間。 如果外部資料來源是在特定時間重新整理 (例如，每日或每週重新整理的資料倉儲)，而且您想要避免每次要求報表都擷取相同資料的負擔，排程報表的資料處理就很有用。 此外，如果您想要控制外部資料庫伺服器的處理負載，或者當您想要針對必須使用相同資料集的多位使用者提供一致的結果時，排程資料處理也很有用。 若為變動資料，視需要報表可能會在不同的時間產生不同的結果。 相對地，報表快照集可讓您針對包含相同時間資料的其他報表或分析工具，進行有效的比較。  
  
 報表快照集是一種報表，它包含在特定時間點擷取的配置指示和查詢結果。 報表快照集和視需要報表不同，視需要報表會在您選取報表時取得最新的查詢結果，而報表快照集是依排程處理，並儲存至報表伺服器。 您選取報表快照集以供檢視時，報表伺服器會從報表伺服器資料庫擷取儲存的報表，並顯示建立快照集當時的資料與配置。  
  
 報表快照集不會以特定轉譯格式儲存。 而是只有在使用者或應用程式要求它時，報表快照集才以最後的檢視格式轉譯 (例如 HTML)。 延遲轉譯讓快照集具有可攜性。 報表可以使用要求的裝置或 Web 瀏覽器的正確格式轉譯。  
  
### <a name="to-configure-report-processing-options"></a>若要設定報表處理選項  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)。  
  
2.  導覽至您想要設定處理選項的報表，然後開啟報表。  
  
 將滑鼠停留在該報表上，然後按一下下拉箭號。  
  
1.  在下拉式功能表中，按一下 [管理]****，然後選取 [處理選項]**** 索引標籤。  
  
2.  按一下 [從報表執行快照集轉譯此報表]****，然後選取下列其中一個選項：  
  
    -   如果想要建立快照集，請選取 [使用下列排程建立報表執行快照集]****，然後定義報表特定的排程或從 [共用排程]**** 清單中選取。  
  
    -   如果您要立即建立快照集，請選取 [當您在此頁面上按一下 [套用] 按鈕時，會建立報表快照集]****。  
  
3.  按一下 [套用]。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表處理屬性](../report-server/set-report-processing-properties.md)   
 [開啟並關閉報表 &#40;報表管理員&#41;](../reports/open-and-close-a-report-report-manager.md)   
 [內容頁面 &#40;報表管理員&#41;](../contents-page-report-manager.md)   
 [報表伺服器內容管理 &#40;SSRS 原生模式&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [處理選項屬性頁面 &#40;報表管理員&#41;](../processing-options-properties-page-report-manager.md)  
  
  
