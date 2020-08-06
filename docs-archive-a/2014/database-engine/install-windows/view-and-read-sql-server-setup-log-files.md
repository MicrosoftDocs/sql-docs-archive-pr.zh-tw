---
title: 檢視與讀取 SQL Server 安裝程式記錄檔 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- displaying log files
- Setup [SQL Server], logs
- installation log files [SQL Server]
- installing SQL Server, logs
- errors [SQL Server], Setup
- logs [SQL Server], Setup
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 70f9bbb9a8ed72503dc6fe90077232748b2c4ac2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87698515"
---
# <a name="view-and-read-sql-server-setup-log-files"></a>檢視與讀取 SQL Server 安裝程式記錄檔
  每次執行安裝程式時，都會使用新的時間戳記記錄檔資料夾（位於% programfiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log）來建立記錄檔 \\ 。 時間戳記記錄檔資料夾的名稱格式為 YYYYMMDD_hhmmss。 在自動安裝模式下執行安裝程式時，會在 % temp%\sqlsetup*.log 建立記錄檔。 記錄檔資料夾中的所有檔案都會封存到個別記錄檔資料夾的 Log\*.cab 檔中。  
  
 典型的安裝程式要求會經過三個執行階段：  
  
1.  全域規則文字  
  
2.  元件更新  
  
3.  使用者要求的動作  
  
 在每個階段，安裝程式都會產生詳細和摘要的記錄檔，並且會依需要建立其他的記錄檔。 每個使用者要求的安裝程式動作都會至少呼叫安裝程式三次。  
  
 資料存放區檔案包含安裝程序所追蹤的所有組態物件的狀態快照，對於疑難排解組態錯誤很有用。 XML 檔案傾印會針對每個執行階段為資料存放區物件而建立。 這些會儲存在本身的記錄子資料夾的時間戳記記錄檔資料夾下方，如下所示：  
  
-   Datastore_GlobalRules  
  
-   Datastore_ComponentUpdated  
  
-   資料存放區  
  
 下列各節描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式記錄檔。  
  
## <a name="summary-text"></a>摘要文字  
  
### <a name="overview"></a>概觀  
 此檔案會顯示安裝期間偵測到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件、作業系統環境、命令列參數值 (如果有指定)，以及已執行之每個 MSI/MSP 的整體狀態。  
  
 記錄檔組織成下列各區段：  
  
-   執行的整體摘要  
  
-   執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式所在電腦的屬性和組態  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 先前安裝在電腦上的產品功能  
  
-   安裝版本與安裝套件屬性的描述  
  
-   安裝期間提供的執行階段輸入設定  
  
-   組態檔的位置  
  
-   執行結果的詳細資料  
  
-   全域規則  
  
-   安裝狀況專屬的規則  
  
-   失敗的規則  
  
-   規則報表檔案的位置  
  
### <a name="location"></a>Location  
 它位於% programfiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log \\ 。  
  
 若要尋找摘要文字檔中的錯誤，使用 "error" 或 "failed" 等關鍵字搜尋檔案。  
  
## <a name="summary_engine-base_yyyymmdd_hhmmsstxt"></a>Summary_engine-base_YYYYMMDD_HHMMss.txt  
  
### <a name="overview"></a>概觀  
 summary_engine base 檔案與摘要檔案類似，而且是在主要工作流程期間產生的。  
  
### <a name="location"></a>Location  
 它位於% programfiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log \\<YYYYMMDD_HHMM>\\ 。  
  
## <a name="summary_engine-base_yyyymmdd_hhmmss_componentupdatetxt"></a>Summary_engine-base_YYYYMMDD_HHMMss_ComponentUpdate.txt  
  
### <a name="overview"></a>概觀  
 元件更新摘要記錄檔與摘要檔案類似，而且是在元件更新工作流程期間產生的。  
  
### <a name="location"></a>Location  
 它位於% programfiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log \\<YYYYMMDD_HHMM>\\ 。  
  
## <a name="summary_engine-base_versionnumbermmdd_hhmmss_globalrulestxt"></a>Summary_engine base_ \<VersionNumber>MMDD_HHMMss_GlobalRules.txt  
  
### <a name="overview"></a>概觀  
 全域規則摘要記錄檔與摘要檔案類似，而且是在全域規則工作流程期間產生的。  
  
### <a name="location"></a>Location  
 它位於% programfiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log \\<YYYYMMDD_HHMM>\\ 。  
  
## <a name="detailtxt"></a>Detail.txt  
  
### <a name="overview"></a>概觀  
 安裝或升級之類的主要工作流程會產生 Detail.txt，並提供執行的詳細資料。 針對安裝叫用每個動作時，檔案中的記錄會隨著時間而產生，並顯示執行動作的順序及其相依性。  
  
### <a name="location"></a>Location  
 它位於% programfiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup  
  
 Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt.  
  
 如果在安裝程序期間發生錯誤，就會在此檔案的結尾記錄例外狀況或錯誤。 若要尋找此檔案中的錯誤，請先檢查檔案的結尾，然後再搜尋檔案中的 "error" 或 "exception" 等關鍵字。  
  
## <a name="detail_componentupdatetxt"></a>Detail_ComponentUpdate.txt  
  
### <a name="overview"></a>概觀  
 元件更新工作流程會產生 Detail_ComponentUpdate.txt 檔，而且與 Detail.txt 類似。  
  
### <a name="location"></a>Location  
 它位於% programfiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log \\<YYYYMMDD_HHMM>\\ 。  
  
## <a name="detail_globalrulestxt"></a>Detail_GlobalRules.txt  
  
### <a name="overview"></a>概觀  
 全域規則執行會產生 Detail_GlobalRules.txt，而且與 Detail.txt 類似。  
  
### <a name="location"></a>Location  
 它位於% programfiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log \\<YYYYMMDD_HHMM>\\ 。  
  
## <a name="msi-log-files"></a>MSI 記錄檔  
  
### <a name="overview"></a>概觀  
 MSI 記錄檔會提供安裝套件程序的詳細資料。 在指定之套件的安裝期間，MSIEXEC 會產生這些記錄檔。  
  
 MSI 記錄檔的類型：  
  
-   \<Feature>_\<Architecture>\_\<Interaction>.log  
  
-   \<Feature>_\<Architecture>\_\<Language>\_\<Interaction>.log  
  
-   \<Feature>_\<Architecture>\_\<Interaction>\_\<workflow>.log  
  
### <a name="location"></a>Location  
 MSI 記錄檔位於% programfiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log \\<YYYYMMDD_HHMM>\\<名稱 \> .log。  
  
 檔案的結尾是執行的摘要，其中包含成功或失敗狀態以及屬性。 若要尋找 MSI 檔中的錯誤，請搜尋 "value 3"，通常就可以在該字串的附近找到錯誤。  
  
## <a name="configurationfileini"></a>ConfigurationFile.ini  
  
### <a name="overview"></a>概觀  
 組態檔包含安裝期間提供的輸入設定。 該檔案可以用來重新啟動安裝，而不必手動輸入設定。 不過，帳號的密碼、PID 與某些參數不會儲存在組態檔中。 這些設定可以加入至檔案，或者使用命令列或安裝程式使用者介面提供。 如需詳細資訊，請參閱[使用設定檔安裝 SQL Server 2014](install-sql-server-using-a-configuration-file.md)。  
  
### <a name="location"></a>Location  
 它位於% programfiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log \\<YYYYMMDD_HHMM>\\ 。  
  
## <a name="systemconfigurationcheck_reporthtm"></a>SystemConfigurationCheck_Report.htm  
  
### <a name="overview"></a>概觀  
 系統組態檢查報告包含每個已執行規則以及執行狀態的簡短描述。  
  
### <a name="location"></a>Location  
 它位於% programfiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log \\<YYYYMMDD_HHMM>\\ 。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 how to 主題](../../sql-server/install/installation-how-to-topics.md)   
 [安裝 SQL Server 2014](install-sql-server.md)  
  
  
