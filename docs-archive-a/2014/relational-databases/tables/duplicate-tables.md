---
title: 複製資料表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- copying tables
- tables [SQL Server], duplicating
- duplicating tables
- table copying [SQL Server]
ms.assetid: c6b07423-d1e5-4e5e-8681-5088921f5df3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 793a38416f86a5b43a3e3bb2420127d7acf2af1f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593918"
---
# <a name="duplicate-tables"></a>複製資料表
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來建立新的資料表，然後從現有的資料表複製資料行資訊，藉以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中複製現有的資料表。  
  
> [!IMPORTANT]  
>  這個作業只會複製資料表的結構，不會複製任何資料表資料列。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來複製資料表：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要目的地資料庫中的 CREATE TABLE 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-duplicate-a-table"></a>若要複製資料表  
  
1.  請確定已連接至要建立資料表的資料庫，以及已在 [物件總管] 中選取資料庫。  
  
2.  在 [物件總管] 中，以滑鼠右鍵按一下 [資料表]  ，再按一下 [新增資料表]  。  
  
3.  在 [物件總管] 中，以滑鼠右鍵按一下您要複製的資料表，然後按一下 [設計]  。  
  
4.  選取現有資料表中的資料行，再從 **[編輯]** 功能表中按一下 **[複製]** 。  
  
5.  切換回新的資料表，並選取第一列。  
  
6.  從 **[編輯]** 功能表中，按一下 **[貼上]** 。  
  
7.  從 [檔案]  功能表中，按一下 [儲存]  _table name_。  
  
8.  在 **[選擇名稱]** 對話方塊中，輸入新資料表的名稱，並按一下 **[確定]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-duplicate-a-table-in-query-editor"></a>若要在查詢編輯器中複製資料表  
  
1.  請確定已連接至要建立資料表的資料庫，以及已在 [物件總管] 中選取資料庫。  
  
2.  以滑鼠右鍵按一下您想要複製的資料表，並依序指向 [編寫資料表的指令碼為]  和 [CREATE 至]  ，然後選取 [新增查詢編輯器視窗]  。  
  
3.  變更資料表的名稱。  
  
4.  移除新資料表不需要的任何資料行。  
  
5.  按一下 **[執行]** 。  
  
  
