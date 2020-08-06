---
title: Broker:Conversation 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Conversation event class
ms.assetid: 784707b5-cc67-46a3-8ae6-8f8ecf4b27c0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 921b23c6aab8be27534d67d7a85bd7adc8258409
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705133"
---
# <a name="brokerconversation-event-class"></a><span data-ttu-id="170a8-102">Broker:Conversation 事件類別</span><span class="sxs-lookup"><span data-stu-id="170a8-102">Broker:Conversation Event Class</span></span>
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="170a8-103">產生 **Broker:Conversation** 事件以報告 Service Broker 交談的進度。</span><span class="sxs-lookup"><span data-stu-id="170a8-103">generates a **Broker:Conversation** event to report the progress of a Service Broker conversation.</span></span>  
  
## <a name="brokerconversation-event-class-data-columns"></a><span data-ttu-id="170a8-104">Broker:Conversation 事件類別資料行</span><span class="sxs-lookup"><span data-stu-id="170a8-104">Broker:Conversation Event Class Data Columns</span></span>  
  
|<span data-ttu-id="170a8-105">資料行</span><span class="sxs-lookup"><span data-stu-id="170a8-105">Data column</span></span>|<span data-ttu-id="170a8-106">類型</span><span class="sxs-lookup"><span data-stu-id="170a8-106">Type</span></span>|<span data-ttu-id="170a8-107">描述</span><span class="sxs-lookup"><span data-stu-id="170a8-107">Description</span></span>|<span data-ttu-id="170a8-108">資料行編號</span><span class="sxs-lookup"><span data-stu-id="170a8-108">Column number</span></span>|<span data-ttu-id="170a8-109">可篩選</span><span class="sxs-lookup"><span data-stu-id="170a8-109">Filterable</span></span>|  
|-----------------|----------|-----------------|-------------------|----------------|  
|<span data-ttu-id="170a8-110">**ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="170a8-110">**ApplicationName**</span></span>|`nvarchar`|<span data-ttu-id="170a8-111">建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="170a8-111">The name of the client application that created the connection to an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="170a8-112">這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="170a8-112">This column is populated with the values passed by the application instead of the displayed name of the program.</span></span>|<span data-ttu-id="170a8-113">10</span><span class="sxs-lookup"><span data-stu-id="170a8-113">10</span></span>|<span data-ttu-id="170a8-114">是</span><span class="sxs-lookup"><span data-stu-id="170a8-114">Yes</span></span>|  
|<span data-ttu-id="170a8-115">**ClientProcessID**</span><span class="sxs-lookup"><span data-stu-id="170a8-115">**ClientProcessID**</span></span>|`int`|<span data-ttu-id="170a8-116">主機電腦指派給用戶端應用程式執行中處理序的識別碼。</span><span class="sxs-lookup"><span data-stu-id="170a8-116">The ID assigned by the host computer to the process where the client application is running.</span></span> <span data-ttu-id="170a8-117">如果用戶端提供處理序識別碼，這個資料行就會擴展。</span><span class="sxs-lookup"><span data-stu-id="170a8-117">This data column is populated if the client process ID is provided by the client.</span></span>|<span data-ttu-id="170a8-118">9</span><span class="sxs-lookup"><span data-stu-id="170a8-118">9</span></span>|<span data-ttu-id="170a8-119">是</span><span class="sxs-lookup"><span data-stu-id="170a8-119">Yes</span></span>|  
|<span data-ttu-id="170a8-120">**DatabaseID**</span><span class="sxs-lookup"><span data-stu-id="170a8-120">**DatabaseID**</span></span>|`int`|<span data-ttu-id="170a8-121">USE *database* 陳述式指定之資料庫的識別碼。</span><span class="sxs-lookup"><span data-stu-id="170a8-121">The ID of the database that is specified by the USE *database* statement.</span></span> <span data-ttu-id="170a8-122">如果未發出 USE *database*陳述式，則為預設資料庫的識別碼。</span><span class="sxs-lookup"><span data-stu-id="170a8-122">If no USE *database*statement has been issued, the ID of the default database.</span></span> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] <span data-ttu-id="170a8-123">資料行，則 **ServerName** 會顯示資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="170a8-123">displays the name of the database if the **ServerName** data column is captured in the trace and the server is available.</span></span> <span data-ttu-id="170a8-124">使用**DB_ID**函數來決定資料庫的值。</span><span class="sxs-lookup"><span data-stu-id="170a8-124">Determine the value for a database by using the **DB_ID** function.</span></span>|<span data-ttu-id="170a8-125">3</span><span class="sxs-lookup"><span data-stu-id="170a8-125">3</span></span>|<span data-ttu-id="170a8-126">是</span><span class="sxs-lookup"><span data-stu-id="170a8-126">Yes</span></span>|  
|<span data-ttu-id="170a8-127">**EventClass**</span><span class="sxs-lookup"><span data-stu-id="170a8-127">**EventClass**</span></span>|`int`|<span data-ttu-id="170a8-128">擷取的事件類別類型。</span><span class="sxs-lookup"><span data-stu-id="170a8-128">The type of event class captured.</span></span> <span data-ttu-id="170a8-129">**Broker:Conversation** 永遠為 **124**。</span><span class="sxs-lookup"><span data-stu-id="170a8-129">Always **124** for **Broker:Conversation**.</span></span>|<span data-ttu-id="170a8-130">27</span><span class="sxs-lookup"><span data-stu-id="170a8-130">27</span></span>|<span data-ttu-id="170a8-131">否</span><span class="sxs-lookup"><span data-stu-id="170a8-131">No</span></span>|  
|<span data-ttu-id="170a8-132">**EventSequence**</span><span class="sxs-lookup"><span data-stu-id="170a8-132">**EventSequence**</span></span>|`int`|<span data-ttu-id="170a8-133">此事件的序號。</span><span class="sxs-lookup"><span data-stu-id="170a8-133">Sequence number for this event.</span></span>|<span data-ttu-id="170a8-134">51</span><span class="sxs-lookup"><span data-stu-id="170a8-134">51</span></span>|<span data-ttu-id="170a8-135">否</span><span class="sxs-lookup"><span data-stu-id="170a8-135">No</span></span>|  
|<span data-ttu-id="170a8-136">**EventSubClass**</span><span class="sxs-lookup"><span data-stu-id="170a8-136">**EventSubClass**</span></span>|`nvarchar`|<span data-ttu-id="170a8-137">事件子類別的類型。</span><span class="sxs-lookup"><span data-stu-id="170a8-137">The type of event subclass.</span></span> <span data-ttu-id="170a8-138">這會提供有關每一個事件類別的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="170a8-138">This provides more information about each event class.</span></span>|<span data-ttu-id="170a8-139">21</span><span class="sxs-lookup"><span data-stu-id="170a8-139">21</span></span>|<span data-ttu-id="170a8-140">是</span><span class="sxs-lookup"><span data-stu-id="170a8-140">Yes</span></span>|  
|<span data-ttu-id="170a8-141">**GUID**</span><span class="sxs-lookup"><span data-stu-id="170a8-141">**GUID**</span></span>|`uniqueidentifier`|<span data-ttu-id="170a8-142">對話的交談識別碼。</span><span class="sxs-lookup"><span data-stu-id="170a8-142">The conversation ID of the dialog.</span></span> <span data-ttu-id="170a8-143">此識別碼是以訊息的一部份傳送，並在交談的兩端之間共用。</span><span class="sxs-lookup"><span data-stu-id="170a8-143">This identifier is transmitted as part of the message, and is shared between both sides of the conversation.</span></span>|<span data-ttu-id="170a8-144">54</span><span class="sxs-lookup"><span data-stu-id="170a8-144">54</span></span>|<span data-ttu-id="170a8-145">否</span><span class="sxs-lookup"><span data-stu-id="170a8-145">No</span></span>|  
|<span data-ttu-id="170a8-146">**HostName**</span><span class="sxs-lookup"><span data-stu-id="170a8-146">**HostName**</span></span>|`nvarchar`|<span data-ttu-id="170a8-147">執行用戶端的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="170a8-147">The name of the computer on which the client is running.</span></span> <span data-ttu-id="170a8-148">這個資料行會在用戶端提供主機名稱時填入。</span><span class="sxs-lookup"><span data-stu-id="170a8-148">This data column is populated if the host name is provided by the client.</span></span> <span data-ttu-id="170a8-149">若要判斷主機名稱，請使用**HOST_NAME**函數。</span><span class="sxs-lookup"><span data-stu-id="170a8-149">To determine the host name, use the **HOST_NAME** function.</span></span>|<span data-ttu-id="170a8-150">8</span><span class="sxs-lookup"><span data-stu-id="170a8-150">8</span></span>|<span data-ttu-id="170a8-151">是</span><span class="sxs-lookup"><span data-stu-id="170a8-151">Yes</span></span>|  
|<span data-ttu-id="170a8-152">**IsSystem**</span><span class="sxs-lookup"><span data-stu-id="170a8-152">**IsSystem**</span></span>|`int`|<span data-ttu-id="170a8-153">指出事件是發生在系統處理序或使用者處理序。</span><span class="sxs-lookup"><span data-stu-id="170a8-153">Indicates whether the event occurred on a system process or a user process.</span></span><br /><br /> <span data-ttu-id="170a8-154">0 = 使用者</span><span class="sxs-lookup"><span data-stu-id="170a8-154">0 = user</span></span><br /><br /> <span data-ttu-id="170a8-155">1 = 系統</span><span class="sxs-lookup"><span data-stu-id="170a8-155">1 = system</span></span>|<span data-ttu-id="170a8-156">60</span><span class="sxs-lookup"><span data-stu-id="170a8-156">60</span></span>|<span data-ttu-id="170a8-157">否</span><span class="sxs-lookup"><span data-stu-id="170a8-157">No</span></span>|  
|<span data-ttu-id="170a8-158">**LoginSid**</span><span class="sxs-lookup"><span data-stu-id="170a8-158">**LoginSid**</span></span>|`image`|<span data-ttu-id="170a8-159">已登入之使用者的安全性識別碼 (SID)。</span><span class="sxs-lookup"><span data-stu-id="170a8-159">The security identification number (SID) of the logged-in user.</span></span> <span data-ttu-id="170a8-160">伺服器上的每一個登入之 SID 是唯一的。</span><span class="sxs-lookup"><span data-stu-id="170a8-160">Each SID is unique for each login in the server.</span></span>|<span data-ttu-id="170a8-161">41</span><span class="sxs-lookup"><span data-stu-id="170a8-161">41</span></span>|<span data-ttu-id="170a8-162">是</span><span class="sxs-lookup"><span data-stu-id="170a8-162">Yes</span></span>|  
|<span data-ttu-id="170a8-163">**名稱**</span><span class="sxs-lookup"><span data-stu-id="170a8-163">**MethodName**</span></span>|`nvarchar`|<span data-ttu-id="170a8-164">交談所屬的交談群組。</span><span class="sxs-lookup"><span data-stu-id="170a8-164">The conversation group that the conversation belongs to.</span></span>|<span data-ttu-id="170a8-165">47</span><span class="sxs-lookup"><span data-stu-id="170a8-165">47</span></span>|<span data-ttu-id="170a8-166">否</span><span class="sxs-lookup"><span data-stu-id="170a8-166">No</span></span>|  
|<span data-ttu-id="170a8-167">**NTDomainName**</span><span class="sxs-lookup"><span data-stu-id="170a8-167">**NTDomainName**</span></span>|`nvarchar`|<span data-ttu-id="170a8-168">使用者所隸屬的 Windows 網域。</span><span class="sxs-lookup"><span data-stu-id="170a8-168">The Windows domain to which the user belongs.</span></span>|<span data-ttu-id="170a8-169">7</span><span class="sxs-lookup"><span data-stu-id="170a8-169">7</span></span>|<span data-ttu-id="170a8-170">是</span><span class="sxs-lookup"><span data-stu-id="170a8-170">Yes</span></span>|  
|<span data-ttu-id="170a8-171">**NTUserName**</span><span class="sxs-lookup"><span data-stu-id="170a8-171">**NTUserName**</span></span>|`nvarchar`|<span data-ttu-id="170a8-172">擁有產生此事件之連接的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="170a8-172">The name of the user that owns the connection that generated this event.</span></span>|<span data-ttu-id="170a8-173">6</span><span class="sxs-lookup"><span data-stu-id="170a8-173">6</span></span>|<span data-ttu-id="170a8-174">是</span><span class="sxs-lookup"><span data-stu-id="170a8-174">Yes</span></span>|  
|<span data-ttu-id="170a8-175">**ObjectName**</span><span class="sxs-lookup"><span data-stu-id="170a8-175">**ObjectName**</span></span>|`nvarchar`|<span data-ttu-id="170a8-176">對話的交談控制代碼。</span><span class="sxs-lookup"><span data-stu-id="170a8-176">The conversation handle of the dialog.</span></span>|<span data-ttu-id="170a8-177">34</span><span class="sxs-lookup"><span data-stu-id="170a8-177">34</span></span>|<span data-ttu-id="170a8-178">否</span><span class="sxs-lookup"><span data-stu-id="170a8-178">No</span></span>|  
|<span data-ttu-id="170a8-179">**優先順序**</span><span class="sxs-lookup"><span data-stu-id="170a8-179">**Priority**</span></span>|`int`|<span data-ttu-id="170a8-180">交談的優先權等級。</span><span class="sxs-lookup"><span data-stu-id="170a8-180">The priority level of the conversation</span></span>|<span data-ttu-id="170a8-181">5</span><span class="sxs-lookup"><span data-stu-id="170a8-181">5</span></span>|<span data-ttu-id="170a8-182">是</span><span class="sxs-lookup"><span data-stu-id="170a8-182">Yes</span></span>|  
|<span data-ttu-id="170a8-183">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="170a8-183">**RoleName**</span></span>|`nvarchar`|<span data-ttu-id="170a8-184">交談控制代碼的角色。</span><span class="sxs-lookup"><span data-stu-id="170a8-184">The role of the conversation handle.</span></span> <span data-ttu-id="170a8-185">為 **initiator** 或 **target**其中一個角色。</span><span class="sxs-lookup"><span data-stu-id="170a8-185">This is either **initiator** or **target**.</span></span>|<span data-ttu-id="170a8-186">38</span><span class="sxs-lookup"><span data-stu-id="170a8-186">38</span></span>|<span data-ttu-id="170a8-187">否</span><span class="sxs-lookup"><span data-stu-id="170a8-187">No</span></span>|  
|<span data-ttu-id="170a8-188">**ServerName**</span><span class="sxs-lookup"><span data-stu-id="170a8-188">**ServerName**</span></span>|`nvarchar`|<span data-ttu-id="170a8-189">所追蹤的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="170a8-189">The name of the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] that is being traced.</span></span>|<span data-ttu-id="170a8-190">26</span><span class="sxs-lookup"><span data-stu-id="170a8-190">26</span></span>|<span data-ttu-id="170a8-191">否</span><span class="sxs-lookup"><span data-stu-id="170a8-191">No</span></span>|  
|<span data-ttu-id="170a8-192">**嚴重性**</span><span class="sxs-lookup"><span data-stu-id="170a8-192">**Severity**</span></span>|`int`|<span data-ttu-id="170a8-193">如果此事件報告錯誤，即為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤嚴重性。</span><span class="sxs-lookup"><span data-stu-id="170a8-193">The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] error severity, if this event reports an error.</span></span>|<span data-ttu-id="170a8-194">29</span><span class="sxs-lookup"><span data-stu-id="170a8-194">29</span></span>|<span data-ttu-id="170a8-195">否</span><span class="sxs-lookup"><span data-stu-id="170a8-195">No</span></span>|  
|<span data-ttu-id="170a8-196">**SPID**</span><span class="sxs-lookup"><span data-stu-id="170a8-196">**SPID**</span></span>|`int`|<span data-ttu-id="170a8-197">由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指派給用戶端相關之處理序的伺服器處理序識別碼。</span><span class="sxs-lookup"><span data-stu-id="170a8-197">The server process ID that is assigned by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] to the process that is associated with the client.</span></span>|<span data-ttu-id="170a8-198">12</span><span class="sxs-lookup"><span data-stu-id="170a8-198">12</span></span>|<span data-ttu-id="170a8-199">是</span><span class="sxs-lookup"><span data-stu-id="170a8-199">Yes</span></span>|  
|<span data-ttu-id="170a8-200">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="170a8-200">**StartTime**</span></span>|`datetime`|<span data-ttu-id="170a8-201">事件啟動的時間 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="170a8-201">The time when the event started, when available.</span></span>|<span data-ttu-id="170a8-202">14</span><span class="sxs-lookup"><span data-stu-id="170a8-202">14</span></span>|<span data-ttu-id="170a8-203">是</span><span class="sxs-lookup"><span data-stu-id="170a8-203">Yes</span></span>|  
|<span data-ttu-id="170a8-204">**TextData**</span><span class="sxs-lookup"><span data-stu-id="170a8-204">**TextData**</span></span>|`ntext`|<span data-ttu-id="170a8-205">交談的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="170a8-205">The current state of the conversation.</span></span> <span data-ttu-id="170a8-206">下列其中之一：</span><span class="sxs-lookup"><span data-stu-id="170a8-206">One of the following:</span></span><br /><br /> <span data-ttu-id="170a8-207">**因此**。</span><span class="sxs-lookup"><span data-stu-id="170a8-207">**SO**.</span></span> <span data-ttu-id="170a8-208">已開始傳出。</span><span class="sxs-lookup"><span data-stu-id="170a8-208">Started outbound.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="170a8-209">已處理此交談的 BEGIN CONVERSATION，但尚未傳送任何訊息。</span><span class="sxs-lookup"><span data-stu-id="170a8-209">processed a BEGIN CONVERSATION for this conversation, but no messages have been sent.</span></span><br /><br /> <span data-ttu-id="170a8-210">**SI**。</span><span class="sxs-lookup"><span data-stu-id="170a8-210">**SI**.</span></span> <span data-ttu-id="170a8-211">已起始傳入。</span><span class="sxs-lookup"><span data-stu-id="170a8-211">Started inbound.</span></span> <span data-ttu-id="170a8-212">另一個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體啟動了與目前執行個體的新交談，但是目前的執行個體尚未完成第一個訊息的接收動作。</span><span class="sxs-lookup"><span data-stu-id="170a8-212">Another instance of the [!INCLUDE[ssDE](../../includes/ssde-md.md)] started a new conversation with the current instance, but the current instance has not finished receiving the first message.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="170a8-213">如果第一個訊息被分割或者 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 收到訊息的順序不正確，就可能會建立處於此狀態的交談。</span><span class="sxs-lookup"><span data-stu-id="170a8-213">might create the conversation in this state if the first message is fragmented or [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] receives messages out of order.</span></span> <span data-ttu-id="170a8-214">然而，如果收到交談的第一次傳輸包含完整的第一則訊息，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會建立 CO 狀態的交談。</span><span class="sxs-lookup"><span data-stu-id="170a8-214">However, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] might create the conversation in the CO state if the first transmission that was received for the conversation contains the complete first message.</span></span><br /><br /> <span data-ttu-id="170a8-215">**CO**。</span><span class="sxs-lookup"><span data-stu-id="170a8-215">**CO**.</span></span> <span data-ttu-id="170a8-216">正在交談。</span><span class="sxs-lookup"><span data-stu-id="170a8-216">Conversing.</span></span> <span data-ttu-id="170a8-217">已建立交談，且交談兩端可以傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="170a8-217">The conversation is established, and both sides of the conversation can send messages.</span></span> <span data-ttu-id="170a8-218">一般服務的大部分通訊都發生在這個狀態的交談中。</span><span class="sxs-lookup"><span data-stu-id="170a8-218">Most communication for a typical service happens when the conversation is in this state.</span></span><br /><br /> <span data-ttu-id="170a8-219">**DI**。</span><span class="sxs-lookup"><span data-stu-id="170a8-219">**DI**.</span></span> <span data-ttu-id="170a8-220">已中斷傳入。</span><span class="sxs-lookup"><span data-stu-id="170a8-220">Disconnected inbound.</span></span> <span data-ttu-id="170a8-221">交談的遠端發出了 END CONVERSATION。</span><span class="sxs-lookup"><span data-stu-id="170a8-221">The remote side of the conversation has issued an END CONVERSATION.</span></span> <span data-ttu-id="170a8-222">交談會保留在這個狀態中，直到交談的本機端發出 END CONVERSATION 為止。</span><span class="sxs-lookup"><span data-stu-id="170a8-222">The conversation remains in this state until the local side of the conversation issues an END CONVERSATION.</span></span> <span data-ttu-id="170a8-223">應用程式仍可接收交談的訊息。</span><span class="sxs-lookup"><span data-stu-id="170a8-223">An application can still receive messages for the conversation.</span></span> <span data-ttu-id="170a8-224">由於交談的遠端已經結束交談，所以應用程式無法在此交談中傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="170a8-224">Because the remote side of the conversation has ended the conversation, an application cannot send messages on this conversation.</span></span> <span data-ttu-id="170a8-225">當應用程式發出 END CONVERSATION 時，交談會移到已關閉 (CD) 狀態。</span><span class="sxs-lookup"><span data-stu-id="170a8-225">When an application issues an END CONVERSATION, the conversation moves to the Closed (CD) state.</span></span><br /><br /> <span data-ttu-id="170a8-226">**執行**。</span><span class="sxs-lookup"><span data-stu-id="170a8-226">**DO**.</span></span> <span data-ttu-id="170a8-227">已中斷傳出。</span><span class="sxs-lookup"><span data-stu-id="170a8-227">Disconnected outbound.</span></span> <span data-ttu-id="170a8-228">交談的本機端發出了 END CONVERSATION。</span><span class="sxs-lookup"><span data-stu-id="170a8-228">The local side of the conversation has issued an END CONVERSATION.</span></span> <span data-ttu-id="170a8-229">交談會保留在這個狀態中，直到交談的遠端收到 END CONVERSATION 為止。</span><span class="sxs-lookup"><span data-stu-id="170a8-229">The conversation remains in this state until the remote side of the conversation acknowledges the END CONVERSATION.</span></span> <span data-ttu-id="170a8-230">應用程式無法傳送或接收交談的訊息。</span><span class="sxs-lookup"><span data-stu-id="170a8-230">An application cannot send or receive messages for the conversation.</span></span> <span data-ttu-id="170a8-231">當交談的遠端收到 END CONVERSATION 時，交談會移到已關閉 (CD) 狀態。</span><span class="sxs-lookup"><span data-stu-id="170a8-231">When the remote side of the conversation acknowledges the END CONVERSATION, the conversation moves to the Closed (CD) state.</span></span><br /><br /> <span data-ttu-id="170a8-232">**ER**。</span><span class="sxs-lookup"><span data-stu-id="170a8-232">**ER**.</span></span> <span data-ttu-id="170a8-233">錯誤。</span><span class="sxs-lookup"><span data-stu-id="170a8-233">Error.</span></span> <span data-ttu-id="170a8-234">這個端點發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="170a8-234">An error has occurred on this endpoint.</span></span> <span data-ttu-id="170a8-235">錯誤、嚴重性和狀態資料行包含有關發生之特定錯誤的資訊。</span><span class="sxs-lookup"><span data-stu-id="170a8-235">The Error, Severity, and State columns contain information about the specific error that occurred.</span></span><br /><br /> <span data-ttu-id="170a8-236">**CD**。</span><span class="sxs-lookup"><span data-stu-id="170a8-236">**CD**.</span></span> <span data-ttu-id="170a8-237">已關閉。</span><span class="sxs-lookup"><span data-stu-id="170a8-237">Closed.</span></span> <span data-ttu-id="170a8-238">交談端點已不在使用中。</span><span class="sxs-lookup"><span data-stu-id="170a8-238">The conversation endpoint is no longer in use.</span></span>|<span data-ttu-id="170a8-239">1</span><span class="sxs-lookup"><span data-stu-id="170a8-239">1</span></span>|<span data-ttu-id="170a8-240">是</span><span class="sxs-lookup"><span data-stu-id="170a8-240">Yes</span></span>|  
|<span data-ttu-id="170a8-241">**Transaction ID**</span><span class="sxs-lookup"><span data-stu-id="170a8-241">**Transaction ID**</span></span>|`bigint`|<span data-ttu-id="170a8-242">系統指派的交易識別碼。</span><span class="sxs-lookup"><span data-stu-id="170a8-242">The system-assigned ID of the transaction.</span></span>|<span data-ttu-id="170a8-243">4</span><span class="sxs-lookup"><span data-stu-id="170a8-243">4</span></span>|<span data-ttu-id="170a8-244">否</span><span class="sxs-lookup"><span data-stu-id="170a8-244">No</span></span>|  
  
 <span data-ttu-id="170a8-245">下表列出此事件類別的子類別值。</span><span class="sxs-lookup"><span data-stu-id="170a8-245">The following table lists the subclass values for this event class.</span></span>  
  
|<span data-ttu-id="170a8-246">ID</span><span class="sxs-lookup"><span data-stu-id="170a8-246">ID</span></span>|<span data-ttu-id="170a8-247">子類別</span><span class="sxs-lookup"><span data-stu-id="170a8-247">Subclass</span></span>|<span data-ttu-id="170a8-248">描述</span><span class="sxs-lookup"><span data-stu-id="170a8-248">Description</span></span>|  
|--------|--------------|-----------------|  
|<span data-ttu-id="170a8-249">1</span><span class="sxs-lookup"><span data-stu-id="170a8-249">1</span></span>|<span data-ttu-id="170a8-250">SEND Message</span><span class="sxs-lookup"><span data-stu-id="170a8-250">SEND Message</span></span>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<span data-ttu-id="170a8-251">當執行 SEND 語句時，會產生**Send Message**事件 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="170a8-251">generates a **SEND Message** event when the [!INCLUDE[ssDE](../../includes/ssde-md.md)] executes a SEND statement.</span></span>|  
|<span data-ttu-id="170a8-252">2</span><span class="sxs-lookup"><span data-stu-id="170a8-252">2</span></span>|<span data-ttu-id="170a8-253">END CONVERSATION</span><span class="sxs-lookup"><span data-stu-id="170a8-253">END CONVERSATION</span></span>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<span data-ttu-id="170a8-254">當**END CONVERSATION** [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行不包含 WITH ERROR 子句的 end 交談語句時，會產生結束交談事件。</span><span class="sxs-lookup"><span data-stu-id="170a8-254">generates an **END CONVERSATION** event when the [!INCLUDE[ssDE](../../includes/ssde-md.md)] executes an END CONVERSATION statement that does not include the WITH ERROR clause.</span></span>|  
|<span data-ttu-id="170a8-255">3</span><span class="sxs-lookup"><span data-stu-id="170a8-255">3</span></span>|<span data-ttu-id="170a8-256">END CONVERSATION WITH ERROR</span><span class="sxs-lookup"><span data-stu-id="170a8-256">END CONVERSATION WITH ERROR</span></span>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<span data-ttu-id="170a8-257">當執行包含 WITH ERROR 子句的 END 交談語句時，會產生**END 交談並出現錯誤**事件 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="170a8-257">generates an **END CONVERSATION WITH ERROR** event when the [!INCLUDE[ssDE](../../includes/ssde-md.md)] executes an END CONVERSATION statement that includes the WITH ERROR clause.</span></span>|  
|<span data-ttu-id="170a8-258">4</span><span class="sxs-lookup"><span data-stu-id="170a8-258">4</span></span>|<span data-ttu-id="170a8-259">Broker Initiated Error</span><span class="sxs-lookup"><span data-stu-id="170a8-259">Broker Initiated Error</span></span>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<span data-ttu-id="170a8-260">每當建立錯誤訊息時，就會產生**Broker 起始的錯誤**事件 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="170a8-260">generates a **Broker Initiated Error** event whenever [!INCLUDE[ssSB](../../includes/sssb-md.md)] creates an error message.</span></span> <span data-ttu-id="170a8-261">例如，當 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 未能成功地路由傳送對話的訊息時，Broker 會針對該對話建立一個錯誤訊息，並產生此事件。</span><span class="sxs-lookup"><span data-stu-id="170a8-261">For example, when [!INCLUDE[ssSB](../../includes/sssb-md.md)] cannot successfully route a message for a dialog, the broker creates an error message for the dialog and generates this event.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="170a8-262">如果應用程式結束交談時發生錯誤，不會產生此事件。</span><span class="sxs-lookup"><span data-stu-id="170a8-262">does not generate this event when an application program ends a conversation with an error.</span></span>|  
|<span data-ttu-id="170a8-263">5</span><span class="sxs-lookup"><span data-stu-id="170a8-263">5</span></span>|<span data-ttu-id="170a8-264">Terminate Dialog</span><span class="sxs-lookup"><span data-stu-id="170a8-264">Terminate Dialog</span></span>|[!INCLUDE[ssSB](../../includes/sssb-md.md)] <span data-ttu-id="170a8-265">會結束此對話。</span><span class="sxs-lookup"><span data-stu-id="170a8-265">terminated the dialog.</span></span> [!INCLUDE[ssSB](../../includes/sssb-md.md)] <span data-ttu-id="170a8-266">對於無法繼續使用對話的情況 (但並不是錯誤或正常結束交談的情況)，會終止對話來加以回應。</span><span class="sxs-lookup"><span data-stu-id="170a8-266">terminates dialogs in response to conditions that prevent the dialog from continuing, but which are not errors or the normal end of a conversation.</span></span> <span data-ttu-id="170a8-267">例如，卸除服務會導致 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 終止該項服務的所有對話。</span><span class="sxs-lookup"><span data-stu-id="170a8-267">For example, dropping a service causes [!INCLUDE[ssSB](../../includes/sssb-md.md)] to terminate all dialogs for that service.</span></span>|  
|<span data-ttu-id="170a8-268">6</span><span class="sxs-lookup"><span data-stu-id="170a8-268">6</span></span>|<span data-ttu-id="170a8-269">Received Sequenced Message</span><span class="sxs-lookup"><span data-stu-id="170a8-269">Received Sequenced Message</span></span>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<span data-ttu-id="170a8-270">當收到包含訊息序號的訊息時，會產生 Received sequence **Message**事件類別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="170a8-270">generates a **Received Sequenced Message** event class when [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] receives a message that contains a message sequence number.</span></span> <span data-ttu-id="170a8-271">所有使用者定義的訊息類型都是循序訊息。</span><span class="sxs-lookup"><span data-stu-id="170a8-271">All user-defined message types are sequenced messages.</span></span> [!INCLUDE[ssSB](../../includes/sssb-md.md)] <span data-ttu-id="170a8-272">會在兩個情況下產生非循序訊息：</span><span class="sxs-lookup"><span data-stu-id="170a8-272">generates an unsequenced message in two cases:</span></span><br /><br /> <span data-ttu-id="170a8-273">由 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 產生的錯誤訊息即非循序。</span><span class="sxs-lookup"><span data-stu-id="170a8-273">Error messages generated by [!INCLUDE[ssSB](../../includes/sssb-md.md)] are unsequenced.</span></span><br /><br /> <span data-ttu-id="170a8-274">訊息收條可能為非循序。</span><span class="sxs-lookup"><span data-stu-id="170a8-274">Message acknowledgements might be unsequenced.</span></span> <span data-ttu-id="170a8-275">為了提高效率， [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會將任何可用的收條當做循序訊息的一部分併入訊息中。</span><span class="sxs-lookup"><span data-stu-id="170a8-275">For efficiency, [!INCLUDE[ssSB](../../includes/sssb-md.md)] includes message any available acknowledgement as part of a sequenced message .</span></span> <span data-ttu-id="170a8-276">但是，如果應用程式未能在某一段時間內，將循序訊息傳送到遠端端點， [!INCLUDE[ssSB](../../includes/sssb-md.md)] 就會為訊息收條建立非循序訊息。</span><span class="sxs-lookup"><span data-stu-id="170a8-276">However, if an application does not send a sequenced message to the remote endpoint within a certain period of time, [!INCLUDE[ssSB](../../includes/sssb-md.md)] creates an unsequenced message for the message acknowledgement.</span></span>|  
|<span data-ttu-id="170a8-277">7</span><span class="sxs-lookup"><span data-stu-id="170a8-277">7</span></span>|<span data-ttu-id="170a8-278">Received END CONVERSATION</span><span class="sxs-lookup"><span data-stu-id="170a8-278">Received END CONVERSATION</span></span>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="170a8-279">當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 收到交談另一端的「結束對話」訊息時，會產生 Received END CONVERSATION 事件。</span><span class="sxs-lookup"><span data-stu-id="170a8-279">generates a Received END CONVERSATION event when [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] receives an End Dialog message from the other side of the conversation.</span></span>|  
|<span data-ttu-id="170a8-280">8</span><span class="sxs-lookup"><span data-stu-id="170a8-280">8</span></span>|<span data-ttu-id="170a8-281">Received END CONVERSATION WITH ERROR</span><span class="sxs-lookup"><span data-stu-id="170a8-281">Received END CONVERSATION WITH ERROR</span></span>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<span data-ttu-id="170a8-282">當收到來自交談另一端的使用者定義錯誤時，會產生**接收的結束交談，並出現錯誤**事件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="170a8-282">generates a **Received END CONVERSATION WITH ERROR** event when [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] receives a user-defined error from the other side of the conversation.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="170a8-283">當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 收到 Broker 定義的錯誤時，不會產生此事件。</span><span class="sxs-lookup"><span data-stu-id="170a8-283">does not generate this event when [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] receives a broker-defined error.</span></span>|  
|<span data-ttu-id="170a8-284">9</span><span class="sxs-lookup"><span data-stu-id="170a8-284">9</span></span>|<span data-ttu-id="170a8-285">Received Broker Error Message</span><span class="sxs-lookup"><span data-stu-id="170a8-285">Received Broker Error Message</span></span>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<span data-ttu-id="170a8-286">當收到來自交談另一端的 broker 定義錯誤訊息時，會產生**Received Broker Error message**事件 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="170a8-286">generates a **Received Broker Error Message** event when [!INCLUDE[ssSB](../../includes/sssb-md.md)] receives a broker-defined error message from the other side of the conversation.</span></span> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="170a8-287">當 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 收到由應用程式產生的錯誤訊息時，不會產生此事件。</span><span class="sxs-lookup"><span data-stu-id="170a8-287">does not generate this event when [!INCLUDE[ssSB](../../includes/sssb-md.md)] receives an error message that was generated by an application.</span></span><br /><br /> <span data-ttu-id="170a8-288">例如，如果目前的資料庫包含轉寄資料庫的預設路由， [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會以未知的服務名稱將訊息路由傳送到轉寄資料庫。</span><span class="sxs-lookup"><span data-stu-id="170a8-288">For example, if the current database contains a default route to a forwarding database, [!INCLUDE[ssSB](../../includes/sssb-md.md)] routes a message with an unknown service name to the forwarding database.</span></span> <span data-ttu-id="170a8-289">如果那個資料庫無法路由訊息，則資料庫中的 Broker 就會建立錯誤訊息，然後將該錯誤訊息傳回目前的資料庫。</span><span class="sxs-lookup"><span data-stu-id="170a8-289">If that database cannot route the message, the broker in that database creates an error message and returns that error message to the current database.</span></span> <span data-ttu-id="170a8-290">當目前的資料庫從轉寄資料庫收到 Broker 產生的錯誤，目前的資料庫就會產生 **Received Broker Error Message** 事件。</span><span class="sxs-lookup"><span data-stu-id="170a8-290">When the current database receives the broker-generated error from the forwarding database, the current database generates a **Received Broker Error Message** event.</span></span>|  
|<span data-ttu-id="170a8-291">10</span><span class="sxs-lookup"><span data-stu-id="170a8-291">10</span></span>|<span data-ttu-id="170a8-292">Received END CONVERSATION Ack</span><span class="sxs-lookup"><span data-stu-id="170a8-292">Received END CONVERSATION Ack</span></span>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<span data-ttu-id="170a8-293">當交談的另一端認可由交談的這一端傳送的結束對話或錯誤訊息時，會產生**已接收的「結束對話 Ack** 」事件類別。</span><span class="sxs-lookup"><span data-stu-id="170a8-293">generates a **Received END CONVERSATION Ack** event class when the other side of a conversation acknowledges an End Dialog or Error message sent by this side of the conversation.</span></span>|  
|<span data-ttu-id="170a8-294">11</span><span class="sxs-lookup"><span data-stu-id="170a8-294">11</span></span>|<span data-ttu-id="170a8-295">BEGIN DIALOG</span><span class="sxs-lookup"><span data-stu-id="170a8-295">BEGIN DIALOG</span></span>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<span data-ttu-id="170a8-296">當資料庫引擎執行 BEGIN DIALOG 命令時，會產生**BEGIN dialog**事件。</span><span class="sxs-lookup"><span data-stu-id="170a8-296">generates a **BEGIN DIALOG** event when the Database Engine executes a BEGIN DIALOG command.</span></span>|  
|<span data-ttu-id="170a8-297">12</span><span class="sxs-lookup"><span data-stu-id="170a8-297">12</span></span>|<span data-ttu-id="170a8-298">Dialog Created</span><span class="sxs-lookup"><span data-stu-id="170a8-298">Dialog Created</span></span>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<span data-ttu-id="170a8-299">當建立對話方塊的端點時，會產生**對話方塊建立**的事件 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="170a8-299">generates a **Dialog Created** event when [!INCLUDE[ssSB](../../includes/sssb-md.md)] creates an endpoint for a dialog.</span></span> [!INCLUDE[ssSB](../../includes/sssb-md.md)] <span data-ttu-id="170a8-300">每當建立新的對話時，就會建立一個端點，不論目前的資料庫是否為該對話的起始端或目標。</span><span class="sxs-lookup"><span data-stu-id="170a8-300">creates an endpoint whenever a new dialog is established, regardless of whether the current database is the initiator or the target of the dialog.</span></span>|  
|<span data-ttu-id="170a8-301">13</span><span class="sxs-lookup"><span data-stu-id="170a8-301">13</span></span>|<span data-ttu-id="170a8-302">END CONVERSATION WITH CLEANUP</span><span class="sxs-lookup"><span data-stu-id="170a8-302">END CONVERSATION WITH CLEANUP</span></span>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="170a8-303">當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行包括 WITH CLEANUP 子句的 END CONVERSATION 陳述式時，會產生 END CONVERSATION WITH CLEANUP 事件。</span><span class="sxs-lookup"><span data-stu-id="170a8-303">generates an END CONVERSATION WITH CLEANUP event when the [!INCLUDE[ssDE](../../includes/ssde-md.md)] executes an END CONVERSATION statement that includes the WITH CLEANUP clause.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="170a8-304">另請參閱</span><span class="sxs-lookup"><span data-stu-id="170a8-304">See Also</span></span>  
 [<span data-ttu-id="170a8-305">SQL Server Service Broker</span><span class="sxs-lookup"><span data-stu-id="170a8-305">SQL Server Service Broker</span></span>](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  