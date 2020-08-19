---
title: 預存程序 (Database Engine) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- storing programs as stored procedures
- stored procedures [SQL Server], about stored procedures
ms.assetid: cc6daf62-9663-4c3e-950a-ab42e2830427
author: stevestein
ms.author: sstein
ms.openlocfilehash: b1d8d7d0684d528276cc18adfdd3df837a79d551
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598771"
---
# <a name="stored-procedures-database-engine"></a><span data-ttu-id="07832-102">預存程序 (Database Engine)</span><span class="sxs-lookup"><span data-stu-id="07832-102">Stored Procedures (Database Engine)</span></span>
  <span data-ttu-id="07832-103">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預存程序是一或多個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的群組，或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR) 方法的參考。</span><span class="sxs-lookup"><span data-stu-id="07832-103">A stored procedure in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is a group of one or more [!INCLUDE[tsql](../../includes/tsql-md.md)] statements or a reference to a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common runtime language (CLR) method.</span></span> <span data-ttu-id="07832-104">預存程序類似於其他程式設計語言中的建構，因為這些程序可以：</span><span class="sxs-lookup"><span data-stu-id="07832-104">Procedures resemble constructs in other programming languages because they can:</span></span>  
  
-   <span data-ttu-id="07832-105">接受輸入參數，並以輸出參數的形式將多個數值傳回呼叫程式。</span><span class="sxs-lookup"><span data-stu-id="07832-105">Accept input parameters and return multiple values in the form of output parameters to the calling program.</span></span>  
  
-   <span data-ttu-id="07832-106">包含可在資料庫中執行作業的程式陳述式。</span><span class="sxs-lookup"><span data-stu-id="07832-106">Contain programming statements that perform operations in the database.</span></span> <span data-ttu-id="07832-107">這些功能包括呼叫其他程序。</span><span class="sxs-lookup"><span data-stu-id="07832-107">These include calling other procedures.</span></span>  
  
-   <span data-ttu-id="07832-108">將狀態值傳回呼叫程式，以指示成功或失敗 (及失敗原因)。</span><span class="sxs-lookup"><span data-stu-id="07832-108">Return a status value to a calling program to indicate success or failure (and the reason for failure).</span></span>  
  
## <a name="benefits-of-using-stored-procedures"></a><span data-ttu-id="07832-109">使用預存程序的好處</span><span class="sxs-lookup"><span data-stu-id="07832-109">Benefits of Using Stored Procedures</span></span>  
 <span data-ttu-id="07832-110">下列清單說明使用這些程序的一些優點。</span><span class="sxs-lookup"><span data-stu-id="07832-110">The following list describes some benefits of using procedures.</span></span>  
  
 <span data-ttu-id="07832-111">減少伺服器/用戶端網路流量</span><span class="sxs-lookup"><span data-stu-id="07832-111">Reduced server/client network traffic</span></span>  
 <span data-ttu-id="07832-112">程序中的指令會以單一批次的程式碼來執行。</span><span class="sxs-lookup"><span data-stu-id="07832-112">The commands in a procedure are executed as a single batch of code.</span></span> <span data-ttu-id="07832-113">這可以大幅降低伺服器與用戶端之間的網路流量，因為網路之間只會傳送執行程序的呼叫。</span><span class="sxs-lookup"><span data-stu-id="07832-113">This can significantly reduce network traffic between the server and client because only the call to execute the procedure is sent across the network.</span></span> <span data-ttu-id="07832-114">若程序沒有提供程式碼封裝，則每個個別的程式碼行都會在網路上傳送。</span><span class="sxs-lookup"><span data-stu-id="07832-114">Without the code encapsulation provided by a procedure, every individual line of code would have to cross the network.</span></span>  
  
 <span data-ttu-id="07832-115">更強的安全性</span><span class="sxs-lookup"><span data-stu-id="07832-115">Stronger security</span></span>  
 <span data-ttu-id="07832-116">多個使用者和用戶端程式都可以透過程序，在基礎資料庫物件上執行作業，即使使用者和程式不具備這些基礎物件的直接權限亦可。</span><span class="sxs-lookup"><span data-stu-id="07832-116">Multiple users and client programs can perform operations on underlying database objects through a procedure, even if the users and programs do not have direct permissions on those underlying objects.</span></span> <span data-ttu-id="07832-117">程序也會控制要執行哪些程序和活動，並保護基礎資料庫物件。</span><span class="sxs-lookup"><span data-stu-id="07832-117">The procedure controls what processes and activities are performed and protects the underlying database objects.</span></span> <span data-ttu-id="07832-118">這可避免在個別物件層級授與權限的需求，而簡化安全層。</span><span class="sxs-lookup"><span data-stu-id="07832-118">This eliminates the requirement to grant permissions at the individual object level and simplifies the security layers.</span></span>  
  
 <span data-ttu-id="07832-119">[EXECUTE AS](/sql/t-sql/statements/execute-as-clause-transact-sql) 子句可指定在 CREATE PROCEDURE 陳述式中，以模擬其他使用者，或讓使用者或應用程式執行特定資料庫活動，而不需要具備基礎物件和指令的直接權限。</span><span class="sxs-lookup"><span data-stu-id="07832-119">The [EXECUTE AS](/sql/t-sql/statements/execute-as-clause-transact-sql) clause can be specified in the CREATE PROCEDURE statement to enable impersonating another user, or enable users or applications to perform certain database activities without needing direct permissions on the underlying objects and commands.</span></span> <span data-ttu-id="07832-120">例如，有些動作 (如 TRUNCATE TABLE) 沒有可授與的權限。</span><span class="sxs-lookup"><span data-stu-id="07832-120">For example, some actions such as TRUNCATE TABLE, do not have grantable permissions.</span></span> <span data-ttu-id="07832-121">若要執行 TRUNCATE TABLE，使用者必須擁有指定資料表的 ALTER 權限。</span><span class="sxs-lookup"><span data-stu-id="07832-121">To execute TRUNCATE TABLE, the user must have ALTER permissions on the specified table.</span></span> <span data-ttu-id="07832-122">授與使用者資料表的 ALTER 權限可能不是很理想，因為使用者實際上將擁有不只截斷資料表的權限。</span><span class="sxs-lookup"><span data-stu-id="07832-122">Granting a user ALTER permissions on a table may not be ideal because the user will effectively have permissions well beyond the ability to truncate a table.</span></span> <span data-ttu-id="07832-123">透過合併模組中的 TRUNCATE TABLE 陳述式，並指定有權限修改資料表的使用者來執行該模組，您即可針對授與該模組 EXECUTE 權限的使用者擴充其權限，使其可截斷資料表。</span><span class="sxs-lookup"><span data-stu-id="07832-123">By incorporating the TRUNCATE TABLE statement in a module and specifying that module execute as a user who has permissions to modify the table, you can extend the permissions to truncate the table to the user that you grant EXECUTE permissions on the module.</span></span>  
  
 <span data-ttu-id="07832-124">當透過網路呼叫程序時，僅有執行程序的呼叫是可見的。</span><span class="sxs-lookup"><span data-stu-id="07832-124">When calling a procedure over the network, only the call to execute the procedure is visible.</span></span> <span data-ttu-id="07832-125">因此，惡意使用者就無法查看資料表及資料庫物件名稱、內嵌自己的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或搜尋重要的資料。</span><span class="sxs-lookup"><span data-stu-id="07832-125">Therefore, malicious users cannot see table and database object names, embed [!INCLUDE[tsql](../../includes/tsql-md.md)] statements of their own, or search for critical data.</span></span>  
  
 <span data-ttu-id="07832-126">使用程序參數可協助預防 SQL 資料隱碼攻擊。</span><span class="sxs-lookup"><span data-stu-id="07832-126">Using procedure parameters helps guard against SQL injection attacks.</span></span> <span data-ttu-id="07832-127">由於參數輸入會被視為常值而不是可執行的程式碼，因此更難以將指令插入程序中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式以進行攻擊，並危及安全性。</span><span class="sxs-lookup"><span data-stu-id="07832-127">Since parameter input is treated as a literal value and not as executable code, it is more difficult for an attacker to insert a command into the [!INCLUDE[tsql](../../includes/tsql-md.md)] statement(s) inside the procedure and compromise security.</span></span>  
  
 <span data-ttu-id="07832-128">您也可以加密程序，協助模糊化原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="07832-128">Procedures can be encrypted, helping to obfuscate the source code.</span></span> <span data-ttu-id="07832-129">如需詳細資訊，請參閱 [SQL Server 加密](../security/encryption/sql-server-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="07832-129">For more information, see [SQL Server Encryption](../security/encryption/sql-server-encryption.md).</span></span>  
  
 <span data-ttu-id="07832-130">重複使用程式碼</span><span class="sxs-lookup"><span data-stu-id="07832-130">Reuse of code</span></span>  
 <span data-ttu-id="07832-131">任何重複資料庫作業的程式碼，都是程序中非常適合封裝的項目。</span><span class="sxs-lookup"><span data-stu-id="07832-131">The code for any repetitious database operation is the perfect candidate for encapsulation in procedures.</span></span> <span data-ttu-id="07832-132">這可避免重複撰寫相同程式碼、減少程式碼不一致，並且可讓具備所需權限的任何使用者或應用程式存取及執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="07832-132">This eliminates needless rewrites of the same code, decreases code inconsistency, and allows the code to be accessed and executed by any user or application possessing the necessary permissions.</span></span>  
  
 <span data-ttu-id="07832-133">維護更簡易</span><span class="sxs-lookup"><span data-stu-id="07832-133">Easier maintenance</span></span>  
 <span data-ttu-id="07832-134">當用戶端應用程式呼叫程序並將資料庫作業保留在資料層中時，若基礎資料庫中有任何變更，只有程序必須更新。</span><span class="sxs-lookup"><span data-stu-id="07832-134">When client applications call procedures and keep database operations in the data tier, only the procedures must be updated for any changes in the underlying database.</span></span> <span data-ttu-id="07832-135">應用程式層會維持獨立，也不需要知道資料庫配置、關聯性或程序間有什麼變更。</span><span class="sxs-lookup"><span data-stu-id="07832-135">The application tier remains separate and does not have to know how about any changes to database layouts, relationships, or processes.</span></span>  
  
 <span data-ttu-id="07832-136">提升效能</span><span class="sxs-lookup"><span data-stu-id="07832-136">Improved performance</span></span>  
 <span data-ttu-id="07832-137">依預設，第一次編譯程序時，將執行並建立執行計畫，以利後續的執行中重複使用。</span><span class="sxs-lookup"><span data-stu-id="07832-137">By default, a procedure compiles the first time it is executed and creates an execution plan that is reused for subsequent executions.</span></span> <span data-ttu-id="07832-138">由於查詢處理器不需要建立新計畫，通常可以花較少的時間來處理程序。</span><span class="sxs-lookup"><span data-stu-id="07832-138">Since the query processor does not have to create a new plan, it typically takes less time to process the procedure.</span></span>  
  
 <span data-ttu-id="07832-139">若資料表或程序所參照的資料有大幅變更，先行編譯的計畫實際上可能會導致程序執行變慢。</span><span class="sxs-lookup"><span data-stu-id="07832-139">If there has been significant change to the tables or data referenced by the procedure, the precompiled plan may actually cause the procedure to perform slower.</span></span> <span data-ttu-id="07832-140">在此情況下，重新編譯程序並強制新的執行計畫可以改善效能。</span><span class="sxs-lookup"><span data-stu-id="07832-140">In this case, recompiling the procedure and forcing a new execution plan can improve performance.</span></span>  
  
## <a name="types-of-stored-procedures"></a><span data-ttu-id="07832-141">預存程序類型</span><span class="sxs-lookup"><span data-stu-id="07832-141">Types of Stored Procedures</span></span>  
 <span data-ttu-id="07832-142">使用者定義</span><span class="sxs-lookup"><span data-stu-id="07832-142">User-defined</span></span>  
 <span data-ttu-id="07832-143">您可以在使用者定義的資料庫或所有系統資料庫 ( **Resource** 資料庫除外) 中，建立使用者定義的程序。</span><span class="sxs-lookup"><span data-stu-id="07832-143">A user-defined procedure can be created in a user-defined database or in all system databases except the **Resource** database.</span></span> <span data-ttu-id="07832-144">您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR) 方法作為參照的形式來建立程序。</span><span class="sxs-lookup"><span data-stu-id="07832-144">The procedure can be developed in either [!INCLUDE[tsql](../../includes/tsql-md.md)] or as a reference to a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common runtime language (CLR) method.</span></span>  
  
 <span data-ttu-id="07832-145">暫存</span><span class="sxs-lookup"><span data-stu-id="07832-145">Temporary</span></span>  
 <span data-ttu-id="07832-146">暫存程序是一種使用者定義的程序。</span><span class="sxs-lookup"><span data-stu-id="07832-146">Temporary procedures are a form of user-defined procedures.</span></span> <span data-ttu-id="07832-147">暫存程序與永久程序類似，只不過暫存程序是儲存於 **tempdb**中。</span><span class="sxs-lookup"><span data-stu-id="07832-147">The temporary procedures are like a permanent procedure, except temporary procedures are stored in **tempdb**.</span></span> <span data-ttu-id="07832-148">暫存程序有兩種：本機與全域。</span><span class="sxs-lookup"><span data-stu-id="07832-148">There are two types of temporary procedures: local and global.</span></span> <span data-ttu-id="07832-149">它們在名稱、可見性和可用性方面有些差異。</span><span class="sxs-lookup"><span data-stu-id="07832-149">They differ from each other in their names, their visibility, and their availability.</span></span> <span data-ttu-id="07832-150">本機暫存程序是以單一數字符號 (#) 做為名稱的第一個字元；只有目前使用者連接才能看見，當連接中斷時，會將其刪除。</span><span class="sxs-lookup"><span data-stu-id="07832-150">Local temporary procedures have a single number sign (#) as the first character of their names; they are visible only to the current user connection, and they are deleted when the connection is closed.</span></span> <span data-ttu-id="07832-151">全域暫存程序是以兩個數字符號 (#) 做為名稱的前兩個字元；只要一建立好，任何使用者都能看見，只有當使用程序的最後一個工作階段結束時，才會將其刪除。</span><span class="sxs-lookup"><span data-stu-id="07832-151">Global temporary procedures have two number signs (##) as the first two characters of their names; they are visible to any user after they are created, and they are deleted at the end of the last session using the procedure.</span></span>  
  
 <span data-ttu-id="07832-152">系統</span><span class="sxs-lookup"><span data-stu-id="07832-152">System</span></span>  
 <span data-ttu-id="07832-153">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中包括系統程序。</span><span class="sxs-lookup"><span data-stu-id="07832-153">System procedures are included with [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="07832-154">它們實際上是儲存在內部隱藏的 **Resource** 資料庫中，但邏輯上會出現在每個系統和使用者定義資料庫的 **sys** 結構描述中。</span><span class="sxs-lookup"><span data-stu-id="07832-154">They are physically stored in the internal, hidden **Resource** database and logically appear in the **sys** schema of every system- and user-defined database.</span></span> <span data-ttu-id="07832-155">此外， **msdb** 資料庫也包含 **dbo** 結構描述中用於排程警示和作業的系統預存程序。</span><span class="sxs-lookup"><span data-stu-id="07832-155">In addition, the **msdb** database also contains system stored procedures in the **dbo** schema that are used for scheduling alerts and jobs.</span></span> <span data-ttu-id="07832-156">因為系統程序會以 **sp_** 作為前置詞開頭，因此建議您命名使用者定義的程序時不要使用此前置詞。</span><span class="sxs-lookup"><span data-stu-id="07832-156">Because system procedures start with the prefix **sp_**, we recommend that you do not use this prefix when naming user-defined procedures.</span></span> <span data-ttu-id="07832-157">如需系統程序的完整清單，請參閱[系統預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="07832-157">For a complete list of system procedures, see [System Stored Procedures &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)</span></span>  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="07832-158">支援的系統程序，可對各種維護活動提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 到外部程式的介面。</span><span class="sxs-lookup"><span data-stu-id="07832-158">supports the system procedures that provide an interface from [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] to external programs for various maintenance activities.</span></span> <span data-ttu-id="07832-159">這些擴充程序會使用 xp_ 前置詞。</span><span class="sxs-lookup"><span data-stu-id="07832-159">These extended procedures use the xp_ prefix.</span></span> <span data-ttu-id="07832-160">如需擴充程序的完整清單，請參閱[一般擴充預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="07832-160">For a complete list of extended procedures, see [General Extended Stored Procedures &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql).</span></span>  
  
 <span data-ttu-id="07832-161">擴充使用者定義</span><span class="sxs-lookup"><span data-stu-id="07832-161">Extended User-Defined</span></span>  
 <span data-ttu-id="07832-162">擴充程序能夠在 C 這類程式設計語言中，建立外部常式。這些程序是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體可以動態載入和執行的 DLL。</span><span class="sxs-lookup"><span data-stu-id="07832-162">Extended procedures enable creating external routines in a programming language such as C. These procedures are DLLs that an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] can dynamically load and run.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="07832-163">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的未來版本將移除擴充預存程序。</span><span class="sxs-lookup"><span data-stu-id="07832-163">Extended stored procedures will be removed in a future version of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="07832-164">請勿在新的開發工作中使用此功能，並且儘速修改使用此功能的應用程式。</span><span class="sxs-lookup"><span data-stu-id="07832-164">Do not use this feature in new development work, and modify applications that currently use this feature as soon as possible.</span></span> <span data-ttu-id="07832-165">改為建立 CLR 程序。</span><span class="sxs-lookup"><span data-stu-id="07832-165">Create CLR procedures instead.</span></span> <span data-ttu-id="07832-166">此方法會提供更強固及安全的替代方法來撰寫擴充程序。</span><span class="sxs-lookup"><span data-stu-id="07832-166">This method provides a more robust and secure alternative to writing extended procedures.</span></span>  
  
## <a name="related-tasks"></a><span data-ttu-id="07832-167">相關工作</span><span class="sxs-lookup"><span data-stu-id="07832-167">Related Tasks</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="07832-168">**工作描述**</span><span class="sxs-lookup"><span data-stu-id="07832-168">**Task Description**</span></span>|<span data-ttu-id="07832-169">**主題**</span><span class="sxs-lookup"><span data-stu-id="07832-169">**Topic**</span></span>|  
|<span data-ttu-id="07832-170">描述如何建立預存程序。</span><span class="sxs-lookup"><span data-stu-id="07832-170">Describes how to create a stored procedure.</span></span>|[<span data-ttu-id="07832-171">建立預存程序</span><span class="sxs-lookup"><span data-stu-id="07832-171">Create a Stored Procedure</span></span>](../stored-procedures/create-a-stored-procedure.md)|  
|<span data-ttu-id="07832-172">描述如何修改預存程序。</span><span class="sxs-lookup"><span data-stu-id="07832-172">Describes how to modify a stored procedure.</span></span>|[<span data-ttu-id="07832-173">修改預存程序</span><span class="sxs-lookup"><span data-stu-id="07832-173">Modify a Stored Procedure</span></span>](../stored-procedures/modify-a-stored-procedure.md)|  
|<span data-ttu-id="07832-174">描述如何刪除預存程序。</span><span class="sxs-lookup"><span data-stu-id="07832-174">Describes how to delete a stored procedure.</span></span>|[<span data-ttu-id="07832-175">刪除預存程序</span><span class="sxs-lookup"><span data-stu-id="07832-175">Delete a Stored Procedure</span></span>](../stored-procedures/delete-a-stored-procedure.md)|  
|<span data-ttu-id="07832-176">描述如何執行預存程序。</span><span class="sxs-lookup"><span data-stu-id="07832-176">Describes how to execute a stored procedure.</span></span>|[<span data-ttu-id="07832-177">執行預存程序</span><span class="sxs-lookup"><span data-stu-id="07832-177">Execute a Stored Procedure</span></span>](../stored-procedures/execute-a-stored-procedure.md)|  
|<span data-ttu-id="07832-178">描述如何授與預存程序的權限。</span><span class="sxs-lookup"><span data-stu-id="07832-178">Describes how to grant permissions on a stored procedure.</span></span>|[<span data-ttu-id="07832-179">授與預存程序的權限</span><span class="sxs-lookup"><span data-stu-id="07832-179">Grant Permissions on a Stored Procedure</span></span>](../stored-procedures/grant-permissions-on-a-stored-procedure.md)|  
|<span data-ttu-id="07832-180">描述如何從預存程序將資料傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="07832-180">Describes how to return data from a stored procedure to an application.</span></span>|[<span data-ttu-id="07832-181">從預存程序傳回資料</span><span class="sxs-lookup"><span data-stu-id="07832-181">Return Data from a Stored Procedure</span></span>](../stored-procedures/return-data-from-a-stored-procedure.md)|  
|<span data-ttu-id="07832-182">描述如何重新編譯預存程序。</span><span class="sxs-lookup"><span data-stu-id="07832-182">Describes how to recompile a stored procedure.</span></span>|[<span data-ttu-id="07832-183">重新編譯預存程序</span><span class="sxs-lookup"><span data-stu-id="07832-183">Recompile a Stored Procedure</span></span>](../stored-procedures/recompile-a-stored-procedure.md)|  
|<span data-ttu-id="07832-184">描述如何重新命名預存程序。</span><span class="sxs-lookup"><span data-stu-id="07832-184">Describes how to rename a stored procedure.</span></span>|[<span data-ttu-id="07832-185">重新命名預存程序</span><span class="sxs-lookup"><span data-stu-id="07832-185">Rename a Stored Procedure</span></span>](../stored-procedures/rename-a-stored-procedure.md)|  
|<span data-ttu-id="07832-186">描述如何檢視預存程序的定義。</span><span class="sxs-lookup"><span data-stu-id="07832-186">Describes how to view the definition of a stored procedure.</span></span>|[<span data-ttu-id="07832-187">檢視預存程序的定義</span><span class="sxs-lookup"><span data-stu-id="07832-187">View the Definition of a Stored Procedure</span></span>](view-the-definition-of-a-stored-procedure.md)|  
|<span data-ttu-id="07832-188">描述如何檢視預存程序的相依性。</span><span class="sxs-lookup"><span data-stu-id="07832-188">Describes how to view the dependencies on a stored procedure.</span></span>|[<span data-ttu-id="07832-189">檢視預存程序的相依性</span><span class="sxs-lookup"><span data-stu-id="07832-189">View the Dependencies of a Stored Procedure</span></span>](view-the-dependencies-of-a-stored-procedure.md)|  
  
## <a name="related-content"></a><span data-ttu-id="07832-190">相關內容</span><span class="sxs-lookup"><span data-stu-id="07832-190">Related Content</span></span>  
 [<span data-ttu-id="07832-191">CLR 預存程序</span><span class="sxs-lookup"><span data-stu-id="07832-191">CLR Stored Procedures</span></span>](../../database-engine/dev-guide/clr-stored-procedures.md)  
  
  