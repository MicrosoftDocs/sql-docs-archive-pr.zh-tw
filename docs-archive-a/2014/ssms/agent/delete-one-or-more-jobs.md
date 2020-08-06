---
title: 刪除一個或多個作業 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, deleting
- dropping jobs
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 67dcdad0-57b2-431c-b77f-4ffc926af93d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 436625f9ad629a6b0e574aa046059f4e7e9c2bf2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585758"
---
# <a name="delete-one-or-more-jobs"></a>刪除一個或多個作業
  本主題描述如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 、或 SQL Server 管理物件，在中刪除 Agent 作業 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 除非您是 **系統管理員 (sysadmin)** 固定伺服器角色的成員，否則您只能刪除您擁有的作業步驟。  
  
 
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-job"></a>若要刪除作業  
  
1.  在**物件總管中，** 連接到的實例 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然後展開該實例。  
  
2.  展開 **[SQL Server Agent]**，展開 **[作業]**，以滑鼠右鍵按一下要刪除的作業，然後按一下 **[刪除]**。  
  
3.  在 **[刪除物件]** 對話方塊中，確認已選取您要刪除的作業。  
  
4.  按一下 [確定]  。  
  
#### <a name="to-delete-multiple-jobs"></a>若要刪除多個作業  
  
1.  在**物件總管中，** 連接到的實例 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然後展開該實例。  
  
2.  展開 **[SQL Server Agent]**。  
  
3.  以滑鼠右鍵按一下 **[作業活動監視器]**，然後按一下 **[檢視作業活動]**。  
  
4.  在「作業活動監視器」中，選取要刪除的作業，以滑鼠右鍵按一下選取範圍，然後選擇 **[刪除作業]**。  
  

  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-job"></a>若要刪除作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```sql
    USE msdb ;  
    GO  
  
    EXEC sp_delete_job  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_delete_job &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-job-transact-sql)。  

##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理物件  

### <a name="to-delete-multiple-jobs"></a>若要刪除多個作業
  
 透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 `JobCollection` 類別。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
