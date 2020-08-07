---
title: 建立伺服器角色 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverrole.members.f1
- SQL12.SWB.SERVERROLE.GENERAL.F1
- sql12.swb.serverrole.memberships.f1
helpviewer_keywords:
- SERVER ROLE, creating
ms.assetid: 74f19992-8082-4ed7-92a1-04fe676ee82d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 45c3d5bb9c9c7fdae9abe18ab3cb808cae4c1fa1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598786"
---
# <a name="create-a-server-role"></a>建立伺服器角色
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中建立新的伺服器角色。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要建立新的伺服器角色，可使用下列項目：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
 不能將資料庫層級安全性實體授與伺服器角色。 若要建立資料庫角色，請參閱 [CREATE ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-role-transact-sql)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
  
-   需要 CREATE SERVER ROLE 權限或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。  
  
-   此外，也需要登入之 *server_principal* 的 IMPERSONATE、作為 *server_principal*之伺服器角色的 ALTER 權限，或作為 server_principal 之 Windows 群組中的成員資格。  
  
-   當您使用 AUTHORIZATION 選項指派伺服器角色擁有權時，也必須具備下列權限：  
  
    -   若要指派伺服器角色擁有權給另一個登入，則需要該登入的 IMPERSONATE 權限。  
  
    -   若要指派伺服器角色擁有權給另一個伺服器角色，則需要收件者伺服器角色中的成員資格，或該伺服器角色的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-new-server-role"></a>若要建立新的伺服器角色  
  
1.  在 [物件總管] 中，展開要建立新伺服器角色的伺服器。  
  
2.  展開 **[安全性]** 資料夾。  
  
3.  以滑鼠右鍵按一下 [伺服器角色] 資料夾，然後選取 [新增伺服器角色...]。  
  
4.  在 [**新增伺服器角色-**_server_role_name_ ] 對話方塊的 [**一般**] 頁面上，于 [**伺服器角色名稱**] 方塊中輸入新伺服器角色的名稱。  
  
5.  在 **[擁有者]** 方塊中，輸入將擁有新角色之伺服器主體的名稱。 或者，按一下省略符號 **(...)** ，開啟 [選取伺服器登入或角色] 對話方塊。  
  
6.  在 [安全性實體] 底下，選取一或多個伺服器層級安全性實體。 已選取安全性實體時，您可以對這個伺服器角色授與或拒絕該安全性實體的權限。  
  
7.  在 [權限；明確] 方塊中，選取核取方塊，對此伺服器角色授與、以授與選項授與 (grant with grant)，或拒絕所選取安全性實體的權限。 如果不能授與或拒絕所有選取之安全性實體的權限，此權限表示為部分選取。  
  
8.  在 **[成員]** 頁面上，使用 **[加入]** 按鈕，將代表個人或群組的登入加入至新的伺服器角色。  
  
9. 使用者定義的伺服器角色可以是另一個伺服器角色的成員。 在 [成員資格] 頁面上，選取核取方塊，讓目前使用者定義的伺服器角色成為選取之伺服器角色的成員。  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-new-server-role"></a>若要建立新的伺服器角色  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    --Creates the server role auditors that is owned the securityadmin fixed server role.  
    USE master;  
    CREATE SERVER ROLE auditors AUTHORIZATION securityadmin;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-role-transact-sql)。  
  
  
