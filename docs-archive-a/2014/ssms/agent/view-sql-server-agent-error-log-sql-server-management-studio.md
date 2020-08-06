---
title: 檢視 SQL Server Agent 錯誤記錄檔 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- viewing SQL Server Agent error logs
- displaying SQL Server Agent error logs
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: de920425-fa44-469f-b83d-49e3f97e97f4
author: stevestein
ms.author: sstein
ms.openlocfilehash: b88214a158a970a754c5f313bde3d53f2652ae73
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87703733"
---
# <a name="view-sql-server-agent-error-log-sql-server-management-studio"></a>View SQL Server Agent Error Log (SQL Server Management Studio)
  此主題描述如何使用  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中檢視 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Agent 錯誤記錄檔。  
  
 記錄檔檢視器會顯示許多不同元件的記錄資訊。 當記錄檔檢視器開啟時，使用 **[選取記錄]** 窗格以選取您要顯示的記錄檔。 每個記錄檔都會顯示適用於該記錄檔類型的資料行。 可用的記錄檔取決於記錄檔檢視器的開啟方式而定。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   [若要使用 SQL Server Management Studio 檢視 SQL Server Agent 錯誤記錄檔](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
 只有當您擁有使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 節點的權限時，[物件總管] 才會顯示該節點。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 若要執行功能，您必須將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 設定為使用帳戶認證，此帳戶必須是 **中** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](系統管理員) 固定伺服器角色的成員。 此帳戶必須擁有下列 Windows 權限：  
  
-   以服務登入 (SeServiceLogonRight)  
  
-   取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)  
  
-   略過跨越檢查 (SeChangeNotifyPrivilege)  
  
-   調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)  
  
 如需 Agent 服務帳戶所需之 Windows 許可權的詳細資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱[選取 SQL Server Agent 服務的帳戶](select-an-account-for-the-sql-server-agent-service.md)和[設定 Windows 服務帳戶與許可權](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-ssnoversion-agent-error-log"></a>若要檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 錯誤記錄檔  
  
1.  在 **[物件總管]** 中，按一下加號展開伺服器，此伺服器包含要檢視的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 錯誤記錄檔。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  按一下加號展開 **[錯誤記錄檔]** 資料夾。  
  
4.  以滑鼠右鍵按一下要檢視的錯誤記錄檔，然後選取 [檢視代理程式記錄]****。  
  
     [**記錄檔檢視器-**_server_name_ ] 對話方塊中有下列選項：  
  
     **載入記錄**  
     開啟對話方塊供您指定所要載入的記錄檔。  
  
     **匯出**  
     開啟對話方塊，以讓您將 [記錄檔摘要] 格線中所顯示的資訊匯出至文字檔。  
  
     **[重新整理]**  
     重新整理所選取之記錄檔的檢視。 當套用任何篩選設定時， **[重新整理]** 按鈕會從目標伺服器重新讀取選取的記錄檔。  
  
     **Filter**  
     開啟對話方塊，以讓您指定用來篩選記錄檔的設定，例如 [連接]、[日期] 或其他的 [一般] 篩選準則。  
  
     **搜尋**  
     搜尋記錄檔中的特定文字。 不支援使用萬用字元搜尋。  
  
     **停止**  
     停止載入記錄檔項目。 例如，如果遠端或離線記錄檔需要長時間才能載入，而您只要檢視最新項目時，就可以使用這個選項。  
  
     **記錄檔摘要**  
     此資訊面板會顯示記錄檔篩選的摘要。 如果未篩選檔案，則會看到下列文字： **[未套用篩選]** 。 若篩選已套用到記錄，則會看到下列文字：**篩選記錄項目的準則：\<filter criteria>** 。  
  
     **選取的資料列詳細資料**  
     選取資料列以顯示頁面下方有關選取之事件資料列的其他詳細資料。 將資料行拖曳至方格中的新位置，以重新排序資料行。 將方格標頭中的資料行分隔線拖曳至左邊或右邊，以調整資料行大小。 在方格標頭中按兩下資料行分隔線，自動將資料行大小調整為內容寬度。  
  
     **執行個體**  
     發生事件之執行個體的名稱。 顯示為 *&lt;電腦名稱*\\*執行個體名稱&gt;* 。  
  
     **日期**  
     顯示事件的日期。  
  
     **Source**  
     顯示事件建立的來源功能，例如服務名稱 (如 MSSQLSERVER)。 不是所有記錄檔類型都會出現來源。  
  
     **訊息**  
     顯示與事件相關聯的任何訊息。  
  
     **記錄類型**  
     顯示事件所屬之記錄檔的類型。 所有選取的記錄檔都會出現在記錄檔摘要視窗中。  
  
     **記錄來源**  
     顯示擷取事件之來源記錄的描述。  
  
5.  完成後，請按一下 **[關閉]** 。  
  
  
