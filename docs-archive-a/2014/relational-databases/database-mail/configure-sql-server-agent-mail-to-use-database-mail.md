---
title: 設定 SQL Server Agent Mail 使用 Database Mail | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], SQL Server Agent Mail
- SQL Server Agent Mail
ms.assetid: 4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce
author: stevestein
ms.author: sstein
ms.openlocfilehash: 31d116c0bc8d7e148fc2ef6d2e344400516ad923
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686979"
---
# <a name="configure-sql-server-agent-mail-to-use-database-mail"></a>設定 SQL Server Agent Mail 使用 Database Mail
  本主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中將 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Agent 設定為使用 Database Mail 來傳送通知和警示。  
  
-   **開始之前：**  
  
-   [先決條件](#Prerequisites)  
  
-   [安全性](#Security)  
  
-   [使用 SQL Server Management Studio 將 SQL Server Agent 設定為使用 Database Mail](#SSMSProcedure)  
  
-   [後續工作](#Follow_Up)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
  
-   啟用 Database Mail。  
  
-   對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶建立要使用的 Database Mail 帳戶。  
  
-   建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶要使用的 Database Mail 設定檔，並新增使用者至 **msdb** 資料庫中的 **DatabaseMailUserRole** 。  
  
-   將設定檔設為 **msdb** 資料庫的預設設定檔。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 建立設定檔帳戶以及執行預存程序的使用者，應該是系統管理員 (sysadmin) 固定伺服器角色的成員。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **設定 SQL Server Agent 使用 Database Mail**  
  
-   在 [物件總管] 中，展開 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
-   以滑鼠右鍵按一下 [SQL Server Agent]****，然後按一下 [屬性]****。  
  
-   按一下 **[警示系統]**。  
  
-   選取 **[啟用郵件設定檔]**。  
  
-   在 **[郵件系統]** 清單中，選取 **[Database Mail]**。  
  
-   在 **[郵件設定檔]** 清單中，選取 Database Mail 的郵件設定檔。  
  
-   重新啟動 SQL Server Agent。  
  
##  <a name="follow-up-tasks"></a><a name="Follow_Up"></a> 後續工作  
 需要進行下列工作，才能完成將 Agent 設定為傳送警示和通知的作業。  
  
-   [警示](../../ssms/agent/alerts.md)  
  
     將警示設定為在發生特定資料庫事件或作業系統狀況時通知操作員。  
  
-   [運算子](../../ssms/agent/operators.md)  
  
     操作員是可接收電子通知之人員或群組使用的別名  
  
  
