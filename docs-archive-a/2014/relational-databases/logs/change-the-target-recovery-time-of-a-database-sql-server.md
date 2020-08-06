---
title: 變更資料庫的目標復原時間 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: e466419a-d8a4-48f7-8d97-13a903ad6b15
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4c4331d2ade2819d172189a0de9daddecf3d9f6b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594548"
---
# <a name="change-the-target-recovery-time-of-a-database-sql-server"></a>變更資料庫的目標復原時間 (SQL Server)
  本主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中設定或變更 [!INCLUDE[tsql](../../includes/tsql-md.md)]資料庫的目標復原時間。 根據預設，目標復原時間為 0，而且資料庫會使用 *「自動檢查點」* (Automatic Checkpoint) (由 **recovery interval** 伺服器選項控制)。 如果將目標復原時間設定為大於 0，就會導致資料庫使用 *「間接檢查點」* (Indirect-Checkpoint) 並且建立這個資料庫的復原時間上限。  
  
> [!NOTE]  
>  如果長時間執行的交易造成過多的復原次數，可能會超過目標復原時間設定針對給定資料庫所指定的上限。  
  
-   **開始之前：** [限制事項](#Restrictions)、[安全性](#Security)  
  
-   **使用以下方式變更目標復原時間：** [SQL Server Management Studio](#SSMSProcedure) 或 [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a>  
  
> [!CAUTION]  
>  設定間接檢查點的資料庫線上交易式工作負載可能會導致效能降低。 間接檢查點可確定中途分頁的數目，低於特定臨界值，如此即可在目標復原時間內完成資料庫的復原。 復原間隔組態選項會使用異動數目來判斷復原時間，而間接檢查點則是會利用中途分頁數目來判斷復原時間。 在收到大量 DML 作業的資料庫上啟用間接檢查點時，背景寫入器可開始積極排清磁碟的中途緩衝區，以確保執行復原所需的時間，落在資料庫所設的目標復原時間內。 如此會在某些系統上造成額外的 I/O 活動，而若磁碟子系統的運作超過或接近 I/O 臨界值，就會形成效能瓶頸。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料庫的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要變更目標復原時間**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下您想要變更的資料庫，然後按一下 [屬性] **** 命令。  
  
3.  在 [資料庫屬性]  對話方塊中按一下 [選項]  頁面。  
  
4.  在 [復原] **** 面板的 [目標復原時間 (秒)] **** 欄位中，指定您想要設定為這個資料庫之復原時間上限的秒數。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要變更目標復原時間**  
  
1.  連接到資料庫所在的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
2.  使用下列 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options)陳述式，如下所示：  
  
     TARGET_RECOVERY_TIME **=** _target_recovery_time_ { SECONDS | MINUTES }  
  
     *目標復原時間*  
     如果大於 0 (預設值)，便指定發生損毀時，指定之資料庫的復原時間上限。  
  
     SECONDS  
     指出 *target_recovery_time* 應以秒數表示。  
  
     MINUTES  
     指出 *target_recovery_time* 應以分鐘數表示。  
  
     下列範例會將 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的目標復原時間設定為 `60` 秒。  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET TARGET_RECOVERY_TIME = 60 SECONDS;  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [資料庫檢查點 &#40;SQL Server&#41;](database-checkpoints-sql-server.md)   
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
  
