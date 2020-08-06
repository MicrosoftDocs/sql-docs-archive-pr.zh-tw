---
title: 建立資料庫使用者 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.DATABASEUSER.GENERAL.F1
- sql12.swb.user.securables.f1
helpviewer_keywords:
- database users, creating
- creating users with Management Studio
- mapping users
- users [SQL Server], creating
- database user additions [SQL Server]
- database users, mapping
- CREATE USER [Management Studio]
- users [SQL Server], adding
- mapping database users
ms.assetid: 782798d3-9552-4514-9f58-e87be4b264e4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 97fc758c754f5fc8803e988d55147670fc3ff45b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87697762"
---
# <a name="create-a-database-user"></a>建立資料庫使用者
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中建立對應到登入的資料庫使用者。 連接到資料庫時，資料庫使用者是登入的識別。 資料庫使用者可以使用相同的名稱做為登入，但是並非必要。 本主題假設 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中已有登入存在。 如需如何建立登入的詳細資訊，請參閱[建立登](create-a-login.md)入。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [背景](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目建立資料庫使用者：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="background"></a><a name="Restrictions"></a> 背景  
 使用者是資料庫層級的安全性主體。 登入必須對應到資料庫使用者，才能連接到資料庫。 登入可以做為不同的使用者對應到不同的資料庫，但在每一個資料庫中只能對應為一位使用者。 在部分自主資料庫中，可以建立沒有登入的使用者。 如需自主資料庫使用者的詳細資訊，請參閱 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)。 如果資料庫中啟用 guest 使用者，則未對應到資料庫使用者的登入就可以用 guest 使用者的身分進入資料庫。  
  
> [!IMPORTANT]  
>  guest 使用者通常為停用狀態。 除非必要，否則不要啟用 guest 使用者。  
  
 使用者做為安全性主體時，可以將權限授與使用者。 使用者的範圍為資料庫。 若要連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體上的特定資料庫，則登入必須對應到資料庫使用者。 資料庫內的權限是對資料庫使用者授與或拒絕，而不是登入。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料庫的 `ALTER ANY USER` 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
##### <a name="to-create-a-database-user"></a>若要建立資料庫使用者  
  
1.  在 [物件總管] 中，展開 **[資料庫]** 資料夾。  
  
2.  展開要建立新資料庫使用者的資料庫。  
  
3.  以滑鼠右鍵按一下 [安全性] 資料夾，指向 [新增]，然後選取 [使用者...]。  
  
4.  在 [**資料庫使用者-新增**] 對話方塊的 [**一般**] 頁面上，從 [**使用者類型**] 清單中選取下列其中一個使用者類型： [**具有登**入的 sql 使用者]、[**沒有登**入的 sql 使用者]、[**對應到憑證**的使用者]、[**對應到非對稱金鑰**的使用者] 或 [ **Windows 使用者**]。  
  
5.  在 **[使用者名稱]** 方塊中，輸入新使用者的名稱。 如果您已經從 [使用者類型] 清單中選擇 [Windows 使用者]，也可以按一下省略符號 **(...)** 開啟 [選取使用者或群組] 對話方塊。  
  
6.  在 **[登入名稱]** 方塊中，輸入使用者的登入。 或者，按一下省略符號 **(...)** ，開啟 [選取登入] 對話方塊。 如果您從 **[使用者類型]** 清單中選取 **[有登入的 SQL 使用者]** 或 **[Windows 使用者]** ， **[登入名稱]** 就是可用的。  
  
7.  在 **[預設結構描述]** 方塊中，指定擁有此使用者建立的物件之結構描述。 或者，按一下省略符號 **(...)** ，開啟 [選取結構描述] 對話方塊。 如果您從 **[使用者類型]** 清單中選取 **[有登入的 SQL 使用者]** , **[沒有登入的 SQL 使用者]** 或 **[Windows 使用者]** ， **[預設結構描述]** 就是可用的。  
  
8.  在 **[憑證名稱]** 方塊中，輸入要用於資料庫使用者的憑證。 或者，按一下省略符號 **(...)** ，開啟 [選取憑證] 對話方塊。 如果您從 **[使用者類型]** 清單中選取 **[對應到憑證的使用者]** ， **[憑證名稱]** 就是可用的。  
  
9. 在 **[非對稱金鑰名稱]**  方塊中，輸入要用於資料庫使用者的金鑰。 或者，按一下省略符號 **(...)** ，開啟 [選取非對稱金鑰] 對話方塊。 如果您從 **[使用者類型]** 清單中選取 **[對應到非對稱金鑰的使用者]** ， **[非對稱金鑰名稱]** 就是可用的。  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>其他選項  
 [資料庫使用者 - 新增] 對話方塊也會在其他四個頁面上提供選項：[自有結構描述]、[成員資格]、[安全性實體] 和 [延伸屬性]。  
  
-   **[擁有的結構描述]** 頁面列出新資料庫使用者可擁有的所有可能結構描述。 若要在資料庫使用者中加入或移除結構描述，請在 **[這個使用者擁有的結構描述]** 底下選取或清除結構描述旁邊的核取方塊。  
  
-   **[成員資格]** 頁面列出新資料庫使用者可擁有的所有可能的資料庫角色成員資格。 若要在資料庫使用者中加入或移除角色，請在 **[資料庫角色成員資格]** 底下選取或清除角色旁邊的核取方塊。  
  
-   **[安全性實體]** 頁面列出所有可能的安全性實體以及可授與登入的安全性實體權限。  
  
-   **[擴充屬性]** 頁面讓您能夠將自訂屬性加入至資料庫使用者。 此頁面提供下列選項。  
  
     **Database**  
     顯示選取之資料庫的名稱。 此欄位是唯讀的。  
  
     **定序**  
     顯示用於所選取資料庫的定序。 此欄位是唯讀的。  
  
     **屬性**  
     檢視或指定物件的擴充屬性。 每個擴充屬性都包含與物件相關聯的一對名稱/值中繼資料。  
  
     **省略符號 (...)**  
     按一下 [值] 後面的省略符號 **(...)** ，開啟 [擴充屬性的值] 對話方塊。 在這個較大的位置輸入或檢視擴充屬性的值。 如需詳細資訊，請參閱＜ [擴充屬性的值對話方塊](../../databases/value-for-extended-property-dialog-box.md)＞。  
  
     **刪除**  
     移除選取的擴充屬性。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-database-user"></a>若要建立資料庫使用者  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- Creates the login AbolrousHazem with password '340$Uuxwp7Mcxo7Khy'.  
    CREATE LOGIN AbolrousHazem   
        WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
    GO  
  
    -- Creates a database user for the login created above.  
    CREATE USER AbolrousHazem FOR LOGIN AbolrousHazem;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [主體 &#40;Database Engine&#41;](principals-database-engine.md)  
  
  
