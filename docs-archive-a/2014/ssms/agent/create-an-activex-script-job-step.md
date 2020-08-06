---
title: 建立 ActiveX Script 指令碼作業步驟 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- ActiveX scripting jobs [SQL Server]
- job steps [Analysis Services]
ms.assetid: e6c46c6b-2d61-4571-bc8e-a831cd6e6302
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6604ba75af7acdd5bd2521433e8310c74150ce8f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686757"
---
# <a name="create-an-activex-script-job-step"></a>Create an ActiveX Script Job Step
  本主題描述如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 、或 SQL Server 管理物件，在中建立和定義執行 ActiveX script 的 Agent 作業步驟 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目建立 Transact-SQL 作業步驟：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理物件](#SMO)  
  
## <a name="before-you-begin"></a>開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
###  <a name="security"></a><a name="Security"></a> Security  
 如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)＞。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-an-activex-script-job-step"></a>若要建立 ActiveX 指令碼作業步驟  
  
1.  在**物件總管中，** 連接到的實例 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然後展開該實例。  
  
2.  展開 **SQL Server Agent**，建立新作業或以滑鼠右鍵按一下現有作業，然後按一下 [屬性]****。 如需建立作業的詳細資訊，請參閱＜ [建立作業](create-jobs.md)＞。  
  
3.  在 **[作業屬性]** 方塊中，按一下 **[步驟]** 頁面，然後按一下 **[新增]**。  
  
4.  在 **[新增作業步驟]** 對話方塊中，輸入一個作業 **步驟名稱**。  
  
5.  在 **[類型]** 清單中，按一下 **[ActiveX Script]**。  
  
6.  在 **[執行身分]** 清單中，選取具有作業將會使用之認證的 Proxy 帳戶。  
  
7.  選取當初撰寫指令碼所用的 **[語言]** 。 或者，按一下 **[其他]** ，然後輸入將用來撰寫指令碼的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX 指令碼語言的名稱。  
  
8.  在 **[命令]** 方塊中，輸入將為作業步驟執行的指令碼語法。 或者，請按一下 **[開啟舊檔]** ，然後選取包含指令碼語法的檔案。  
  
9. 按一下 **[進階]** 頁面，設定下列作業步驟選項：作業步驟成功或失敗時要採取什麼動作、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 應該嘗試執行作業步驟多少次，以及應該多久重試一次。  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-create-an-activex-script-job-step"></a>若要建立 ActiveX 指令碼作業步驟  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```sql
    -- create an ActiveX Script job step written in VBScript that creates a restore point  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Create a restore point',  
        @subsystem = N'ACTIVESCRIPTING',  
        @command = N'Const RESTORE_POINT = 20  
  
    strComputer = "."  
    Set objWMIService = GetObject("winmgmts:" _  
        & "{impersonationLevel=impersonate}!\\" & strComputer & "\root\default")  
  
    Set objItem = objWMIService.Get("SystemRestore")  
    errResults = objItem.Restore(RESTORE_POINT)',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_add_jobstep &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)。  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理物件  
 **若要建立 ActiveX 指令碼作業步驟**  
  
 透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 `JobStep` 類別。  
