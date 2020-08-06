---
title: SQL Server 2014 中已停止的 SQL Server 功能 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 0678bfbc-5d3f-44f4-89c0-13e8e52404da
author: rothja
ms.author: jroth
ms.openlocfilehash: 6d8b1b10e2da693bb2cd5c66bf44eda248b05037
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607007"
---
# <a name="discontinued-sql-server-features-in-sql-server-2014"></a>在 SQL Server 2014 中停止 SQL Server 的功能
  本主題描述升級至 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 之後無法再使用的功能。  
  
## <a name="discontinued-features-in-sssql14"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中沒有已停止的功能。  
  
## <a name="discontinued-features-in-sssql11"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="discontinued-active-directory-helper-service"></a>不再提供的 Active Directory Helper 服務  
 已移除 Active Directory Helper 服務和相關元件。 下表列出因此一併移除的相關聯元件：  
  
|類別|已停止的功能|取代|  
|--------------|--------------------------|-----------------|  
|系統預存程序|sp_ActiveDirectory_Obj<br /><br /> sp_ActiveDirectory_SCP<br /><br /> sp_ActiveDirectory_Start|沒有可用的取代項目|  
  
## <a name="discontinued-features-in-sql-server-2008-r2"></a>SQL Server 2008 R2 中停止的功能  
  
### <a name="64-bit-platform-support-in-reporting-services"></a>Reporting Services 中的 64 位元平台支援  
 從 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 開始，[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 元件不再支援執行 Windows Server 2003 或 Windows Server 2003 R2 的以 Itanium 為基礎的伺服器。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]繼續支援其他 64 位元的作業系統，包括以 Itanium 為基礎系統的 Windows Server 2008 Datacenter 或 Windows Server°2008°R2。 若要從 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 安裝升級為 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]，而此安裝所含 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 是在以 Itanium 為基礎系統版本 Windows Server 2003 或 Windows Server 2003 R2 上，則必須先升級作業系統。  
  
## <a name="discontinued-features-in-sql-server-2008"></a>SQL Server 2008 中停止的功能  
  
### <a name="discontinued-sql-dmo-from-sql-server-express-installation"></a>已停止 SQL Server Express 安裝中的 SQL-DMO  
 已經從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中移除適用於 [!INCLUDE[ssExpressEd10](../includes/ssexpressed10-md.md)] 的 SQL-DMO。 我們建議您盡快修改目前仍使用這項功能的應用程式。 如果您必須支援 SQL-DMO for [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express，請從 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [Microsoft 下載中心](https://www.microsoft.com/download/)的 Feature Pack 安裝回溯相容性元件。 請在新的開發工作中使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Objects (SMO)。  
  
### <a name="discontinued-option-for-web-assistant"></a>已停止用於 Web 助理的選項  
 啟用 Web 助理的 `sp_configure` 選項已經從 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中移除了。 我們建議您改用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 。  
  
### <a name="surface-area-configuration-tool"></a>介面區組態工具  
 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 已停止介面區組態工具。 下表將顯示您可以在這個版本中用來設定組態、選項和元件功能的項目。  
  
|取代設定和元件功能|如何設定|  
|-------------------------------------------------|----------------------|  
|通訊協定、連接和啟動選項|使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員。|  
|[!INCLUDE[ssDE](../includes/ssde-md.md)] 功能|使用以原則為基礎的管理、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的屬性設定，或 sp_Configure。|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 功能|使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的屬性設定。|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] - EnableIntegrated Security 屬性|使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的屬性設定。|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -「排程事件和報表傳遞」與「Web 服務和 HTTP 存取」|編輯 RSReportServer.config 組態檔。|  
|命令列選項|這個版本不支援。|  
|SOAP 和 [!INCLUDE[ssSB](../includes/sssb-md.md)] 端點|使用[CREATE endpoint](/sql/t-sql/statements/create-endpoint-transact-sql)和[ALTER endpoint](/sql/t-sql/statements/alter-endpoint-transact-sql)。|  
  
### <a name="discontinued-command-prompt-parameters-for-sql-server-setup"></a>SQL Server 安裝程式中已停止的命令提示字元參數  
 下表將顯示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不支援的舊版 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 安裝程式命令提示字元參數。  
  
|已停止的參數|取代參數|  
|----------------------------|---------------------------|  
|ADDLOCAL|/ACTION=Uninstall 和 /FEATURES|  
|DISABLENETWORKPROTOCOLS|適用于 TCP/IP 的/TCPENABLED<sup>1</sup>|  
|DISABLENETWORKPROTOCOLS|具名管道的/NPENABLED<sup>1</sup>|  
|INSTALLSQLDATADIR|/SQLUSERDBDIR<br /><br /> /SQLUSERDBLOGDIR<br /><br /> /SQLBACKUPDIR<br /><br /> /SQLTEMPDBDIR<br /><br /> /SQLTEMPDBLOGDIR|  
|REINSTALL|這個版本中沒有對等項目。|  
|REINSTALLMODE|這個版本中沒有對等項目。|  
|REMOVE|/ACTION=Uninstall 和 /FEATURES|  
|SAMPLEDATABASE|這個版本中沒有對等項目。|  
|SAVESYSDB|這個版本中沒有對等項目。|  
|SKUUPGRADE<sup>2</sup>|這個版本中沒有對等項目。|  
|UPGRADE|/ACTION=Upgrade 和 /FEATURES|  
|USESYSDB|這個版本中沒有對等項目。|  
  
 <sup>1</sup>這些參數只有在安裝時才有效。  
  
 <sup>2</sup>從開始 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] ，指定/Action = EditionUpgrade，在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不使用原始安裝媒體的情況下，隨時將現有的版本升級至不同的版本。 如需有關支援之版本與版別升級的詳細資訊，請參閱＜ [Supported Version and Edition Upgrades](../database-engine/install-windows/supported-version-and-edition-upgrades.md)＞。  
  
 如需詳細資訊，請參閱[從命令提示字元安裝 SQL Server 2014](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
  
