---
title: 檢視鏡像資料庫的狀態 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- states [SQL Server], database mirroring
- database mirroring [SQL Server], states
ms.assetid: 544f4194-253e-4c57-96ca-31c16301434f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fc691e8b746a816ab88448e3399aebad6d8844e9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594676"
---
# <a name="view-the-state-of-a-mirrored-database-sql-server-management-studio"></a>檢視鏡像資料庫的狀態 (SQL Server Management Studio)
  在資料庫鏡像工作階段中，您可以在 [資料庫屬性] 對話方塊的 [鏡像] 頁面上檢視狀態。  
  
### <a name="to-view-the-status-of-a-database-mirroring-session"></a>若要檢視資料庫鏡像工作階段的狀態  
  
1.  連接到主體伺服器執行個體後，在 [物件總管] 中按一下伺服器名稱，以展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]** ，然後選取要鏡像的資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，選取 [工作]，然後按一下 [鏡像]。 這將會開啟在 **[資料庫屬性]** 對話方塊中的 **[鏡像]** 頁面。  
  
4.  在鏡像開始後，[狀態] 面板便會顯示資料庫鏡像工作階段的狀態 (此狀態是從您選取 [鏡像] 頁面或按了 [重新整理] 按鈕後的狀態)。 可能的狀態如下：  
  
    |狀態|說明|  
    |------------|-----------------|  
    |\<blank>|資料庫鏡像工作階段不存在，並且在 [鏡像] 頁面上沒有可以報告的活動。|  
    |已暫停|主體資料庫正在執行中，但沒有傳送任何記錄到鏡像伺服器。 無法使用資料庫的鏡像副本。|  
    |沒有連接|主體伺服器執行個體無法連接到其夥伴或見證伺服器執行個體 (若有的話)。|  
    |正在同步處理|鏡像資料庫的內容落後於主體資料庫的內容。 主體伺服器執行個體正在將記錄傳送到鏡像伺服器執行個體，這時會將變更套用至鏡像資料庫，以便向前復原。<br /><br /> 在資料庫鏡像工作階段的開始時，鏡像和主體資料庫處於同步狀態。|  
    |容錯移轉|在主體伺服器執行個體上，手動容錯移轉 (角色交換) 已經開始，但鏡像尚未接受。|  
    |已同步處理|鏡像資料庫和主體資料庫包含相同的資料。 只有在已同步處理狀態中，才可能執行手動與自動容錯移轉。|  
  
## <a name="see-also"></a>另請參閱  
 [鏡像狀態 &#40;SQL Server&#41;](mirroring-states-sql-server.md)  
  
  
