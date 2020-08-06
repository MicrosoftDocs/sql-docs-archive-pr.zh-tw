---
title: '[散發者設定] 對話方塊 |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.DistributorSettings.f1
helpviewer_keywords:
- Distributor Settings dialog box
ms.assetid: 8276a521-bdd1-4783-bdb6-7ab43499c0ca
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b864620f155e899868c95f58350f98e2b659c4e4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585862"
---
# <a name="sql-server-replication-distributor-settings-dialog-box"></a>SQL Server 複寫 [散發者設定] 對話方塊
  **[散發者設定]** 對話方塊，可讓您針對已加入至複寫監視器之左窗格的散發者變更設定。  
  
## <a name="options"></a>選項。  
 **啟動複寫監視器時自動連接**  
 選取以讓複寫監視器連接到「散發者」並擷取狀態資訊。  
  
 **[連接]**  
 按一下以顯示 **[連接到伺服器]** 對話方塊。 這可讓您檢視和變更連接屬性以及複寫監視器用來連接到散發者的認證。  
  
 **自動重新整理此散發者和其發行集的狀態**  
 選取以讓複寫監視器自動重新整理「散發者」的狀態。 如果選取此選項，複寫監視器就會輪詢散發者，以使用 **[重新整理的頻率]** 選項所設定的輪詢間隔做為依據來取得狀態資訊。 如需複寫監視器中之重新整理的詳細資訊，請參閱＜ [Caching, Refresh, and Replication Monitor Performance](monitor/caching-refresh-and-replication-monitor-performance.md)＞。  
  
 **[重新整理的頻率]**  
 輸入一個值 (以秒為單位)，來指定複寫監視器應輪詢散發者以取得狀態的頻率。 較低的值會產生較頻繁的輪詢。 如果您正在監視大量的發行者，這會影響散發者端的效能。 建議您測試自己的系統，以決定適當的值。 如果您在複寫監視器的任何一個詳細資料視窗中選取 **[自動重新整理]** ，也會使用 **[重新整理的頻率]** 設定。  
  
 **在下列群組中顯示此散發者的所有發行者**  
 從清單中選取一個發行者群組。 發行者會在左窗格中的這個群組之下顯示。 群組為您提供了組織發行者的方式，且對於複寫的運作方式沒有影響。  
  
 **新增群組**  
 按一下即可建立新的發行者群組。 發行者群組為您提供了在複寫監視器內組織發行者的便利方式。 群組不會影響資料的複寫，也不會影響複寫拓撲中各伺服器間的關聯性。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](monitor/start-the-replication-monitor.md)   
 [監視複寫](monitoring-replication.md)  
  
  
