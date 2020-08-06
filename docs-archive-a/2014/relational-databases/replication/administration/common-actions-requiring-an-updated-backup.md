---
title: 需要更新之備份的常見動作 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server replication], actions requiring a backup
- restoring [SQL Server replication], actions requiring a backup
- backups [SQL Server replication], actions requiring a backup
ms.assetid: a5975bf4-183e-42e3-b7d1-ad02f89d2e1d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3eb10bdca8ee188f7b322a46665c38129d57052b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687757"
---
# <a name="common-actions-requiring-an-updated-backup"></a>需要更新之備份的常見動作
  如果您執行一般記錄備份，就必須在記錄備份中擷取任何複寫相關的變更。 如果您未執行記錄備份，請在修改複寫結構描述或拓撲之後執行發行、散發、訂閱、 **msdb**和 **master** 資料庫的備份。  
  
## <a name="publication-database"></a>發行集資料庫  
 在下述動作之後備份發行集資料庫：  
  
-   建立新的發行集。  
  
-   變更包含篩選在內的任何發行集屬性。  
  
-   新增發行項 (Article) 至現有的發行集。  
  
-   執行訂閱的發行集全區重新初始化。  
  
-   在已發行的資料表上進行結構描述變更。  
  
-   使用 [sp_addscriptexec &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql)，執行隨選的指令碼。  
  
-   變更任何發行項的屬性。  
  
-   卸除發行集。  
  
-   卸除發行項。  
  
-   停用複寫。  
  
## <a name="distribution-database"></a>散發資料庫  
 在下述動作之後備份散發資料庫：  
  
-   建立或修改複寫代理程式設定檔。  
  
-   修改複寫代理程式設定檔參數。  
  
-   變更發送訂閱的複寫代理程式屬性 (包括排程)。  
  
-   由自動識別範圍管理功能指派新的識別範圍。  
  
## <a name="subscription-database"></a>訂閱資料庫  
 在下述動作之後備份訂閱資料庫：  
  
-   變更訂閱的屬性。  
  
-   變更「發行者」端合併訂閱的優先權。  
  
-   卸除訂閱。  
  
-   停用複寫。  
  
## <a name="msdb-database"></a>msdb 資料庫  
 下述動作後，於適當的節點備份 **msdb** 系統資料庫：  
  
-   啟用或停用複寫。  
  
-   新增或卸除散發資料庫 (於「散發者」處)。  
  
-   啟用或停用發行所使用的資料庫 (於「發行者」處)。  
  
-   建立或修改複寫代理程式設定檔 (於「散發者」處)。  
  
-   修改複寫代理程式設定檔參數 (於「散發者」處)。  
  
-   變更發送訂閱的複寫代理程式屬性 (包括排程) (於「散發者」處)。  
  
-   變更提取訂閱的複寫代理程式屬性 (包括排程) (於「訂閱者」處)。  
  
-   建立與使用可轉換訂閱的交易式發行集相關聯的 DTS 封裝 (於「散發者」和「訂閱者」端)。  
  
-   新增或卸除可轉換訂閱 (於「散發者」和「訂閱者」端)。  
  
## <a name="master-database"></a>master 資料庫  
 下述動作後，於適當的節點備份 **master** 系統資料庫：  
  
-   啟用或停用複寫。  
  
-   新增或卸除散發資料庫 (於「散發者」處)。  
  
-   啟用或停用發行所使用的資料庫 (於「發行者」處)。  
  
-   在任何資料庫中新增第一個或卸除最後一個發行集 (於「發行者」處)。  
  
-   在任何資料庫中新增第一個或卸除最後一個訂閱 (於「訂閱者」處)。  
  
-   啟用或停用「散發發行者」的「發行者」(於「發行者」及「散發者」處)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 資料庫的備份與還原](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [備份及還原複寫的資料庫](back-up-and-restore-replicated-databases.md)  
  
  
