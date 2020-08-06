---
title: 壓縮資料庫 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.shrinkdatabase.f1
helpviewer_keywords:
- shrinking databases
- databases [SQL Server], shrinking
- decreasing database size
- database shrinking [SQL Server]
- reducing database size
ms.assetid: 83afbf74-fd50-4c39-831c-b1f473a50620
author: stevestein
ms.author: sstein
ms.openlocfilehash: 246036bfea6dc8431f878165330f7f0571949897
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686971"
---
# <a name="shrink-a-database"></a>壓縮資料庫
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ， [!INCLUDE[tsql](../../includes/tsql-md.md)]中壓縮資料庫。  
  
 將資料頁面從檔案結尾移到靠近檔案前端的未使用空間，以壓縮資料並復原儲存空間。 當檔案結尾建立了足夠的可用空間後，檔案結尾的資料頁面便可取消配置並返回檔案系統。  
  

  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   資料庫的大小不得小於資料庫的大小下限。 大小下限是最初建立資料庫時所指定的大小，或利用檔案大小變更作業 (如 DBCC SHRINKFILE) 來設定的最後一個明確大小。 例如，如果資料庫最初建立時為 10 MB 的大小，而後擴充到 100 MB，則該資料庫最多只能縮小到 10 MB，即使該資料庫中的所有資料都已刪除，也是如此。  
  
-   資料庫在備份時不能進行壓縮。 相反地，當資料庫上正在進行壓縮作業時，也不能對其進行備份。  
  
-   遇到 xVelocity 記憶體最佳化的資料行存放區索引時，DBCC SHRINKDATABASE 將會失敗。 遇到資料行存放區索引之前完成的工作將會成功，因此資料庫可能會較小。 若要完成 DBCC SHRINKDATABASE，請在執行 DBCC SHRINKDATABASE 前停用所有資料行存放區索引，然後重建資料行存放區索引。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   檢視資料庫中目前的可用 (未配置) 空間量。 如需相關資訊，請參閱 [顯示資料庫的資料和記錄空間資訊](display-data-and-log-space-information-for-a-database.md)  
  
-   當您計畫壓縮資料庫時，請考量下列資訊：  
  
    -   壓縮作業在截斷資料表或卸除資料表等產生大量未用空間的作業之後最有效。  
  
    -   大部分資料庫都需要一些可用空間來執行每天的例行作業。 如果您反覆壓縮資料庫，發現資料庫再次增長，就表示例行作業需要被壓縮的空間。 在這些情況之下，反覆壓縮資料庫是一項會造成浪費的作業。  
  
    -   壓縮作業不會保留資料庫中索引的片段狀態，它通常會使片段增加到某個程度。 這就是不要反覆壓縮資料庫的另一個原因。  
  
    -   除非您有特定的需求，否則請不要將 AUTO_SHRINK 資料庫選項設定為 ON。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要 **系統管理員** 固定伺服器角色或 **db_owner** 固定資料庫角色中的成員資格。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-shrink-a-database"></a>若要壓縮資料庫  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 [資料庫]，然後以滑鼠右鍵按一下您要壓縮的資料庫。  
  
3.  指向 **[工作]** 的 **[壓縮]** ，然後按一下 **[資料庫]** 。  
  
     **Database**  
     顯示選取之資料庫的名稱。  
  
     **目前配置的空間**  
     顯示選取之資料庫的總計已使用和未使用的空間。  
  
     **可用空間**  
     顯示選取之資料庫的記錄檔和資料檔中可用空間的總和。  
  
     **釋放未使用的空間之前，先重新組織檔案**  
     選取這個選項相當於執行 DBCC SHRINKDATABASE 指定目標百分比選項。 清除此選項相當於搭配 TRUNCATEONLY 選項執行 DBCC SHRINKDATABASE。 依預設，開啟對話方塊時並不會選取此選項。 如果選取此選項，使用者必須指定目標百分比選項。  
  
     **壓縮後檔案的最大可用空間**  
     輸入在資料庫壓縮後，資料庫檔案中剩餘可用空間的最大百分比。 允許值介於 0 和 99 之間。  
  
4.  按一下 [確定]。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-shrink-a-database"></a>若要壓縮資料庫  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例會使用 [DBCC SHRINKDATABASE](/sql/t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql) 縮小 `UserDB` 資料庫中的資料和記錄檔大小，使資料庫中能有 `10` % 的可用空間。  
  
 [!code-sql[DBCC#DBCC_SHRINKDB1](../../snippets/tsql/SQL14/tsql/dbcc/transact-sql/dbcc_other.sql#dbcc_shrinkdb1)]  
  
##  <a name="follow-up-after-you-shrink-a-database"></a><a name="FollowUp"></a> 後續操作：壓縮資料庫之後  
 為壓縮檔案所移動的資料可散佈至檔案中的任何可用位置。 如此會造成索引片段，並可能導致大範圍之索引搜尋的查詢效能變慢。 若要消除資料片段，可考慮在壓縮之後重建該檔案的索引。  
  
## <a name="see-also"></a>另請參閱  
 [壓縮檔案](shrink-a-file.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [DBCC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)   
 [DBCC SHRINKFILE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-shrinkfile-transact-sql)   
 [資料庫檔案與檔案群組](database-files-and-filegroups.md)  
  
  
