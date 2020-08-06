---
title: 停用複寫的外部索引鍵條件約束 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- constraints [SQL Server], foreign keys
- foreign keys [SQL Server], disabling constraints
- disabling constraints
ms.assetid: 4211f2fd-d16a-4081-995c-43f1f0827f0b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4ee7f2fb7b0a27870a09a9d99b723b7faf739aeb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594967"
---
# <a name="disable-foreign-key-constraints-for-replication"></a>停用複寫的外部索引鍵條件約束
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中停用複寫的外部索引鍵條件約束。 這有助於從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行資料。  
  
> [!NOTE]  
>  如果使用複寫發行資料表，則會自動停用複寫代理程式所執行作業的外部索引鍵條件約束。 當複寫代理程式在訂閱者端執行插入、更新或刪除時，不會檢查條件約束；如果使用者執行插入、更新或刪除，則會檢查條件約束。 停用複製代理程式的條件約束，是因為原本插入、更新或刪除資料時，就已在發行者端檢查過條件約束。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **使用下列方法，停用複寫的外部索引鍵條件約束：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料表的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>停用複寫的外部索引鍵條件約束  
  
1.  在 **[物件總管]** 中，展開您要修改其外部索引鍵條件約束的資料表，然後展開 **[索引鍵]** 資料夾。  
  
2.  以滑鼠右鍵按一下外部索引鍵條件約束，然後按一下 [修改]  。  
  
3.  在 **[外部索引鍵關聯性]** 對話方塊中，針對 **[強制複寫]** 選取 **[否]** 值。  
  
4.  按一下 [關閉]  。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>停用複寫的外部索引鍵條件約束  
  
1.  若要在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中執行此工作，請卸除外部索引鍵條件約束。 然後加入新的外部索引鍵條件約束，並指定 NOT FOR REPLICATION 選項。  
  
 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)。  
  
###  <a name="TsqlExample"></a>  
