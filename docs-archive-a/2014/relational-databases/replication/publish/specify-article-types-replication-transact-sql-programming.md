---
title: 指定發行項類型 (複寫 Transact-SQL 程式設計) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- stored procedures [SQL Server replication], publishing
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7864825891203530bf30015471ca22a1daccf9b9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705002"
---
# <a name="specify-article-types-replication-transact-sql-programming"></a><span data-ttu-id="9dafc-102">指定發行項類型 (複寫 Transact-SQL 程式設計)</span><span class="sxs-lookup"><span data-stu-id="9dafc-102">Specify Article Types (Replication Transact-SQL Programming)</span></span>
  <span data-ttu-id="9dafc-103">複寫的預設發行項類型為資料表發行項，但是您可以將其他資料庫物件發行為發行項，包括檢視、預存程序、使用者定義函數及預存程序執行。</span><span class="sxs-lookup"><span data-stu-id="9dafc-103">The default article types for replication are table articles, but you can publish other database objects as articles, including views, stored procedures, user-defined functions, and stored procedure execution.</span></span> <span data-ttu-id="9dafc-104">您可以使用複寫預存程序，於定義發行項時以程式設計方式指定發行項類型。</span><span class="sxs-lookup"><span data-stu-id="9dafc-104">You can use replication stored procedures to specify an article type programmatically when you define an article.</span></span> <span data-ttu-id="9dafc-105">使用哪些預存程序取決於複寫的類型和發行項類型而定。</span><span class="sxs-lookup"><span data-stu-id="9dafc-105">The procedures that you use depend on the type of replication and article type.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="9dafc-106">在定義資料表、檢視和預存程序發行項時的僅限結構描述指定會指示，只會複寫物件定義。</span><span class="sxs-lookup"><span data-stu-id="9dafc-106">The schema-only designation when defining table, view, and stored procedure articles indicates that only the object definition is replicated.</span></span>  
  
### <a name="to-publish-a-table-article-in-a-transactional-or-snapshot-publication"></a><span data-ttu-id="9dafc-107">在交易式或快照式發行集中發行資料表發行項</span><span class="sxs-lookup"><span data-stu-id="9dafc-107">To publish a table article in a transactional or snapshot publication</span></span>  
  
1.  <span data-ttu-id="9dafc-108">在發行集資料庫的發行者上，執行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-108">At the Publisher on the publication database, execute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql).</span></span> <span data-ttu-id="9dafc-109">為\*\* \@ type\*\*指定下列其中一個值，以定義發行項的類型：</span><span class="sxs-lookup"><span data-stu-id="9dafc-109">Specify one of the following values for **\@type** to define the type of article:</span></span>  
  
    -   <span data-ttu-id="9dafc-110">**logbased** - 記錄式資料表發行項，這是交易式和快照式複寫的預設值。</span><span class="sxs-lookup"><span data-stu-id="9dafc-110">**logbased** - a log-based table article, which is the default for transactional and snapshot replication.</span></span> <span data-ttu-id="9dafc-111">複寫會自動產生用於水平篩選的預存程序以及定義垂直篩選之發行項的檢視。</span><span class="sxs-lookup"><span data-stu-id="9dafc-111">Replication automatically generates the stored procedure used for horizontal filtering and the view that defines a vertically filtered article.</span></span>  
  
    -   <span data-ttu-id="9dafc-112">**logbased manualfilter** -記錄式、水準篩選的發行項，其中用於水準篩選的預存程式是由使用者手動建立及定義，而且是針對\*\* \@ filter\*\*所指定。</span><span class="sxs-lookup"><span data-stu-id="9dafc-112">**logbased manualfilter** - a log-based, horizontally filtered article where the stored procedure used for horizontal filtering is manually created and defined by the user and specified for **\@filter**.</span></span> <span data-ttu-id="9dafc-113">如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-113">For more information, see [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md).</span></span>  
  
    -   <span data-ttu-id="9dafc-114">**logbased manualview** -記錄式、垂直篩選的發行項，其中定義垂直篩選之發行項的視圖是由使用者所建立及定義，而且是針對\*\* \@ sync_object\*\*所指定。</span><span class="sxs-lookup"><span data-stu-id="9dafc-114">**logbased manualview** - a log-based, vertically filtered article where the view that defines the vertically filtered article is created and defined by the user and specified for **\@sync_object**.</span></span> <span data-ttu-id="9dafc-115">如需相關資訊，請參閱 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) 及 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-115">For more information, see [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) and [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).</span></span>  
  
    -   <span data-ttu-id="9dafc-116">**logbased manualboth** -記錄式、水準和垂直篩選的發行項，其中用於水準篩選的預存程式及定義垂直篩選之發行項的視圖，都是由使用者建立及定義，並分別指定為\*\* \@ filter**和** \@ sync_object\*\*。</span><span class="sxs-lookup"><span data-stu-id="9dafc-116">**logbased manualboth** - a log-based, horizontally and vertically filtered article where both the stored procedure used for horizontal filtering and the view that defines the vertically filtered article are created and defined by the user and specified for **\@filter** and **\@sync_object**, respectively.</span></span> <span data-ttu-id="9dafc-117">如需相關資訊，請參閱 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) 及 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-117">For more information, see [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) and [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).</span></span>  
  
     <span data-ttu-id="9dafc-118">這樣會為發行集定義新的發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-118">This defines a new article for the publication.</span></span> <span data-ttu-id="9dafc-119">如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-119">For more information, see [Define an Article](define-an-article.md).</span></span>  
  
2.  <span data-ttu-id="9dafc-120">如果是 **logbased manualboth** 和 **logbased manualfilter** 發行項，請執行 [sp_articlefilter](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql) 來產生用於水平篩選之發行項的篩選預存程序。</span><span class="sxs-lookup"><span data-stu-id="9dafc-120">For **logbased manualboth** and **logbased manualfilter** articles, execute [sp_articlefilter](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql) to generate the filtering stored procedure for a horizontally filtered article.</span></span> <span data-ttu-id="9dafc-121">如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-121">For more information, see [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md).</span></span>  
  
3.  <span data-ttu-id="9dafc-122">如果是 **logbased manualboth**、 **logbased manualview**和 **logbased manualfilter** 發行項，請執行 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql) 來產生用於定義垂直篩選之發行項的檢視。</span><span class="sxs-lookup"><span data-stu-id="9dafc-122">For **logbased manualboth**, **logbased manualview**, and **logbased manualfilter** articles, execute [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql) to generate the view that defines the vertically filtered article.</span></span> <span data-ttu-id="9dafc-123">如需詳細資訊，請參閱 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-123">For more information, see [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).</span></span>  
  
### <a name="to-publish-a-view-or-indexed-view-article-in-a-transactional-or-snapshot-publication"></a><span data-ttu-id="9dafc-124">在交易式或快照式發行集中發行檢視或索引檢視發行項</span><span class="sxs-lookup"><span data-stu-id="9dafc-124">To publish a view or indexed view article in a transactional or snapshot publication</span></span>  
  
1.  <span data-ttu-id="9dafc-125">在發行集資料庫的發行者上，執行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-125">At the Publisher on the publication database, execute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql).</span></span> <span data-ttu-id="9dafc-126">為\*\* \@ type\*\*指定下列其中一個值，以定義發行項的類型：</span><span class="sxs-lookup"><span data-stu-id="9dafc-126">Specify one of the following values for **\@type** to define the type of article:</span></span>  
  
    -   <span data-ttu-id="9dafc-127">**indexed view logbased** - 記錄式索引檢視發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-127">**indexed view logbased** - a log-based indexed view article.</span></span> <span data-ttu-id="9dafc-128">複寫會自動產生用於水平篩選的預存程序以及定義垂直篩選之發行項的檢視。</span><span class="sxs-lookup"><span data-stu-id="9dafc-128">Replication automatically generates the stored procedure used for horizontal filtering and the view that defines a vertically filtered article.</span></span>  
  
    -   <span data-ttu-id="9dafc-129">**view schema only** - 僅限結構描述的檢視發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-129">**view schema only** - a schema-only view article.</span></span> <span data-ttu-id="9dafc-130">也必須要複寫基底資料表。</span><span class="sxs-lookup"><span data-stu-id="9dafc-130">The base table must also be replicated.</span></span>  
  
    -   <span data-ttu-id="9dafc-131">**indexed view schema only** - 僅限結構描述的索引檢視發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-131">**indexed view schema only** - a schema-only indexed view article.</span></span> <span data-ttu-id="9dafc-132">也必須要複寫基底資料表。</span><span class="sxs-lookup"><span data-stu-id="9dafc-132">The base table must also be replicated.</span></span>  
  
    -   <span data-ttu-id="9dafc-133">**indexed view logbased manualfilter** -記錄式、水準篩選的索引 view 發行項，其中用於水準篩選的預存程式是由使用者手動建立及定義，而且是針對\*\* \@ filter\*\*所指定。</span><span class="sxs-lookup"><span data-stu-id="9dafc-133">**indexed view logbased manualfilter** - a log-based, horizontally filtered indexed view article where the stored procedure used for horizontal filtering is manually created and defined by the user and specified for **\@filter**.</span></span> <span data-ttu-id="9dafc-134">如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-134">For more information, see [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md).</span></span>  
  
    -   <span data-ttu-id="9dafc-135">已**編制索引的 view logbased manualview** -記錄式、篩選的索引 view 發行項，其中定義垂直篩選之發行項的視圖是由使用者所建立及定義，而且是針對\*\* \@ sync_object\*\*所指定。</span><span class="sxs-lookup"><span data-stu-id="9dafc-135">**indexed view logbased manualview** - a log-based, filtered indexed view article where the view that defines a vertically filtered article is created and defined by the user and specified for **\@sync_object**.</span></span> <span data-ttu-id="9dafc-136">如需相關資訊，請參閱 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) 及 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-136">For more information, see [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) and [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).</span></span>  
  
    -   <span data-ttu-id="9dafc-137">**索引視圖 logbased manualboth** -記錄式、已篩選的索引 view 發行項，其中用於水準篩選的預存程式，以及定義垂直篩選之發行項的視圖，是由使用者建立及定義，並分別指定為\*\* \@ filter**和** \@ sync_object\*\*。</span><span class="sxs-lookup"><span data-stu-id="9dafc-137">**indexed view logbased manualboth** - a log-based, filtered indexed view article where both the stored procedure used for horizontal filtering and the view that defines a vertically filtered article are created and defined by the user and specified for **\@filter** and **\@sync_object**, respectively.</span></span> <span data-ttu-id="9dafc-138">如需相關資訊，請參閱 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) 及 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-138">For more information, see [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) and [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).</span></span>  
  
     <span data-ttu-id="9dafc-139">這樣會為發行集定義新的發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-139">This defines a new article for the publication.</span></span> <span data-ttu-id="9dafc-140">如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-140">For more information, see [Define an Article](define-an-article.md).</span></span>  
  
2.  <span data-ttu-id="9dafc-141">如果是 **logbased manualboth** 和 **logbased manualfilter** 發行項，請執行 [sp_articlefilter](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql) 來產生用於水平篩選之發行項的篩選預存程序。</span><span class="sxs-lookup"><span data-stu-id="9dafc-141">For **logbased manualboth** and **logbased manualfilter** articles, execute [sp_articlefilter](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql) to generate the filtering stored procedure for a horizontally filtered article.</span></span> <span data-ttu-id="9dafc-142">如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-142">For more information, see [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md).</span></span>  
  
3.  <span data-ttu-id="9dafc-143">如果是 **logbased manualboth**、 **logbased manualview**和 **logbased manualfilter** 發行項，請執行 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql) 來產生用於定義垂直篩選之發行項的檢視。</span><span class="sxs-lookup"><span data-stu-id="9dafc-143">For **logbased manualboth**, **logbased manualview**, and **logbased manualfilter** articles, execute [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql) to generate the view that defines the vertically filtered article.</span></span> <span data-ttu-id="9dafc-144">如需詳細資訊，請參閱 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-144">For more information, see [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).</span></span>  
  
### <a name="to-publish-a-stored-procedure-stored-procedure-execution-or-user-defined-function-article-in-a-transactional-or-snapshot-publication"></a><span data-ttu-id="9dafc-145">在交易式或快照式發行集中發行預存程序、預存程序執行或使用者定義函數發行項</span><span class="sxs-lookup"><span data-stu-id="9dafc-145">To publish a stored procedure, stored procedure execution, or user-defined function article in a transactional or snapshot publication</span></span>  
  
1.  <span data-ttu-id="9dafc-146">在發行集資料庫的發行者上，執行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-146">At the Publisher on the publication database, execute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql).</span></span> <span data-ttu-id="9dafc-147">為\*\* \@ type\*\*指定下列其中一個值，以定義發行項的類型：</span><span class="sxs-lookup"><span data-stu-id="9dafc-147">Specify one of the following values for **\@type** to define the type of article:</span></span>  
  
    -   <span data-ttu-id="9dafc-148">**proc schema only** - 僅限結構描述的預存程序發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-148">**proc schema only** - a schema-only stored procedure article.</span></span>  
  
    -   <span data-ttu-id="9dafc-149">**proc exec** - 將預存程序的執行複寫到發行項的所有訂閱者。</span><span class="sxs-lookup"><span data-stu-id="9dafc-149">**proc exec** - replicates the execution of the stored procedure to all Subscribers of the article.</span></span> <span data-ttu-id="9dafc-150">如需詳細資訊，請參閱 [Publishing Stored Procedure Execution in Transactional Replication](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-150">For more information, see [Publishing Stored Procedure Execution in Transactional Replication](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md).</span></span>  
  
    -   <span data-ttu-id="9dafc-151">**serializable proc exec** - 只有當預存程序執行於可序列化交易的環境內時，才複寫預存程序的執行。</span><span class="sxs-lookup"><span data-stu-id="9dafc-151">**serializable proc exec** - replicates the execution of the stored procedure only if it is executed within the context of a serializable transaction.</span></span> <span data-ttu-id="9dafc-152">如需詳細資訊，請參閱 [Publishing Stored Procedure Execution in Transactional Replication](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-152">For more information, see [Publishing Stored Procedure Execution in Transactional Replication](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md).</span></span>  
  
    -   <span data-ttu-id="9dafc-153">**func schema only** - 僅限結構描述的使用者定義函數發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-153">**func schema only** - a schema-only user-defined function article.</span></span>  
  
     <span data-ttu-id="9dafc-154">這樣會為發行集定義新的發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-154">This defines a new article for the publication.</span></span> <span data-ttu-id="9dafc-155">如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-155">For more information, see [Define an Article](define-an-article.md).</span></span>  
  
### <a name="to-publish-a-table-or-view-article-in-a-merge-publication"></a><span data-ttu-id="9dafc-156">在合併式發行集中發行資料表或檢視發行項</span><span class="sxs-lookup"><span data-stu-id="9dafc-156">To publish a table or view article in a merge publication</span></span>  
  
1.  <span data-ttu-id="9dafc-157">在發行集資料庫的發行者上，執行 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-157">At the Publisher on the publication database, execute [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql).</span></span> <span data-ttu-id="9dafc-158">為\*\* \@ type\*\*指定下列其中一個值，以定義發行項的類型：</span><span class="sxs-lookup"><span data-stu-id="9dafc-158">Specify one of the following values for **\@type** to define the type of article:</span></span>  
  
    -   <span data-ttu-id="9dafc-159">**table** - 資料表發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-159">**table** - a table article.</span></span>  
  
    -   <span data-ttu-id="9dafc-160">**indexed view schema only** - 僅限結構描述的索引檢視發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-160">**indexed view schema only** - a schema-only indexed view article.</span></span>  
  
    -   <span data-ttu-id="9dafc-161">**view schema only** - 僅限結構描述的檢視發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-161">**view schema only** - a schema-only view article.</span></span>  
  
     <span data-ttu-id="9dafc-162">這樣會為發行集定義新的發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-162">This defines a new article for the publication.</span></span> <span data-ttu-id="9dafc-163">如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-163">For more information, see [Define an Article](define-an-article.md).</span></span>  
  
### <a name="to-publish-a-stored-procedure-or-user-defined-function-article-in-a-merge-publication"></a><span data-ttu-id="9dafc-164">在合併式發行集中發行預存程序或使用者定義函數發行項</span><span class="sxs-lookup"><span data-stu-id="9dafc-164">To publish a stored procedure or user-defined function article in a merge publication</span></span>  
  
1.  <span data-ttu-id="9dafc-165">在發行集資料庫的發行者上，執行 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-165">At the Publisher on the publication database, execute [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql).</span></span> <span data-ttu-id="9dafc-166">為\*\* \@ type\*\*指定下列其中一個值，以定義發行項的類型：</span><span class="sxs-lookup"><span data-stu-id="9dafc-166">Specify one of the following values for **\@type** to define the type of article:</span></span>  
  
    -   <span data-ttu-id="9dafc-167">**func schema only** - 僅限結構描述的使用者定義函數發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-167">**func schema only** - a schema-only user-defined function article.</span></span>  
  
    -   <span data-ttu-id="9dafc-168">**proc schema only** - 僅限結構描述的預存程序發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-168">**proc schema only** - a schema-only stored procedure article.</span></span>  
  
     <span data-ttu-id="9dafc-169">這樣會為發行集定義新的發行項。</span><span class="sxs-lookup"><span data-stu-id="9dafc-169">This defines a new article for the publication.</span></span> <span data-ttu-id="9dafc-170">如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。</span><span class="sxs-lookup"><span data-stu-id="9dafc-170">For more information, see [Define an Article](define-an-article.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9dafc-171">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9dafc-171">See Also</span></span>  
 <span data-ttu-id="9dafc-172">[Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md) </span><span class="sxs-lookup"><span data-stu-id="9dafc-172">[Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md) </span></span>  
 [<span data-ttu-id="9dafc-173">發行資料和資料庫物件</span><span class="sxs-lookup"><span data-stu-id="9dafc-173">Publish Data and Database Objects</span></span>](publish-data-and-database-objects.md)  
  
  