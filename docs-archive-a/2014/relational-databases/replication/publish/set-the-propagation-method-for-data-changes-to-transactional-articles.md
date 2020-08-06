---
title: 設定對交易式發行項之資料變更的傳播方法 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, propagation methods
- propagating data changes [SQL Server replication]
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a3f8be8b6df1034b06d0aaff6ee61c0c494833c5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87702706"
---
# <a name="set-the-propagation-method-for-data-changes-to-transactional-articles"></a>設定對交易式發行項之資料變更的傳播方法
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，針對 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中交易式發行項的資料變更設定傳播方法。  
  
 根據預設，異動複寫會針對各發行項使用一組預存程序將變更傳遞至「訂閱者」。 您也可以使用自訂程序取代這些程序。 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要針對交易式發行項的資料變更設定傳播方法，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## <a name="before-you-begin"></a>開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   編輯複寫所產生的任何快照集檔案時必須特別小心。 您必須在自訂預存程序中測試並支援自訂邏輯。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 不提供自訂邏輯的支援。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在 [發行項屬性 - \<Article>] 對話方塊的 [屬性] 索引標籤上指定傳播方法，其可於 [新增發行集精靈] 和 [發行集屬性 - \<Publication>] 對話方塊中取得。 如需使用精靈及存取對話方塊的詳細資訊，請參閱[建立發行集](create-a-publication.md)和[檢視及修改發行集屬性](view-and-modify-publication-properties.md)。  
  
#### <a name="to-specify-the-propagation-method"></a>指定傳遞方法  
  
1.  在 [新增發行集] 精靈的 [發行項] 頁面上，或是在 [發行集屬性 - \<Publication>] 對話方塊中，選取一個資料表，然後按一下 [發行項屬性]。  
  
2.  按一下 **[設定反白顯示資料表發行項的屬性]** 。  
  
3.  在 [發行項屬性 - \<Article>] 對話方塊其 [屬性] 索引標籤的 [陳述式傳遞] 區段中，使用 [INSERT 傳遞格式]、[UPDATE 傳遞格式] 以及 [DELETE 傳遞格式] 功能表，以指定各項作業的傳播方法。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果位於 [發行集屬性 - \<Publication>] 對話方塊中，請按一下 [確定] 以儲存並關閉對話方塊。  
  
#### <a name="to-generate-and-use-custom-stored-procedures"></a>產生及使用自訂預存程序  
  
1.  在 [新增發行集] 精靈的 [發行項] 頁面上，或是在 [發行集屬性 - \<Publication>] 對話方塊中，選取一個資料表，然後按一下 [發行項屬性]。  
  
2.  按一下 **[設定反白顯示資料表發行項的屬性]** 。  
  
     在 [發行項屬性 - \<Article>] 對話方塊的 [屬性] 索引標籤上，於 [陳述式傳遞] 區段中適當的傳遞格式功能表 ([INSERT 傳遞格式]、[UPDATE 傳遞格式] 或 [DELETE 傳遞格式]) 中選取 CALL 語法，然後鍵入要在 [INSERT 預存程序]、[DELETE 預存程序] 或 [UPDATE 預存程序] 中使用的程序名稱。 如需 CALL 語法的詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../transactional/transactional-articles-specify-how-changes-are-propagated.md)中的＜預存程序的 Call 語法＞一節。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  如果位於 [發行集屬性 - \<Publication>] 對話方塊中，請按一下 [確定] 以儲存並關閉對話方塊。  
  
5.  產生發行集的快照集時，其中會包含您在前一個步驟中指定的程序。 這些程序將使用您指定的 CALL 語法，但是會包含複寫使用的預設邏輯。  
  
     產生快照集之後，導覽至這個發行項所屬發行集的快照集資料夾，並尋找與該發行項同名的 **.sch** 檔。 使用「記事本」或其他文字編輯器開啟這個檔案，尋找插入、更新或刪除預存程序的 CREATE PROCEDURE 命令，然後編輯程序定義以便提供傳遞資料變更所需的任何自訂邏輯。 如果快照集是重新產生的，則必須重新建立自訂程序。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 異動複寫可讓您控制變更要如何從發行者傳播至訂閱者，而且在建立發行項時，可以透過程式設計方式設定此傳播方法，並在稍後使用複寫預存程序加以變更。  
  
> [!NOTE]  
>  您可以針對發生在發行之資料列上的每一種類型的 DML (資料操作語言) 作業 (插入、更新或刪除) 指定不同的傳播方法。  
  
 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
#### <a name="to-create-an-article-that-uses-transact-sql-commands-to-propagate-data-changes"></a>建立使用 Transact-SQL 命令的發行項來傳播資料變更  
  
1.  在發行集資料庫的發行者上，執行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。 針對 **\@publication** 指定發行項所屬的發行集名稱、針對 **\@article** 指定發行項名稱、針對 **\@source_object** 指定發佈的資料庫物件，以及至少針對下列其中一個參數指定 **SQL** 的值：  
  
    -   **\@ins_cmd** - 控制 [INSERT](/sql/t-sql/statements/insert-transact-sql) 命令的複寫。  
  
    -   **\@upd_cmd** - 控制 [UPDATE](/sql/t-sql/queries/update-transact-sql) 命令的複寫。  
  
    -   **\@del_cmd** - 控制 [DELETE](/sql/t-sql/statements/delete-transact-sql) 命令的複寫。  
  
    > [!NOTE]  
    >  當針對以上任何參數指定 **SQL** 的值時，該類型的命令將會以適當的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 命令形式複寫到訂閱者。  
  
     如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  
  
#### <a name="to-create-an-article-that-does-not-propagate-data-changes"></a>建立不會傳播資料變更的發行項  
  
1.  在發行集資料庫的發行者上，執行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。 針對 **\@publication** 指定發行項所屬的發行集名稱、針對 **\@article** 指定發行項名稱、針對 **\@source_object** 指定發佈的資料庫物件，以及至少針對下列其中一個參數指定 **NONE** 的值：  
  
    -   **\@ins_cmd** - 控制 [INSERT](/sql/t-sql/statements/insert-transact-sql) 命令的複寫。  
  
    -   **\@upd_cmd** - 控制 [UPDATE](/sql/t-sql/queries/update-transact-sql) 命令的複寫。  
  
    -   **\@del_cmd** - 控制 [DELETE](/sql/t-sql/statements/delete-transact-sql) 命令的複寫。  
  
    > [!NOTE]  
    >  當針對以上任何參數指定 **NONE** 的值時，該類型的命令將不會複寫到訂閱者。  
  
     如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  
  
#### <a name="to-create-an-article-with-user-modified-custom-stored-procedures"></a>使用使用者修改的自訂預存程序建立發行項  
  
1.  在發行集資料庫的發行者上，執行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。 針對 **\@publication** 指定發行項所屬的發行集名稱、針對 **\@article** 指定發行項名稱、針對 **\@source_object** 指定發佈的資料庫物件、針對包含 **0x02** 值 (可自動產生自訂預存程序) 的 **\@schema_option** 位元遮罩指定一個值，以及至少指定下列其中一個參數：  
  
    -   ** \@ ins_cmd** -指定<strong>CALL sp_MSins_*article_name*</strong>的值，其中**_article_name_** **是針對發行項指定的值 \@ **。  
  
    -   ** \@ del_cmd** -指定<strong>CALL sp_MSdel_*article_name* </strong>或<strong>XCALL sp_MSdel_*article_name*</strong>的值，其中**_article_name_** 是針對 _ * 文章 * * 所指定的值 \@ 。  
  
    -   ** \@ upd_cmd** -指定<strong>SCALL sp_MSupd_*article_name*</strong>的值、<strong>呼叫 sp_MSupd_*article_name*</strong>、 <strong>XCALL sp_MSupd__article_name *</strong> 或<strong>MCALL sp_MSupd_* article_name *</strong>，其中_**article_name**_ 是針對發行項指定的值** \@ **。  
  
    > [!NOTE]  
    >  您可以針對上述的每一個命令參數，為複寫產生的預存程序指定您自己的名稱。  
  
    > [!NOTE]  
    >  如需 CALL、SCALL、XCALL 和 MCALL 語法的詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
     如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  
  
2.  產生快照集之後，導覽至這個發行項所屬發行集的快照集資料夾，並尋找與該發行項同名的 **.sch** 檔。 使用 Notepad.exe 開啟這個檔案，尋找插入、更新或刪除預存程序的 CREATE PROCEDURE 命令，然後編輯程序定義以便提供傳播資料變更所需的任何自訂邏輯。 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
#### <a name="to-create-an-article-with-custom-scripting-in-the-custom-stored-procedures-to-propagate-data-changes"></a>使用自訂預存程序中的自訂指令碼建立發行項，以傳播資料變更  
  
1.  在發行集資料庫的發行者上，執行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。 針對 **\@publication** 指定發行項所屬的發行集名稱、針對 **\@article** 指定發行項名稱、針對 **\@source_object** 指定發佈的資料庫物件、針對包含 **0x02** 值 (可自動產生自訂預存程序) 的 **\@schema_option** 位元遮罩指定一個值，以及至少指定下列其中一個參數：  
  
    -   ** \@ ins_cmd** -指定<strong>CALL sp_MSins_*article_name*</strong>的值，其中_**article_name**_ **是針對發行項指定的值 \@ **。  
  
    -   ** \@ del_cmd** -指定<strong>CALL sp_MSdel_*article_name* </strong>或<strong>XCALL sp_MSdel_*article_name*</strong>的值，其中_**article_name**_ **是針對發行項指定的值 \@ **。  
  
    -   ** \@ upd_cmd** -指定<strong>SCALL sp_MSupd_*article_name*</strong>的值，<strong>呼叫 sp_MSupd_*article_name*</strong>， <strong>XCALL sp_MSupd_*article_name*</strong>， <strong>MCALL sp_MSupd_*article_name*</strong>，其中_**article_name**_ 是針對發行項指定的**值 \@ **。  
  
    > [!NOTE]  
    >  您可以針對上述的每一個命令參數，為複寫產生的預存程序指定您自己的名稱。  
  
    > [!NOTE]  
    >  如需 CALL、SCALL、XCALL 和 MCALL 語法的詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
     如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  
  
2.  在發行集資料庫的發行者上，使用 [ALTER PROCEDURE](/sql/t-sql/statements/alter-procedure-transact-sql) 陳述式編輯 [sp_scriptpublicationcustomprocs](/sql/relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql) ，好讓它針對插入、更新或刪除自訂預存程序傳回 [CREATE PROCEDURE](/sql/t-sql/statements/create-procedure-transact-sql) 指令碼。 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
#### <a name="to-change-the-method-of-propagating-changes-for-an-existing-article"></a>變更傳播現有發行項之變更的方法  
  
1.  在發行集資料庫的發行者上，執行 [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)。 指定 **\@publication**、 **\@article**，並針對 **\@property** 指定 **ins_cmd**、**upd_cmd**、或 **del_cmd** 的值，以及針對 **\@value** 指定適當的傳播方法。  
  
2.  針對要變更的每一個傳播方法重複步驟 1。  
  
## <a name="see-also"></a>另請參閱  
 [指定交易式發行項變更的傳播方式](../transactional/transactional-articles-specify-how-changes-are-propagated.md)   
 [建立發行集](create-a-publication.md)  
  
  
