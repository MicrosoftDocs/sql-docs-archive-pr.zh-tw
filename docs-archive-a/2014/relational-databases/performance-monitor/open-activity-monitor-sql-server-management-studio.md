---
title: 開啟活動監視器 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server], setting the refresh interval
- refresh interval for Activity Monitor
- Activity Monitor [SQL Server], opening
- opening Activity Monitor
ms.assetid: 0a6eeb16-f02b-479d-9a60-543e40ebf46b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ea74122ad18a0a1ede5eef1e09684606ca0ce073
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707398"
---
# <a name="open-activity-monitor-sql-server-management-studio"></a>開啟活動監視器 (SQL Server Management Studio)
  本主題描述如何開啟 [活動監視器] 來取得有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序以及這些處理序如何影響目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的資訊。 此外，本主題也描述如何設定 [活動監視器] 的重新整理間隔。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來開啟活動監視器：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
-   **使用下列項目，設定重新整理間隔：**  [SQL Server Management Studio](#Refresh)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
 [活動監視器] 會在監視的執行個體上執行查詢，以便取得 [活動監視器] 顯示窗格的資訊。 當重新整理間隔的設定小於 10 秒時，用來執行這些查詢的時間就可能會影響伺服器效能。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 若要檢視 [活動監視器]，使用者必須擁有 VIEW SERVER STATE 權限。 若要檢視活動監視器的 [資料檔案 I/O] 區段，除了 VIEW SERVER STATE 之外，您也必須具有 CREATE DATABASE、ALTER ANY DATABASE 或 VIEW ANY DEFINITION 權限。  
  
 若要針對處理序執行 KILL 命令，使用者必須是系統管理員 (sysadmin) 或處理序管理員 (processadmin) 固定伺服器角色的成員。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-open-activity-monitor-in-sql-server-management-studio"></a>若要在 SQL Server Management Studio 中開啟活動監視器  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 標準工具列上，按一下 **[活動監視器]**。  
  
2.  在 **[連接到伺服器]** 對話方塊中，選取伺服器名稱和驗證模式，然後按一下 **[連接]**。  
  
 您也可以隨時按下 CTRL+ALT A，藉以開啟 [活動監視器]。  
  
#### <a name="to-open-activity-monitor-in-object-explorer"></a>若要在物件總管中開啟活動監視器  
  
-   在物件總管中，以滑鼠右鍵按一下實例名稱，然後選取 [**活動監視器**]。  
  
#### <a name="to-open-activity-monitor-when-opening-sql-server-management-studio"></a>若要在開啟 SQL Server Management Studio 時開啟活動監視器  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]** 。  
  
2.  在 **[選項]** 對話方塊中，展開 **[環境]**，然後選取 **[一般]**。  
  
3.  在 **[啟動時]** 方塊中，選取 **[開啟物件總管和活動監視器]**。  
  
4.  若要啟動這些變更，請關閉並重新開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
###  <a name="to-set-the-activity-monitor-refresh-interval"></a><a name="Refresh"></a>若要設定活動監視器的重新整理間隔  
  
-   開啟 [活動監視器]。  
  
-   以滑鼠右鍵按一下 [概觀]，選取 [重新整理間隔]，然後選取活動監視器應該用來取得新執行個體資訊的間隔。  
  
  
