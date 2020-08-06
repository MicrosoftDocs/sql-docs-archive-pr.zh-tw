---
title: 完整的資料庫還原 (簡單復原模式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- complete database restores
- database restores [SQL Server], complete database
- restoring databases [SQL Server], complete database
- simple recovery model [SQL Server]
- restoring [SQL Server], database
ms.assetid: 49828927-1727-4d1d-9ef5-3de43f68c026
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 67eee8d7d6f44c9ff83795bf2a8bd612309bf0a5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606924"
---
# <a name="complete-database-restores-simple-recovery-model"></a>完整資料庫還原 (簡單復原模式)
  在完整資料庫還原中，目標是還原整個資料庫。 在還原期間，整個資料庫為離線狀態。 在讓資料庫的任何部分上線之前，所有的資料都必須復原到一致的位置；此時資料庫的所有部分都會回到相同的時間點，而且沒有未認可的交易存在。  
  
 在簡單復原模式下，無法將資料庫還原到特定備份中的特定時間點。  
  
> [!IMPORTANT]  
>  建議您不要附加或還原來源不明或來源不受信任的資料庫。 這些資料庫可能包含惡意程式碼，因此可能執行非預期的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 程式碼，或是修改結構描述或實體資料庫結構而造成錯誤。 使用來源不明或來源不受信任的資料庫之前，請先在非實際執行伺服器的資料庫上執行 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) ，同時檢查資料庫中的程式碼，例如預存程序或其他使用者定義程式碼。  
  

  
> [!NOTE]  
>  如需舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之備份支援的相關資訊，請參閱 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)的＜相容性支援＞一節。  
  
##  <a name="overview-of-database-restore-under-the-simple-recovery-model"></a><a name="Overview"></a> 簡單復原模式下的資料庫備份概觀  
 在簡單復原模式下進行完整資料庫還原只需要一個或兩個 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 陳述式，視是否想要還原差異資料庫備份而定。 如果您只使用完整資料庫備份，則只需要還原最近的備份，如下圖所示。  
  
 ![只還原完整資料庫備份](../../database-engine/media/bnrr-rmsimple1-fulldbbu.gif "只還原完整資料庫備份")  
  
 如果也要使用差異資料庫備份，請還原最近一次完整資料庫備份，但不要復原資料庫，然後才還原最近一次差異資料庫備份，並復原資料庫。 下圖顯示這項程序。  
  
 ![還原完整和差異資料庫備份](../../database-engine/media/bnrr-rmsimple2-diffdbbu.gif "還原完整和差異資料庫備份")  
  
> [!NOTE]  
>  若您想將資料庫備份還原至不同的伺服器執行個體，請參閱 [使用備份與還原複製資料庫](../databases/copy-databases-with-backup-and-restore.md)。  
  
###  <a name="basic-transact-sql-restore-syntax"></a><a name="TsqlSyntax"></a> 基本 Transact-SQL RESTORE 語法  
 用於還原完整資料庫備份的基本 [!INCLUDE[tsql](../../../includes/tsql-md.md)][RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 語法為：  
  
 RESTORE DATABASE *database_name* FROM *backup_device* [ WITH NORECOVERY ]  
  
> [!NOTE]  
>  若您也想還原差異資料庫備份，請使用 WITH NORECOVERY。  
  
 用於還原資料庫備份的基本 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 語法為：  
  
 RESTORE DATABASE *database_name* FROM *backup_device* WITH RECOVERY  
  
###  <a name="example-transact-sql"></a><a name="Example"></a> 範例 &#40;Transact-SQL&#41;  
 下列範例首先顯示如何使用 [BACKUP](/sql/t-sql/statements/backup-transact-sql) 陳述式來建立 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的完整資料庫備份及差異資料庫備份。 此範例接著依序還原這些備份。 資料庫會還原到差異資料庫備份完成時的狀態。  
  
 這個範例顯示在完整資料庫還原實例中，還原順序的一些關鍵選項。 *「還原順序」* (Restore sequence) 包含一個或多個還原作業，會在一個或多個還原階段中移動資料。 會省略與這個檔案還原無關的語法和詳細資料。 為了清楚起見，建議您在復原資料庫時明確指定 RECOVERY 選項，即使它是預設的。  
  
> [!NOTE]  
>  此範例會從設定復原模式為 [的](/sql/t-sql/statements/alter-database-transact-sql) ALTER DATABASE `SIMPLE`陳述式開始進行。  
  
```  
USE master;  
--Make sure the database is using the simple recovery model.  
ALTER DATABASE AdventureWorks2012 SET RECOVERY SIMPLE;  
GO  
-- Back up the full AdventureWorks2012 database.  
BACKUP DATABASE AdventureWorks2012   
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
  WITH FORMAT;  
GO  
--Create a differential database backup.  
BACKUP DATABASE AdventureWorks2012   
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH DIFFERENTIAL;  
GO  
--Restore the full database backup (from backup set 1).  
RESTORE DATABASE AdventureWorks2012   
FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
   WITH FILE=1, NORECOVERY;  
--Restore the differential backup (from backup set 2).  
RESTORE DATABASE AdventureWorks2012   
FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
   WITH FILE=2, RECOVERY;  
GO  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
 **還原完整資料庫備份**  
  
-   [在簡單復原模式下還原資料庫備份 &#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [還原資料庫備份 &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [將資料庫還原到新位置 &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
 **還原差異資料庫備份**  
  
-   [還原差異資料庫備份 &#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)  
  
 **使用 SQL Server 管理物件 (SMO) 還原備份**  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A>  
  

  
## <a name="see-also"></a>另請參閱  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [完整資料庫備份 &#40;SQL Server&#41;](full-database-backups-sql-server.md)   
 [差異備份 &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [備份概觀 &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [還原和復原概觀 &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
  
  
