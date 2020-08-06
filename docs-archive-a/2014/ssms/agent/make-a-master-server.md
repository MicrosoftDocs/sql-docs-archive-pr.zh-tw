---
title: 設為主要伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.msxwiz.complete.f1
- sql12.ag.msxwiz.target.f1
- sql12.ag.msxwiz.login.f1
- sql12.ag.msxwiz.cover.f1
- sql12.ag.msxwiz.operator.f1
helpviewer_keywords:
- master servers [SQL Server], creating
- wizards [SQL Server Management Studio], Master Server Wizard
- SQL Server Agent jobs, master servers
- Master Server Wizard
ms.assetid: 05739a73-1fdf-4d9d-92a6-70f328380322
author: stevestein
ms.author: sstein
ms.openlocfilehash: ce8e7428aaf8ba459bcf6831988c61da3f192bac
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595358"
---
# <a name="make-a-master-server"></a>設定為主要伺服器
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 設為主要伺服器 [!INCLUDE[tsql](../../includes/tsql-md.md)]。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要設為主要伺服器，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
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
  
#### <a name="to-make-a-master-server"></a>若要設為主要伺服器  
  
1.  在**物件總管中，** 連接到的實例 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然後展開該實例。  
  
2.  以滑鼠右鍵按一下 **[SQL Server Agent]**，指向 **[多重伺服器管理]**，然後按一下 **[設為主要伺服器]**。 **「主要伺服器精靈」** 會引導您完成設定主要伺服器與新增目標伺服器的步驟。  
  
3.  從 [主要伺服器操作員]**** 頁面設定主要伺服器的操作員。若要使用電子郵件或呼叫器傳送通知給操作員，則必須設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來傳送電子郵件。 若要使用 **net send**傳送通知給操作員， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 所在伺服器上必須執行 Messenger 服務。  
  
     **電子郵件地址**  
     設定操作員的電子郵件地址。  
  
     **呼叫器號碼**  
     設定操作員的呼叫器電子郵件地址。  
  
     **Net Send 位址**  
     設定操作員的 **net send** 地址。  
  
4.  從 **[目標伺服器]** 頁面選取主要伺服器的目標伺服器。  
  
     **已註冊的伺服器**  
     列出在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 註冊，但尚未成為目標伺服器的伺服器。  
  
     **目標伺服器**  
     列出目標伺服器。  
  
     **>**  
     將選取的伺服器移動至目標伺服器清單。  
  
     **>>**  
     將所有的伺服器移動至目標伺服器清單。  
  
     **<**  
     將選取的伺服器從目標伺服器清單中移除。  
  
     **<<**  
     將所有的伺服器從目標伺服器清單中移除。  
  
     **加入連接**  
     將伺服器加入目標伺服器清單中，但不註冊伺服器。  
  
     **[連接]**  
     變更選取之伺服器的連接屬性。  
  
5.  從 **[主要伺服器登入認證]** 頁面指定在必要時，是否要為目標伺服器建立新的登入，並指派存取主要伺服器的權限給該登入。  
  
     **如有必要，請建立新的登入，並指派存取 MSX 的權限給該登入**  
     如果指定的登入並不存在，就會在目標伺服器上建立新的登入。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-make-a-master-server"></a>若要設為主要伺服器  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例會將目前的伺服器列入 AdventureWorks1 主要伺服器中。 目前伺服器的位置是「第 21 棟，309 室，機架 5」。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
    N'Building 21, Room 309, Rack 5' ;   
GO;  
```  
  
 如需詳細資訊，請參閱[sp_msx_enlist &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [建立多伺服器環境](create-a-multiserver-environment.md)   
 [將整個企業的管理自動化](automated-administration-across-an-enterprise.md)  
  
  
