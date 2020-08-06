---
title: Model 資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- template databases [SQL Server]
- model database [SQL Server], about model databases
- model database [SQL Server]
ms.assetid: 4e4f739b-fd27-4dce-8be6-3d808040d8d7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 298723c5031299b1b105f686e188e1e27cfd758c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709522"
---
# <a name="model-database"></a>Model 資料庫
  **model** 資料庫可做為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上建立之所有資料庫的範本。 因為每次 **啟動時，都會建立** tempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，所以 **model** 資料庫一定要存在於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統中。 **model** 資料庫的完整內容 (包括資料庫選項) 都會複製到新的資料庫。 在啟動期間， **model** 的某些設定也會用於建立新的 **tempdb** ，所以 **model** 資料庫必須一直存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統上。  
  
 新建立的使用者資料庫會使用與 model 資料庫相同的 [復原模式](../backup-restore/recovery-models-sql-server.md) 。 使用者可以設定預設值。 若要了解模型的目前復原模式，請參閱[檢視或變更資料庫的復原模式 &#40;SQL Server &#41;](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)。  
  
> [!IMPORTANT]  
>  如果您使用使用者特定的範本資訊來修改 **model** 資料庫，建議您備份 **model**。 如需詳細資訊，請參閱[系統資料庫的備份與還原 &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)。  
  
## <a name="model-usage"></a>model 使用方式  
 發出 CREATE DATABASE 陳述式時，會複製 **model** 資料庫的內容，來建立資料庫的第一個部分。 新資料庫的剩餘部份則填入空白頁。  
  
 如果您修改 **model** 資料庫，則此後建立的所有資料庫都會繼承那些變更。 例如，您可以設定權限或資料庫選項，或是加入資料表、函數、預存程序之類的物件。 **model** 資料庫的檔案屬性是例外狀況，且已加以忽略 (資料檔案的初始大小除外)。  
  
## <a name="physical-properties-of-model"></a>model 的實體屬性  
 下表列出 **model** 資料檔和記錄檔的初始組態值。 對於不同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這些檔案的大小稍有不同。  
  
|檔案|邏輯名稱|實體名稱|檔案成長|  
|----------|------------------|-------------------|-----------------|  
|主要資料|modeldev|model.mdf|以 10% 的比例自動成長，直到磁碟已滿。|  
|Log|modellog|modellog.ldf|以 10% 的比例自動成長，最大至 2 TB。|  
  
 若要移動 **Model** 資料庫或記錄檔，請參閱 [移動系統資料庫](system-databases.md)。  
  
### <a name="database-options"></a>資料庫選項  
 下表列出 **model** 資料庫中每一個資料庫選項的預設值，以及是否可以修改選項。 若要檢視這些選項目前的設定，請參閱 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 目錄檢視。  
  
|資料庫選項|預設值|可以修改|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|是|  
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
|DB_CHAINING|OFF|否|  
|ENCRYPTION|OFF|否|  
|NUMERIC_ROUNDABORT|OFF|是|  
|PAGE_VERIFY|CHECKSUM|是|  
|PARAMETERIZATION|簡單|是|  
|QUOTED_IDENTIFIER|OFF|是|  
|READ_COMMITTED_SNAPSHOT|OFF|是|  
|RECOVERY|取決於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本<sup>1</sup>|是|  
|RECURSIVE_TRIGGERS|OFF|是|  
|Service Broker 選項|DISABLE_BROKER|否|  
|TRUSTWORTHY|OFF|否|  
  
 <sup>1</sup>若要驗證資料庫目前的復原模式，請參閱[View Or Change a Database 的復原模式 &#40;SQL Server&#41;](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)或[sys.databases &#40;transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)。  
  
 如需這些資料庫選項的描述，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)。  
  
## <a name="restrictions"></a>限制  
 下列作業無法在 **model** 資料庫上執行：  
  
-   加入檔案或檔案群組。  
  
-   變更定序。 預設定序是伺服器定序。  
  
-   變更資料庫擁有者。 **model** 是由 **sa**所擁有。  
  
-   卸除資料庫。  
  
-   從資料庫卸載**來賓**使用者。  
  
-   啟用異動資料擷取。  
  
-   參與資料庫鏡像。  
  
-   移除主要檔案群組、主要資料檔或記錄檔。  
  
-   重新命名資料庫或主要檔案群組。  
  
-   將資料庫設定為 OFFLINE。  
  
-   將主要檔案群組設為 READ_ONLY。  
  
-   使用 WITH ENCRYPTION 選項來建立程序、檢視表或觸發程序。 此加密金鑰會繫結至在其中建立物件的資料庫。 在 **model** 資料庫中建立的加密物件只能用於 **model**。  
  
## <a name="related-content"></a>相關內容  
 [系統資料庫](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [移動資料庫檔案](move-database-files.md)  
  
  
