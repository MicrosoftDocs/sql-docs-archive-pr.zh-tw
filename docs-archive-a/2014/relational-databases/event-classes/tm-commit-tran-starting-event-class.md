---
title: 'TM: Commit Tran Starting 事件類別 | Microsoft 文件'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- 'TM: Commit Tran Starting event class'
ms.assetid: 3e1ac37e-6093-4dc9-9e5d-4270db18b547
author: stevestein
ms.author: sstein
ms.openlocfilehash: 82a806dd6beefe98094c4ba1d43ae0ae318aa16c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87710633"
---
# <a name="tm-commit-tran-starting-event-class"></a><span data-ttu-id="41a3d-102">TM: Commit Tran Starting 事件類別</span><span class="sxs-lookup"><span data-stu-id="41a3d-102">TM: Commit Tran Starting Event Class</span></span>
  <span data-ttu-id="41a3d-103">TM: Commit Tran Starting 事件類別指出正在啟動 COMMIT TRANSACTION 要求。</span><span class="sxs-lookup"><span data-stu-id="41a3d-103">The TM: Commit Tran Starting event class indicates that a COMMIT TRANSACTION request is starting.</span></span> <span data-ttu-id="41a3d-104">要求是從用戶端透過交易管理介面傳送。</span><span class="sxs-lookup"><span data-stu-id="41a3d-104">The request is sent from the client through the transaction management interface.</span></span> <span data-ttu-id="41a3d-105">EventSubClass 資料行指出在認可目前交易之後，是否會啟動新交易。</span><span class="sxs-lookup"><span data-stu-id="41a3d-105">The EventSubClass column indicates if a new transaction will be started after the current transaction is committed.</span></span>  
  
## <a name="tm-commit-tran-starting-event-class-data-columns"></a><span data-ttu-id="41a3d-106">TM: Commit Tran Starting 事件類別資料行</span><span class="sxs-lookup"><span data-stu-id="41a3d-106">TM: Commit Tran Starting Event Class Data Columns</span></span>  
  
|<span data-ttu-id="41a3d-107">資料行名稱</span><span class="sxs-lookup"><span data-stu-id="41a3d-107">Data column name</span></span>|<span data-ttu-id="41a3d-108">資料類型</span><span class="sxs-lookup"><span data-stu-id="41a3d-108">Data type</span></span>|<span data-ttu-id="41a3d-109">描述</span><span class="sxs-lookup"><span data-stu-id="41a3d-109">Description</span></span>|<span data-ttu-id="41a3d-110">資料行識別碼</span><span class="sxs-lookup"><span data-stu-id="41a3d-110">Column ID</span></span>|<span data-ttu-id="41a3d-111">可篩選</span><span class="sxs-lookup"><span data-stu-id="41a3d-111">Filterable</span></span>|  
|----------------------|---------------|-----------------|---------------|----------------|  
|<span data-ttu-id="41a3d-112">ApplicationName</span><span class="sxs-lookup"><span data-stu-id="41a3d-112">ApplicationName</span></span>|`nvarchar`|<span data-ttu-id="41a3d-113">建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="41a3d-113">Name of the client application that created the connection to an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="41a3d-114">這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="41a3d-114">This column is populated with the values passed by the application rather than the displayed name of the program.</span></span>|<span data-ttu-id="41a3d-115">10</span><span class="sxs-lookup"><span data-stu-id="41a3d-115">10</span></span>|<span data-ttu-id="41a3d-116">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-116">Yes</span></span>|  
|<span data-ttu-id="41a3d-117">ClientProcessID</span><span class="sxs-lookup"><span data-stu-id="41a3d-117">ClientProcessID</span></span>|`int`|<span data-ttu-id="41a3d-118">由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="41a3d-118">ID assigned by the host computer to the process where the client application is running.</span></span> <span data-ttu-id="41a3d-119">如果用戶端提供處理序識別碼，這個資料行就會擴展。</span><span class="sxs-lookup"><span data-stu-id="41a3d-119">This data column is populated if the client process ID is provided by the client.</span></span>|<span data-ttu-id="41a3d-120">9</span><span class="sxs-lookup"><span data-stu-id="41a3d-120">9</span></span>|<span data-ttu-id="41a3d-121">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-121">Yes</span></span>|  
|<span data-ttu-id="41a3d-122">DatabaseID</span><span class="sxs-lookup"><span data-stu-id="41a3d-122">DatabaseID</span></span>|`int`|<span data-ttu-id="41a3d-123">由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。</span><span class="sxs-lookup"><span data-stu-id="41a3d-123">ID of the database specified by the USE *database* statement or the default database if no USE *database* statement has been issued for a given instance.</span></span> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] <span data-ttu-id="41a3d-124">如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="41a3d-124">displays the name of the database if the ServerName data column is captured in the trace and the server is available.</span></span> <span data-ttu-id="41a3d-125">請使用 DB_ID 函數判斷資料庫的值。</span><span class="sxs-lookup"><span data-stu-id="41a3d-125">Determine the value for a database by using the DB_ID function.</span></span>|<span data-ttu-id="41a3d-126">3</span><span class="sxs-lookup"><span data-stu-id="41a3d-126">3</span></span>|<span data-ttu-id="41a3d-127">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-127">Yes</span></span>|  
|<span data-ttu-id="41a3d-128">DatabaseName</span><span class="sxs-lookup"><span data-stu-id="41a3d-128">DatabaseName</span></span>|`nvarchar`|<span data-ttu-id="41a3d-129">正在執行使用者陳述式的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="41a3d-129">Name of the database in which the user statement is running.</span></span>|<span data-ttu-id="41a3d-130">35</span><span class="sxs-lookup"><span data-stu-id="41a3d-130">35</span></span>|<span data-ttu-id="41a3d-131">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-131">Yes</span></span>|  
|<span data-ttu-id="41a3d-132">EventClass</span><span class="sxs-lookup"><span data-stu-id="41a3d-132">EventClass</span></span>|`int`|<span data-ttu-id="41a3d-133">事件類型 = 185。</span><span class="sxs-lookup"><span data-stu-id="41a3d-133">Type of event = 185.</span></span>|<span data-ttu-id="41a3d-134">27</span><span class="sxs-lookup"><span data-stu-id="41a3d-134">27</span></span>|<span data-ttu-id="41a3d-135">否</span><span class="sxs-lookup"><span data-stu-id="41a3d-135">No</span></span>|  
|<span data-ttu-id="41a3d-136">EventSequence</span><span class="sxs-lookup"><span data-stu-id="41a3d-136">EventSequence</span></span>|`int`|<span data-ttu-id="41a3d-137">要求中的給定事件順序。</span><span class="sxs-lookup"><span data-stu-id="41a3d-137">Sequence of a given event within the request.</span></span>|<span data-ttu-id="41a3d-138">51</span><span class="sxs-lookup"><span data-stu-id="41a3d-138">51</span></span>|<span data-ttu-id="41a3d-139">否</span><span class="sxs-lookup"><span data-stu-id="41a3d-139">No</span></span>|  
|<span data-ttu-id="41a3d-140">EventSubClass</span><span class="sxs-lookup"><span data-stu-id="41a3d-140">EventSubClass</span></span>|`int`|<span data-ttu-id="41a3d-141">事件子類別的類型。</span><span class="sxs-lookup"><span data-stu-id="41a3d-141">Type of event subclass.</span></span><br /><br /> <span data-ttu-id="41a3d-142">1=認可</span><span class="sxs-lookup"><span data-stu-id="41a3d-142">1=Commit</span></span><br /><br /> <span data-ttu-id="41a3d-143">2=認可並開始</span><span class="sxs-lookup"><span data-stu-id="41a3d-143">2=Commit and Begin</span></span>|<span data-ttu-id="41a3d-144">21</span><span class="sxs-lookup"><span data-stu-id="41a3d-144">21</span></span>|<span data-ttu-id="41a3d-145">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-145">Yes</span></span>|  
|<span data-ttu-id="41a3d-146">GroupID</span><span class="sxs-lookup"><span data-stu-id="41a3d-146">GroupID</span></span>|`int`|<span data-ttu-id="41a3d-147">SQL 追蹤事件引發所在之工作負載群組的識別碼。</span><span class="sxs-lookup"><span data-stu-id="41a3d-147">ID of the workload group where the SQL Trace event fires.</span></span>|<span data-ttu-id="41a3d-148">66</span><span class="sxs-lookup"><span data-stu-id="41a3d-148">66</span></span>|<span data-ttu-id="41a3d-149">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-149">Yes</span></span>|  
|<span data-ttu-id="41a3d-150">HostName</span><span class="sxs-lookup"><span data-stu-id="41a3d-150">HostName</span></span>|`nvarchar`|<span data-ttu-id="41a3d-151">執行用戶端的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="41a3d-151">Name of the computer on which the client is running.</span></span> <span data-ttu-id="41a3d-152">如果用戶端提供主機名稱，這個資料行就會擴展。</span><span class="sxs-lookup"><span data-stu-id="41a3d-152">This data column is populated if the client provides the host name.</span></span> <span data-ttu-id="41a3d-153">若要判斷主機名稱，請使用 HOST_NAME 函數。</span><span class="sxs-lookup"><span data-stu-id="41a3d-153">To determine the host name, use the HOST_NAME function.</span></span>|<span data-ttu-id="41a3d-154">8</span><span class="sxs-lookup"><span data-stu-id="41a3d-154">8</span></span>|<span data-ttu-id="41a3d-155">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-155">Yes</span></span>|  
|<span data-ttu-id="41a3d-156">IsSystem</span><span class="sxs-lookup"><span data-stu-id="41a3d-156">IsSystem</span></span>|`int`|<span data-ttu-id="41a3d-157">指出事件是發生在系統處理序或使用者處理序。</span><span class="sxs-lookup"><span data-stu-id="41a3d-157">Indicates whether the event occurred on a system process or a user process.</span></span> <span data-ttu-id="41a3d-158">1 = 系統，0 = 使用者。</span><span class="sxs-lookup"><span data-stu-id="41a3d-158">1 = system, 0 = user.</span></span>|<span data-ttu-id="41a3d-159">60</span><span class="sxs-lookup"><span data-stu-id="41a3d-159">60</span></span>|<span data-ttu-id="41a3d-160">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-160">Yes</span></span>|  
|<span data-ttu-id="41a3d-161">LoginName</span><span class="sxs-lookup"><span data-stu-id="41a3d-161">LoginName</span></span>|`nvarchar`|<span data-ttu-id="41a3d-162">使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。</span><span class="sxs-lookup"><span data-stu-id="41a3d-162">Name of the login of the user (either [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] security login or the [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows login credentials in the form of DOMAIN\username).</span></span>|<span data-ttu-id="41a3d-163">11</span><span class="sxs-lookup"><span data-stu-id="41a3d-163">11</span></span>|<span data-ttu-id="41a3d-164">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-164">Yes</span></span>|  
|<span data-ttu-id="41a3d-165">LoginSid</span><span class="sxs-lookup"><span data-stu-id="41a3d-165">LoginSid</span></span>|`image`|<span data-ttu-id="41a3d-166">已登入之使用者的安全性識別碼 (SID)。</span><span class="sxs-lookup"><span data-stu-id="41a3d-166">Security identification number (SID) of the logged-in user.</span></span> <span data-ttu-id="41a3d-167">您可以在 sys.server_principals 目錄檢視中找到這項資訊。</span><span class="sxs-lookup"><span data-stu-id="41a3d-167">You can find this information in the sys.server_principals catalog view.</span></span> <span data-ttu-id="41a3d-168">伺服器上的每一個登入之 SID 是唯一的。</span><span class="sxs-lookup"><span data-stu-id="41a3d-168">Each SID is unique for each login in the server.</span></span>|<span data-ttu-id="41a3d-169">41</span><span class="sxs-lookup"><span data-stu-id="41a3d-169">41</span></span>|<span data-ttu-id="41a3d-170">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-170">Yes</span></span>|  
|<span data-ttu-id="41a3d-171">NTDomainName</span><span class="sxs-lookup"><span data-stu-id="41a3d-171">NTDomainName</span></span>|`nvarchar`|<span data-ttu-id="41a3d-172">使用者所隸屬的 Windows 網域。</span><span class="sxs-lookup"><span data-stu-id="41a3d-172">Windows domain to which the user belongs.</span></span>|<span data-ttu-id="41a3d-173">7</span><span class="sxs-lookup"><span data-stu-id="41a3d-173">7</span></span>|<span data-ttu-id="41a3d-174">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-174">Yes</span></span>|  
|<span data-ttu-id="41a3d-175">NTUserName</span><span class="sxs-lookup"><span data-stu-id="41a3d-175">NTUserName</span></span>|`nvarchar`|<span data-ttu-id="41a3d-176">Windows 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="41a3d-176">Windows user name.</span></span>|<span data-ttu-id="41a3d-177">6</span><span class="sxs-lookup"><span data-stu-id="41a3d-177">6</span></span>|<span data-ttu-id="41a3d-178">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-178">Yes</span></span>|  
|<span data-ttu-id="41a3d-179">RequestID</span><span class="sxs-lookup"><span data-stu-id="41a3d-179">RequestID</span></span>|`int`|<span data-ttu-id="41a3d-180">包含陳述式之要求的識別碼。</span><span class="sxs-lookup"><span data-stu-id="41a3d-180">ID of the request containing the statement.</span></span>|<span data-ttu-id="41a3d-181">49</span><span class="sxs-lookup"><span data-stu-id="41a3d-181">49</span></span>|<span data-ttu-id="41a3d-182">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-182">Yes</span></span>|  
|<span data-ttu-id="41a3d-183">ServerName</span><span class="sxs-lookup"><span data-stu-id="41a3d-183">ServerName</span></span>|`nvarchar`|<span data-ttu-id="41a3d-184">正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="41a3d-184">Name of the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] being traced.</span></span>|<span data-ttu-id="41a3d-185">26</span><span class="sxs-lookup"><span data-stu-id="41a3d-185">26</span></span>|<span data-ttu-id="41a3d-186">否</span><span class="sxs-lookup"><span data-stu-id="41a3d-186">No</span></span>|  
|<span data-ttu-id="41a3d-187">SessionLoginName</span><span class="sxs-lookup"><span data-stu-id="41a3d-187">SessionLoginName</span></span>|`nvarchar`|<span data-ttu-id="41a3d-188">引發工作階段之使用者的登入名稱。</span><span class="sxs-lookup"><span data-stu-id="41a3d-188">Login name of the user who originated the session.</span></span> <span data-ttu-id="41a3d-189">例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。</span><span class="sxs-lookup"><span data-stu-id="41a3d-189">For example, if you connect to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] using Login1 and execute a statement as Login2, SessionLoginName shows Login1 and LoginName shows Login2.</span></span> <span data-ttu-id="41a3d-190">此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。</span><span class="sxs-lookup"><span data-stu-id="41a3d-190">This column displays both [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and Windows logins.</span></span>|<span data-ttu-id="41a3d-191">64</span><span class="sxs-lookup"><span data-stu-id="41a3d-191">64</span></span>|<span data-ttu-id="41a3d-192">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-192">Yes</span></span>|  
|<span data-ttu-id="41a3d-193">SPID</span><span class="sxs-lookup"><span data-stu-id="41a3d-193">SPID</span></span>|`int`|<span data-ttu-id="41a3d-194">事件發生所在之工作階段的識別碼。</span><span class="sxs-lookup"><span data-stu-id="41a3d-194">ID of the session on which the event occurred.</span></span>|<span data-ttu-id="41a3d-195">12</span><span class="sxs-lookup"><span data-stu-id="41a3d-195">12</span></span>|<span data-ttu-id="41a3d-196">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-196">Yes</span></span>|  
|<span data-ttu-id="41a3d-197">StartTime</span><span class="sxs-lookup"><span data-stu-id="41a3d-197">StartTime</span></span>|`datetime`|<span data-ttu-id="41a3d-198">事件的開始時間 (如果可以取得的話)。</span><span class="sxs-lookup"><span data-stu-id="41a3d-198">Time at which the event started, when available.</span></span>|<span data-ttu-id="41a3d-199">14</span><span class="sxs-lookup"><span data-stu-id="41a3d-199">14</span></span>|<span data-ttu-id="41a3d-200">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-200">Yes</span></span>|  
|<span data-ttu-id="41a3d-201">TextData</span><span class="sxs-lookup"><span data-stu-id="41a3d-201">TextData</span></span>|`ntext`|<span data-ttu-id="41a3d-202">與追蹤中所擷取的事件類別有關的文字值。</span><span class="sxs-lookup"><span data-stu-id="41a3d-202">Text value dependent on the event class captured in the trace.</span></span>|<span data-ttu-id="41a3d-203">1</span><span class="sxs-lookup"><span data-stu-id="41a3d-203">1</span></span>|<span data-ttu-id="41a3d-204">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-204">Yes</span></span>|  
|<span data-ttu-id="41a3d-205">TransactionID</span><span class="sxs-lookup"><span data-stu-id="41a3d-205">TransactionID</span></span>|`bigint`|<span data-ttu-id="41a3d-206">由系統指派給交易的識別碼。</span><span class="sxs-lookup"><span data-stu-id="41a3d-206">System-assigned ID of the transaction.</span></span>|<span data-ttu-id="41a3d-207">4</span><span class="sxs-lookup"><span data-stu-id="41a3d-207">4</span></span>|<span data-ttu-id="41a3d-208">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-208">Yes</span></span>|  
|<span data-ttu-id="41a3d-209">XactSequence</span><span class="sxs-lookup"><span data-stu-id="41a3d-209">XactSequence</span></span>|`bigint`|<span data-ttu-id="41a3d-210">描述目前交易的 Token。</span><span class="sxs-lookup"><span data-stu-id="41a3d-210">Token that describes the current transaction.</span></span>|<span data-ttu-id="41a3d-211">50</span><span class="sxs-lookup"><span data-stu-id="41a3d-211">50</span></span>|<span data-ttu-id="41a3d-212">是</span><span class="sxs-lookup"><span data-stu-id="41a3d-212">Yes</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="41a3d-213">另請參閱</span><span class="sxs-lookup"><span data-stu-id="41a3d-213">See Also</span></span>  
 <span data-ttu-id="41a3d-214">[COMMIT TRANSACTION &#40;Transact-sql&#41;](/sql/t-sql/language-elements/commit-transaction-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="41a3d-214">[COMMIT TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/commit-transaction-transact-sql) </span></span>  
 [<span data-ttu-id="41a3d-215">sp_trace_setevent &#40;Transact-SQL&#41;</span><span class="sxs-lookup"><span data-stu-id="41a3d-215">sp_trace_setevent &#40;Transact-SQL&#41;</span></span>](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  