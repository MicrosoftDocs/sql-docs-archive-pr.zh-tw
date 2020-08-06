---
title: Database Mirroring Connection 事件類別 | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: b59dccc9-f40d-4c82-aa35-ac40acea86ff
author: stevestein
ms.author: sstein
ms.openlocfilehash: db652167bd3136b0c57e68ca1ada0f13d272d011
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705126"
---
# <a name="database-mirroring-connection-event-class"></a><span data-ttu-id="a69e9-102">資料庫鏡像連接事件類別</span><span class="sxs-lookup"><span data-stu-id="a69e9-102">Database Mirroring Connection Event Class</span></span>
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="a69e9-103">會產生 **資料庫鏡像連接** 事件，以報告資料庫鏡像所管理的傳輸連線狀態。</span><span class="sxs-lookup"><span data-stu-id="a69e9-103">generates a **Database Mirroring Connection** event to report the status of a transport connection managed by Database Mirroring.</span></span>  
  
## <a name="database-mirroringconnection-event-class-data-columns"></a><span data-ttu-id="a69e9-104">資料庫鏡像：連接事件類別資料行</span><span class="sxs-lookup"><span data-stu-id="a69e9-104">Database Mirroring:Connection Event Class Data Columns</span></span>  
  
|<span data-ttu-id="a69e9-105">資料行</span><span class="sxs-lookup"><span data-stu-id="a69e9-105">Data column</span></span>|<span data-ttu-id="a69e9-106">類型</span><span class="sxs-lookup"><span data-stu-id="a69e9-106">Type</span></span>|<span data-ttu-id="a69e9-107">描述</span><span class="sxs-lookup"><span data-stu-id="a69e9-107">Description</span></span>|<span data-ttu-id="a69e9-108">資料行編號</span><span class="sxs-lookup"><span data-stu-id="a69e9-108">Column number</span></span>|<span data-ttu-id="a69e9-109">可篩選</span><span class="sxs-lookup"><span data-stu-id="a69e9-109">Filterable</span></span>|  
|-----------------|----------|-----------------|-------------------|----------------|  
|<span data-ttu-id="a69e9-110">**ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="a69e9-110">**ApplicationName**</span></span>|`nvarchar`|<span data-ttu-id="a69e9-111">建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="a69e9-111">The name of the client application that created the connection to an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="a69e9-112">這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="a69e9-112">This column is populated with the values passed by the application rather than the displayed name of the program.</span></span>|<span data-ttu-id="a69e9-113">10</span><span class="sxs-lookup"><span data-stu-id="a69e9-113">10</span></span>|<span data-ttu-id="a69e9-114">是</span><span class="sxs-lookup"><span data-stu-id="a69e9-114">Yes</span></span>|  
|<span data-ttu-id="a69e9-115">**ClientProcessID**</span><span class="sxs-lookup"><span data-stu-id="a69e9-115">**ClientProcessID**</span></span>|`int`|<span data-ttu-id="a69e9-116">主機電腦指派給用戶端應用程式執行中處理序的識別碼。</span><span class="sxs-lookup"><span data-stu-id="a69e9-116">The ID assigned by the host computer to the process where the client application is running.</span></span> <span data-ttu-id="a69e9-117">如果用戶端提供處理序識別碼，這個資料行就會擴展。</span><span class="sxs-lookup"><span data-stu-id="a69e9-117">This data column is populated if the client process ID is provided by the client.</span></span>|<span data-ttu-id="a69e9-118">9</span><span class="sxs-lookup"><span data-stu-id="a69e9-118">9</span></span>|<span data-ttu-id="a69e9-119">是</span><span class="sxs-lookup"><span data-stu-id="a69e9-119">Yes</span></span>|  
|<span data-ttu-id="a69e9-120">**DatabaseID**</span><span class="sxs-lookup"><span data-stu-id="a69e9-120">**DatabaseID**</span></span>|`int`|<span data-ttu-id="a69e9-121">由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database*陳述式，則是預設資料庫的識別碼。</span><span class="sxs-lookup"><span data-stu-id="a69e9-121">The ID of the database specified by the USE *database* statement, or the ID of the default database if no USE *database*statement has been issued for a given instance.</span></span> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] <span data-ttu-id="a69e9-122">資料行，則 **ServerName** 會顯示資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="a69e9-122">displays the name of the database if the **ServerName** data column is captured in the trace and the server is available.</span></span> <span data-ttu-id="a69e9-123">使用**DB_ID**函數來決定資料庫的值。</span><span class="sxs-lookup"><span data-stu-id="a69e9-123">Determine the value for a database by using the **DB_ID** function.</span></span>|<span data-ttu-id="a69e9-124">3</span><span class="sxs-lookup"><span data-stu-id="a69e9-124">3</span></span>|<span data-ttu-id="a69e9-125">是</span><span class="sxs-lookup"><span data-stu-id="a69e9-125">Yes</span></span>|  
|<span data-ttu-id="a69e9-126">**錯誤**</span><span class="sxs-lookup"><span data-stu-id="a69e9-126">**Error**</span></span>|`int`|<span data-ttu-id="a69e9-127">事件中文字的訊息識別碼（以**sys.databases**表示）。</span><span class="sxs-lookup"><span data-stu-id="a69e9-127">The message ID number in **sys.messages** for the text in the event.</span></span> <span data-ttu-id="a69e9-128">如果此事件報告錯誤，這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤號碼。</span><span class="sxs-lookup"><span data-stu-id="a69e9-128">If this event reports an error, this is the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] error number.</span></span>|<span data-ttu-id="a69e9-129">31</span><span class="sxs-lookup"><span data-stu-id="a69e9-129">31</span></span>|<span data-ttu-id="a69e9-130">否</span><span class="sxs-lookup"><span data-stu-id="a69e9-130">No</span></span>|  
|<span data-ttu-id="a69e9-131">**EventClass**</span><span class="sxs-lookup"><span data-stu-id="a69e9-131">**EventClass**</span></span>|`int`|<span data-ttu-id="a69e9-132">擷取的事件類別類型。</span><span class="sxs-lookup"><span data-stu-id="a69e9-132">The type of event class captured.</span></span> <span data-ttu-id="a69e9-133">**資料庫鏡像連接** 一律為 **151**。</span><span class="sxs-lookup"><span data-stu-id="a69e9-133">Always **151** for **Database Mirroring Connection**.</span></span>|<span data-ttu-id="a69e9-134">27</span><span class="sxs-lookup"><span data-stu-id="a69e9-134">27</span></span>|<span data-ttu-id="a69e9-135">否</span><span class="sxs-lookup"><span data-stu-id="a69e9-135">No</span></span>|  
|<span data-ttu-id="a69e9-136">**EventSequence**</span><span class="sxs-lookup"><span data-stu-id="a69e9-136">**EventSequence**</span></span>|`int`|<span data-ttu-id="a69e9-137">此事件的序號。</span><span class="sxs-lookup"><span data-stu-id="a69e9-137">Sequence number for this event.</span></span>|<span data-ttu-id="a69e9-138">51</span><span class="sxs-lookup"><span data-stu-id="a69e9-138">51</span></span>|<span data-ttu-id="a69e9-139">否</span><span class="sxs-lookup"><span data-stu-id="a69e9-139">No</span></span>|  
|<span data-ttu-id="a69e9-140">**EventSubClass**</span><span class="sxs-lookup"><span data-stu-id="a69e9-140">**EventSubClass**</span></span>|`nvarchar`|<span data-ttu-id="a69e9-141">此連線的連線狀態。</span><span class="sxs-lookup"><span data-stu-id="a69e9-141">The connection state of this connection.</span></span> <span data-ttu-id="a69e9-142">對於此事件，子類別將為下列其中一個值。</span><span class="sxs-lookup"><span data-stu-id="a69e9-142">For this event, the subclass is one the following values.</span></span><br /><br /> <span data-ttu-id="a69e9-143">**正在連接**。</span><span class="sxs-lookup"><span data-stu-id="a69e9-143">**Connecting**.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="a69e9-144">正在起始傳輸連接。</span><span class="sxs-lookup"><span data-stu-id="a69e9-144">is initiating a transport connection.</span></span><br /><br /> <span data-ttu-id="a69e9-145">**已連線**。</span><span class="sxs-lookup"><span data-stu-id="a69e9-145">**Connected**.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="a69e9-146">已建立傳輸連接。</span><span class="sxs-lookup"><span data-stu-id="a69e9-146">has established a transport connection.</span></span><br /><br /> <span data-ttu-id="a69e9-147">**Connect Failed**。</span><span class="sxs-lookup"><span data-stu-id="a69e9-147">**Connect Failed**.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="a69e9-148">無法建立傳輸連接。</span><span class="sxs-lookup"><span data-stu-id="a69e9-148">failed to establish a transport connection.</span></span><br /><br /> <span data-ttu-id="a69e9-149">**關閉**。</span><span class="sxs-lookup"><span data-stu-id="a69e9-149">**Closing**.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="a69e9-150">正在關閉傳輸連接。</span><span class="sxs-lookup"><span data-stu-id="a69e9-150">is closing the transport connection.</span></span><br /><br /> <span data-ttu-id="a69e9-151">**已關閉**。</span><span class="sxs-lookup"><span data-stu-id="a69e9-151">**Closed**.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="a69e9-152">已經關閉傳輸連接。</span><span class="sxs-lookup"><span data-stu-id="a69e9-152">has closed the transport connection.</span></span><br /><br /> <span data-ttu-id="a69e9-153">**接受**。</span><span class="sxs-lookup"><span data-stu-id="a69e9-153">**Accept**.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="a69e9-154">已經接受另一個執行個體的傳輸連接。</span><span class="sxs-lookup"><span data-stu-id="a69e9-154">has accepted a transport connection from another instance.</span></span><br /><br /> <span data-ttu-id="a69e9-155">**Send IO Error**。</span><span class="sxs-lookup"><span data-stu-id="a69e9-155">**Send IO Error**.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="a69e9-156">在傳送訊息時遭遇到傳輸錯誤。</span><span class="sxs-lookup"><span data-stu-id="a69e9-156">encountered a transport error while sending a message.</span></span><br /><br /> <span data-ttu-id="a69e9-157">**Receive IO Error**。</span><span class="sxs-lookup"><span data-stu-id="a69e9-157">**Receive IO Error**.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="a69e9-158">在接收訊息時遭遇到傳輸錯誤。</span><span class="sxs-lookup"><span data-stu-id="a69e9-158">encountered a transport error while receiving a message.</span></span>|<span data-ttu-id="a69e9-159">21</span><span class="sxs-lookup"><span data-stu-id="a69e9-159">21</span></span>|<span data-ttu-id="a69e9-160">是</span><span class="sxs-lookup"><span data-stu-id="a69e9-160">Yes</span></span>|  
|<span data-ttu-id="a69e9-161">**GUID**</span><span class="sxs-lookup"><span data-stu-id="a69e9-161">**GUID**</span></span>|`uniqueidentifier`|<span data-ttu-id="a69e9-162">此連線的結束點識別碼。</span><span class="sxs-lookup"><span data-stu-id="a69e9-162">The endpoint ID of this connection.</span></span>|<span data-ttu-id="a69e9-163">54</span><span class="sxs-lookup"><span data-stu-id="a69e9-163">54</span></span>|<span data-ttu-id="a69e9-164">否</span><span class="sxs-lookup"><span data-stu-id="a69e9-164">No</span></span>|  
|<span data-ttu-id="a69e9-165">**HostName**</span><span class="sxs-lookup"><span data-stu-id="a69e9-165">**HostName**</span></span>|`nvarchar`|<span data-ttu-id="a69e9-166">執行用戶端的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="a69e9-166">The name of the computer on which the client is running.</span></span> <span data-ttu-id="a69e9-167">這個資料行會在用戶端提供主機名稱時填入。</span><span class="sxs-lookup"><span data-stu-id="a69e9-167">This data column is populated if the host name is provided by the client.</span></span> <span data-ttu-id="a69e9-168">若要判斷主機名稱，請使用**HOST_NAME**函數。</span><span class="sxs-lookup"><span data-stu-id="a69e9-168">To determine the host name, use the **HOST_NAME** function.</span></span>|<span data-ttu-id="a69e9-169">8</span><span class="sxs-lookup"><span data-stu-id="a69e9-169">8</span></span>|<span data-ttu-id="a69e9-170">是</span><span class="sxs-lookup"><span data-stu-id="a69e9-170">Yes</span></span>|  
|<span data-ttu-id="a69e9-171">**IntegerData**</span><span class="sxs-lookup"><span data-stu-id="a69e9-171">**IntegerData**</span></span>|`int`|<span data-ttu-id="a69e9-172">此連線已經關閉的次數</span><span class="sxs-lookup"><span data-stu-id="a69e9-172">The number of times this connection has been closed.</span></span>|<span data-ttu-id="a69e9-173">25</span><span class="sxs-lookup"><span data-stu-id="a69e9-173">25</span></span>|<span data-ttu-id="a69e9-174">是</span><span class="sxs-lookup"><span data-stu-id="a69e9-174">Yes</span></span>|  
|<span data-ttu-id="a69e9-175">**IsSystem**</span><span class="sxs-lookup"><span data-stu-id="a69e9-175">**IsSystem**</span></span>|`int`|<span data-ttu-id="a69e9-176">指出事件是發生在系統處理序或使用者處理序。</span><span class="sxs-lookup"><span data-stu-id="a69e9-176">Indicates whether the event occurred on a system process or a user process.</span></span><br /><br /> <span data-ttu-id="a69e9-177">0 = 使用者</span><span class="sxs-lookup"><span data-stu-id="a69e9-177">0 = user</span></span><br /><br /> <span data-ttu-id="a69e9-178">1 = 系統</span><span class="sxs-lookup"><span data-stu-id="a69e9-178">1 = system</span></span>|<span data-ttu-id="a69e9-179">60</span><span class="sxs-lookup"><span data-stu-id="a69e9-179">60</span></span>|<span data-ttu-id="a69e9-180">否</span><span class="sxs-lookup"><span data-stu-id="a69e9-180">No</span></span>|  
|<span data-ttu-id="a69e9-181">**LoginSid**</span><span class="sxs-lookup"><span data-stu-id="a69e9-181">**LoginSid**</span></span>|`image`|<span data-ttu-id="a69e9-182">已登入之使用者的安全性識別碼 (SID)。</span><span class="sxs-lookup"><span data-stu-id="a69e9-182">The security identification number (SID) of the logged-in user.</span></span> <span data-ttu-id="a69e9-183">伺服器上的每一個登入之 SID 是唯一的。</span><span class="sxs-lookup"><span data-stu-id="a69e9-183">Each SID is unique for each login in the server.</span></span>|<span data-ttu-id="a69e9-184">41</span><span class="sxs-lookup"><span data-stu-id="a69e9-184">41</span></span>|<span data-ttu-id="a69e9-185">是</span><span class="sxs-lookup"><span data-stu-id="a69e9-185">Yes</span></span>|  
|<span data-ttu-id="a69e9-186">**NTDomainName**</span><span class="sxs-lookup"><span data-stu-id="a69e9-186">**NTDomainName**</span></span>|`nvarchar`|<span data-ttu-id="a69e9-187">使用者所隸屬的 Windows 網域。</span><span class="sxs-lookup"><span data-stu-id="a69e9-187">The Windows domain to which the user belongs.</span></span>|<span data-ttu-id="a69e9-188">7</span><span class="sxs-lookup"><span data-stu-id="a69e9-188">7</span></span>|<span data-ttu-id="a69e9-189">是</span><span class="sxs-lookup"><span data-stu-id="a69e9-189">Yes</span></span>|  
|<span data-ttu-id="a69e9-190">**NTUserName**</span><span class="sxs-lookup"><span data-stu-id="a69e9-190">**NTUserName**</span></span>|`nvarchar`|<span data-ttu-id="a69e9-191">擁有產生此事件之連接的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="a69e9-191">The name of the user that owns the connection that generated this event.</span></span>|<span data-ttu-id="a69e9-192">6</span><span class="sxs-lookup"><span data-stu-id="a69e9-192">6</span></span>|<span data-ttu-id="a69e9-193">是</span><span class="sxs-lookup"><span data-stu-id="a69e9-193">Yes</span></span>|  
|<span data-ttu-id="a69e9-194">**ObjectName**</span><span class="sxs-lookup"><span data-stu-id="a69e9-194">**ObjectName**</span></span>|`nvarchar`|<span data-ttu-id="a69e9-195">對話的交談控制代碼。</span><span class="sxs-lookup"><span data-stu-id="a69e9-195">The conversation handle of the dialog.</span></span>|<span data-ttu-id="a69e9-196">34</span><span class="sxs-lookup"><span data-stu-id="a69e9-196">34</span></span>|<span data-ttu-id="a69e9-197">否</span><span class="sxs-lookup"><span data-stu-id="a69e9-197">No</span></span>|  
|<span data-ttu-id="a69e9-198">**ServerName**</span><span class="sxs-lookup"><span data-stu-id="a69e9-198">**ServerName**</span></span>|`nvarchar`|<span data-ttu-id="a69e9-199">正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="a69e9-199">The name of the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] being traced.</span></span>|<span data-ttu-id="a69e9-200">26</span><span class="sxs-lookup"><span data-stu-id="a69e9-200">26</span></span>|<span data-ttu-id="a69e9-201">否</span><span class="sxs-lookup"><span data-stu-id="a69e9-201">No</span></span>|  
|<span data-ttu-id="a69e9-202">**SPID**</span><span class="sxs-lookup"><span data-stu-id="a69e9-202">**SPID**</span></span>|`int`|<span data-ttu-id="a69e9-203">由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指派給用戶端關聯之處理序的伺服器處理序識別碼。</span><span class="sxs-lookup"><span data-stu-id="a69e9-203">The server process ID assigned by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] to the process associated with the client.</span></span>|<span data-ttu-id="a69e9-204">12</span><span class="sxs-lookup"><span data-stu-id="a69e9-204">12</span></span>|<span data-ttu-id="a69e9-205">是</span><span class="sxs-lookup"><span data-stu-id="a69e9-205">Yes</span></span>|  
|<span data-ttu-id="a69e9-206">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="a69e9-206">**StartTime**</span></span>|`datetime`|<span data-ttu-id="a69e9-207">事件啟動的時間 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="a69e9-207">The time at which the event started, when available.</span></span>|<span data-ttu-id="a69e9-208">14</span><span class="sxs-lookup"><span data-stu-id="a69e9-208">14</span></span>|<span data-ttu-id="a69e9-209">是</span><span class="sxs-lookup"><span data-stu-id="a69e9-209">Yes</span></span>|  
|<span data-ttu-id="a69e9-210">**TextData**</span><span class="sxs-lookup"><span data-stu-id="a69e9-210">**TextData**</span></span>|`ntext`|<span data-ttu-id="a69e9-211">與此事件相關的錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="a69e9-211">The text of the error message related to the event.</span></span> <span data-ttu-id="a69e9-212">對於未報告錯誤的事件，此欄位是空白的。</span><span class="sxs-lookup"><span data-stu-id="a69e9-212">For events that do not report an error, this field is empty.</span></span> <span data-ttu-id="a69e9-213">錯誤訊息有可能是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤訊息或是 Windows 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="a69e9-213">The error message may either be a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] error message or a Windows error message.</span></span>|<span data-ttu-id="a69e9-214">1</span><span class="sxs-lookup"><span data-stu-id="a69e9-214">1</span></span>|<span data-ttu-id="a69e9-215">是</span><span class="sxs-lookup"><span data-stu-id="a69e9-215">Yes</span></span>|  
|<span data-ttu-id="a69e9-216">**TransactionID**</span><span class="sxs-lookup"><span data-stu-id="a69e9-216">**TransactionID**</span></span>|`bigint`|<span data-ttu-id="a69e9-217">系統指派的交易識別碼。</span><span class="sxs-lookup"><span data-stu-id="a69e9-217">The system-assigned ID of the transaction.</span></span>|<span data-ttu-id="a69e9-218">4</span><span class="sxs-lookup"><span data-stu-id="a69e9-218">4</span></span>|<span data-ttu-id="a69e9-219">否</span><span class="sxs-lookup"><span data-stu-id="a69e9-219">No</span></span>|  
  
  