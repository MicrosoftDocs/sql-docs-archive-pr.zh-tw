---
title: Lock:Acquired 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Acquired event class
ms.assetid: a6b1df2a-06ed-4fc3-8a84-f0becd5810d5
author: stevestein
ms.author: sstein
ms.openlocfilehash: e781e1ed4e632b11bff6f559392d829ec57bed94
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597834"
---
# <a name="lockacquired-event-class"></a><span data-ttu-id="685cf-102">Lock:Acquired 事件類別</span><span class="sxs-lookup"><span data-stu-id="685cf-102">Lock:Acquired Event Class</span></span>
  <span data-ttu-id="685cf-103">Lock:Acquired 事件類別指出已完成對資源 (例如資料頁) 取得鎖定。</span><span class="sxs-lookup"><span data-stu-id="685cf-103">The Lock:Acquiredevent class indicates that acquisition of a lock on a resource, such as a data page, has been achieved.</span></span>  
  
 <span data-ttu-id="685cf-104">Lock:Acquired 與 Lock:Released 事件類別可用來監視物件何時鎖定、採用的鎖定類型以及鎖定已保留多久的時間。</span><span class="sxs-lookup"><span data-stu-id="685cf-104">The Lock:Acquired and Lock:Released event classes can be used to monitor when objects are being locked, the type of locks taken, and for how long the locks were retained.</span></span> <span data-ttu-id="685cf-105">長期保留的鎖定可能會造成競爭問題，應該加以調查。</span><span class="sxs-lookup"><span data-stu-id="685cf-105">Locks retained for long periods of time may cause contention issues and should be investigated.</span></span> <span data-ttu-id="685cf-106">例如，某個應用程式可能取得資料表中資料列的鎖定，然後等候使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="685cf-106">For example, an application can be acquiring locks on rows in a table, and then waiting for user input.</span></span> <span data-ttu-id="685cf-107">由於使用者可能要很長時間來輸入，因此鎖定可能會封鎖其他使用者。</span><span class="sxs-lookup"><span data-stu-id="685cf-107">Because the user input can take a long time to occur, the locks can block other users.</span></span> <span data-ttu-id="685cf-108">在這個例子中，應重新設計應用程式，只在需要時才提出鎖定要求，而且取得鎖定後不需要使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="685cf-108">In this instance, the application should be redesigned to make lock requests only when needed and not require user input when locks have been acquired.</span></span>  
  
## <a name="lockacquired-event-class-data-columns"></a><span data-ttu-id="685cf-109">Lock:Acquired 事件類別資料行</span><span class="sxs-lookup"><span data-stu-id="685cf-109">Lock:Acquired Event Class Data Columns</span></span>  
  
|<span data-ttu-id="685cf-110">資料行名稱</span><span class="sxs-lookup"><span data-stu-id="685cf-110">Data column name</span></span>|<span data-ttu-id="685cf-111">資料類型</span><span class="sxs-lookup"><span data-stu-id="685cf-111">Data type</span></span>|<span data-ttu-id="685cf-112">描述</span><span class="sxs-lookup"><span data-stu-id="685cf-112">Description</span></span>|<span data-ttu-id="685cf-113">資料行識別碼</span><span class="sxs-lookup"><span data-stu-id="685cf-113">Column ID</span></span>|<span data-ttu-id="685cf-114">可篩選</span><span class="sxs-lookup"><span data-stu-id="685cf-114">Filterable</span></span>|  
|----------------------|---------------|-----------------|---------------|----------------|  
|<span data-ttu-id="685cf-115">ApplicationName</span><span class="sxs-lookup"><span data-stu-id="685cf-115">ApplicationName</span></span>|`nvarchar`|<span data-ttu-id="685cf-116">建立 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體連線的用戶端應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="685cf-116">Name of the client application that created the connection to an instance of [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="685cf-117">這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="685cf-117">This column is populated with the values passed by the application rather than the displayed name of the program.</span></span>|<span data-ttu-id="685cf-118">10</span><span class="sxs-lookup"><span data-stu-id="685cf-118">10</span></span>|<span data-ttu-id="685cf-119">是</span><span class="sxs-lookup"><span data-stu-id="685cf-119">Yes</span></span>|  
|<span data-ttu-id="685cf-120">BigintData1</span><span class="sxs-lookup"><span data-stu-id="685cf-120">BigintData1</span></span>|`bigint`|<span data-ttu-id="685cf-121">資料分割識別碼 (如果鎖定資源已分割)。</span><span class="sxs-lookup"><span data-stu-id="685cf-121">Partition ID if the lock resource is partitioned.</span></span>|<span data-ttu-id="685cf-122">52</span><span class="sxs-lookup"><span data-stu-id="685cf-122">52</span></span>|<span data-ttu-id="685cf-123">是</span><span class="sxs-lookup"><span data-stu-id="685cf-123">Yes</span></span>|  
|<span data-ttu-id="685cf-124">BinaryData</span><span class="sxs-lookup"><span data-stu-id="685cf-124">BinaryData</span></span>|`image`|<span data-ttu-id="685cf-125">鎖定資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="685cf-125">Lock resource identifier.</span></span>|<span data-ttu-id="685cf-126">2</span><span class="sxs-lookup"><span data-stu-id="685cf-126">2</span></span>|<span data-ttu-id="685cf-127">是</span><span class="sxs-lookup"><span data-stu-id="685cf-127">Yes</span></span>|  
|<span data-ttu-id="685cf-128">ClientProcessID</span><span class="sxs-lookup"><span data-stu-id="685cf-128">ClientProcessID</span></span>|`int`|<span data-ttu-id="685cf-129">由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="685cf-129">ID assigned by the host computer to the process where the client application is running.</span></span> <span data-ttu-id="685cf-130">如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。</span><span class="sxs-lookup"><span data-stu-id="685cf-130">This data column is populated if the client provides the client process ID.</span></span>|<span data-ttu-id="685cf-131">9</span><span class="sxs-lookup"><span data-stu-id="685cf-131">9</span></span>|<span data-ttu-id="685cf-132">是</span><span class="sxs-lookup"><span data-stu-id="685cf-132">Yes</span></span>|  
|<span data-ttu-id="685cf-133">DatabaseID</span><span class="sxs-lookup"><span data-stu-id="685cf-133">DatabaseID</span></span>|`int`|<span data-ttu-id="685cf-134">取得鎖定之資料庫的識別碼。</span><span class="sxs-lookup"><span data-stu-id="685cf-134">ID of the database in which the lock was acquired.</span></span> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] <span data-ttu-id="685cf-135">如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="685cf-135">displays the name of the database if the ServerName data column is captured in the trace and the server is available.</span></span> <span data-ttu-id="685cf-136">請使用 DB_ID 函數判斷資料庫的值。</span><span class="sxs-lookup"><span data-stu-id="685cf-136">Determine the value for a database by using the DB_ID function.</span></span>|<span data-ttu-id="685cf-137">3</span><span class="sxs-lookup"><span data-stu-id="685cf-137">3</span></span>|<span data-ttu-id="685cf-138">是</span><span class="sxs-lookup"><span data-stu-id="685cf-138">Yes</span></span>|  
|<span data-ttu-id="685cf-139">Duration</span><span class="sxs-lookup"><span data-stu-id="685cf-139">Duration</span></span>|`bigint`|<span data-ttu-id="685cf-140">發出鎖定要求和取得鎖定之間的時間量 (以百萬分之一秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="685cf-140">Amount of time (in microseconds) between the time the lock request was issued and the time the lock was acquired.</span></span>|<span data-ttu-id="685cf-141">13</span><span class="sxs-lookup"><span data-stu-id="685cf-141">13</span></span>|<span data-ttu-id="685cf-142">是</span><span class="sxs-lookup"><span data-stu-id="685cf-142">Yes</span></span>|  
|<span data-ttu-id="685cf-143">EndTime</span><span class="sxs-lookup"><span data-stu-id="685cf-143">EndTime</span></span>|`datetime`|<span data-ttu-id="685cf-144">事件結束的時間。</span><span class="sxs-lookup"><span data-stu-id="685cf-144">Time at which the event ended.</span></span>|<span data-ttu-id="685cf-145">15</span><span class="sxs-lookup"><span data-stu-id="685cf-145">15</span></span>|<span data-ttu-id="685cf-146">是</span><span class="sxs-lookup"><span data-stu-id="685cf-146">Yes</span></span>|  
|<span data-ttu-id="685cf-147">EventClass</span><span class="sxs-lookup"><span data-stu-id="685cf-147">EventClass</span></span>|`int`|<span data-ttu-id="685cf-148">事件類型 = 24。</span><span class="sxs-lookup"><span data-stu-id="685cf-148">Type of event = 24.</span></span>|<span data-ttu-id="685cf-149">27</span><span class="sxs-lookup"><span data-stu-id="685cf-149">27</span></span>|<span data-ttu-id="685cf-150">否</span><span class="sxs-lookup"><span data-stu-id="685cf-150">No</span></span>|  
|<span data-ttu-id="685cf-151">EventSequence</span><span class="sxs-lookup"><span data-stu-id="685cf-151">EventSequence</span></span>|`int`|<span data-ttu-id="685cf-152">要求中的給定事件順序。</span><span class="sxs-lookup"><span data-stu-id="685cf-152">Sequence of a given event within the request.</span></span>|<span data-ttu-id="685cf-153">51</span><span class="sxs-lookup"><span data-stu-id="685cf-153">51</span></span>|<span data-ttu-id="685cf-154">否</span><span class="sxs-lookup"><span data-stu-id="685cf-154">No</span></span>|  
|<span data-ttu-id="685cf-155">GroupID</span><span class="sxs-lookup"><span data-stu-id="685cf-155">GroupID</span></span>|`int`|<span data-ttu-id="685cf-156">SQL 追蹤事件引發所在之工作負載群組的識別碼。</span><span class="sxs-lookup"><span data-stu-id="685cf-156">ID of the workload group where the SQL Trace event fires.</span></span>|<span data-ttu-id="685cf-157">66</span><span class="sxs-lookup"><span data-stu-id="685cf-157">66</span></span>|<span data-ttu-id="685cf-158">是</span><span class="sxs-lookup"><span data-stu-id="685cf-158">Yes</span></span>|  
|<span data-ttu-id="685cf-159">HostName</span><span class="sxs-lookup"><span data-stu-id="685cf-159">HostName</span></span>|`nvarchar`|<span data-ttu-id="685cf-160">執行用戶端的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="685cf-160">Name of the computer on which the client is running.</span></span> <span data-ttu-id="685cf-161">如果用戶端提供主機名稱，這個資料行就會擴展。</span><span class="sxs-lookup"><span data-stu-id="685cf-161">This data column is populated if the client provides the host name.</span></span> <span data-ttu-id="685cf-162">若要判斷主機名稱，請使用 HOST_NAME 函數。</span><span class="sxs-lookup"><span data-stu-id="685cf-162">To determine the host name, use the HOST_NAME function.</span></span>|<span data-ttu-id="685cf-163">8</span><span class="sxs-lookup"><span data-stu-id="685cf-163">8</span></span>|<span data-ttu-id="685cf-164">是</span><span class="sxs-lookup"><span data-stu-id="685cf-164">Yes</span></span>|  
|<span data-ttu-id="685cf-165">IntegerData2</span><span class="sxs-lookup"><span data-stu-id="685cf-165">IntegerData2</span></span>|`int`|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|<span data-ttu-id="685cf-166">55</span><span class="sxs-lookup"><span data-stu-id="685cf-166">55</span></span>|<span data-ttu-id="685cf-167">是</span><span class="sxs-lookup"><span data-stu-id="685cf-167">Yes</span></span>|  
|<span data-ttu-id="685cf-168">IsSystem</span><span class="sxs-lookup"><span data-stu-id="685cf-168">IsSystem</span></span>|`int`|<span data-ttu-id="685cf-169">指出事件是發生在系統處理序或使用者處理序。</span><span class="sxs-lookup"><span data-stu-id="685cf-169">Indicates whether the event occurred on a system process or a user process.</span></span> <span data-ttu-id="685cf-170">1 = 系統，0 = 使用者。</span><span class="sxs-lookup"><span data-stu-id="685cf-170">1 = system, 0 = user.</span></span>|<span data-ttu-id="685cf-171">60</span><span class="sxs-lookup"><span data-stu-id="685cf-171">60</span></span>|<span data-ttu-id="685cf-172">是</span><span class="sxs-lookup"><span data-stu-id="685cf-172">Yes</span></span>|  
|<span data-ttu-id="685cf-173">LoginName</span><span class="sxs-lookup"><span data-stu-id="685cf-173">LoginName</span></span>|`nvarchar`|<span data-ttu-id="685cf-174">使用者的登入名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 Windows 登入認證)。</span><span class="sxs-lookup"><span data-stu-id="685cf-174">Name of the login of the user (either [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] security login or the Windows login credentials in the form of DOMAIN\username).</span></span>|<span data-ttu-id="685cf-175">11</span><span class="sxs-lookup"><span data-stu-id="685cf-175">11</span></span>|<span data-ttu-id="685cf-176">是</span><span class="sxs-lookup"><span data-stu-id="685cf-176">Yes</span></span>|  
|<span data-ttu-id="685cf-177">LoginSid</span><span class="sxs-lookup"><span data-stu-id="685cf-177">LoginSid</span></span>|`image`|<span data-ttu-id="685cf-178">已登入之使用者的安全性識別碼 (SID)。</span><span class="sxs-lookup"><span data-stu-id="685cf-178">Security identification number (SID) of the logged-in user.</span></span> <span data-ttu-id="685cf-179">您可以在 sys.server_principals 目錄檢視中找到這項資訊。</span><span class="sxs-lookup"><span data-stu-id="685cf-179">You can find this information in the sys.server_principals catalog view.</span></span> <span data-ttu-id="685cf-180">伺服器上的每一個登入之 SID 是唯一的。</span><span class="sxs-lookup"><span data-stu-id="685cf-180">Each SID is unique for each login in the server.</span></span>|<span data-ttu-id="685cf-181">41</span><span class="sxs-lookup"><span data-stu-id="685cf-181">41</span></span>|<span data-ttu-id="685cf-182">是</span><span class="sxs-lookup"><span data-stu-id="685cf-182">Yes</span></span>|  
|<span data-ttu-id="685cf-183">[模式]</span><span class="sxs-lookup"><span data-stu-id="685cf-183">Mode</span></span>|`int`|<span data-ttu-id="685cf-184">取得鎖定之後產生的模式。</span><span class="sxs-lookup"><span data-stu-id="685cf-184">Resulting mode after the lock was acquired.</span></span><br /><br /> <span data-ttu-id="685cf-185">0=NULL - 與其他所有鎖定模式相容 (LCK_M_NL)</span><span class="sxs-lookup"><span data-stu-id="685cf-185">0=NULL - Compatible with all other lock modes (LCK_M_NL)</span></span><br /><br /> <span data-ttu-id="685cf-186">1=結構描述穩定性鎖定 (LCK_M_SCH_S)</span><span class="sxs-lookup"><span data-stu-id="685cf-186">1=Schema Stability lock (LCK_M_SCH_S)</span></span><br /><br /> <span data-ttu-id="685cf-187">2=結構描述修改鎖定 (LCK_M_SCH_M)</span><span class="sxs-lookup"><span data-stu-id="685cf-187">2=Schema Modification Lock (LCK_M_SCH_M)</span></span><br /><br /> <span data-ttu-id="685cf-188">3=共用鎖定 (LCK_M_S)</span><span class="sxs-lookup"><span data-stu-id="685cf-188">3=Shared Lock (LCK_M_S)</span></span><br /><br /> <span data-ttu-id="685cf-189">4=更新鎖定 (LCK_M_U)</span><span class="sxs-lookup"><span data-stu-id="685cf-189">4=Update Lock (LCK_M_U)</span></span><br /><br /> <span data-ttu-id="685cf-190">5=獨佔鎖定 (LCK_M_X)</span><span class="sxs-lookup"><span data-stu-id="685cf-190">5=Exclusive Lock (LCK_M_X)</span></span><br /><br /> <span data-ttu-id="685cf-191">6=意圖共用鎖定 (LCK_M_IS)</span><span class="sxs-lookup"><span data-stu-id="685cf-191">6=Intent Shared Lock (LCK_M_IS)</span></span><br /><br /> <span data-ttu-id="685cf-192">7=意圖更新鎖定 (LCK_M_IU)</span><span class="sxs-lookup"><span data-stu-id="685cf-192">7=Intent Update Lock (LCK_M_IU)</span></span><br /><br /> <span data-ttu-id="685cf-193">8=意圖獨佔鎖定 (LCK_M_IX)</span><span class="sxs-lookup"><span data-stu-id="685cf-193">8=Intent Exclusive Lock (LCK_M_IX)</span></span><br /><br /> <span data-ttu-id="685cf-194">9=與意圖更新共用 (LCK_M_SIU)</span><span class="sxs-lookup"><span data-stu-id="685cf-194">9=Shared with intent to Update (LCK_M_SIU)</span></span><br /><br /> <span data-ttu-id="685cf-195">10=與意圖獨佔共用 (LCK_M_SIX)</span><span class="sxs-lookup"><span data-stu-id="685cf-195">10=Shared with Intent Exclusive (LCK_M_SIX)</span></span><br /><br /> <span data-ttu-id="685cf-196">11=以意圖獨佔更新 (LCK_M_UIX)</span><span class="sxs-lookup"><span data-stu-id="685cf-196">11=Update with Intent Exclusive (LCK_M_UIX)</span></span><br /><br /> <span data-ttu-id="685cf-197">12=大量更新鎖定 (LCK_M_BU)</span><span class="sxs-lookup"><span data-stu-id="685cf-197">12=Bulk Update Lock (LCK_M_BU)</span></span><br /><br /> <span data-ttu-id="685cf-198">13=關鍵範圍共用/共用 (LCK_M_RS_S)</span><span class="sxs-lookup"><span data-stu-id="685cf-198">13=Key range Shared/Shared (LCK_M_RS_S)</span></span><br /><br /> <span data-ttu-id="685cf-199">14=關鍵範圍共用/更新 (LCK_M_RS_U)</span><span class="sxs-lookup"><span data-stu-id="685cf-199">14=Key range Shared/Update (LCK_M_RS_U)</span></span><br /><br /> <span data-ttu-id="685cf-200">15=關鍵範圍插入 NULL (LCK_M_RI_NL)</span><span class="sxs-lookup"><span data-stu-id="685cf-200">15=Key Range Insert NULL (LCK_M_RI_NL)</span></span><br /><br /> <span data-ttu-id="685cf-201">16=關鍵範圍插入共用 (LCK_M_RI_S)</span><span class="sxs-lookup"><span data-stu-id="685cf-201">16=Key Range Insert Shared (LCK_M_RI_S)</span></span><br /><br /> <span data-ttu-id="685cf-202">17=關鍵範圍插入更新 (LCK_M_RI_U)</span><span class="sxs-lookup"><span data-stu-id="685cf-202">17=Key Range Insert Update (LCK_M_RI_U)</span></span><br /><br /> <span data-ttu-id="685cf-203">18=關鍵範圍插入獨佔 (LCK_M_RI_X)</span><span class="sxs-lookup"><span data-stu-id="685cf-203">18=Key Range Insert Exclusive (LCK_M_RI_X)</span></span><br /><br /> <span data-ttu-id="685cf-204">19=關鍵範圍獨佔共用 (LCK_M_RX_S)</span><span class="sxs-lookup"><span data-stu-id="685cf-204">19=Key Range Exclusive Shared (LCK_M_RX_S)</span></span><br /><br /> <span data-ttu-id="685cf-205">20=關鍵範圍獨佔更新 (LCK_M_RX_U)</span><span class="sxs-lookup"><span data-stu-id="685cf-205">20=Key Range Exclusive Update (LCK_M_RX_U)</span></span><br /><br /> <span data-ttu-id="685cf-206">21=關鍵範圍獨佔獨佔 (LCK_M_RX_X)</span><span class="sxs-lookup"><span data-stu-id="685cf-206">21=Key Range Exclusive Exclusive (LCK_M_RX_X)</span></span>|<span data-ttu-id="685cf-207">32</span><span class="sxs-lookup"><span data-stu-id="685cf-207">32</span></span>|<span data-ttu-id="685cf-208">是</span><span class="sxs-lookup"><span data-stu-id="685cf-208">Yes</span></span>|  
|<span data-ttu-id="685cf-209">NTDomainName</span><span class="sxs-lookup"><span data-stu-id="685cf-209">NTDomainName</span></span>|`nvarchar`|<span data-ttu-id="685cf-210">使用者所隸屬的 Windows 網域。</span><span class="sxs-lookup"><span data-stu-id="685cf-210">Windows domain to which the user belongs.</span></span>|<span data-ttu-id="685cf-211">7</span><span class="sxs-lookup"><span data-stu-id="685cf-211">7</span></span>|<span data-ttu-id="685cf-212">是</span><span class="sxs-lookup"><span data-stu-id="685cf-212">Yes</span></span>|  
|<span data-ttu-id="685cf-213">NTUserName</span><span class="sxs-lookup"><span data-stu-id="685cf-213">NTUserName</span></span>|`nvarchar`|<span data-ttu-id="685cf-214">Windows 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="685cf-214">Windows user name.</span></span>|<span data-ttu-id="685cf-215">6</span><span class="sxs-lookup"><span data-stu-id="685cf-215">6</span></span>|<span data-ttu-id="685cf-216">是</span><span class="sxs-lookup"><span data-stu-id="685cf-216">Yes</span></span>|  
|<span data-ttu-id="685cf-217">ObjectID</span><span class="sxs-lookup"><span data-stu-id="685cf-217">ObjectID</span></span>|`int`|<span data-ttu-id="685cf-218">在其上取得鎖定的物件識別碼 (如果有且適用的話)。</span><span class="sxs-lookup"><span data-stu-id="685cf-218">ID of the object on which the lock was acquired, if available and applicable.</span></span>|<span data-ttu-id="685cf-219">22</span><span class="sxs-lookup"><span data-stu-id="685cf-219">22</span></span>|<span data-ttu-id="685cf-220">是</span><span class="sxs-lookup"><span data-stu-id="685cf-220">Yes</span></span>|  
|<span data-ttu-id="685cf-221">ObjectID2</span><span class="sxs-lookup"><span data-stu-id="685cf-221">ObjectID2</span></span>|`bigint`|<span data-ttu-id="685cf-222">相關物件或實體的識別碼 (如果有且適用的話)。</span><span class="sxs-lookup"><span data-stu-id="685cf-222">ID of the related object or entity, if available and applicable.</span></span>|<span data-ttu-id="685cf-223">56</span><span class="sxs-lookup"><span data-stu-id="685cf-223">56</span></span>|<span data-ttu-id="685cf-224">是</span><span class="sxs-lookup"><span data-stu-id="685cf-224">Yes</span></span>|  
|<span data-ttu-id="685cf-225">OwnerID</span><span class="sxs-lookup"><span data-stu-id="685cf-225">OwnerID</span></span>|`int`|<span data-ttu-id="685cf-226">1=TRANSACTION</span><span class="sxs-lookup"><span data-stu-id="685cf-226">1=TRANSACTION</span></span><br /><br /> <span data-ttu-id="685cf-227">2=CURSOR</span><span class="sxs-lookup"><span data-stu-id="685cf-227">2=CURSOR</span></span><br /><br /> <span data-ttu-id="685cf-228">3=SESSION</span><span class="sxs-lookup"><span data-stu-id="685cf-228">3=SESSION</span></span><br /><br /> <span data-ttu-id="685cf-229">4=SHARED_TRANSACTION_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="685cf-229">4=SHARED_TRANSACTION_WORKSPACE</span></span><br /><br /> <span data-ttu-id="685cf-230">5=EXCLUSIVE_TRANSACTION_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="685cf-230">5=EXCLUSIVE_TRANSACTION_WORKSPACE</span></span>|<span data-ttu-id="685cf-231">58</span><span class="sxs-lookup"><span data-stu-id="685cf-231">58</span></span>|<span data-ttu-id="685cf-232">是</span><span class="sxs-lookup"><span data-stu-id="685cf-232">Yes</span></span>|  
|<span data-ttu-id="685cf-233">RequestID</span><span class="sxs-lookup"><span data-stu-id="685cf-233">RequestID</span></span>|`int`|<span data-ttu-id="685cf-234">包含陳述式之要求的識別碼。</span><span class="sxs-lookup"><span data-stu-id="685cf-234">ID of the request containing the statement.</span></span>|<span data-ttu-id="685cf-235">49</span><span class="sxs-lookup"><span data-stu-id="685cf-235">49</span></span>|<span data-ttu-id="685cf-236">是</span><span class="sxs-lookup"><span data-stu-id="685cf-236">Yes</span></span>|  
|<span data-ttu-id="685cf-237">ServerName</span><span class="sxs-lookup"><span data-stu-id="685cf-237">ServerName</span></span>|`nvarchar`|<span data-ttu-id="685cf-238">正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="685cf-238">Name of the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] being traced.</span></span>|<span data-ttu-id="685cf-239">26</span><span class="sxs-lookup"><span data-stu-id="685cf-239">26</span></span>|<span data-ttu-id="685cf-240">否</span><span class="sxs-lookup"><span data-stu-id="685cf-240">No</span></span>|  
|<span data-ttu-id="685cf-241">SessionLoginName</span><span class="sxs-lookup"><span data-stu-id="685cf-241">SessionLoginName</span></span>|`nvarchar`|<span data-ttu-id="685cf-242">引發工作階段之使用者的登入名稱。</span><span class="sxs-lookup"><span data-stu-id="685cf-242">Login name of the user who originated the session.</span></span> <span data-ttu-id="685cf-243">例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。</span><span class="sxs-lookup"><span data-stu-id="685cf-243">For example, if you connect to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] using Login1 and execute a statement as Login2, SessionLoginName shows Login1 and LoginName shows Login2.</span></span> <span data-ttu-id="685cf-244">此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。</span><span class="sxs-lookup"><span data-stu-id="685cf-244">This column displays both [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and Windows logins.</span></span>|<span data-ttu-id="685cf-245">64</span><span class="sxs-lookup"><span data-stu-id="685cf-245">64</span></span>|<span data-ttu-id="685cf-246">是</span><span class="sxs-lookup"><span data-stu-id="685cf-246">Yes</span></span>|  
|<span data-ttu-id="685cf-247">SPID</span><span class="sxs-lookup"><span data-stu-id="685cf-247">SPID</span></span>|`int`|<span data-ttu-id="685cf-248">事件發生所在之工作階段的識別碼。</span><span class="sxs-lookup"><span data-stu-id="685cf-248">ID of the session on which the event occurred.</span></span>|<span data-ttu-id="685cf-249">12</span><span class="sxs-lookup"><span data-stu-id="685cf-249">12</span></span>|<span data-ttu-id="685cf-250">是</span><span class="sxs-lookup"><span data-stu-id="685cf-250">Yes</span></span>|  
|<span data-ttu-id="685cf-251">StartTime</span><span class="sxs-lookup"><span data-stu-id="685cf-251">StartTime</span></span>|`datetime`|<span data-ttu-id="685cf-252">事件啟動的時間 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="685cf-252">Time at which the event started, if available.</span></span>|<span data-ttu-id="685cf-253">14</span><span class="sxs-lookup"><span data-stu-id="685cf-253">14</span></span>|<span data-ttu-id="685cf-254">是</span><span class="sxs-lookup"><span data-stu-id="685cf-254">Yes</span></span>|  
|<span data-ttu-id="685cf-255">TextData</span><span class="sxs-lookup"><span data-stu-id="685cf-255">TextData</span></span>|`ntext`|<span data-ttu-id="685cf-256">與取得的鎖定類型有關的文字值。</span><span class="sxs-lookup"><span data-stu-id="685cf-256">Text value dependent on the lock type that was acquired.</span></span> <span data-ttu-id="685cf-257">這和 sys.dm_tran_locks 中的 resource_description 資料行是相同的值。</span><span class="sxs-lookup"><span data-stu-id="685cf-257">This is the same value as the resource_description column in sys.dm_tran_locks.</span></span>|<span data-ttu-id="685cf-258">1</span><span class="sxs-lookup"><span data-stu-id="685cf-258">1</span></span>|<span data-ttu-id="685cf-259">是</span><span class="sxs-lookup"><span data-stu-id="685cf-259">Yes</span></span>|  
|<span data-ttu-id="685cf-260">TransactionID</span><span class="sxs-lookup"><span data-stu-id="685cf-260">TransactionID</span></span>|`bigint`|<span data-ttu-id="685cf-261">由系統指派給交易的識別碼。</span><span class="sxs-lookup"><span data-stu-id="685cf-261">System-assigned ID of the transaction.</span></span>|<span data-ttu-id="685cf-262">4</span><span class="sxs-lookup"><span data-stu-id="685cf-262">4</span></span>|<span data-ttu-id="685cf-263">是</span><span class="sxs-lookup"><span data-stu-id="685cf-263">Yes</span></span>|  
|<span data-ttu-id="685cf-264">類型</span><span class="sxs-lookup"><span data-stu-id="685cf-264">Type</span></span>|`int`|<span data-ttu-id="685cf-265">1=NULL_RESOURCE</span><span class="sxs-lookup"><span data-stu-id="685cf-265">1=NULL_RESOURCE</span></span><br /><br /> <span data-ttu-id="685cf-266">2=DATABASE</span><span class="sxs-lookup"><span data-stu-id="685cf-266">2=DATABASE</span></span><br /><br /> <span data-ttu-id="685cf-267">3=FILE</span><span class="sxs-lookup"><span data-stu-id="685cf-267">3=FILE</span></span><br /><br /> <span data-ttu-id="685cf-268">5=OBJECT</span><span class="sxs-lookup"><span data-stu-id="685cf-268">5=OBJECT</span></span><br /><br /> <span data-ttu-id="685cf-269">6=PAGE</span><span class="sxs-lookup"><span data-stu-id="685cf-269">6=PAGE</span></span><br /><br /> <span data-ttu-id="685cf-270">7=KEY</span><span class="sxs-lookup"><span data-stu-id="685cf-270">7=KEY</span></span><br /><br /> <span data-ttu-id="685cf-271">8=EXTENT</span><span class="sxs-lookup"><span data-stu-id="685cf-271">8=EXTENT</span></span><br /><br /> <span data-ttu-id="685cf-272">9=RID</span><span class="sxs-lookup"><span data-stu-id="685cf-272">9=RID</span></span><br /><br /> <span data-ttu-id="685cf-273">10=APPLICATION</span><span class="sxs-lookup"><span data-stu-id="685cf-273">10=APPLICATION</span></span><br /><br /> <span data-ttu-id="685cf-274">11=METADATA</span><span class="sxs-lookup"><span data-stu-id="685cf-274">11=METADATA</span></span><br /><br /> <span data-ttu-id="685cf-275">12=AUTONAMEDB</span><span class="sxs-lookup"><span data-stu-id="685cf-275">12=AUTONAMEDB</span></span><br /><br /> <span data-ttu-id="685cf-276">13=HOBT</span><span class="sxs-lookup"><span data-stu-id="685cf-276">13=HOBT</span></span><br /><br /> <span data-ttu-id="685cf-277">14=ALLOCATION_UNIT</span><span class="sxs-lookup"><span data-stu-id="685cf-277">14=ALLOCATION_UNIT</span></span>|<span data-ttu-id="685cf-278">57</span><span class="sxs-lookup"><span data-stu-id="685cf-278">57</span></span>|<span data-ttu-id="685cf-279">是</span><span class="sxs-lookup"><span data-stu-id="685cf-279">Yes</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="685cf-280">另請參閱</span><span class="sxs-lookup"><span data-stu-id="685cf-280">See Also</span></span>  
 <span data-ttu-id="685cf-281">[Lock：已釋放事件類別](lock-released-event-class.md) </span><span class="sxs-lookup"><span data-stu-id="685cf-281">[Lock:Released Event Class](lock-released-event-class.md) </span></span>  
 <span data-ttu-id="685cf-282">[sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="685cf-282">[sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql) </span></span>  
 [<span data-ttu-id="685cf-283">sys.dm_tran_locks &#40;Transact-SQL&#41;</span><span class="sxs-lookup"><span data-stu-id="685cf-283">sys.dm_tran_locks &#40;Transact-SQL&#41;</span></span>](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql)  
  
  