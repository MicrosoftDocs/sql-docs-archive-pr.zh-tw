---
title: 更新資料表對話方塊 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 426c842b85d6404ba101b57a9b572107dbc76bb5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597491"
---
# <a name="update-table-dialog-box-visual-database-tools"></a><span data-ttu-id="d4d54-102">更新資料表對話方塊 (Visual Database Tools)</span><span class="sxs-lookup"><span data-stu-id="d4d54-102">Update Table Dialog Box (Visual Database Tools)</span></span>
  <span data-ttu-id="d4d54-103">這個對話方塊可以讓您指定要更新的資料表。</span><span class="sxs-lookup"><span data-stu-id="d4d54-103">This dialog box allows you to specify the table to be updated.</span></span>  
  
 <span data-ttu-id="d4d54-104">當您將查詢類型變更為更新查詢時，如果 [圖表] 窗格中顯示一個以上的資料表，此對話方塊就會出現。</span><span class="sxs-lookup"><span data-stu-id="d4d54-104">This dialog box appears if more than one table is displayed in the Diagram pane when you change a query's type to be an Update query.</span></span>  
  
 <span data-ttu-id="d4d54-105">選取要更新的資料表，然後選擇 [**確定]**。</span><span class="sxs-lookup"><span data-stu-id="d4d54-105">Select the table to update, and then choose **OK**.\</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="d4d54-106">如果資料表是要發佈以進行複寫，則必須使用 Transact-SQL 陳述式 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) 或 SQL Server 管理物件 (SMO) 變更結構描述。</span><span class="sxs-lookup"><span data-stu-id="d4d54-106">If the table is published for replication, you must make schema changes using the Transact-SQL statement [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) or SQL Server Management Objects (SMO).</span></span> <span data-ttu-id="d4d54-107">使用 [資料表設計工具] 或 [資料庫圖表設計工具] 變更結構描述時，會嘗試卸除並重新建立資料表。</span><span class="sxs-lookup"><span data-stu-id="d4d54-107">When schema changes are made using the Table Designer or the Database Diagram Designer, it attempts to drop and recreate the table.</span></span> <span data-ttu-id="d4d54-108">您無法卸除已發行的物件，因此結構描述變更將會失敗。</span><span class="sxs-lookup"><span data-stu-id="d4d54-108">You cannot drop published objects, therefore the schema change will fail.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d4d54-109">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d4d54-109">See Also</span></span>  
 [<span data-ttu-id="d4d54-110">建立更新查詢 &#40;Visual Database Tools&#41;</span><span class="sxs-lookup"><span data-stu-id="d4d54-110">Create Update Queries &#40;Visual Database Tools&#41;</span></span>](visual-database-tools.md)  
  
  
