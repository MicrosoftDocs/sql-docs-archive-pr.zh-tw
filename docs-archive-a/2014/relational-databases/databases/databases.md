---
title: 資料庫 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- data warehouse [SQL Server]
- OLTP databases [SQL Server]
- databases [SQL Server], about databases
ms.assetid: 316eea58-81b8-4bf3-a1fc-801946740e94
author: stevestein
ms.author: sstein
ms.openlocfilehash: ea3da64ce6da8cbcb32b5854f14e8d24349c0c25
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709561"
---
# <a name="databases"></a><span data-ttu-id="977b2-102">資料庫</span><span class="sxs-lookup"><span data-stu-id="977b2-102">Databases</span></span>
  <span data-ttu-id="977b2-103">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的資料庫是由資料表集合所組成，該集合內儲存了一組特定的結構資料。</span><span class="sxs-lookup"><span data-stu-id="977b2-103">A database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is made up of a collection of tables that stores a specific set of structured data.</span></span> <span data-ttu-id="977b2-104">而資料表中則包含資料列集合 (也稱為記錄或 Tuple) 和資料行 (也稱為屬性) 集合。</span><span class="sxs-lookup"><span data-stu-id="977b2-104">A table contains a collection of rows, also referred to as records or tuples, and columns, also referred to as attributes.</span></span> <span data-ttu-id="977b2-105">資料表中的每個資料行都是為了儲存某類型資訊而設計，例如，日期、名稱、金額和數字。</span><span class="sxs-lookup"><span data-stu-id="977b2-105">Each column in the table is designed to store a certain type of information, for example, dates, names, dollar amounts, and numbers.</span></span>  
  
## <a name="basic-information-about-databases"></a><span data-ttu-id="977b2-106">資料庫的基本資訊</span><span class="sxs-lookup"><span data-stu-id="977b2-106">Basic Information about Databases</span></span>  
 <span data-ttu-id="977b2-107">一部電腦可以安裝一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。</span><span class="sxs-lookup"><span data-stu-id="977b2-107">A computer can have one or more than one instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installed.</span></span> <span data-ttu-id="977b2-108">每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體都可以包含一個或多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="977b2-108">Each instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] can contain one or many databases.</span></span>  <span data-ttu-id="977b2-109">在資料庫內，存在一個或多個物件擁有權群組 (稱為結構描述)。</span><span class="sxs-lookup"><span data-stu-id="977b2-109">Within a database, there are one or many object ownership groups called schemas.</span></span> <span data-ttu-id="977b2-110">在每個結構描述內，都會包含資料庫物件 (例如資料表、檢視及預存程序)。</span><span class="sxs-lookup"><span data-stu-id="977b2-110">Within each schema there are database objects such as tables, views, and stored procedures.</span></span> <span data-ttu-id="977b2-111">部分物件 (例如憑證和非對稱金鑰) 是包含在資料庫內，但未包含在結構描述內。</span><span class="sxs-lookup"><span data-stu-id="977b2-111">Some objects such as certificates and asymmetric keys are contained within the database, but are not contained within a schema.</span></span> <span data-ttu-id="977b2-112">如需有關建立資料表的詳細資訊，請參閱＜ [Tables](../tables/tables.md)＞。</span><span class="sxs-lookup"><span data-stu-id="977b2-112">For more information about creating tables, see [Tables](../tables/tables.md).</span></span>  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="977b2-113">資料庫是儲存在檔案系統的檔案中。</span><span class="sxs-lookup"><span data-stu-id="977b2-113">databases are stored in the file system in files.</span></span> <span data-ttu-id="977b2-114">檔案可以分組為檔案群組。</span><span class="sxs-lookup"><span data-stu-id="977b2-114">Files can be grouped into filegroups.</span></span> <span data-ttu-id="977b2-115">如需有關檔案和檔案群組的詳細資訊，請參閱＜ [Database Files and Filegroups](database-files-and-filegroups.md)＞。</span><span class="sxs-lookup"><span data-stu-id="977b2-115">For more information about files and filegroups, see [Database Files and Filegroups](database-files-and-filegroups.md).</span></span>  
  
 <span data-ttu-id="977b2-116">使用者在取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的存取權時會視為已登入。</span><span class="sxs-lookup"><span data-stu-id="977b2-116">When people gain access to an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] they are identified as a login.</span></span> <span data-ttu-id="977b2-117">使用者在取得資料庫的存取權時會視為資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="977b2-117">When people gain access to a database they are identified as a database user.</span></span> <span data-ttu-id="977b2-118">資料庫使用者可以根據登入來建立。</span><span class="sxs-lookup"><span data-stu-id="977b2-118">A database user can be based on a login.</span></span> <span data-ttu-id="977b2-119">若啟用自主資料庫，則可建立不是根據登入的資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="977b2-119">If contained databases are enabled, a database user can be created that is not based on a login.</span></span> <span data-ttu-id="977b2-120">如需使用者的詳細資訊，請參閱 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="977b2-120">For more information about users, see [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql).</span></span>  
  
 <span data-ttu-id="977b2-121">具有資料庫存取權的使用者可以獲得存取資料庫中物件的權限。</span><span class="sxs-lookup"><span data-stu-id="977b2-121">A user that has access to a database can be given permission to access the objects in the database.</span></span> <span data-ttu-id="977b2-122">雖然權限可以授與個別使用者，但是建議建立資料庫角色，並將資料庫使用者加入至角色，然後授與角色的存取權。</span><span class="sxs-lookup"><span data-stu-id="977b2-122">Though permissions can be granted to individual users, we recommend creating database roles, adding the database users to the roles, and then grant access permission to the roles.</span></span> <span data-ttu-id="977b2-123">授與角色的權限，而非使用者的權限，如此即可在使用者數目成長並持續變更時，更輕鬆地保持權限的一致性，且使權限更容易了解。</span><span class="sxs-lookup"><span data-stu-id="977b2-123">Granting permissions to roles instead of users makes it easier to keep permissions consistent and understandable as the number of users grow and continually change.</span></span> <span data-ttu-id="977b2-124">如需角色權限的詳細資訊，請參閱 [CREATE ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-role-transact-sql) 和[主體 &#40;Database Engine&#41;](../security/authentication-access/principals-database-engine.md)。</span><span class="sxs-lookup"><span data-stu-id="977b2-124">For more information about roles permissions, see [CREATE ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-role-transact-sql) and [Principals &#40;Database Engine&#41;](../security/authentication-access/principals-database-engine.md).</span></span>  
  
## <a name="working-with-databases"></a><span data-ttu-id="977b2-125">使用資料庫</span><span class="sxs-lookup"><span data-stu-id="977b2-125">Working with Databases</span></span>  
 <span data-ttu-id="977b2-126">使用資料庫的大多數使用者都會使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 工具。</span><span class="sxs-lookup"><span data-stu-id="977b2-126">Most people who work with databases use the [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tool.</span></span> <span data-ttu-id="977b2-127">[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 工具具有用於建立資料庫和資料庫中物件的圖形化使用者介面。</span><span class="sxs-lookup"><span data-stu-id="977b2-127">The [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] tool has a graphical user interface for creating databases and the objects in the databases.</span></span> [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] <span data-ttu-id="977b2-128">也具有查詢編輯器，可透過寫入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式與資料庫互動。</span><span class="sxs-lookup"><span data-stu-id="977b2-128">also has a query editor for interacting with databases by writing [!INCLUDE[tsql](../../includes/tsql-md.md)] statements.</span></span> [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] <span data-ttu-id="977b2-129">可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝磁碟進行安裝，或從 MSDN 進行下載。</span><span class="sxs-lookup"><span data-stu-id="977b2-129">can be installed from the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installation disk, or downloaded from MSDN.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="977b2-130">本節內容</span><span class="sxs-lookup"><span data-stu-id="977b2-130">In This Section</span></span>  
  
|||  
|-|-|  
|[<span data-ttu-id="977b2-131">系統資料庫</span><span class="sxs-lookup"><span data-stu-id="977b2-131">System Databases</span></span>](system-databases.md)|[<span data-ttu-id="977b2-132">刪除資料庫的資料或記錄檔</span><span class="sxs-lookup"><span data-stu-id="977b2-132">Delete Data or Log Files from a Database</span></span>](delete-data-or-log-files-from-a-database.md)|  
|[<span data-ttu-id="977b2-133">自主資料庫</span><span class="sxs-lookup"><span data-stu-id="977b2-133">Contained Databases</span></span>](contained-databases.md)|[<span data-ttu-id="977b2-134">顯示資料庫的資料和記錄空間資訊</span><span class="sxs-lookup"><span data-stu-id="977b2-134">Display Data and Log Space Information for a Database</span></span>](display-data-and-log-space-information-for-a-database.md)|  
|[<span data-ttu-id="977b2-135">在 Azure 中 SQL Server 資料檔案</span><span class="sxs-lookup"><span data-stu-id="977b2-135">SQL Server Data Files in Azure</span></span>](sql-server-data-files-in-microsoft-azure.md)|[<span data-ttu-id="977b2-136">增加資料庫的大小</span><span class="sxs-lookup"><span data-stu-id="977b2-136">Increase the Size of a Database</span></span>](increase-the-size-of-a-database.md)|  
|[<span data-ttu-id="977b2-137">資料庫檔案與檔案群組</span><span class="sxs-lookup"><span data-stu-id="977b2-137">Database Files and Filegroups</span></span>](database-files-and-filegroups.md)|[<span data-ttu-id="977b2-138">重新命名資料庫</span><span class="sxs-lookup"><span data-stu-id="977b2-138">Rename a Database</span></span>](rename-a-database.md)|  
|[<span data-ttu-id="977b2-139">資料庫狀態</span><span class="sxs-lookup"><span data-stu-id="977b2-139">Database States</span></span>](database-states.md)|[<span data-ttu-id="977b2-140">將資料庫設定為單一使用者模式</span><span class="sxs-lookup"><span data-stu-id="977b2-140">Set a Database to Single-user Mode</span></span>](set-a-database-to-single-user-mode.md)|  
|[<span data-ttu-id="977b2-141">檔案狀態</span><span class="sxs-lookup"><span data-stu-id="977b2-141">File States</span></span>](file-states.md)|[<span data-ttu-id="977b2-142">壓縮資料庫</span><span class="sxs-lookup"><span data-stu-id="977b2-142">Shrink a Database</span></span>](shrink-a-database.md)|  
|[<span data-ttu-id="977b2-143">估計資料庫的大小</span><span class="sxs-lookup"><span data-stu-id="977b2-143">Estimate the Size of a Database</span></span>](estimate-the-size-of-a-database.md)|[<span data-ttu-id="977b2-144">壓縮檔案</span><span class="sxs-lookup"><span data-stu-id="977b2-144">Shrink a File</span></span>](shrink-a-file.md)|  
|[<span data-ttu-id="977b2-145">複製資料庫至其他伺服器</span><span class="sxs-lookup"><span data-stu-id="977b2-145">Copy Databases to Other Servers</span></span>](copy-databases-to-other-servers.md)|[<span data-ttu-id="977b2-146">檢視或變更資料庫的屬性</span><span class="sxs-lookup"><span data-stu-id="977b2-146">View or Change the Properties of a Database</span></span>](view-or-change-the-properties-of-a-database.md)|  
|[<span data-ttu-id="977b2-147">資料庫卸離與附加 &#40;SQL Server&#41;</span><span class="sxs-lookup"><span data-stu-id="977b2-147">Database Detach and Attach &#40;SQL Server&#41;</span></span>](database-detach-and-attach-sql-server.md)|[<span data-ttu-id="977b2-148">檢視 SQL Server 執行個體上的資料庫清單</span><span class="sxs-lookup"><span data-stu-id="977b2-148">View a List of Databases on an Instance of SQL Server</span></span>](view-a-list-of-databases-on-an-instance-of-sql-server.md)|  
|[<span data-ttu-id="977b2-149">將資料或記錄檔加入資料庫</span><span class="sxs-lookup"><span data-stu-id="977b2-149">Add Data or Log Files to a Database</span></span>](add-data-or-log-files-to-a-database.md)|[<span data-ttu-id="977b2-150">檢視或變更資料庫的相容性層級</span><span class="sxs-lookup"><span data-stu-id="977b2-150">View or Change the Compatibility Level of a Database</span></span>](view-or-change-the-compatibility-level-of-a-database.md)|  
|[<span data-ttu-id="977b2-151">變更資料庫的組態設定</span><span class="sxs-lookup"><span data-stu-id="977b2-151">Change the Configuration Settings for a Database</span></span>](change-the-configuration-settings-for-a-database.md)|[<span data-ttu-id="977b2-152">使用維護計畫精靈</span><span class="sxs-lookup"><span data-stu-id="977b2-152">Use the Maintenance Plan Wizard</span></span>](../maintenance-plans/use-the-maintenance-plan-wizard.md)|  
|[<span data-ttu-id="977b2-153">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="977b2-153">Create a Database</span></span>](create-a-database.md)|[<span data-ttu-id="977b2-154">建立使用者定義資料類型別名</span><span class="sxs-lookup"><span data-stu-id="977b2-154">Create a User-Defined Data Type Alias</span></span>](create-a-user-defined-data-type-alias.md)|  
|[<span data-ttu-id="977b2-155">刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="977b2-155">Delete a Database</span></span>](delete-a-database.md)|[<span data-ttu-id="977b2-156">資料庫快照集 &#40;SQL Server&#41;</span><span class="sxs-lookup"><span data-stu-id="977b2-156">Database Snapshots &#40;SQL Server&#41;</span></span>](database-snapshots-sql-server.md)|  
  
## <a name="related-content"></a><span data-ttu-id="977b2-157">相關內容</span><span class="sxs-lookup"><span data-stu-id="977b2-157">Related Content</span></span>  
 [<span data-ttu-id="977b2-158">索引數</span><span class="sxs-lookup"><span data-stu-id="977b2-158">Indexes</span></span>](../indexes/indexes.md)  
  
 [<span data-ttu-id="977b2-159">檢視</span><span class="sxs-lookup"><span data-stu-id="977b2-159">Views</span></span>](../views/views.md)  
  
 [<span data-ttu-id="977b2-160">預存程序 &#40;Database Engine&#41;</span><span class="sxs-lookup"><span data-stu-id="977b2-160">Stored Procedures &#40;Database Engine&#41;</span></span>](../stored-procedures/stored-procedures-database-engine.md)  
  
  