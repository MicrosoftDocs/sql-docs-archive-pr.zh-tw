---
title: 可用性群組尚未準備進行自動容錯移轉 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp3autofailover.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 28261014-342c-442a-bd89-6d04b8d4e8b7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2995ddec51cd70d8a3f209229d0ecb9b0132c79e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585619"
---
# <a name="availability-group-is-not-ready-for-automatic-failover"></a>可用性群組尚未就緒，無法自動容錯
    
## <a name="introduction"></a>簡介  
  
|||  
|-|-|  
|**原則名稱**|可用性群組自動容錯移轉整備|  
|**問題**|可用性群組尚未準備進行自動容錯移轉。|  
|**類別目錄**|**嚴重**|  
|**Facet**|可用性群組|  
  
## <a name="description"></a>描述  
 這項原則檢查可用性群組是否至少有一個已做好容錯移轉準備的次要複本。 當主要複本的容錯移轉模式為自動，但是可用性群組中的次要複本都未準備進行容錯移轉時，原則為狀況不良並會引發警示。  
  
 至少一個次要複本已做好自動容錯移轉的準備時，原則為狀況良好。  
  
> [!NOTE]  
>  在此 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]版本中，可能原因和解決方案的資訊位於 TechNet Wiki 上的 [Availability group is not ready for automatic failover](https://go.microsoft.com/fwlink/p/?LinkId=220851) (可用性群組尚未準備進行自動容錯移轉)。  
  
## <a name="possible-causes"></a>可能的原因  
 可用性群組尚未準備進行自動容錯移轉。 主要複本已設定為自動容錯移轉，不過次要複本尚未準備進行自動容錯移轉。 設定為自動容錯移轉的次要複本可能無法使用，或者其資料同步處理狀態目前不是 SYNCHRONIZED。  
  
## <a name="possible-solutions"></a>可能的解決方案  
 此問題的可能解決方案如下：  
  
-   請確認至少一個次要複本已設定為自動容錯移轉。 如果沒有設定為自動容錯移轉的次要複本，請以同步認可將次要複本的組態更新為自動容錯移轉目標。  
  
-   使用此原則確認資料處於同步處理狀態而且自動容錯移轉目標為 SYNCHRONIZED，然後解決可用性複本上的問題。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
