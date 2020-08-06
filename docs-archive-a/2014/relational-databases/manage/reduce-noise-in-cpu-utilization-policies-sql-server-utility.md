---
title: 降低 CPU 使用量原則的雜訊 (SQL Server 公用程式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.SWB.UE.ReduceNoise.F1
ms.assetid: 94bf4d93-c0ff-4869-bde7-80c24866092e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 70677d5b21b47af87d596db1f18d0b5bc14145a2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706490"
---
# <a name="reduce-noise-in-cpu-utilization-policies-sql-server-utility"></a>降低 CPU 使用量原則的雜訊 (SQL Server 公用程式)
  使用下列策略，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式資源使用量原則中減少報告雜訊及不必要的違規。  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-overutilized"></a>將處理器使用量報告為過高之前，其違規的頻率應該是多少？  
 您可以在公用程式總管中，使用 **[公用程式管理]** 節點的 **[原則]** 索引標籤設定來設定評估期間和違規百分比的容錯。 若要變更原則，請使用原則描述右邊的滑動軸控制項，然後按一下 **[套用]** 。 您也可以使用顯示畫面底部的按鈕來還原預設值或捨棄變更。  
  
-   資料收集間隔是 15 分鐘。 您無法設定這個值。  
  
-   處理器使用量原則的預設臨界值上限為 70%。 選項的範圍是從 0% 到 100%。  
  
-   處理器使用量過高的預設評估期間是 1 小時。 選項的範圍是從 1 小時到 1 週。  
  
-   將 CPU 報告為使用量過高之前，資料點違規的預設百分比為 20%。 選項的範圍是從 0% 到 100%。  
  
 例如，根據預設值，每個小時將會收集 4 個資料點，而且原則臨界值為 20%。 因此，根據預設值，1 小時收集期間內的任何違規將會是 4 個資料點的 25%。 預設值會報告 CPU 使用量過高原則臨界值的任何違規。  
  
 若要減少單一違規所產生的雜訊，請考慮下列選項：  
  
-   增加評估期間的 1 個增量，使其成為 6 小時。 6 小時內的單一違規將會是取樣大小 24 中的 1 個資料點。 在此情況下，原則將會容許 6 個小時內原則臨界值有 4 個違規 (16.7% 的資料點)，但是會在 6 小時的收集期間內，報告 5 或 5 個以上的違規有使用量過高情形 (>20% 的資料點)。  
  
-   將違規的百分比容錯提高 1 個增量，成為 30%。 1 小時內的單一違規將會是取樣大小 4 中的 1 個資料點。 在此情況下，此原則將會容許每個小時有 1 個違規，但是會在 1 小時的收集期間內，報告 2 或 2 個以上的違規有使用量過高情形 (>30% 的資料點)。  
  
-   提高 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Managed 執行個體和資料層應用程式之處理器使用量的原則臨界值。 如需如何變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體或資料層應用程式之全域 CPU 使用量原則的詳細資訊，請參閱 [公用程式管理 &#40;SQL Server 公用程式&#41;](../../database-engine/utility-administration-sql-server-utility.md)。 如需如何變更個別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之 CPU 使用量原則的詳細資訊，請參閱[受管理的執行個體詳細資料 &#40;SQL Server 公用程式&#41;](../../database-engine/managed-instance-details-sql-server-utility.md)。 如需如何變更個別資料層應用程式之 CPU 使用量原則的詳細資訊，請參閱[部署的資料層應用程式詳細資料 &#40;SQL Server 公用程式&#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md)。  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-underutilized"></a>將處理器使用量報告為過低之前，其違規的頻率應該是多少？  
 您可以在公用程式總管中，使用 **[公用程式管理]** 節點的 **[原則]** 索引標籤設定來設定評估期間和違規百分比的容錯。 若要變更原則，請使用原則描述右邊的滑動軸控制項，然後按一下 **[套用]** 。 您也可以使用顯示畫面底部的按鈕來還原預設值或捨棄變更。  
  
-   資料收集間隔是 15 分鐘。 您無法設定這個值。  
  
-   處理器使用量原則的預設臨界值下限為 0%。 選項的範圍是從 0% 到 100%。  
  
-   處理器使用量過低的預設評估期間是 1 週。 選項的範圍是從 1 天到 1 個月。  
  
-   將 CPU 報告為使用量過低之前，資料點違規的預設百分比為 90%。 選項的範圍是從 0% 到 100%。  
  
 根據預設值，每週將會收集 672 個資料點，而且原則臨界值為 0%。 所以根據預設，這個原則不會產生處理器使用量過低的違規情形。 如需如何變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體或資料層應用程式之全域 CPU 使用量原則的詳細資訊，請參閱 [公用程式管理 &#40;SQL Server 公用程式&#41;](../../database-engine/utility-administration-sql-server-utility.md)。 如需如何變更個別 SQL Server 執行個體之 CPU 使用量原則的詳細資訊，請參閱[受管理的執行個體詳細資料 &#40;SQL Server 公用程式&#41;](../../database-engine/managed-instance-details-sql-server-utility.md)。 如需如何變更個別資料層應用程式之 CPU 使用量原則的詳細資訊，請參閱[部署的資料層應用程式詳細資料 &#40;SQL Server 公用程式&#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md)。  
  
## <a name="see-also"></a>另請參閱  
 [公用程式管理 &#40;SQL Server 公用程式&#41;](../../database-engine/utility-administration-sql-server-utility.md)   
 [監視 SQL Server 公用程式中的 SQL Server 執行個體](monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [修改資源健康情況原則定義 &#40;SQL Server 公用程式&#41;](modify-a-resource-health-policy-definition-sql-server-utility.md)   
 [SQL Server 公用程式的功能與工作](sql-server-utility-features-and-tasks.md)  
  
  
