---
title: 資料流程的分析 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5654cb30-cad2-470c-97b3-59cb331033e5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 184b53d3e982cd80d7c9c0909538a751585ae21d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593530"
---
# <a name="analysis-of-data-flow"></a>資料流程分析
  您可以使用 [ [catalog.execution_data_statistics](../relational-databases/statistics/statistics.md) `SSISDB` 資料庫] 視圖來分析封裝的資料流程。 每當資料流程元件傳送資料至下游元件，此檢視就會顯示一個資料列。 您可以使用這項資訊深入了解傳送至每個元件的資料列。  
  
> [!NOTE]  
>  您必須將記錄層次設定為 [詳細資訊]  ，以透過 catalog.execution_data_statistics 檢視來擷取資訊。  
  
 下列範例顯示在封裝元件之間傳送的資料列數。  
  
```  
use SSISDB  
select package_name, task_name, source_component_name, destination_component_name, rows_sent  
from catalog.execution_data_statistics  
where execution_id = 132  
order by source_component_name, destination_component_name  
  
```  
  
 下列範例計算針對特定執行，每個元件每毫秒所傳送的資料列數目。 計算值包括：  
  
-   **total_rows** - 元件傳送的所有資料列總和  
  
-   **wall_clock_time_ms** - 每個元件經過的執行時間總計 (以毫秒為單位)  
  
-   **num_rows_per_millisecond** - 每個元件每毫秒傳送的資料列數  
  
 `HAVING`子句是用來防止計算中發生零除的錯誤。  
  
```  
use SSISDB  
select source_component_name, destination_component_name,  
    sum(rows_sent) as total_rows,  
    DATEDIFF(ms,min(created_time),max(created_time)) as wall_clock_time_ms,  
    ((0.0+sum(rows_sent)) / (datediff(ms,min(created_time),max(created_time)))) as [num_rows_per_millisecond]  
from [catalog].[execution_data_statistics]  
where execution_id = 132  
group by source_component_name, destination_component_name  
having (datediff(ms,min(created_time),max(created_time))) > 0  
order by source_component_name desc  
  
```  
  
## <a name="related-tasks"></a>相關工作  
 [偵錯資料流程](troubleshooting/debugging-data-flow.md)  
  
 [套件執行的疑難排解工具](troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料流程中的資料](data-flow/data-in-data-flows.md)  
  
  
