---
title: 限制報表記錄 (報表管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- viewing report history
- report history [Reporting Services], viewing history
- report history [Reporting Services], configuring history
- historical data [Reporting Services]
- displaying report history
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 01318b1e1ccf0b0bf4512ab57de90cbf5ebc7365
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688505"
---
# <a name="limit-report-history-report-manager"></a><span data-ttu-id="7fd7a-102">限制報表記錄 (報表管理員)</span><span class="sxs-lookup"><span data-stu-id="7fd7a-102">Limit Report History (Report Manager)</span></span>
  <span data-ttu-id="7fd7a-103">報表記錄是您在經過一段時間後建立之報表快照集的集合。</span><span class="sxs-lookup"><span data-stu-id="7fd7a-103">Report history is a collection of report snapshots that you create over time.</span></span> <span data-ttu-id="7fd7a-104">您可以視需要建立報表記錄，或是排程在報表記錄中建立和加入快照集的頻率。</span><span class="sxs-lookup"><span data-stu-id="7fd7a-104">You can create report history on demand, or schedule how often a snapshot is created and added to report history.</span></span>  
  
 <span data-ttu-id="7fd7a-105">報表記錄會儲存在報表伺服器資料庫中。</span><span class="sxs-lookup"><span data-stu-id="7fd7a-105">Report history is stored in the report server database.</span></span> <span data-ttu-id="7fd7a-106">如果報表快照集包含大量資料，您可能會考慮限制報表記錄，以便盡可能減少快照集保留對資料庫大小的影響。</span><span class="sxs-lookup"><span data-stu-id="7fd7a-106">If report snapshots contain a large amount of data, you might consider limiting report history to minimize the affect of snapshot retention on database size.</span></span>  
  
### <a name="to-configure-report-history-for-a-report-server"></a><span data-ttu-id="7fd7a-107">若要設定報表伺服器的報表記錄</span><span class="sxs-lookup"><span data-stu-id="7fd7a-107">To configure report history for a report server</span></span>  
  
1.  <span data-ttu-id="7fd7a-108">在報表管理員中，按一下全域工具列上的 [網站設定]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="7fd7a-108">In Report Manager, click **Site Settings** on the global toolbar.</span></span>  
  
2.  <span data-ttu-id="7fd7a-109">若要無限地保存所有報表記錄，請選取 [不限制報表記錄中的快照集數目]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="7fd7a-109">Select **Keep an unlimited number of snapshots in report history** if you want to keep all report history indefinitely.</span></span> <span data-ttu-id="7fd7a-110">否則，請選取 [限制報表記錄的副本]\*\*\*\*，指定可以為任一給定報表保存的快照集最大數目。</span><span class="sxs-lookup"><span data-stu-id="7fd7a-110">Otherwise, select **Limit the copies of report history** to specify the maximum number of snapshots that can be kept for any given report.</span></span>  
  
3.  <span data-ttu-id="7fd7a-111">按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="7fd7a-111">Click **Apply**.</span></span>  
  
### <a name="to-configure-report-history-for-a-specific-report"></a><span data-ttu-id="7fd7a-112">若要設定特定報表的報表記錄</span><span class="sxs-lookup"><span data-stu-id="7fd7a-112">To configure report history for a specific report</span></span>  
  
1.  <span data-ttu-id="7fd7a-113">在報表管理員中，導覽至您要設定記錄的報表，然後按一下該報表來開啟它。</span><span class="sxs-lookup"><span data-stu-id="7fd7a-113">In Report Manager, navigate to the report for which you want to configure history, and then click the report to open it.</span></span>  
  
2.  <span data-ttu-id="7fd7a-114">按一下 [屬性] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7fd7a-114">Click the **Properties** tab.</span></span>  
  
3.  <span data-ttu-id="7fd7a-115">按一下 [**歷程記錄**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7fd7a-115">Click the **History** tab.</span></span>  
  
4.  <span data-ttu-id="7fd7a-116">選取報表的選項，然後按一下 [套用]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="7fd7a-116">Select the options for your report and click **Apply**.</span></span> <span data-ttu-id="7fd7a-117">如需每個選項的詳細資訊，請參閱[快照集選項屬性頁 &#40;報表管理員&#41;](../snapshot-options-properties-page-report-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="7fd7a-117">For details about each option, see [Snapshot Options Properties Page &#40;Report Manager&#41;](../snapshot-options-properties-page-report-manager.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7fd7a-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7fd7a-118">See Also</span></span>  
 <span data-ttu-id="7fd7a-119">[將快照集加入至報表記錄 &#40;報表管理員&#41;](../report-server/add-a-snapshot-to-report-history-report-manager.md) </span><span class="sxs-lookup"><span data-stu-id="7fd7a-119">[Add a Snapshot to Report History &#40;Report Manager&#41;](../report-server/add-a-snapshot-to-report-history-report-manager.md) </span></span>  
 [<span data-ttu-id="7fd7a-120">報表管理員 &#40;SSRS 原生模式&#41;</span><span class="sxs-lookup"><span data-stu-id="7fd7a-120">Report Manager  &#40;SSRS Native Mode&#41;</span></span>](../report-manager-ssrs-native-mode.md)  
  
  
