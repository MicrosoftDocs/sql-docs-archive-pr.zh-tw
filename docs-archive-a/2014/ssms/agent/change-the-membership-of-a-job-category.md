---
title: 變更作業類別目錄的成員資格 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- members [SQL Server], job categories
ms.assetid: 6a18f7f0-eb50-485f-a9c7-df31ae0f994e
author: stevestein
ms.author: sstein
ms.openlocfilehash: d9ed0db394f63594937ad923734b07fed8050955
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606587"
---
# <a name="change-the-membership-of-a-job-category"></a>變更作業類別的成員資格
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 SQL Server 管理物件，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中變更作業類別目錄的成員資格。  
  
 作業類別目錄可幫助您組織作業，以便於篩選與分組。 您可以建立自己的作業類別目錄。 您還可以變更作業類別目錄中的 Microsoft SQL Server Agent 作業成員資格。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目變更作業類別目錄的成員資格：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)＞。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>變更作業類別目錄的成員資格  
  
1.  在 **[物件總管]** 中，按一下加號展開要編輯作業類別目錄所在的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  以滑鼠右鍵按一下 [作業]**** 資料夾，然後選取 [管理作業類別目錄]****。  
  
4.  在 [管理作業類別目錄 <伺服器名稱>]****__ 對話方塊中，選取要編輯的作業類別目錄，然後按一下 [檢視作業]****。  
  
5.  選取 **[顯示所有作業]** 核取方塊。  
  
6.  若要將作業加入至類別目錄，在主要方格中選取該作業所對應之 **[選取]** 資料行中的核取方塊。 若要移除類別目錄中的作業，請清除該方塊。 完成後，請按一下 **[確定]** 。  
  
7.  關閉 [管理作業類別目錄 <伺服器名稱>]****__ 對話方塊。  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>變更作業類別目錄的成員資格  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```sql
    -- adding a new job category to the "NightlyBackups" job  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @category_name = N'[Uncategorized (Local)]';  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_update_job &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)。  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理物件  
 **變更作業類別目錄的成員資格**  
  
 透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 `JobCategory` 類別。  
