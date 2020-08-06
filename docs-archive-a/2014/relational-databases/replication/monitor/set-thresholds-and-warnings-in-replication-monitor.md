---
title: 在複寫監視器中設定閾值和警告 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server replication]
- Merge Agent, thresholds and warnings
- Distribution Agent, thresholds and warnings
- thresholds [SQL Server replication]
- Replication Monitor, thresholds and warnings
- monitoring performance [SQL Server replication], thresholds and warnings
ms.assetid: 3a409c2c-b77e-4001-b81a-1dcd918618ec
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f34878a6398df34e55e6dd3783f2da736bee0959
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709189"
---
# <a name="set-thresholds-and-warnings-in-replication-monitor"></a>在複寫監視器中設定臨界值和警告
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)]「複寫監視器」會顯示發行集 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和訂閱的狀態資訊。 依預設，複寫監視器只針對未初始化的訂閱顯示警告，但您可以啟用於其他條件下發出警告。 建議您啟用拓撲警告，這樣您才能收到即時的狀態和效能資訊。  
  
 在您啟用警告時，必須指定臨界值。 達到或超過臨界值時，會顯示警告 (除非有更高優先順序的問題需要顯示)。 除了在複寫監視器顯示警告外，達到臨界值也會觸發警示。 您可啟用滿足下列條件時的警告：  
  
-   即將發生訂閱過期  
  
     此條件套用於所有類型的複寫。 如果達到或超過指定的臨界值，訂閱狀態會顯示為 **[即將過期/已過期]**。  
  
-   超過指定的延遲 (交易受發行者認可與對應交易受訂閱者認可之間所經過的時間)。  
  
     這可以套用於異動複寫。 如果達到或超過指定臨界值，訂閱狀態將顯示為 **[效能嚴重不足]**。  
  
-   超過指定的同步處理時間。  
  
     這可以套用於合併式複寫。 若已達到或超過指定臨界值，狀態顯示為 **[長期執行合併]**。 您可以為撥號連接和區域網路 (LAN) 連接，指定不同的臨界值。  
  
-   在給定時間內處理的資料列數達不到指定數目。  
  
     這可以套用於合併式複寫。 若已達到或超過指定臨界值，狀態顯示為 **[效能嚴重不足]**。 您可以為撥號連接和 LAN 連接，指定不同的臨界值。  
  
 如需 [效能嚴重不足]**** 和 [長期執行合併]**** 警告的詳細資訊，請參閱[使用複寫監視器監視效能](monitor-performance-with-replication-monitor.md)。  
  
 **本主題內容**  
  
-   [設定交易式發行集的臨界值與警告](#Transactional)  
  
-   [設定合併式發行集的臨界值和警告](#Merge)  
  
-   [設定快照式發行集的臨界值和警告](#Snapshot)  
  
##  <a name="to-set-thresholds-and-warnings-for-a-transactional-publication"></a><a name="Transactional"></a> 若要設定交易式發行集的臨界值與警告  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 [**警告**] 索引標籤。若要查看此索引標籤上選項的詳細資訊 **，請按一下功能表列上的**[說明]。  
  
3.  透過選取適當的核取方塊啟用警告： **[若訂閱將在臨界值內過期，就發出警告]** 或 **[若延遲超過臨界值，就發出警告]**。  
  
4.  在 **[臨界值]** 資料行中設定警告的臨界值。 例如，如果您在步驟 3 選取 **[若延遲超過臨界值，就發出警告]** ，便可以在 **[臨界值]** 資料行中選取 **[60 秒]** 的延遲。  
  
5.  按一下 **[儲存變更]** 。  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>若要設定臨界值的警示  
  
1.  按一下 **[設定警示]**。  
  
2.  在 **[設定複寫警示]** 對話方塊中選取一個警示，然後按一下 **[設定]** 。  
  
     這個對話方塊會顯示所有發行集類型的警示，包括與監視臨界值無關的警示。 如需詳細資訊，請參閱[使用複寫代理程式事件的警示](../agents/use-alerts-for-replication-agent-events.md)。  
  
3.  在 [\<AlertName> 警示屬性] 對話方塊中設定選項：  
  
    -   在 **[一般]** 頁面上，按一下 **[啟用]** ；指定警示應套用至哪個資料庫。  
  
    -   在 **[回應]** 頁面上，指定是否應傳送電子郵件及 (或) 是否應執行作業。  
  
    -   在 **[選項]** 頁面上，自訂回應的文字。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  按一下 [關閉] 。  
  
##  <a name="set-thresholds-and-warnings-for-a-merge-publication"></a><a name="Merge"></a>設定合併式發行集的臨界值和警告  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 [**警告**] 索引標籤。若要查看此索引標籤上選項的詳細資訊，**請按一下功能表**欄上的 [說明]。  
  
3.  透過選取適當的核取方塊啟用警告：  
  
    -   **[若訂閱將在臨界值內過期，就發出警告]**  
  
    -   **如果撥號連接的合併長度超過臨界值，則發出警告**  
  
    -   **如果 LAN 連接的合併長度超過臨界值，則發出警告**  
  
    -   **如果 LAN 連接的每秒合併資料列少於臨界值，則發出警告**  
  
    -   **如果撥號連接之每秒的合併資料列少於臨界值，則發出警告**  
  
4.  在 **[臨界值]** 資料行中設定警告的臨界值。 例如，如果您在步驟 3 選取 **[若撥號連接的合併長度超過臨界值，就發出警告]** ，便可以在 **[臨界值]** 資料行中選取 **[10 分鐘]** 的時間。  
  
5.  按一下 **[儲存變更]** 。  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>若要設定臨界值的警示  
  
1.  按一下 **[設定警示]**。  
  
2.  在 **[設定複寫警示]** 對話方塊中選取一個警示，然後按一下 **[設定]** 。  
  
     這個對話方塊會顯示所有發行集類型的警示，包括與監視臨界值無關的警示。  
  
3.  在 [\<AlertName> 警示屬性] 對話方塊中設定選項：  
  
    -   在 **[一般]** 頁面上，按一下 **[啟用]** ；指定警示應套用至哪個資料庫。  
  
    -   在 **[回應]** 頁面上，指定是否應傳送電子郵件及 (或) 是否應執行作業。  
  
    -   在 **[選項]** 頁面上，自訂回應的文字。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  按一下 [關閉] 。  
  
##  <a name="set-thresholds-and-warnings-for-a-snapshot-publication"></a><a name="Snapshot"></a>設定快照式發行集的臨界值和警告  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 [**警告**] 索引標籤。若要查看此索引標籤上選項的詳細資訊 **，請按一下上方功能表上的**[說明]。  
  
3.  透過選取 **[若訂閱將在臨界值內過期，就發出警告]** 核取方塊啟用警告。  
  
4.  在 **[臨界值]** 資料行中設定警告的臨界值。 例如，可在 **[臨界值]** 資料行中選取值 **[70%]** 。  
  
5.  按一下 **[儲存變更]** 。  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>若要設定臨界值的警示  
  
1.  按一下 **[設定警示]**。  
  
2.  在 **[設定複寫警示]** 對話方塊中選取一個警示，然後按一下 **[設定]** 。  
  
     這個對話方塊會顯示所有發行集類型的警示，包括與監視臨界值無關的警示。 如需詳細資訊，請參閱[使用複寫代理程式事件的警示](../agents/use-alerts-for-replication-agent-events.md)。  
  
3.  在 [\<AlertName> 警示屬性] 對話方塊中設定選項：  
  
    -   在 **[一般]** 頁面上，按一下 **[啟用]** ；指定警示應套用至哪個資料庫。  
  
    -   在 **[回應]** 頁面上，指定是否應傳送電子郵件及 (或) 是否應執行作業。  
  
    -   在 **[選項]** 頁面上，自訂回應的文字。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  按一下 [關閉] 。  
  
## <a name="see-also"></a>另請參閱  
 [監視複寫](../monitoring-replication.md)  
  
  
