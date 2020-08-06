---
title: 資料庫演進問題 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], multuser database changes
- database evolution [SQL Server]
ms.assetid: 1ed6ae10-d212-4ec2-8569-1b94ab1cba6d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 80daa694cd015a83657368902b07da254e6196ec
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708017"
---
# <a name="issues-of-database-evolution-visual-database-tools"></a><span data-ttu-id="aabda-102">資料庫演進問題 (Visual Database Tools)</span><span class="sxs-lookup"><span data-stu-id="aabda-102">Issues of Database Evolution (Visual Database Tools)</span></span>
  <span data-ttu-id="aabda-103">如果您變更了某部署資料庫的結構，您必須特別注意您的變更是否與現有資料和資料庫結構相容。</span><span class="sxs-lookup"><span data-stu-id="aabda-103">If you change the structure of a deployed database, you must take special care that your alteration is compatible with the existing data and database structure.</span></span> <span data-ttu-id="aabda-104">進行下列修改時您可能必須採取特殊步驟：</span><span class="sxs-lookup"><span data-stu-id="aabda-104">You might need to take special steps when you make the following modifications:</span></span>  
  
-   <span data-ttu-id="aabda-105">**新增條件約束**：如果您新增某樣條件約束，該資料庫可能已含有無法滿足該條件約束的資料。</span><span class="sxs-lookup"><span data-stu-id="aabda-105">**Adding a Constraint** If you add a constraint, the database might already contain data that does not satisfy it.</span></span> <span data-ttu-id="aabda-106">當您儲存新的條件約束時，[儲存後告知對話方塊 &#40;Visual Database Tools&#41;](visual-database-tools.md) 將通知您資料庫伺服器無法建立該條件約束。</span><span class="sxs-lookup"><span data-stu-id="aabda-106">When you try to save the new constraint, the [Post-Save Notifications Dialog Box &#40;Visual Database Tools&#41;](visual-database-tools.md) informs you that the database server could not create the constraint.</span></span> <span data-ttu-id="aabda-107">若要強制資料庫接受新的條件約束，您可以清除 [建立時立即檢查現有資料]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="aabda-107">To force the database to accept the new constraint, you can clear the **Check existing data on creation** check box.</span></span>  
  
-   <span data-ttu-id="aabda-108">**新增關聯性**：如果新增關聯性，該資料庫可能已含有外部索引鍵資料表資料列，該資料列在主索引資料列中並未有對應的資料列。</span><span class="sxs-lookup"><span data-stu-id="aabda-108">**Adding a Relationship** If you add a relationship, the database might already contain rows of the foreign-key table that do not have corresponding rows in the primary-key table.</span></span> <span data-ttu-id="aabda-109">也就是說，現有資料可能無法滿足參考完整性。</span><span class="sxs-lookup"><span data-stu-id="aabda-109">That is, the existing data might not satisfy referential integrity.</span></span> <span data-ttu-id="aabda-110">當您儲存新的關聯性時，[儲存後告知對話方塊 &#40;Visual Database Tools&#41;](visual-database-tools.md) 將通知您資料庫伺服器無法儲存修改過的外部索引鍵資料表。</span><span class="sxs-lookup"><span data-stu-id="aabda-110">When you try to save the new relationship, the[Post-Save Notifications Dialog Box &#40;Visual Database Tools&#41;](visual-database-tools.md) informs you that the database server could not save the revised foreign-key table.</span></span> <span data-ttu-id="aabda-111">若要強制資料庫接受修改，您可以清除 [建立時立即檢查現有資料]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="aabda-111">To force the database to accept the modification, you can clear the **Check existing data on creation** check box.</span></span>  
  
-   <span data-ttu-id="aabda-112">**修改提供索引檢視的資料表**：如果您修改提供 Microsoft SQL Server 索引檢視的資料表，將會遺失該檢視上的所有索引。</span><span class="sxs-lookup"><span data-stu-id="aabda-112">**Modifying a Table Contributing to an Indexed View** If you modify a table that contributes to a Microsoft SQL Server indexed view, the indexes on the view will be lost.</span></span> <span data-ttu-id="aabda-113">如需重建索引的詳細資訊，請參閱《SQL Server 線上叢書》。</span><span class="sxs-lookup"><span data-stu-id="aabda-113">See the SQL Server Books Online for information on recreating indexes.</span></span>  
  
-   <span data-ttu-id="aabda-114">**刪除物件** ：如果您刪除資料行、資料表或檢視之類的物件，請先進行檢查，確認資料庫中並無其他物件參考該物件。</span><span class="sxs-lookup"><span data-stu-id="aabda-114">**Deleting an Object** If you delete an object, such as a column, table, or view, check first to be sure that the object is not referenced by another object in the database.</span></span>  
  
 <span data-ttu-id="aabda-115">不論您如何變更資料庫設計，您應該保留一份變更記錄。</span><span class="sxs-lookup"><span data-stu-id="aabda-115">No matter how you alter the database design, you should retain a history of the alterations.</span></span> <span data-ttu-id="aabda-116">方法之一就是保留您對實際執行資料庫進行的所有 SQL 指令碼修改。</span><span class="sxs-lookup"><span data-stu-id="aabda-116">One approach is to retain SQL scripts for all modifications that you ever make to your production database.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="aabda-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="aabda-117">See Also</span></span>  
 <span data-ttu-id="aabda-118">[Unique 條件約束和 Check 條件約束](../../relational-databases/tables/unique-constraints-and-check-constraints.md) </span><span class="sxs-lookup"><span data-stu-id="aabda-118">[Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md) </span></span>  
 [<span data-ttu-id="aabda-119">多使用者環境 &#40;Visual Database Tools&#41;</span><span class="sxs-lookup"><span data-stu-id="aabda-119">Multiuser Environments &#40;Visual Database Tools&#41;</span></span>](multiuser-environments-visual-database-tools.md)  
  
  