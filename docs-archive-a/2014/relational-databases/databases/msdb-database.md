---
title: msdb 資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 11/10/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, msdb database
- alerts [SQL Server], msdb database
- jobs [SQL Server], msdb database
- msdb database [SQL Server]
ms.assetid: 5032cb2d-65a0-40dd-b569-4dcecdd58ceb
author: stevestein
ms.author: sstein
ms.openlocfilehash: e1d552efa888b24e0a1c83464c7947343b132b1c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686974"
---
# <a name="msdb-database"></a>msdb 資料庫
  **msdb** 資料庫供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 用來設定警示和作業排程，以及供 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 和 Database Mail 等其他功能使用。  
  
 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動在 **msdb**的資料表中維護一份完整的線上備份和還原記錄。 此資訊包括執行備份者的名稱、備份時間，以及在其中儲存備份的裝置或檔案。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會使用此資訊來提出還原資料庫以及套用任何交易記錄備份的計畫。 即使是以自訂應用程式或協力廠商工具建立備份，所有資料庫的備份事件都會記錄下來。 例如，如果使用會呼叫 SQL Server 管理物件 (SMO) 物件的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 應用程式來執行備份作業，則事件會記錄在 **msdb** 系統資料表、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式記錄檔和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中。 為了協助您保護儲存在 **msdb**中的資訊，我們建議您考慮將 **msdb** 交易記錄放在容錯儲存體上。  
  
 依預設， **msdb** 使用的是簡單復原模式。 如果您使用 [備份與還原記錄](../backup-restore/backup-history-and-header-information-sql-server.md) 資料表，我們建議您針對 **msdb**使用完整復原模式。 如需詳細資訊，請參閱[復原模式 &#40;SQL Server &#41;](../backup-restore/recovery-models-sql-server.md)。 請注意，當您安裝或升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，只要使用 Setup.exe 重建系統資料庫，就會自動將 **msdb** 的復原模式設定為簡單。  
  
> [!IMPORTANT]  
>  進行任何更新 **msdb**的作業 (例如備份或還原任何資料庫) 之後，我們建議您備份 **msdb**。 如需詳細資訊，請參閱[系統資料庫的備份與還原 &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)。  
  
## <a name="physical-properties-of-msdb"></a>msdb 的實體屬性  
 下表列出了 **msdb** 資料與記錄檔的初始組態值。 對於不同版本的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]，這些檔案的大小稍有不同。  
  
|檔案|邏輯名稱|實體名稱|檔案成長|  
|----------|------------------|-------------------|-----------------|  
|主要資料|MSDBData|MSDBData.mdf|以 10% 的比例自動成長，直到磁碟已滿。|  
|Log|MSDBLog|MSDBLog.ldf|以 10% 的比例自動成長，最大至 2 TB。|  
  
 若要移動 **msdb** 資料庫或記錄檔，請參閱 [移動系統資料庫](move-system-databases.md)。  
  
### <a name="database-options"></a>資料庫選項  
 下表列出了 **msdb** 資料庫中每個資料庫選項的預設值，以及是否可修改該選項。 若要檢視這些選項目前的設定，請參閱 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 目錄檢視。  
  
|資料庫選項|預設值|可以修改|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|開啟|否|  
|ANSI_NULL_DEFAULT|OFF|是|  
|ANSI_NULLS|OFF|是|  
|ANSI_PADDING|OFF|是|  
|ANSI_WARNINGS|OFF|是|  
|ARITHABORT|OFF|是|  
|AUTO_CLOSE|OFF|是|  
|AUTO_CREATE_STATISTICS|開啟|是|  
|AUTO_SHRINK|OFF|是|  
|AUTO_UPDATE_STATISTICS|開啟|是|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|是|  
|CHANGE_TRACKING|OFF|否|  
|CONCAT_NULL_YIELDS_NULL|OFF|是|  
|CURSOR_CLOSE_ON_COMMIT|OFF|是|  
|CURSOR_DEFAULT|GLOBAL|是|  
|資料庫可用性選項|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|否<br /><br /> 是<br /><br /> 是|  
|DATE_CORRELATION_OPTIMIZATION|OFF|是|  
|DB_CHAINING|開啟|是|  
|ENCRYPTION|OFF|否|  
|NUMERIC_ROUNDABORT|OFF|是|  
|PAGE_VERIFY|CHECKSUM|是|  
|PARAMETERIZATION|簡單|是|  
|QUOTED_IDENTIFIER|OFF|是|  
|READ_COMMITTED_SNAPSHOT|OFF|否|  
|RECOVERY|簡單|是|  
|RECURSIVE_TRIGGERS|OFF|是|  
|Service Broker 選項|ENABLE_BROKER|是|  
|TRUSTWORTHY|開啟|是|  
  
 如需這些資料庫選項的描述，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)。  
  
## <a name="restrictions"></a>限制  
 您不能在 **msdb** 資料庫上執行下列作業：  
  
-   變更定序。 預設定序是伺服器定序。  
  
-   卸除資料庫。  
  
-   從資料庫卸載**來賓**使用者。  
  
-   啟用異動資料擷取。  
  
-   參與資料庫鏡像。  
  
-   移除主要檔案群組、主要資料檔或記錄檔。  
  
-   重新命名資料庫或主要檔案群組。  
  
-   將資料庫設定為 OFFLINE。  
  
-   將主要檔案群組設為 READ_ONLY。  
  
## <a name="related-content"></a>相關內容  
 [系統資料庫](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [移動資料庫檔案](move-database-files.md)  
  
 [Database Mail](../database-mail/database-mail.md)  
  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
