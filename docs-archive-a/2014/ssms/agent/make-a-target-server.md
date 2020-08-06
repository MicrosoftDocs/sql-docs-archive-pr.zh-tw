---
title: 設為目標伺服器| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.tsxwiz.msx.f1
- sql12.ag.tsxwiz.cover.f1
- sql12.ag.tsxwiz.credentials.f1
- sql12.ag.tsxwiz.complete.f1
helpviewer_keywords:
- Target Server Wizard
- SQL Server Agent jobs, target servers
- target servers [SQL Server], creating
ms.assetid: 13aabe2d-67fe-4c67-8d49-2928dd705b7a
author: stevestein
ms.author: sstein
ms.openlocfilehash: bd60a19234d186bb0912978589fa60fd8e8a8c22
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686756"
---
# <a name="make-a-target-server"></a>設為目標伺服器
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 SQL Server 管理物件 (SMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中設定目標伺服器。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要設定目標伺服器，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 具有與 Proxy 相關聯之步驟的散發式作業，而該 Proxy 是在目標伺服器上的 Proxy 帳戶內容下執行 。 請確保符合以下條件，否則與 Proxy 相關聯之作業步驟將不會從主要伺服器下載至目標：  
  
-   主伺服器登錄子機碼**\ HKEY_LOCAL_MACHINE \software\microsoft\microsoft SQL Server \\ < *instance_name*> \sql server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) 設定為 1 (true) 。 依預設，這個子機碼設為 0 (False)。  
  
-   存在於目標伺服器上的 Proxy 帳戶，而該帳戶名稱與執行作業步驟之主要伺服器上的 Proxy 帳戶名稱相同。  
  
 如果使用 Proxy 帳戶的作業步驟在從主要伺服器下載 Proxy 帳戶至目標伺服器時失敗，您可以在 **msdb** 資料庫的 **sysdownloadlist** 資料表中，檢查 **error_message** 資料行，以了解下列錯誤訊息：  
  
-   「作業步驟需要 Proxy 帳戶，不過目標伺服器上已停用 Proxy 比對。」  
  
     若要解決這個錯誤，請將 **AllowDownloadedJobsToMatchProxyName** 登錄子機碼設為 1。  
  
-   「找不到 Proxy。」  
  
     若要解決這個錯誤，請確定目標伺服器上有 Proxy 帳戶，且帳戶名稱與執行該作業步驟的主要伺服器 Proxy 帳戶相同。  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 這個程序的執行權限預設會授與系統管理員 () 固定伺服器角色的成員。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-make-a-target-server"></a>若要設為目標伺服器  
  
1.  在**物件總管中，** 連接到的實例 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然後展開該實例。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]****、指向 [多重伺服器管理]****，然後按一下 [設為目標伺服器]****。 **[目標伺服器精靈]** 將引導您執行將此伺服器設定為目標伺服器的程序。  
  
3.  從 **[選取主要伺服器]** 頁面選取此目標伺服器將接收作業來源的主要伺服器。  
  
     **挑選伺服器**  
     連接到主要伺服器。  
  
     **此伺服器的描述**  
     鍵入此目標伺服器的描述。 目標伺服器會將此描述上傳至主要伺服器。  
  
4.  從 **[主要伺服器登入認證]** 頁面建立目標伺服器上的新登入 (如有需要)。  
  
     **如有必要，請建立新的登入，並指派存取 MSX 的權限給該登入**  
     如果指定的登入並不存在，就會在目標伺服器上建立新的登入。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-make-a-target-server"></a>若要設為目標伺服器  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例會將目前的伺服器列入 AdventureWorks1 主要伺服器中。 目前伺服器的位置是「第 21 棟，309 室，機架 5」。  
  
    ```sql
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
        N'Building 21, Room 309, Rack 5' ;   
    GO;  
    ```  
  
     如需詳細資訊，請參閱[sp_msx_enlist &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)。  
  
##  <a name="using-sql-server-management-objects-smo"></a><a name="PowerShellProcedure"></a>使用 SQL Server 管理物件 (SMO)   
  
## <a name="see-also"></a>另請參閱  
 [將整個企業的管理自動化](automated-administration-across-an-enterprise.md)  
