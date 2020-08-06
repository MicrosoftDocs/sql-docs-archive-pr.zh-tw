---
title: 調整作業記錄大小 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- resizing job history log
- size [SQL Server], job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: ddee1ce8-9d1b-4017-9894-bf7256aed95d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4c25cc43295d47b2bc19d48b5b257dbbe6bcfe9b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594327"
---
# <a name="resize-the-job-history-log"></a>調整作業記錄大小
  本主題描述如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用，在中設定 Agent 作業記錄的大小限制 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目設定作業記錄的大小限制：**  
  
     [SQL Server Management Studio](#SSMS)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)＞。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-resize-the-job-history-log-based-on-raw-size"></a>若要根據原始大小調整作業記錄大小  
  
1.  在**物件總管中，** 連接到的實例 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然後展開該實例。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]****，然後按一下 [屬性]****。  
  
3.  選取 [記錄]**** 頁面，然後確認已選取 [限制作業記錄大小]****。  
  
4.  在 **[最大作業記錄大小]** 方塊中，輸入作業記錄所允許的最大資料列數。  
  
5.  在 **[每項作業的作業記錄最大資料列數]** 方塊中，輸入作業所允許的最大作業記錄資料列數。  
  
#### <a name="to-resize-the-job-history-log-based-on-time"></a>若要根據時間調整作業記錄大小  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]****，然後按一下 [屬性]****。  
  
3.  選取 **[記錄]** 頁面，然後按一下 **[自動移除代理程式記錄]**。  
  
4.  選取適當的 [天]****、[週]**** 或 [月]**** 數。  
  
  
