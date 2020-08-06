---
title: 設定預先定義的複寫警示 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: aa78a08757cc7bbe809c5e3a1808c9632b76763a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709257"
---
# <a name="configure-predefined-replication-alerts-sql-server-management-studio"></a>設定預先定義的複寫警示 (SQL Server Management Studio)
  複寫提供下列預先定義的警示，這些警示可設定為回應複寫事件：  
  
-   **複寫: 代理程式成功**    
-   **複寫: 代理程式失敗**    
-   **複寫: 代理程式重試**    
-   **複寫: 已卸除逾期的訂閱**    
-   **複寫：驗證失敗後重新初始化訂閱**    
-   **複寫：訂閱者資料驗證失敗**    
-   **複寫：訂閱者已經通過資料驗證**    
-   **複寫: 代理程式自訂關閉**  
  
 從 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中的 [警示] 資料夾或複寫監視器中的 [警告] 索引標籤設定這些警示。 如需存取此索引標籤的詳細資訊，請參閱[使用複寫監視器來查看資訊及執行](../monitor/view-information-and-perform-tasks-replication-monitor.md)工作。  
  
 除了這些警示外，複寫監視器還提供與狀態和效能相關的警告與警示集合。 如需詳細資訊，請參閱在複寫監視器警示基礎結構[中設定臨界值和警告](../monitor/set-thresholds-and-warnings-in-replication-monitor.md)。 如需詳細資訊，請參閱[建立使用者定義的事件](../../../ssms/agent/create-a-user-defined-event.md)。  
  
### <a name="to-configure-a-predefined-replication-alert-in-management-studio"></a>若要在 Management Studio 中設定預先定義的複寫警示  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的散發者，然後展開伺服器節點。    
2.  展開 **[SQL Server Agent]** 資料夾，然後展開 **[警示]** 資料夾。    
3.  以滑鼠右鍵按一下複寫警示，然後按一下 **[屬性]** 。    
4.  在 [\<AlertName> 警示屬性] 對話方塊中設定選項：    
    -   在 **[一般]** 頁面上，按一下 **[啟用]** ；指定警示應套用至哪個資料庫。    
    -   在 **[回應]** 頁面上，指定是否應傳送電子郵件及 (或) 是否應執行作業。  
  
         若警示是**複寫：** 訂閱者資料驗證失敗」，您可以指定複寫為此警示提供的回應作業：選取 [執行作業]，然後按一下瀏覽按鈕 ( **...** )。在 **[尋找作業]** 對話方塊中，按一下 **[瀏覽]** 。 在 **[瀏覽物件]** 對話方塊中，選取 **[重新初始化具有資料驗證失敗的訂閱]** 。 在兩個開啟的對話方塊中按一下 **[確定]** 。 執行作業時，它會使用對預存程序的遠端程序呼叫 (RPC) 重新初始化訂閱。 如果「發行者」使用遠端「散發者」，則必須定義「發行者」端的遠端伺服器登入，以便建立從「散發者」到「發行者」的 RPC。   
    -   在 **[選項]** 頁面上，自訂回應的文字。    
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-configure-an-alert-for-a-threshold-in-replication-monitor"></a>若要在複寫監視器中設定臨界值的警示  
  
1.  在 **[警告]** 索引標籤上，按一下 **[設定警示]** 。    
2.  在 **[設定複寫警示]** 對話方塊中選取一個警示，然後按一下 **[設定]** 。    
3.  在 [\<AlertName> 警示屬性] 對話方塊中設定選項：    
    -   在 **[一般]** 頁面上，按一下 **[啟用]** ；指定警示應套用至哪個資料庫。    
    -   在 **[回應]** 頁面上，指定是否應傳送電子郵件及 (或) 是否應執行作業。    
         若警示是**複寫：** 訂閱者資料驗證失敗」，您可以指定複寫為此警示提供的回應作業：選取 [執行作業]，然後按一下瀏覽按鈕 ( **...** )。在 **[尋找作業]** 對話方塊中，按一下 **[瀏覽]** 。 在 **[瀏覽物件]** 對話方塊中，選取 **[重新初始化具有資料驗證失敗的訂閱]** 。 在兩個開啟的對話方塊中按一下 **[確定]** 。 執行作業時，它會使用對預存程序的遠端程序呼叫 (RPC) 重新初始化訂閱。 如果「發行者」使用遠端「散發者」，則必須定義「發行者」端的遠端伺服器登入，以便建立從「散發者」到「發行者」的 RPC。   
    -   在 **[選項]** 頁面上，自訂回應的文字。    
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]    
5.  按一下 [關閉] 。  
  
## <a name="see-also"></a>另請參閱  
 [使用針對複寫代理程式事件的警示](../agents/use-alerts-for-replication-agent-events.md)  
  
  
