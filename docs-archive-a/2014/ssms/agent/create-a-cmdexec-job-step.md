---
title: 建立 CmdExec 作業步驟 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CmdExec jobs
ms.assetid: b48da5b4-6fe7-4eb7-bade-dc7d697c6d5c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 48c557b8ea4228d27b73d361c50aac62232d1e00
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595359"
---
# <a name="create-a-cmdexec-job-step"></a>建立 CmdExec 作業步驟
  本主題描述如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用或 SQL Server 管理物件，在中建立和定義 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用可執行程式或作業系統命令的 Agent 作業步驟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目建立 CmdExec 作業步驟：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 根據預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員可以建立 CmdExec 作業步驟。 這些作業步驟會以 SQL Server Agent 服務帳戶的身分執行，除非 **系統管理員 (sysadmin)** 使用者建立 Proxy 帳戶。 如果使用者不是 **系統管理員 (sysadmin)** 角色的成員，則必須能夠存取 CmdExec Proxy 帳戶，才能建立 CmdExec 作業步驟。  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)＞。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-cmdexec-job-step"></a>建立 CmdExec 作業步驟  
  
1.  在**物件總管中，** 連接到的實例 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然後展開該實例。  
  
2.  展開 **SQL Server Agent**，建立新作業或以滑鼠右鍵按一下現有作業，然後按一下 [屬性]****。  
  
3.  在 **[作業屬性]** 方塊中，按一下 **[步驟]** 頁面，然後按一下 **[新增]**。  
  
4.  在 **[新增作業步驟]** 對話方塊中，輸入一個作業 **步驟名稱**。  
  
5.  在 [類型]**** 清單中，選擇 [作業系統 (CmdExec)]****。  
  
6.  在 **[執行身分]** 清單中，選取具有作業將會使用之認證的 Proxy 帳戶。 根據預設，CmdExec 作業步驟會以 SQL Server Agent 服務帳戶的身分執行。  
  
7.  在 **[成功命令的處理序結束碼]** 方塊中，輸入介於 0 到 999999 之間的值。  
  
8.  **** 在 [命令]方塊中，輸入作業系統命令或可執行的程式。 如需範例，請參閱＜使用 Transact-SQL＞。  
  
9. 按一下 **[進階]** 頁面設定作業步驟選項，例如：作業步驟成功或失敗時要採取什麼動作、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 應該嘗試執行作業步驟多少次，以及可供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 寫入作業步驟輸出的檔案。 只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，可以將作業步驟輸出寫入作業系統檔案。  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> 使用 Transact-SQL  
  
### <a name="to-create-a-cmdexec-job-step"></a>建立 CmdExec 作業步驟  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```sql
    -- creates a job step that uses CmdExec  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'CMDEXEC',  
        @command = C:\clickme_scripts\SQL11\PostBOLReorg GetHsX.exe',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_add_jobstep &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理物件  

### <a name="to-create-a-cmdexec-job-step"></a>建立 CmdExec 作業步驟
  
 透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 `JobStep` 類別。  
