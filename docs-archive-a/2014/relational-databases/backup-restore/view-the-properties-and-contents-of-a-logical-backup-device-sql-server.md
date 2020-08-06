---
title: 檢視邏輯備份裝置的屬性和內容 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- displaying backup content
- viewing backup content
- database backups [SQL Server], viewing content
- backing up databases [SQL Server], viewing content
- backing up databases [SQL Server], properties
- displaying backup properties
- backup devices [SQL Server], viewing information
- viewing backup properties
- database backups [SQL Server], properties
ms.assetid: 3a309074-e816-454d-b6c3-fcfdde0cbf74
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f2bdf41e3dbda079e3627ff7a7c1c3c78103b728
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87702997"
---
# <a name="view-the-properties-and-contents-of-a-logical-backup-device-sql-server"></a>檢視邏輯備份裝置的屬性和內容 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中檢視邏輯備份裝置的屬性和內容。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目檢視邏輯備份裝置的屬性和內容：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 如需安全性的相關資訊，請參閱 [RESTORE LABELONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-labelonly-transact-sql)。  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本中，取得有關備份組或備份裝置的資訊需要 CREATE DATABASE 權限。 如需詳細資訊，請參閱 [GRANT 資料庫權限 &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-permissions-transact-sql)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>若要檢視邏輯備份裝置的屬性和內容  
  
1.  連線到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體之後，在物件總管中按一下伺服器名稱，以展開伺服器樹狀目錄。  
  
2.  展開 **[伺服器物件]** ，然後展開 **[備份裝置]** 。  
  
3.  按一下裝置，然後以滑鼠右鍵按一下 [屬性]  ，這時會開啟 [備份裝置]  對話方塊。  
  
4.  **[一般]** 頁面會顯示裝置名稱和目的地 (可能是磁帶裝置或檔案路徑)。  
  
5.  在 **[選取頁面]** 窗格中，按一下 **[媒體內容]** 。  
  
6.  右窗格會顯示在下列屬性面板中：  
  
    -   **媒體**  
  
         媒體順序資訊 (如果有的話，則為媒體序號、家族序號及鏡像識別碼) 及媒體建立的日期和時間。  
  
    -   **媒體集**  
  
         媒體集資訊：媒體集名稱和描述 (如果有的話)，以及媒體集的家族數目。  
  
7.  **[備份組]** 方格會顯示媒體集內容的相關資訊。  
  
> [!NOTE]  
>  如需詳細資訊，請參閱 [媒體內容頁面](backup-device-media-contents-page.md)。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>若要檢視邏輯備份裝置的屬性和內容  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  使用 [RESTORE LABELONLY](/sql/t-sql/statements/restore-statements-labelonly-transact-sql) 陳述式。 此範例會傳回 `AdvWrks2008R2Backup` 邏輯備份裝置的資訊。  
  
```sql  
USE AdventureWorks2012 ;  
RESTORE LABELONLY  
   FROM AdvWrks2008R2Backup ;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [backupfilegroup &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfilegroup-transact-sql)   
 [backupfile &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfile-transact-sql)   
 [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [backupmediaset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediaset-transact-sql)   
 [backupmediafamily &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediafamily-transact-sql)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [備份裝置 &#40;SQL Server&#41;](backup-devices-sql-server.md)  
  
  
