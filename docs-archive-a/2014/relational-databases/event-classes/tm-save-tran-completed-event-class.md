---
title: 'TM: Save Tran Completed 事件類別 | Microsoft 文件'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- 'TM: Save Tran Completed event class'
ms.assetid: e6b37780-5ad8-4d50-89a3-d8a22496faac
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4ed85038d9cfc6281d1f9dbd84d4c0b0afeb43b3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686949"
---
# <a name="tm-save-tran-completed-event-class"></a><span data-ttu-id="7b4da-102">TM: Save Tran Completed 事件類別</span><span class="sxs-lookup"><span data-stu-id="7b4da-102">TM: Save Tran Completed Event Class</span></span>
  <span data-ttu-id="7b4da-103">TM: Save Tran Completed 事件類別指出已完成 SAVE TRANSACTION 要求。</span><span class="sxs-lookup"><span data-stu-id="7b4da-103">The TM: Save Tran Completed event class indicates that a SAVE TRANSACTION request has completed.</span></span> <span data-ttu-id="7b4da-104">要求是從用戶端透過交易管理介面傳送。</span><span class="sxs-lookup"><span data-stu-id="7b4da-104">The request was sent from the client through the transaction management interface.</span></span>  
  
## <a name="tm-save-tran-completed-event-class-data-columns"></a><span data-ttu-id="7b4da-105">TM: Save Tran Completed 事件類別資料行</span><span class="sxs-lookup"><span data-stu-id="7b4da-105">TM: Save Tran Completed Event Class Data Columns</span></span>  
  
|<span data-ttu-id="7b4da-106">資料行名稱</span><span class="sxs-lookup"><span data-stu-id="7b4da-106">Data column name</span></span>|<span data-ttu-id="7b4da-107">資料類型</span><span class="sxs-lookup"><span data-stu-id="7b4da-107">Data type</span></span>|<span data-ttu-id="7b4da-108">描述</span><span class="sxs-lookup"><span data-stu-id="7b4da-108">Description</span></span>|<span data-ttu-id="7b4da-109">資料行識別碼</span><span class="sxs-lookup"><span data-stu-id="7b4da-109">Column ID</span></span>|<span data-ttu-id="7b4da-110">可篩選</span><span class="sxs-lookup"><span data-stu-id="7b4da-110">Filterable</span></span>|  
|----------------------|---------------|-----------------|---------------|----------------|  
|<span data-ttu-id="7b4da-111">ApplicationName</span><span class="sxs-lookup"><span data-stu-id="7b4da-111">ApplicationName</span></span>|`nvarchar`|<span data-ttu-id="7b4da-112">建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="7b4da-112">Name of the client application that created the connection to an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="7b4da-113">這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="7b4da-113">This column is populated with the values passed by the application rather than the displayed name of the program.</span></span>|<span data-ttu-id="7b4da-114">10</span><span class="sxs-lookup"><span data-stu-id="7b4da-114">10</span></span>|<span data-ttu-id="7b4da-115">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-115">Yes</span></span>|  
|<span data-ttu-id="7b4da-116">ClientProcessID</span><span class="sxs-lookup"><span data-stu-id="7b4da-116">ClientProcessID</span></span>|`int`|<span data-ttu-id="7b4da-117">由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7b4da-117">ID assigned by the host computer to the process where the client application is running.</span></span> <span data-ttu-id="7b4da-118">如果用戶端提供處理序識別碼，這個資料行就會擴展。</span><span class="sxs-lookup"><span data-stu-id="7b4da-118">This data column is populated if the client process ID is provided by the client.</span></span>|<span data-ttu-id="7b4da-119">9</span><span class="sxs-lookup"><span data-stu-id="7b4da-119">9</span></span>|<span data-ttu-id="7b4da-120">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-120">Yes</span></span>|  
|<span data-ttu-id="7b4da-121">DatabaseID</span><span class="sxs-lookup"><span data-stu-id="7b4da-121">DatabaseID</span></span>|`int`|<span data-ttu-id="7b4da-122">由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7b4da-122">ID of the database specified by the USE *database* statement or the default database if no USE *database* statement has been issued for a given instance.</span></span> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] <span data-ttu-id="7b4da-123">如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="7b4da-123">displays the name of the database if the ServerName data column is captured in the trace and the server is available.</span></span> <span data-ttu-id="7b4da-124">請使用 DB_ID 函數判斷資料庫的值。</span><span class="sxs-lookup"><span data-stu-id="7b4da-124">Determine the value for a database by using the DB_ID function.</span></span>|<span data-ttu-id="7b4da-125">3</span><span class="sxs-lookup"><span data-stu-id="7b4da-125">3</span></span>|<span data-ttu-id="7b4da-126">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-126">Yes</span></span>|  
|<span data-ttu-id="7b4da-127">DatabaseName</span><span class="sxs-lookup"><span data-stu-id="7b4da-127">DatabaseName</span></span>|`nvarchar`|<span data-ttu-id="7b4da-128">正在執行使用者陳述式的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="7b4da-128">Name of the database in which the user statement is running.</span></span>|<span data-ttu-id="7b4da-129">35</span><span class="sxs-lookup"><span data-stu-id="7b4da-129">35</span></span>|<span data-ttu-id="7b4da-130">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-130">Yes</span></span>|  
|<span data-ttu-id="7b4da-131">錯誤</span><span class="sxs-lookup"><span data-stu-id="7b4da-131">Error</span></span>|`int`|<span data-ttu-id="7b4da-132">給定事件的錯誤號碼。</span><span class="sxs-lookup"><span data-stu-id="7b4da-132">Error number of a given event.</span></span> <span data-ttu-id="7b4da-133">通常這是存放在 sys.messages 目錄檢視中的錯誤號碼。</span><span class="sxs-lookup"><span data-stu-id="7b4da-133">Often this is the error number stored in the sys.messages catalog view.</span></span>|<span data-ttu-id="7b4da-134">31</span><span class="sxs-lookup"><span data-stu-id="7b4da-134">31</span></span>|<span data-ttu-id="7b4da-135">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-135">Yes</span></span>|  
|<span data-ttu-id="7b4da-136">EventClass</span><span class="sxs-lookup"><span data-stu-id="7b4da-136">EventClass</span></span>|`int`|<span data-ttu-id="7b4da-137">事件類型 = 192。</span><span class="sxs-lookup"><span data-stu-id="7b4da-137">Type of event = 192.</span></span>|<span data-ttu-id="7b4da-138">27</span><span class="sxs-lookup"><span data-stu-id="7b4da-138">27</span></span>|<span data-ttu-id="7b4da-139">否</span><span class="sxs-lookup"><span data-stu-id="7b4da-139">No</span></span>|  
|<span data-ttu-id="7b4da-140">EventSequence</span><span class="sxs-lookup"><span data-stu-id="7b4da-140">EventSequence</span></span>|`int`|<span data-ttu-id="7b4da-141">要求中的給定事件順序。</span><span class="sxs-lookup"><span data-stu-id="7b4da-141">Sequence of a given event within the request.</span></span>|<span data-ttu-id="7b4da-142">51</span><span class="sxs-lookup"><span data-stu-id="7b4da-142">51</span></span>|<span data-ttu-id="7b4da-143">否</span><span class="sxs-lookup"><span data-stu-id="7b4da-143">No</span></span>|  
|<span data-ttu-id="7b4da-144">GroupID</span><span class="sxs-lookup"><span data-stu-id="7b4da-144">GroupID</span></span>|`int`|<span data-ttu-id="7b4da-145">SQL 追蹤事件引發所在之工作負載群組的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7b4da-145">ID of the workload group where the SQL Trace event fires.</span></span>|<span data-ttu-id="7b4da-146">66</span><span class="sxs-lookup"><span data-stu-id="7b4da-146">66</span></span>|<span data-ttu-id="7b4da-147">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-147">Yes</span></span>|  
|<span data-ttu-id="7b4da-148">HostName</span><span class="sxs-lookup"><span data-stu-id="7b4da-148">HostName</span></span>|`nvarchar`|<span data-ttu-id="7b4da-149">執行用戶端的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="7b4da-149">Name of the computer on which the client is running.</span></span> <span data-ttu-id="7b4da-150">這個資料行會在用戶端提供主機名稱時填入。</span><span class="sxs-lookup"><span data-stu-id="7b4da-150">This data column is populated if the host name is provided by the client.</span></span> <span data-ttu-id="7b4da-151">若要判斷主機名稱，請使用 HOST_NAME 函數。</span><span class="sxs-lookup"><span data-stu-id="7b4da-151">To determine the host name, use the HOST_NAME function.</span></span>|<span data-ttu-id="7b4da-152">8</span><span class="sxs-lookup"><span data-stu-id="7b4da-152">8</span></span>|<span data-ttu-id="7b4da-153">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-153">Yes</span></span>|  
|<span data-ttu-id="7b4da-154">IsSystem</span><span class="sxs-lookup"><span data-stu-id="7b4da-154">IsSystem</span></span>|`int`|<span data-ttu-id="7b4da-155">指出事件是發生在系統處理序或使用者處理序。</span><span class="sxs-lookup"><span data-stu-id="7b4da-155">Indicates whether the event occurred on a system process or a user process.</span></span> <span data-ttu-id="7b4da-156">1 = 系統，0 = 使用者。</span><span class="sxs-lookup"><span data-stu-id="7b4da-156">1 = system, 0 = user.</span></span>|<span data-ttu-id="7b4da-157">60</span><span class="sxs-lookup"><span data-stu-id="7b4da-157">60</span></span>|<span data-ttu-id="7b4da-158">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-158">Yes</span></span>|  
|<span data-ttu-id="7b4da-159">LoginName</span><span class="sxs-lookup"><span data-stu-id="7b4da-159">LoginName</span></span>|`nvarchar`|<span data-ttu-id="7b4da-160">使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。</span><span class="sxs-lookup"><span data-stu-id="7b4da-160">Name of the login of the user (either [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] security login or the [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows login credentials in the form of DOMAIN\username).</span></span>|<span data-ttu-id="7b4da-161">11</span><span class="sxs-lookup"><span data-stu-id="7b4da-161">11</span></span>|<span data-ttu-id="7b4da-162">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-162">Yes</span></span>|  
|<span data-ttu-id="7b4da-163">LoginSid</span><span class="sxs-lookup"><span data-stu-id="7b4da-163">LoginSid</span></span>|`image`|<span data-ttu-id="7b4da-164">已登入之使用者的安全性識別碼 (SID)。</span><span class="sxs-lookup"><span data-stu-id="7b4da-164">Security identifier (SID) of the logged-in user.</span></span> <span data-ttu-id="7b4da-165">您可以在 sys.server_principals 目錄檢視中找到這項資訊。</span><span class="sxs-lookup"><span data-stu-id="7b4da-165">You can find this information in the sys.server_principals catalog view.</span></span> <span data-ttu-id="7b4da-166">伺服器上的每一個登入之 SID 是唯一的。</span><span class="sxs-lookup"><span data-stu-id="7b4da-166">Each SID is unique for each login in the server.</span></span>|<span data-ttu-id="7b4da-167">41</span><span class="sxs-lookup"><span data-stu-id="7b4da-167">41</span></span>|<span data-ttu-id="7b4da-168">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-168">Yes</span></span>|  
|<span data-ttu-id="7b4da-169">NTDomainName</span><span class="sxs-lookup"><span data-stu-id="7b4da-169">NTDomainName</span></span>|`nvarchar`|<span data-ttu-id="7b4da-170">使用者所隸屬的 Windows 網域。</span><span class="sxs-lookup"><span data-stu-id="7b4da-170">Windows domain to which the user belongs.</span></span>|<span data-ttu-id="7b4da-171">7</span><span class="sxs-lookup"><span data-stu-id="7b4da-171">7</span></span>|<span data-ttu-id="7b4da-172">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-172">Yes</span></span>|  
|<span data-ttu-id="7b4da-173">NTUserName</span><span class="sxs-lookup"><span data-stu-id="7b4da-173">NTUserName</span></span>|`nvarchar`|<span data-ttu-id="7b4da-174">Windows 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="7b4da-174">Windows user name.</span></span>|<span data-ttu-id="7b4da-175">6</span><span class="sxs-lookup"><span data-stu-id="7b4da-175">6</span></span>|<span data-ttu-id="7b4da-176">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-176">Yes</span></span>|  
|<span data-ttu-id="7b4da-177">RequestID</span><span class="sxs-lookup"><span data-stu-id="7b4da-177">RequestID</span></span>|`int`|<span data-ttu-id="7b4da-178">包含陳述式之要求的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7b4da-178">ID of the request containing the statement.</span></span>|<span data-ttu-id="7b4da-179">49</span><span class="sxs-lookup"><span data-stu-id="7b4da-179">49</span></span>|<span data-ttu-id="7b4da-180">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-180">Yes</span></span>|  
|<span data-ttu-id="7b4da-181">ServerName</span><span class="sxs-lookup"><span data-stu-id="7b4da-181">ServerName</span></span>|`nvarchar`|<span data-ttu-id="7b4da-182">正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="7b4da-182">Name of the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] being traced.</span></span>|<span data-ttu-id="7b4da-183">26</span><span class="sxs-lookup"><span data-stu-id="7b4da-183">26</span></span>|<span data-ttu-id="7b4da-184">否</span><span class="sxs-lookup"><span data-stu-id="7b4da-184">No</span></span>|  
|<span data-ttu-id="7b4da-185">SessionLoginName</span><span class="sxs-lookup"><span data-stu-id="7b4da-185">SessionLoginName</span></span>|`nvarchar`|<span data-ttu-id="7b4da-186">引發工作階段之使用者的登入名稱。</span><span class="sxs-lookup"><span data-stu-id="7b4da-186">Login name of the user who originated the session.</span></span> <span data-ttu-id="7b4da-187">例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。</span><span class="sxs-lookup"><span data-stu-id="7b4da-187">For example, if you connect to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] using Login1 and execute a statement as Login2, SessionLoginName shows Login1 and LoginName shows Login2.</span></span> <span data-ttu-id="7b4da-188">此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。</span><span class="sxs-lookup"><span data-stu-id="7b4da-188">This column displays both [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and Windows logins.</span></span>|<span data-ttu-id="7b4da-189">64</span><span class="sxs-lookup"><span data-stu-id="7b4da-189">64</span></span>|<span data-ttu-id="7b4da-190">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-190">Yes</span></span>|  
|<span data-ttu-id="7b4da-191">SPID</span><span class="sxs-lookup"><span data-stu-id="7b4da-191">SPID</span></span>|`int`|<span data-ttu-id="7b4da-192">事件發生所在之工作階段的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7b4da-192">ID of the session on which the event occurred.</span></span>|<span data-ttu-id="7b4da-193">12</span><span class="sxs-lookup"><span data-stu-id="7b4da-193">12</span></span>|<span data-ttu-id="7b4da-194">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-194">Yes</span></span>|  
|<span data-ttu-id="7b4da-195">StartTime</span><span class="sxs-lookup"><span data-stu-id="7b4da-195">StartTime</span></span>|`datetime`|<span data-ttu-id="7b4da-196">事件啟動的時間 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="7b4da-196">Time at which the event started, if available.</span></span>|<span data-ttu-id="7b4da-197">14</span><span class="sxs-lookup"><span data-stu-id="7b4da-197">14</span></span>|<span data-ttu-id="7b4da-198">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-198">Yes</span></span>|  
|<span data-ttu-id="7b4da-199">Success</span><span class="sxs-lookup"><span data-stu-id="7b4da-199">Success</span></span>|`int`|<span data-ttu-id="7b4da-200">1 = 成功。</span><span class="sxs-lookup"><span data-stu-id="7b4da-200">1 = success.</span></span> <span data-ttu-id="7b4da-201">0 = 失敗 (例如，1 表示權限檢查成功，而 0 表示該檢查失敗)。</span><span class="sxs-lookup"><span data-stu-id="7b4da-201">0 = failure (for example, a 1 means success of a permissions check and a 0 means a failure of that check).</span></span>|<span data-ttu-id="7b4da-202">23</span><span class="sxs-lookup"><span data-stu-id="7b4da-202">23</span></span>|<span data-ttu-id="7b4da-203">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-203">Yes</span></span>|  
|<span data-ttu-id="7b4da-204">TextData</span><span class="sxs-lookup"><span data-stu-id="7b4da-204">TextData</span></span>|`ntext`|<span data-ttu-id="7b4da-205">與追蹤中所擷取的事件類別有關的文字值。</span><span class="sxs-lookup"><span data-stu-id="7b4da-205">Text value dependent on the event class captured in the trace.</span></span>|<span data-ttu-id="7b4da-206">1</span><span class="sxs-lookup"><span data-stu-id="7b4da-206">1</span></span>|<span data-ttu-id="7b4da-207">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-207">Yes</span></span>|  
|<span data-ttu-id="7b4da-208">TransactionID</span><span class="sxs-lookup"><span data-stu-id="7b4da-208">TransactionID</span></span>|`bigint`|<span data-ttu-id="7b4da-209">由系統指派給交易的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7b4da-209">System-assigned ID of the transaction.</span></span>|<span data-ttu-id="7b4da-210">4</span><span class="sxs-lookup"><span data-stu-id="7b4da-210">4</span></span>|<span data-ttu-id="7b4da-211">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-211">Yes</span></span>|  
|<span data-ttu-id="7b4da-212">XactSequence</span><span class="sxs-lookup"><span data-stu-id="7b4da-212">XactSequence</span></span>|`bigint`|<span data-ttu-id="7b4da-213">描述目前交易的 Token。</span><span class="sxs-lookup"><span data-stu-id="7b4da-213">Token that describes the current transaction.</span></span>|<span data-ttu-id="7b4da-214">50</span><span class="sxs-lookup"><span data-stu-id="7b4da-214">50</span></span>|<span data-ttu-id="7b4da-215">是</span><span class="sxs-lookup"><span data-stu-id="7b4da-215">Yes</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="7b4da-216">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7b4da-216">See Also</span></span>  
 <span data-ttu-id="7b4da-217">[擴充事件](../extended-events/extended-events.md) </span><span class="sxs-lookup"><span data-stu-id="7b4da-217">[Extended Events](../extended-events/extended-events.md) </span></span>  
 <span data-ttu-id="7b4da-218">[sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="7b4da-218">[sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql) </span></span>  
 [<span data-ttu-id="7b4da-219">SAVE TRANSACTION &#40;Transact-SQL&#41;</span><span class="sxs-lookup"><span data-stu-id="7b4da-219">SAVE TRANSACTION &#40;Transact-SQL&#41;</span></span>](/sql/t-sql/language-elements/save-transaction-transact-sql)  
  
  