---
title: " (SQL Server Profiler) 設定全域追蹤選項 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- global trace options [SQL Server]
ms.assetid: 2854608a-c3c7-4eb8-b567-034bfec4b1a9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2f0809ae11776e1bddf42c189b86f48689ff4859
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585725"
---
# <a name="set-global-trace-options-sql-server-profiler"></a>設定全域追蹤選項 (SQL Server Profiler)
  此主題描述如何設定適用於利用特定 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]執行個體而建立之所有追蹤的選項。  
  
### <a name="to-set-global-trace-options"></a>若要設定全域追蹤選項  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]** 。  
  
2.  在 [一般選項]  對話方塊中，按一下 [選擇字型]  修改顯示選項，然後按一下 [確定]  。  
  
3.  (選擇性) 選取 **[進行連接後立即啟動追蹤]** 。  
  
4.  (選擇性) 選取 **[提供者版本變更時，更新追蹤定義 ]** 。 建議使用此選項，且預設為已選取此選項。 選取此選項時，追蹤定義會自動更新成追蹤執行所在伺服器上的目前版本。  
  
5.  (選擇性) 指定伺服器如何管理換用檔案：  
  
    -   選取 **[依序載入所有換用檔案，不另外提示 ]** ，以在重新執行期間自動載入換用檔案。  
  
    -   選取 **[載入換用檔案之前先提示 ]** ，以在重新執行期間控制換用檔案。  
  
    -   選取 **[永不載入後續的換用檔案 ]** ，一次只重新執行一個檔案。  
  
6.  (選擇性) 設定重新執行選項：  
  
    -   [預設重新執行執行緒數目]  控制重新執行期間要使用的處理器執行緒數目。 執行緒數目較多可使重新執行更快速完成，但會導致重新執行期間的伺服器效能降低。 建議設定是 **4**。 下表列出可用選項：  
  
        |值|描述|  
        |-----------|-----------------|  
        |**2**|最小值。 使用兩個執行緒重新執行。|  
        |**4**|預設值。|  
        |**255**|最大值。 設為最大值會影響其他處理緒的效能。|  
  
    -   [預設健全狀況監視器等候間隔 (秒)]  設定重新執行的執行緒可封鎖其他處理序的最長時間量 (以秒為單位)。 下表會說明這些值。  
  
        |值|描述|  
        |-----------|-----------------|  
        |**0**|最小值。 設為 **0** 代表 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 永遠不會停止封鎖處理序。|  
        |**3600**|預設值。 允許封鎖處理序，封鎖時間不超過 **3600** 秒或一小時。|  
        |**86400**|最大值。 允許封鎖處理序，封鎖時間不超過 **86400** 秒或一天。|  
  
    -   [預設健全狀況監視器輪詢間隔 (秒)]  設定輪詢重新執行的執行緒是否有封鎖處理序的頻率。 下表會說明這些值。  
  
        |值|描述|  
        |-----------|-----------------|  
        |**1**|最小值。 設為 **1** 代表 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 會每秒輪詢封鎖處理序一次。|  
        |**60**|預設值。 每分鐘輪詢封鎖處理序一次。|  
        |**86400**|最大值。 每 **86400** 秒或每日輪詢封鎖處理序一次。|  
  
## <a name="see-also"></a>另請參閱  
 [設定追蹤顯示預設值 &#40;SQL Server Profiler&#41;](sql-server-profiler.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
