---
title: 命令提示字元公用程式參考 (資料庫引擎) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server]
- command prompt utilities [SQL Server], about command prompt utilities
- command prompt [SQL Server]
- utilities [SQL Server], command prompt
- command prompt [SQL Server], utilities
ms.assetid: 48364bd9-6ea7-45e9-a332-acf3d81bbfae
author: stevestein
ms.author: sstein
ms.openlocfilehash: ffb5f15bb37bd4e15dd93404be3df47ce359586b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687406"
---
# <a name="command-prompt-utility-reference-database-engine"></a>命令提示字元公用程式參考 (資料庫引擎)
  命令提示字元公用程式可編寫 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 作業指令碼。 下表列出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]隨附的命令提示字元公用程式清單。  
  
|**公用程式**|**說明**|**安裝位置**|  
|-----------------|---------------------|----------------------|  
|[bcp 公用程式](bcp-utility.md)|用來複製 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體和使用者指定格式的資料檔案間資料。|\<*drive*:>\Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[dta 公用程式](dta/dta-utility.md)|用來分析工作負載和建議實體設計結構，以最佳化這項工作負載的伺服器效能。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec 公用程式](../integration-services/packages/dtexec-utility.md)|用以設定及執行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。 此命令提示字元公用程式的使用者介面版本稱為 **DTExecUI**，它會啟動「執行封裝公用程式」。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[dtutil 公用程式](../integration-services/dtutil-utility.md)|用來管理 SSIS 封裝。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[使用部署公用程式部署模型方案](https://docs.microsoft.com/analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility)|用以將 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的執行個體。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VShell\Common7\IDE|  
|[osql 公用程式](osql-utility.md)|可讓您在命令提示字元之下，輸入 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式、系統程序和指令碼檔案。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Profiler 公用程式](profiler-utility.md)|用來從命令提示字元啟動 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[RS.exe 公用程式 &#40;SSRS&#41;](../reporting-services/tools/rs-exe-utility-ssrs.md)|用以執行為了管理 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表伺服器而設計的指令碼。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rsconfig 公用程式 &#40;SSRS&#41;](../reporting-services/tools/rsconfig-utility-ssrs.md)|用來設定報表伺服器連接。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rskeymgmt 公用程式 &#40;SSRS&#41;](../reporting-services/tools/rskeymgmt-utility-ssrs.md)|用來管理報表伺服器的加密金鑰。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 應用程式](sqlagent90-application.md)|用來從命令提示字元啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent。|\<drive>:\Program Files\Microsoft SQL Server\\<*執行個體名稱*>\MSSQL\Binn|  
|[sqlcmd 公用程式](sqlcmd-utility.md)|可讓您在命令提示字元之下，輸入 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式、系統程序和指令碼檔案。|\<*drive*:>\Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[SQLdiag 公用程式](sqldiag-utility.md)|用以收集可供 [!INCLUDE[msCoName](../includes/msconame-md.md)] 客戶服務與支援部門使用的診斷資訊。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqllogship 應用程式](sqllogship-application.md)|應用程式用來對記錄傳送組態執行備份、複製和還原作業以及相關的清除工作，而無須執行備份、複製和還原作業。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SqlLocalDB 公用程式](sqllocaldb-utility.md)|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行模式，專供程式開發人員使用。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlmaint 公用程式](sqlmaint-utility.md)|用來執行舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]所建立的資料庫維護計畫。|\<drive>： \Program Files\Microsoft SQL Server\MSSQL12。MSSQLSERVER\MSSQL\Binn|  
|[sqlps 公用程式](sqlps-utility.md)|用來執行 PowerShell 命令和指令碼。 載入並註冊 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 提供者和 cmdlet。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr 應用程式](sqlservr-application.md)|用來從命令提示字元啟動和停止 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體，以進行疑難排解。|\<drive>： \Program Files\Microsoft SQL Server\MSSQL12。MSSQLSERVER\MSSQL\Binn|  
|[Ssms 公用程式](../ssms/ssms-utility.md)|用來從命令提示字元啟動 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VSShell\Common7\IDE|  
|[tablediff 公用程式](tablediff-utility.md)|用來比較兩份資料表，以找出非聚合狀況，當進行複寫拓撲的疑難排解時，它尤其有用。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]COM|  
  
 **使用 [!INCLUDE[win8](../includes/win8-md.md)] 存取 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 設定管理員**  
  
 由於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員是 [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console 程式的嵌入式管理單元，而不是單獨的程式，在執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 時並不會出現 [!INCLUDE[win8](../includes/win8-md.md)]組態管理員這樣的應用程式。 若要開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager，請在 [**搜尋**] 快速鍵的 [ **SQLServerManager12.msc** **應用程式**] 下，針對 () 輸入適用于 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]) 或**sqlservermanager11.msc**的 (sqlservermanager12.msc，然後 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 按**enter**。  
  
## <a name="command-prompt-utilities-syntax-conventions"></a>命令提示字元公用程式語法慣例  
  
|**慣例**|**用於**|  
|--------------------|------------------|  
|大寫|作業系統層級所用的陳述式和詞彙。|  
|`monospace`|命令和程式碼範例。|  
|*斜體*|使用者提供的參數。|  
|**粗體字**|必須完全依照顯示狀況來輸入的命令、參數和其他語法。|  
  
## <a name="see-also"></a>另請參閱  
 [Replication Distribution Agent](../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replication Log Reader Agent](../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replication Merge Agent](../relational-databases/replication/agents/replication-merge-agent.md)   
 [複寫佇列讀取器代理程式](../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
