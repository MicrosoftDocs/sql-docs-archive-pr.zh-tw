---
title: Audit Database Management 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Database Management event class
ms.assetid: 3e3de528-c3f8-413f-a6b9-d324ca95ad8e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9fc72179193754f4e8b4d52ed0598939f587f676
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87701176"
---
# <a name="audit-database-management-event-class"></a><span data-ttu-id="bd8a3-102">Audit Database Management 事件類別</span><span class="sxs-lookup"><span data-stu-id="bd8a3-102">Audit Database Management Event Class</span></span>
  <span data-ttu-id="bd8a3-103">在建立、變更或卸除資料庫時，即會產生 **Audit Database Management** 事件類別。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-103">The **Audit Database Management** event class occurs when a database is created, altered, or dropped.</span></span>  
  
## <a name="audit-database-management-event-class-data-columns"></a><span data-ttu-id="bd8a3-104">Audit Database Management 事件類別資料行</span><span class="sxs-lookup"><span data-stu-id="bd8a3-104">Audit Database Management Event Class Data Columns</span></span>  
  
|<span data-ttu-id="bd8a3-105">資料行名稱</span><span class="sxs-lookup"><span data-stu-id="bd8a3-105">Data column name</span></span>|<span data-ttu-id="bd8a3-106">資料類型</span><span class="sxs-lookup"><span data-stu-id="bd8a3-106">Data type</span></span>|<span data-ttu-id="bd8a3-107">描述</span><span class="sxs-lookup"><span data-stu-id="bd8a3-107">Description</span></span>|<span data-ttu-id="bd8a3-108">資料行識別碼</span><span class="sxs-lookup"><span data-stu-id="bd8a3-108">Column ID</span></span>|<span data-ttu-id="bd8a3-109">可篩選</span><span class="sxs-lookup"><span data-stu-id="bd8a3-109">Filterable</span></span>|  
|----------------------|---------------|-----------------|---------------|----------------|  
|<span data-ttu-id="bd8a3-110">**ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-110">**ApplicationName**</span></span>|<span data-ttu-id="bd8a3-111">**nvarchar**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-111">**nvarchar**</span></span>|<span data-ttu-id="bd8a3-112">建立 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體連線的用戶端應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-112">Name of the client application that created the connection to an instance of [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="bd8a3-113">這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-113">This column is populated with the values passed by the application rather than the displayed name of the program.</span></span>|<span data-ttu-id="bd8a3-114">10</span><span class="sxs-lookup"><span data-stu-id="bd8a3-114">10</span></span>|<span data-ttu-id="bd8a3-115">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-115">Yes</span></span>|  
|<span data-ttu-id="bd8a3-116">**DatabaseID**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-116">**DatabaseID**</span></span>|<span data-ttu-id="bd8a3-117">**int**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-117">**int**</span></span>|<span data-ttu-id="bd8a3-118">由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-118">ID of the database specified by the USE *database* statement or the default database if no USE *database* statement has been issued for a given instance.</span></span> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] <span data-ttu-id="bd8a3-119">就會顯示資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-119">displays the name of the database if the Server Name data column is captured in the trace and the server is available.</span></span> <span data-ttu-id="bd8a3-120">請使用 DB_ID 函數判斷資料庫的值。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-120">Determine the value for a database by using the DB_ID function.</span></span>|<span data-ttu-id="bd8a3-121">3</span><span class="sxs-lookup"><span data-stu-id="bd8a3-121">3</span></span>|<span data-ttu-id="bd8a3-122">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-122">Yes</span></span>|  
|<span data-ttu-id="bd8a3-123">**DatabaseName**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-123">**DatabaseName**</span></span>|<span data-ttu-id="bd8a3-124">**nvarchar**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-124">**nvarchar**</span></span>|<span data-ttu-id="bd8a3-125">正在執行使用者陳述式的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-125">Name of the database in which the user statement is running.</span></span>|<span data-ttu-id="bd8a3-126">35</span><span class="sxs-lookup"><span data-stu-id="bd8a3-126">35</span></span>|<span data-ttu-id="bd8a3-127">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-127">Yes</span></span>|  
|<span data-ttu-id="bd8a3-128">**DBUserName**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-128">**DBUserName**</span></span>|<span data-ttu-id="bd8a3-129">**nvarchar**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-129">**nvarchar**</span></span>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="bd8a3-130">使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-130">user name of the client.</span></span>|<span data-ttu-id="bd8a3-131">40</span><span class="sxs-lookup"><span data-stu-id="bd8a3-131">40</span></span>|<span data-ttu-id="bd8a3-132">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-132">Yes</span></span>|  
|<span data-ttu-id="bd8a3-133">**EventSequence**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-133">**EventSequence**</span></span>|<span data-ttu-id="bd8a3-134">**int**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-134">**int**</span></span>|<span data-ttu-id="bd8a3-135">要求中的給定事件順序。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-135">Sequence of a given event within the request.</span></span>|<span data-ttu-id="bd8a3-136">51</span><span class="sxs-lookup"><span data-stu-id="bd8a3-136">51</span></span>|<span data-ttu-id="bd8a3-137">否</span><span class="sxs-lookup"><span data-stu-id="bd8a3-137">No</span></span>|  
|<span data-ttu-id="bd8a3-138">**EventSubClass**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-138">**EventSubClass**</span></span>|<span data-ttu-id="bd8a3-139">**int**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-139">**int**</span></span>|<span data-ttu-id="bd8a3-140">事件子類別的類型。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-140">Type of event subclass.</span></span><br /><br /> <span data-ttu-id="bd8a3-141">1=建立</span><span class="sxs-lookup"><span data-stu-id="bd8a3-141">1=Create</span></span><br /><br /> <span data-ttu-id="bd8a3-142">2=改變</span><span class="sxs-lookup"><span data-stu-id="bd8a3-142">2=Alter</span></span><br /><br /> <span data-ttu-id="bd8a3-143">3=卸除</span><span class="sxs-lookup"><span data-stu-id="bd8a3-143">3=Drop</span></span><br /><br /> <span data-ttu-id="bd8a3-144">4=傾印</span><span class="sxs-lookup"><span data-stu-id="bd8a3-144">4=Dump</span></span><br /><br /> <span data-ttu-id="bd8a3-145">11=載入</span><span class="sxs-lookup"><span data-stu-id="bd8a3-145">11=Load</span></span>|<span data-ttu-id="bd8a3-146">21</span><span class="sxs-lookup"><span data-stu-id="bd8a3-146">21</span></span>|<span data-ttu-id="bd8a3-147">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-147">Yes</span></span>|  
|<span data-ttu-id="bd8a3-148">**HostName**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-148">**HostName**</span></span>|<span data-ttu-id="bd8a3-149">**nvarchar**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-149">**nvarchar**</span></span>|<span data-ttu-id="bd8a3-150">執行用戶端的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-150">Name of the computer on which the client is running.</span></span> <span data-ttu-id="bd8a3-151">如果用戶端提供主機名稱，這個資料行就會擴展。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-151">This data column is populated if the client provides the host name.</span></span> <span data-ttu-id="bd8a3-152">若要判斷主機名稱，請使用 HOST_NAME 函數。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-152">To determine the host name, use the HOST_NAME function.</span></span>|<span data-ttu-id="bd8a3-153">8</span><span class="sxs-lookup"><span data-stu-id="bd8a3-153">8</span></span>|<span data-ttu-id="bd8a3-154">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-154">Yes</span></span>|  
|<span data-ttu-id="bd8a3-155">**IsSystem**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-155">**IsSystem**</span></span>|<span data-ttu-id="bd8a3-156">**int**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-156">**int**</span></span>|<span data-ttu-id="bd8a3-157">指出事件是發生在系統處理序或使用者處理序。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-157">Indicates whether the event occurred on a system process or a user process.</span></span> <span data-ttu-id="bd8a3-158">1 = 系統，0 = 使用者。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-158">1 = system, 0 = user.</span></span>|<span data-ttu-id="bd8a3-159">60</span><span class="sxs-lookup"><span data-stu-id="bd8a3-159">60</span></span>|<span data-ttu-id="bd8a3-160">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-160">Yes</span></span>|  
|<span data-ttu-id="bd8a3-161">**LoginName**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-161">**LoginName**</span></span>|<span data-ttu-id="bd8a3-162">**nvarchar**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-162">**nvarchar**</span></span>|<span data-ttu-id="bd8a3-163">使用者的登入名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-163">Name of the login of the user (either the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] security login or the [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows login credentials in the form of DOMAIN\username).</span></span>|<span data-ttu-id="bd8a3-164">11</span><span class="sxs-lookup"><span data-stu-id="bd8a3-164">11</span></span>|<span data-ttu-id="bd8a3-165">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-165">Yes</span></span>|  
|<span data-ttu-id="bd8a3-166">**LoginSid**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-166">**LoginSid**</span></span>|<span data-ttu-id="bd8a3-167">**image**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-167">**image**</span></span>|<span data-ttu-id="bd8a3-168">已登入之使用者的安全性識別碼 (SID)。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-168">Security identification number (SID) of the logged-in user.</span></span> <span data-ttu-id="bd8a3-169">您可以在 **sys.server_principals** 目錄檢視中找到這項資訊。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-169">You can find this information in the **sys.server_principals** catalog view.</span></span> <span data-ttu-id="bd8a3-170">伺服器上的每一個登入之 SID 是唯一的。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-170">Each SID is unique for each login in the server.</span></span>|<span data-ttu-id="bd8a3-171">41</span><span class="sxs-lookup"><span data-stu-id="bd8a3-171">41</span></span>|<span data-ttu-id="bd8a3-172">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-172">Yes</span></span>|  
|<span data-ttu-id="bd8a3-173">**NTDomainName**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-173">**NTDomainName**</span></span>|<span data-ttu-id="bd8a3-174">**nvarchar**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-174">**nvarchar**</span></span>|<span data-ttu-id="bd8a3-175">使用者所隸屬的 Windows 網域。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-175">Windows domain to which the user belongs.</span></span>|<span data-ttu-id="bd8a3-176">7</span><span class="sxs-lookup"><span data-stu-id="bd8a3-176">7</span></span>|<span data-ttu-id="bd8a3-177">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-177">Yes</span></span>|  
|<span data-ttu-id="bd8a3-178">**NTUserName**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-178">**NTUserName**</span></span>|<span data-ttu-id="bd8a3-179">**nvarchar**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-179">**nvarchar**</span></span>|<span data-ttu-id="bd8a3-180">Windows 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-180">Windows user name.</span></span>|<span data-ttu-id="bd8a3-181">6</span><span class="sxs-lookup"><span data-stu-id="bd8a3-181">6</span></span>|<span data-ttu-id="bd8a3-182">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-182">Yes</span></span>|  
|<span data-ttu-id="bd8a3-183">**ObjectName**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-183">**ObjectName**</span></span>|<span data-ttu-id="bd8a3-184">**nvarchar**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-184">**nvarchar**</span></span>|<span data-ttu-id="bd8a3-185">正在參考之物件的名稱。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-185">Name of the object being referenced.</span></span>|<span data-ttu-id="bd8a3-186">34</span><span class="sxs-lookup"><span data-stu-id="bd8a3-186">34</span></span>|<span data-ttu-id="bd8a3-187">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-187">Yes</span></span>|  
|<span data-ttu-id="bd8a3-188">**ObjectType**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-188">**ObjectType**</span></span>|<span data-ttu-id="bd8a3-189">**int**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-189">**int**</span></span>|<span data-ttu-id="bd8a3-190">代表參與事件之物件類型的值。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-190">Value representing the type of the object involved in the event.</span></span> <span data-ttu-id="bd8a3-191">此值對應至 **sysobjects** 資料表中的類型資料行。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-191">This value corresponds to the type column in the **sysobjects** table.</span></span> <span data-ttu-id="bd8a3-192">針對各值，請參閱 [ObjectType 追蹤事件資料行](objecttype-trace-event-column.md)。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-192">For values, see [ObjectType Trace Event Column](objecttype-trace-event-column.md).</span></span>|<span data-ttu-id="bd8a3-193">28</span><span class="sxs-lookup"><span data-stu-id="bd8a3-193">28</span></span>|<span data-ttu-id="bd8a3-194">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-194">Yes</span></span>|  
|<span data-ttu-id="bd8a3-195">**OwnerName**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-195">**OwnerName**</span></span>|<span data-ttu-id="bd8a3-196">**nvarchar**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-196">**nvarchar**</span></span>|<span data-ttu-id="bd8a3-197">物件擁有者的資料庫使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-197">Database user name of the object owner.</span></span>|<span data-ttu-id="bd8a3-198">37</span><span class="sxs-lookup"><span data-stu-id="bd8a3-198">37</span></span>|<span data-ttu-id="bd8a3-199">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-199">Yes</span></span>|  
|<span data-ttu-id="bd8a3-200">**RequestID**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-200">**RequestID**</span></span>|<span data-ttu-id="bd8a3-201">**int**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-201">**int**</span></span>|<span data-ttu-id="bd8a3-202">包含陳述式之要求的識別碼。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-202">ID of the request containing the statement.</span></span>|<span data-ttu-id="bd8a3-203">49</span><span class="sxs-lookup"><span data-stu-id="bd8a3-203">49</span></span>|<span data-ttu-id="bd8a3-204">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-204">Yes</span></span>|  
|<span data-ttu-id="bd8a3-205">**ServerName**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-205">**ServerName**</span></span>|<span data-ttu-id="bd8a3-206">**nvarchar**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-206">**nvarchar**</span></span>|<span data-ttu-id="bd8a3-207">正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-207">Name of the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] being traced.</span></span>|<span data-ttu-id="bd8a3-208">26</span><span class="sxs-lookup"><span data-stu-id="bd8a3-208">26</span></span>|<span data-ttu-id="bd8a3-209">否</span><span class="sxs-lookup"><span data-stu-id="bd8a3-209">No</span></span>|  
|<span data-ttu-id="bd8a3-210">**SessionLoginName**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-210">**SessionLoginName**</span></span>|<span data-ttu-id="bd8a3-211">**nvarchar**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-211">**nvarchar**</span></span>|<span data-ttu-id="bd8a3-212">引發工作階段之使用者的登入名稱。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-212">Login name of the user who originated the session.</span></span> <span data-ttu-id="bd8a3-213">例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-213">For example, if you connect to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] using Login1 and execute a statement as Login2, **SessionLoginName** shows Login1 and **LoginName** shows Login2.</span></span> <span data-ttu-id="bd8a3-214">此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-214">This column displays both [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and Windows logins.</span></span>|<span data-ttu-id="bd8a3-215">64</span><span class="sxs-lookup"><span data-stu-id="bd8a3-215">64</span></span>|<span data-ttu-id="bd8a3-216">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-216">Yes</span></span>|  
|<span data-ttu-id="bd8a3-217">**SPID**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-217">**SPID**</span></span>|<span data-ttu-id="bd8a3-218">**int**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-218">**int**</span></span>|<span data-ttu-id="bd8a3-219">事件發生所在之工作階段的識別碼。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-219">ID of the session on which the event occurred.</span></span>|<span data-ttu-id="bd8a3-220">12</span><span class="sxs-lookup"><span data-stu-id="bd8a3-220">12</span></span>|<span data-ttu-id="bd8a3-221">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-221">Yes</span></span>|  
|<span data-ttu-id="bd8a3-222">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-222">**StartTime**</span></span>|<span data-ttu-id="bd8a3-223">**datetime**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-223">**datetime**</span></span>|<span data-ttu-id="bd8a3-224">事件啟動的時間 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-224">Time at which the event started, if available.</span></span>|<span data-ttu-id="bd8a3-225">14</span><span class="sxs-lookup"><span data-stu-id="bd8a3-225">14</span></span>|<span data-ttu-id="bd8a3-226">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-226">Yes</span></span>|  
|<span data-ttu-id="bd8a3-227">「成功」 </span><span class="sxs-lookup"><span data-stu-id="bd8a3-227">**Success**</span></span>|<span data-ttu-id="bd8a3-228">**int**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-228">**int**</span></span>|<span data-ttu-id="bd8a3-229">1 = 成功。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-229">1 = success.</span></span> <span data-ttu-id="bd8a3-230">0 = 失敗。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-230">0 = failure.</span></span> <span data-ttu-id="bd8a3-231">例如，值為 1 表示權限檢查成功，值為 0 表示該檢查失敗。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-231">For example, a value of 1 means success of a permissions check and a value of 0 means a failure of that check.</span></span>|<span data-ttu-id="bd8a3-232">23</span><span class="sxs-lookup"><span data-stu-id="bd8a3-232">23</span></span>|<span data-ttu-id="bd8a3-233">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-233">Yes</span></span>|  
|<span data-ttu-id="bd8a3-234">**TextData**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-234">**TextData**</span></span>|<span data-ttu-id="bd8a3-235">**ntext**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-235">**ntext**</span></span>|<span data-ttu-id="bd8a3-236">與追蹤中所擷取的事件類別有關的文字值。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-236">Text value dependent on the event class captured in the trace.</span></span>|<span data-ttu-id="bd8a3-237">1</span><span class="sxs-lookup"><span data-stu-id="bd8a3-237">1</span></span>|<span data-ttu-id="bd8a3-238">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-238">Yes</span></span>|  
|<span data-ttu-id="bd8a3-239">**TransactionID**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-239">**TransactionID**</span></span>|<span data-ttu-id="bd8a3-240">**bigint**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-240">**bigint**</span></span>|<span data-ttu-id="bd8a3-241">由系統指派給交易的識別碼。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-241">System-assigned ID of the transaction.</span></span>|<span data-ttu-id="bd8a3-242">4</span><span class="sxs-lookup"><span data-stu-id="bd8a3-242">4</span></span>|<span data-ttu-id="bd8a3-243">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-243">Yes</span></span>|  
|<span data-ttu-id="bd8a3-244">**XactSequence**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-244">**XactSequence**</span></span>|<span data-ttu-id="bd8a3-245">**bigint**</span><span class="sxs-lookup"><span data-stu-id="bd8a3-245">**bigint**</span></span>|<span data-ttu-id="bd8a3-246">用來描述目前交易的 Token。</span><span class="sxs-lookup"><span data-stu-id="bd8a3-246">Token used to describe the current transaction.</span></span>|<span data-ttu-id="bd8a3-247">50</span><span class="sxs-lookup"><span data-stu-id="bd8a3-247">50</span></span>|<span data-ttu-id="bd8a3-248">是</span><span class="sxs-lookup"><span data-stu-id="bd8a3-248">Yes</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="bd8a3-249">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bd8a3-249">See Also</span></span>  
 <span data-ttu-id="bd8a3-250">[sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="bd8a3-250">[sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql) </span></span>  
 <span data-ttu-id="bd8a3-251">[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="bd8a3-251">[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql) </span></span>  
 <span data-ttu-id="bd8a3-252">[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="bd8a3-252">[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql) </span></span>  
 [<span data-ttu-id="bd8a3-253">DROP DATABASE &#40;Transact-SQL&#41;</span><span class="sxs-lookup"><span data-stu-id="bd8a3-253">DROP DATABASE &#40;Transact-SQL&#41;</span></span>](/sql/t-sql/statements/drop-database-audit-specification-transact-sql)  
  
  