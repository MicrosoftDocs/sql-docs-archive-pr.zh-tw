---
title: 使用效能物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
author: stevestein
ms.author: sstein
ms.openlocfilehash: d7c1fe3f4a7d9a5fec901f84d8e913e49a4dbd1b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597532"
---
# <a name="use-performance-objects"></a><span data-ttu-id="a21cb-102">使用效能物件</span><span class="sxs-lookup"><span data-stu-id="a21cb-102">Use Performance Objects</span></span>
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="a21cb-103">Agent 包含效能物件及計數器，可用來監視服務執行的狀況。</span><span class="sxs-lookup"><span data-stu-id="a21cb-103">Agent includes performance objects and counters to monitor how the service is performing.</span></span> <span data-ttu-id="a21cb-104">這些效能物件可讓您使用「效能監視器」(一種 Windows 工具)，來識別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務在背景執行哪些工作。</span><span class="sxs-lookup"><span data-stu-id="a21cb-104">These performance objects allow you to use Performance Monitor, a Windows tool, to identify what the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent service is doing in the background.</span></span> <span data-ttu-id="a21cb-105">例如，您可以識別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務目前正在執行多少使用中的作業，以找出被封鎖的作業。</span><span class="sxs-lookup"><span data-stu-id="a21cb-105">For example, you can identify how many active jobs the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent service is currently running to identify those jobs that are blocked.</span></span>  
  
 <span data-ttu-id="a21cb-106">針對電腦上所安裝的每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，都有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務效能物件及計數器存在。</span><span class="sxs-lookup"><span data-stu-id="a21cb-106">The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent service performance objects and counters exist for each instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] that is installed on a computer.</span></span> <span data-ttu-id="a21cb-107">效能物件是依據每項物件所代表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體來命名的。</span><span class="sxs-lookup"><span data-stu-id="a21cb-107">Performance objects are named according to the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] that each object represents.</span></span>  
  
 <span data-ttu-id="a21cb-108">下表顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務效能物件的命名方式：</span><span class="sxs-lookup"><span data-stu-id="a21cb-108">The following table shows how the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent service performance objects are named:</span></span>  
  
|<span data-ttu-id="a21cb-109">執行個體類型</span><span class="sxs-lookup"><span data-stu-id="a21cb-109">Instance type</span></span>|<span data-ttu-id="a21cb-110">物件名稱</span><span class="sxs-lookup"><span data-stu-id="a21cb-110">Object name</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="a21cb-111">預設</span><span class="sxs-lookup"><span data-stu-id="a21cb-111">Default</span></span>|<span data-ttu-id="a21cb-112">**SQLAgent:** *object*:*counter*</span><span class="sxs-lookup"><span data-stu-id="a21cb-112">**SQLAgent:** *object*:*counter*</span></span>|  
|<span data-ttu-id="a21cb-113">已命名</span><span class="sxs-lookup"><span data-stu-id="a21cb-113">Named</span></span>|<span data-ttu-id="a21cb-114">**SQLAgent$**</span><span class="sxs-lookup"><span data-stu-id="a21cb-114">**SQLAgent$**</span></span><br /> <span data-ttu-id="a21cb-115">***instance_name* ：** *object*：*計數器*</span><span class="sxs-lookup"><span data-stu-id="a21cb-115">***instance_name* :** *object*:*counter*</span></span>|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="a21cb-116">包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的下列效能物件。</span><span class="sxs-lookup"><span data-stu-id="a21cb-116">includes the following performance objects for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.</span></span>  
  
|<span data-ttu-id="a21cb-117">物件名稱</span><span class="sxs-lookup"><span data-stu-id="a21cb-117">Object name</span></span>|<span data-ttu-id="a21cb-118">描述</span><span class="sxs-lookup"><span data-stu-id="a21cb-118">Description</span></span>|  
|-----------------|-----------------|  
|[<span data-ttu-id="a21cb-119">SQLAgent:Jobs</span><span class="sxs-lookup"><span data-stu-id="a21cb-119">SQLAgent:Jobs</span></span>](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|<span data-ttu-id="a21cb-120">有關已啟動作業、成功率及目前狀態的效能資訊</span><span class="sxs-lookup"><span data-stu-id="a21cb-120">Performance information about jobs that have been started, success rates, and current status</span></span>|  
|[<span data-ttu-id="a21cb-121">SQLAgent:JobSteps</span><span class="sxs-lookup"><span data-stu-id="a21cb-121">SQLAgent:JobSteps</span></span>](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|<span data-ttu-id="a21cb-122">作業步驟的狀態資訊</span><span class="sxs-lookup"><span data-stu-id="a21cb-122">Status information about job steps</span></span>|  
|[<span data-ttu-id="a21cb-123">SQLAgent:Alerts</span><span class="sxs-lookup"><span data-stu-id="a21cb-123">SQLAgent:Alerts</span></span>](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|<span data-ttu-id="a21cb-124">警示及通知數的相關資訊</span><span class="sxs-lookup"><span data-stu-id="a21cb-124">Information about number of alerts and notifications</span></span>|  
|[<span data-ttu-id="a21cb-125">SQLAgent:Statistics</span><span class="sxs-lookup"><span data-stu-id="a21cb-125">SQLAgent:Statistics</span></span>](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|<span data-ttu-id="a21cb-126">一般效能資訊</span><span class="sxs-lookup"><span data-stu-id="a21cb-126">General performance information</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="a21cb-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a21cb-127">See Also</span></span>  
 <span data-ttu-id="a21cb-128">[效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md) </span><span class="sxs-lookup"><span data-stu-id="a21cb-128">[Monitor and Tune for Performance](../../relational-databases/performance/monitor-and-tune-for-performance.md) </span></span>  
 [<span data-ttu-id="a21cb-129">啟動系統監視器 &#40;Windows&#41;</span><span class="sxs-lookup"><span data-stu-id="a21cb-129">Start System Monitor &#40;Windows&#41;</span></span>](../../relational-databases/performance/start-system-monitor-windows.md)  
  
  
