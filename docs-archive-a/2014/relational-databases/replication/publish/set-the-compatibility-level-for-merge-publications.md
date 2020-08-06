---
title: 設定合併式發行集的相容性層級 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], replication
- backward compatibility [SQL Server], replication
- publications [SQL Server replication], backward compatibility
ms.assetid: db47ac73-948b-4d77-b272-bb3565135ea5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 04ad80b0c99e7282ff2acfa459a08665efbdee1c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606753"
---
# <a name="set-the-compatibility-level-for-merge-publications"></a>設定合併式發行集的相容性層級
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中設定合併式發行集的相容性層級。 合併式複寫使用發行集相容性層級，來確定發行集可在給定資料庫中使用的功能。  
  
 **本主題內容**  
  
-   **若要設定合併式發行集的相容性層級，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在「新增發行集精靈」的 **[訂閱者類型]** 頁面中設定相容性層級。 如需存取此精靈的詳細資訊，請參閱＜ [Create a Publication](create-a-publication.md)中設定合併式發行集的相容性層級。 建立發行集快照集後，可以提高相容性層級，但不能降低。 您可在 [發行集屬性 - \<Publication>] 對話方塊的 [一般] 頁面上增加相容性層級。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](view-and-modify-publication-properties.md)＞。 如果提高發行集的相容性層級，則對於執行相容性層級之前版本的伺服器，其上的所有現有訂閱均無法再同步處理。  
  
> [!NOTE]  
>  因為相容性層級對其他發行集屬性有影響，並且發行項屬性對其有效，所以不要變更相容性層級以及對話方塊中相同用途的其他屬性。 發行集的快照集應在變更屬性後重新產生。  
  
#### <a name="to-set-the-publication-compatibility-level"></a>若要設定發行集相容性層級  
  
-   在「新增發行集精靈」的 **[訂閱者類型]** 頁面中，選取發行集應支援的「訂閱者」類型。  
  
#### <a name="to-increase-the-publication-compatibility-level"></a>若要提高發行集相容性層級  
  
-   您可在 [發行集屬性 - \<Publication>] 對話方塊的 [一般] 頁面上選取 [相容性層級]。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 合併式發行集的相容性層級可以在建立發行集時以程式設計方式加以設定，或是在之後以程式設計方式加以修改。 您可以使用複寫預存程序來設定或變更此發行集屬性。  
  
#### <a name="to-set-the-publication-compatibility-level-for-a-merge-publication"></a>設定合併式發行集的發行集相容性層級  
  
1.  在發行者上，執行[sp_addmergepublication &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)，指定的值， **@publication_compatibility_level** 讓發行集與舊版相容 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱[建立發行集](create-a-publication.md)。  
  
#### <a name="to-change-the-publication-compatibility-level-of-a-merge-publication"></a>變更合併式發行集的發行集相容性層級  
  
1.  執行[sp_changemergepublication &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)，指定的**publication_compatibility_level** **@property** 和的適當發行集相容性層級 **@value** 。  
  
#### <a name="to-determine-the-publication-compatibility-level-of-a-merge-publication"></a>判斷合併式發行集的發行集相容性層級  
  
1.  執行 [sp_helpmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)，指定所需的發行集。  
  
2.  在結果集的 **backward_comp_level** 欄中尋找發行集相容性層級。  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例會建立合併式發行集，並設定發行集相容性層級。  
  
```  
-- To avoid storing the login and password in the script file, the values   
-- are passed into SQLCMD as scripting variables. For information about   
-- how to use scripting variables on the command line and in SQL Server  
-- Management Studio, see the "Executing Replication Scripts" section in  
-- the topic "Programming Replication Using System Stored Procedures".  
  
--Add a new merge publication.  
DECLARE @publicationDB AS sysname;  
DECLARE @publication AS sysname;  
DECLARE @login AS sysname;  
DECLARE @password AS sysname;  
SET @publicationDB = N'AdventureWorks2012';   
SET @publication = N'AdvWorksSalesOrdersMerge'   
SET @login = $(Login);  
SET @password = $(Password);  
  
-- Create a new merge publication.   
USE [AdventureWorks2012]  
EXEC sp_addmergepublication   
@publication = @publication,   
-- Set the compatibility level to SQL Server 2014.  
@publication_compatibility_level = '120RTM';   
  
-- Create the snapshot job for the publication.  
EXEC sp_addpublication_snapshot   
@publication = @publication,  
@job_login = @login,  
@job_password = @password;  
GO  
```  
  
 此範例會變更合併式發行集的發行集相容性層級。  
  
> [!NOTE]  
>  如果發行集使用任何需要特定相容性層級的功能，則可能不允許變更發行集相容性層級。 如需詳細資訊，請參閱[複寫回溯相容性](../replication-backward-compatibility.md)。  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
  
-- Change the publication compatibility level to   
-- SQL Server 2012.  
EXEC sp_changemergepublication   
@publication = @publication,   
@property = N'publication_compatibility_level',   
@value = N'110RTM';  
GO  
  
```  
  
 此範例會傳回合併式發行集的正確發行集相容性層級。  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
EXEC sp_helpmergepublication   
@publication = @publication;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立發行集](create-a-publication.md)  
  
  
