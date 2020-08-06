---
title: 啟動、停止、暫停、繼續、重新開機資料庫引擎、SQL Server Agent 或 SQL Server Browser 服務 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, start and stop services
- stopping SQL Server Agent
- parameters [SQL Server], startup options
- SQL Server, startup options
- Database Engine [SQL Server], starting and stopping services
- pausing SQL Server
- PowerShell [SQL Server], starting and stopping services
- single-user mode [SQL Server], starting in
- SQL Server Management Studio [SQL Server], starting or stopping services
- stopping SQL Server Browser service
- starting SQL Server Agent
- default instances [SQL Server], starting and stopping
- SQL Server Agent, starting and stopping
- command prompt [SQL Server], starting and stopping SQL Server services
- continuing SQL Server
- starting SQL Server Database Engine
- net stop commands [SQL Server]
- command prompt [SQL Server], SQL Browser service
- Configuration Manager, start and stop services
- resuming SQL Server
- startup options [SQL Server]
- named instances [SQL Server], starting and stopping
- net start commands [SQL Server]
- SQL Server, starting and stopping
- stopping SQL Server
- starting SQL Server Browser service
- SQL Server Database Engine setting startup options
- administering SQL Server, starting and stopping services
- Management Studio [SQL Server], starting or stopping services
ms.assetid: 32660a02-e5a1-411a-9e57-7066ca459df6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f4b102c8fd81923d7386c8e556896e715311a07e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706706"
---
# <a name="start-stop-pause-resume-restart-the-database-engine-sql-server-agent-or-sql-server-browser-service"></a>啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務
  本主題描述如何 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 從命令提示字元、或 PowerShell 使用 Configuration Manager、、 **net**命令 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，啟動、停止、暫停、繼續或重新開機、代理程式或 Browser 服務。  
  
-   **開始之前：**  
  
    -   [這些是什麼服務？](#Services)  
  
    -   [其他資訊](#MoreInformation)  
  
    -   [安全性](#Security)  
  
-   **使用指示：**  
  
    -   [SQL Server 組態管理員](#SSCMProcedure)  
  
    -   [SQL Server Management Studio](#SSMSProcedure)  
  
    -   [命令提示字元視窗中的 net 命令](#CommandPrompt)  
  
    -   [Transact-SQL](#TsqlProcedure)  
  
    -   [PowerShell](#PowerShellProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="what-is-the-ssdenoversion-service-the-ssnoversion-agent-service-and-the-ssnoversion-browser-service"></a><a name="Services"></a> 什麼是 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服務、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務？  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件是當做 Windows 服務執行的可執行程式。 當做 Windows 服務執行的程式可以繼續操作，而不會在電腦螢幕上顯示任何活動。  
  
 **[!INCLUDE[ssDE](../../includes/ssde-md.md)]維護**  
 當做 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的可執行處理序。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 可以是預設執行個體 (每部電腦只限一個執行個體)，或者可以是許多具名 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體的其中一個。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來判斷哪些 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體會安裝在電腦上。 預設實例 (如果您安裝它) 會列為** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) **。 如果您安裝 (命名的實例) 會列為** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( # B0 instance_name>) **。 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 會安裝為** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLEXPRESS) **。  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式服務**  
 一種 Windows 服務，它會執行排程的管理工作 (稱為作業和警示)。 如需詳細資訊，請參閱 [SQL Server Agent](../../ssms/agent/sql-server-agent.md)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本都可使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需版本支援的功能清單 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱[SQL Server 2014 版本支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser 服務**  
 一種 Windows 服務，它會接聽 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源的內送要求，並為用戶端提供有關電腦上所安裝之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資訊。 單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務執行個體會用於電腦上所安裝的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
###  <a name="additional-information"></a><a name="MoreInformation"></a>其他資訊  
  
-   暫停 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務會阻止新的使用者連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，但是已連接的使用者可以繼續工作，直到連接中斷為止。 當您希望在停止服務之前等待使用者完成工作時，請使用暫停。 這樣可讓他們完成正在進行的交易。 「繼續」可讓 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 再次接受新的連接。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務無法暫停或繼續。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會使用以下圖示來顯示目前的服務狀態。  
  
     **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager**  
  
    -   服務名稱旁圖示上的綠色箭頭，表示服務已啟動。  
  
    -   服務名稱旁圖示上的紅色方塊，表示服務已停止。  
  
    -   服務名稱旁圖示上的兩條垂直藍線，表示服務已暫停。  
  
    -   重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)]時，紅色方塊表示服務已停止，綠色箭頭則表示服務已順利啟動。  
  
     **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
    -   服務名稱旁綠色圓形圖示上的白色箭頭，表示服務已啟動。  
  
    -   服務名稱旁紅色圓形圖示上的白色方塊，表示服務已停止。  
  
    -   服務名稱旁藍色圓形圖示上的兩條垂直白線，表示服務已暫停。  
  
-   當使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]時，只能使用可能的選項。 例如，如果此服務已啟動，則無法使用 **[啟動]** 。  
  
-   在叢集上執行時，使用叢集管理員來管理 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服務的效果最佳。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 根據預設，只有本機 Administrators 群組的成員能夠啟動、停止、暫停、繼續或重新啟動服務。 若要將管理服務的能力授與非系統管理員，請參閱 [How to grant users rights to manage services in Windows Server 2003](https://support.microsoft.com/kb/325349)(如何在 Windows Server 2003 中，將管理服務的權限授與使用者)。 (其他 Windows 版本的程序都很相似)。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]使用命令停止， [!INCLUDE[tsql](../../includes/tsql-md.md)] `SHUTDOWN` 需要**sysadmin**或**serveradmin**固定伺服器角色中的成員資格，而且無法轉移。  
  
##  <a name="using-ssnoversion-configuration-manager"></a><a name="SSCMProcedure"></a> 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-ssdenoversion"></a>若要啟動、停止、暫停、繼續或重新啟動 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  指向 **[開始]** 功能表上的 **[所有程式]** ，然後依序指向 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]** ，再按一下 **[SQL Server 組態管理員]** 。  
  
2.  如果出現 **[使用者帳戶控制]** 對話方塊，請按一下 **[是]** 。  
  
3.  在 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員] 中，按一下左窗格中的 **[SQL Server 服務]**。  
  
4.  在結果窗格中，以滑鼠右鍵按一下 [SQL Server (MSSQLServer)] 或具名執行個體，然後按一下 [啟動]、[停止]、[暫停]、[繼續] 或 [重新啟動]。  
  
5.  按一下 **[確定]** ，即可關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員。  
  
> [!NOTE]  
>  若要使用啟動選項啟動 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，請參閱[設定伺服器啟動選項 &#40;SQL Server 組態管理員&#41;](scm-services-configure-server-startup-options.md)。  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-ssnoversion-browser-or-an-instance-of-the-ssnoversion-agent"></a>若要啟動、停止、暫停、繼續或重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 或是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的執行個體  
  
1.  指向 **[開始]** 功能表上的 **[所有程式]** ，然後依序指向 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]** ，再按一下 **[SQL Server 組態管理員]** 。  
  
2.  如果出現 **[使用者帳戶控制]** 對話方塊，請按一下 **[是]** 。  
  
3.  在 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員] 中，按一下左窗格中的 **[SQL Server 服務]**。  
  
4.  在 [結果] 窗格中，以滑鼠右鍵按一下 [ ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 瀏覽器**] 或 [ ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式 (MSSQLServer) **或** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agent ( # B0 instance_name>) **用於已命名的實例，然後按一下 [**啟動**]、[**停止**]、[**暫停**]、[**繼續**] 或 [**重新**  
  
5.  按一下 **[確定]** ，即可關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 無法暫停。  
  
##  <a name="using-ssnoversion-management-studio"></a><a name="SSMSProcedure"></a> 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-ssdenoversion"></a>若要啟動、停止、暫停、繼續或重新啟動 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  在物件總管中，連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，並以滑鼠右鍵按一下您要啟動的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，然後按一下 [啟動]****、[停止]****、[暫停]****、[繼續]**** 或 [重新啟動]****。  
  
     或者在 [已註冊的伺服器] 中，以滑鼠右鍵按一下您要啟動的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體、並指向 [服務控制]****，然後按一下 [啟動]****、[停止]****、[暫停]****、[繼續]**** 或 [重新啟動]****。  
  
2.  如果出現 **[使用者帳戶控制]** 對話方塊，請按一下 **[是]** 。  
  
3.  當系統提示您是否要執行動作時，請按一下 **[是]**。  
  
#### <a name="to-start-stop-or-restart-the-an-instance-of-the-ssnoversion-agent"></a>若要啟動、停止或重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的執行個體  
  
1.  在物件總管中，連接到的實例 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，以滑鼠右鍵按一下 [ ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式**]，然後按一下 [**啟動**]、[**停止**] 或 [**重新開機**]。  
  
2.  如果出現 **[使用者帳戶控制]** 對話方塊，請按一下 **[是]** 。  
  
3.  當系統提示您是否要執行動作時，請按一下 **[是]**。  
  
##  <a name="from-the-command-prompt-window-using-net-commands"></a><a name="CommandPrompt"></a> 從命令提示字元視窗使用 net 命令  
 可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows **net** 命令來啟動、停止或暫停 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
###  <a name="to-start-the-default-instance-of-the-ssde"></a><a name="dbDefault"></a> 若要啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   從命令提示字元，輸入下列其中一個命令：  
  
     **net start "SQL Server (MSSQLSERVER)"**  
  
     -或-  
  
     **net start MSSQLSERVER**  
  
###  <a name="to-start-a-named-instance-of-the-ssde"></a><a name="dbNamed"></a> 若要啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   從命令提示字元，輸入下列其中一個命令。 以想要管理執行個體的名稱來取代 *\<instancename>* 。  
  
     **net start "SQL Server (** *instancename* **)"**  
  
     -或-  
  
     **net start MSSQL$** *instancename*  
  
###  <a name="to-start-the-ssde-with-startup-options"></a><a name="dbStartup"></a> 若要使用啟動選項來啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   將啟動選項加入 **net start "SQL Server (MSSQLSERVER)"** 陳述式結尾，並間隔一個空格。 使用 **net start**啟動時，啟動選項會使用斜線 (/)，而非連字號 (-)。  
  
     **net start "SQL Server (MSSQLSERVER)" /f /m**  
  
     -或-  
  
     **net start MSSQLSERVER /f /m**  
  
    > [!NOTE]  
    >  如需啟動選項的詳細資訊，請參閱 [Database Engine 服務啟動選項](database-engine-service-startup-options.md)。  
  
###  <a name="to-start-the-ssnoversion-agent-on-the-default-instance-of-ssnoversion"></a><a name="agDefault"></a> 若要使用啟動選項來啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設執行個體上啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   從命令提示字元，輸入下列其中一個命令：  
  
     **net start "SQL Server Agent (MSSQLSERVER)"**  
  
     -或-  
  
     **net start SQLSERVERAGENT**  
  
###  <a name="to-start-the-ssnoversion-agent-on-a-named-instance-of-ssnoversion"></a><a name="agNamed"></a> 若要使用啟動選項來啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的具名執行個體上啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   從命令提示字元，輸入下列其中一個命令。 以您要管理之執行個體的名稱取代 *執行個體名稱* 。  
  
     **net start "SQL Server Agent(** *instancename* **)"**  
  
     -或-  
  
     **net start SQLAgent$** *instancename*  
  
 如需如何以詳細資訊模式執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來進行疑難排解的相關資訊，請參閱 [sqlagent90 應用程式](../../tools/sqlagent90-application.md)。  
  
###  <a name="to-start-the-ssnoversion-browser"></a><a name="Browser"></a> 若要啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser  
  
-   從命令提示字元，輸入下列其中一個命令：  
  
     **net start "SQL Server Browser"**  
  
     -或-  
  
     **net start SQLBrowser**  
  
###  <a name="to-pause-or-stop-services-from-the-command-prompt-window"></a><a name="pauseStop"></a> 若要從命令提示字元視窗暫停或停止服務  
  
-   若要暫停或停止服務，請使用以下方式來修改命令。  
  
    -   若要暫停服務，請以 **net pause** 取代 **net start**。  
  
    -   若要停止服務，請以 **net stop** 取代 **net start**。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用 `SHUTDOWN` 陳述式來停止 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
#### <a name="to-stop-the-ssde-using-tsql"></a>若要使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 停止 [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
-   若要等待目前執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式和預存程序完成，然後停止 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，請執行下列陳述式。  
  
    ```sql  
    SHUTDOWN;   
    ```  
  
-   若要立即停止 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，請執行下列陳述式。  
  
    ```sql  
    SHUTDOWN WITH NOWAIT;   
    ```  
  
 如需語句的詳細資訊 `SHUTDOWN` ，請參閱[SHUTDOWN &#40;transact-sql&#41;](/sql/t-sql/language-elements/shutdown-transact-sql)。  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  
  
#### <a name="to-start-and-stop-ssde-services"></a>若要啟動及停止 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務  
  
1.  在 [命令提示字元] 視窗中，執行下列命令來啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell。  
  
    ```ms-dos  
    sqlps  
    ```  
  
2.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 命令提示字元中，執行下列命令。 以電腦的名稱取代 `computername` 。  
  
    ```powershell  
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\computername  
    $Wmi = (Get-Item .).ManagedComputer
    ```  
  
3.  識別您想要停止或啟動的服務。 挑選下列其中一行。 使用具名執行個體的名稱取代 `instancename` 。  
  
    -   取得 [!INCLUDE[ssDE](../../includes/ssde-md.md)]預設執行個體的參考。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQLSERVER']  
        ```  
  
    -   取得 [!INCLUDE[ssDE](../../includes/ssde-md.md)]具名執行個體的參考。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQL$instancename']  
        ```  
  
    -   取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設執行個體上 [!INCLUDE[ssDE](../../includes/ssde-md.md)]Agent 服務的參考。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLSERVERAGENT']  
        ```  
  
    -   取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具名執行個體上 [!INCLUDE[ssDE](../../includes/ssde-md.md)]Agent 服務的參考。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLAGENT$instancename']  
        ```  
  
    -   取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務的參考。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLBROWSER']  
        ```  
  
4.  完成範例，以啟動然後停止選取的服務。  
  
    ```powershell  
    # Display the state of the service.  
    $DfltInstance  
    # Start the service.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [以最基本的設定啟動 SQL Server](start-sql-server-with-minimal-configuration.md)   
 [SQL Server 2014 各版本所支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
