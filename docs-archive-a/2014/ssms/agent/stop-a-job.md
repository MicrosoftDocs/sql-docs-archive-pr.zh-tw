---
title: 停止作業 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
ms.assetid: 4249328a-24d8-4284-9d1d-7d04ed90e3d7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 78986e85dd8ee808f5fb621182d903a94bbc5eb7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686749"
---
# <a name="stop-a-job"></a>停止作業
  本主題描述如何停止 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。 作業是 SQL Server Agent 執行的一系列指定動作。  
  
-   **開始之前：** 、  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目停止作業：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   如果作業目前正在執行 **CmdExec** 或 **PowerShell**類型的步驟，則會強制提前結束執行中的處理序 (如 MyProgram.exe)。 提前結束可能造成無法預期的行為，例如，由維持開啟狀態的處理序所使用的檔案。  
  
-   對於多伺服器作業，作業的 STOP 指令會發佈到作業的所有目標伺服器。  
  
###  <a name="security"></a><a name="Security"></a> Security  
 如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)＞。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-stop-a-job"></a>若要停止作業  
  
1.  在**物件總管中，** 連接到的實例 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然後展開該實例。  
  
2.  展開 **[SQL Server Agent]**，再展開 **[作業]**，以滑鼠右鍵按一下要停止的作業，然後按一下 **[停止作業]**。  
  
3.  若要停止多個作業，請以滑鼠右鍵按一下 **[作業活動監視器]**，然後按一下 **[檢視作業活動]**。 在「作業活動監視器」中，選取要停止的作業，以滑鼠右鍵按一下選取範圍，然後按一下 **[停止作業]**。  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> 使用 Transact-SQL  
  
### <a name="to-stop-a-job"></a>若要停止作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```sql
    -- stops a job named Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_stop_job  
        N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_stop_job &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-stop-job-transact-sql)。  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理物件  

### <a name="to-stop-a-job"></a>若要停止作業
  
 使用所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，呼叫 `Stop` 類別的 `Job` 方法。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
