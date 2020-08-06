---
title: 檢視收集組報表 (SQL Server Management Studio) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.dc.reporthistory.calendar.f1
helpviewer_keywords:
- collection sets [SQL Server], viewing reports
- reports [SQL Server], viewing collection set
ms.assetid: c3b1e791-9aa1-4bba-9622-4954568e1820
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cb8755c67e6c03bb318fdb86d703f6d647d5a3eb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599013"
---
# <a name="view-a-collection-set-report-sql-server-management-studio"></a>檢視收集組報表 (SQL Server Management Studio)
  設定管理資料倉儲之後，您就可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中檢視收集組報表。 這些報表是針對安裝期間所安裝的系統資料收集組提供的。 這些報表包括：  
  
-   磁碟使用量摘要  
  
-   查詢統計資料記錄  
  
-   伺服器活動記錄  
  
 這個程序會顯示 [磁碟使用量]  收集組的報表。 您可以遵循相同的一般程序來檢視其他系統資料收集組的報表。  
  
### <a name="to-view-a-collection-set-report"></a>若要檢視收集組報表  
  
1.  報表的資料表是在第一次上傳所收集的資料時建立的。 如果您嘗試在第一次上傳之前檢視報表，將會發生錯誤，而且不會顯示任何報表。 若要上傳 [磁碟使用量] 收集組的資料，請在物件總管中，依序展開 [管理]  資料夾、[資料收集]  和 [系統資料收集組]  ，以滑鼠右鍵按一下 [磁碟使用量]  收集組，然後按一下 [立即收集和上傳]  。  
  
2.  若要檢視報表，請在物件總管中，展開 [管理]  資料夾，以滑鼠右鍵按一下 [資料收集]  ，依序指向 [報表]  和 [管理資料倉儲]  ，然後按一下 [磁碟使用量摘要]  。  
  
    > [!NOTE]  
    >  有些報告可能會在資料收集時間表下方顯示行事曆按鈕。 按一下此按鈕可存取 [資料收集報表行事曆]  。  
  
#### <a name="data-collection-report-calendar"></a>資料收集報表行事曆  
 使用這個對話方塊指定開始日期、開始時間以及您要報告之資料的持續時間。 例如，您可能想要針對上週三的特定 12 小時期間，報告伺服器的磁碟使用量活動。  
  
 **開始日期**  
 輸入報告資料的開始日期，或從行事曆選取日期。  
  
 **開始時間**  
 輸入報告資料的開始時間，或按一下箭頭來指定時間。  
  
 **有效期間**  
 指定報告中要包含的時間範圍。 預設值為 240 分鐘。 可選取的值包括 15 分鐘、60 分鐘、240 分鐘 (4 小時)、720 分鐘 (12 小時) 和 1440 分鐘 (24 小時)。  
  
## <a name="see-also"></a>另請參閱  
 [資料收集](data-collection.md)   
 [Management Studio 中的自訂報表](../../ssms/object/custom-reports-in-management-studio.md)   
 [設定管理資料倉儲 &#40;SQL Server Management Studio&#41;](configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  
