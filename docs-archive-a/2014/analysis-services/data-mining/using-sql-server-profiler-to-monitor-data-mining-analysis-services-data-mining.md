---
title: 使用 SQL Server Profiler 來監視資料採礦 (Analysis Services-資料採礦) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 655ac93c-5c5c-4565-914b-915327f7d349
author: minewiskan
ms.author: owend
ms.openlocfilehash: eb59d122e07a51c6546eee8affd31cc9eea1028b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584821"
---
# <a name="using-sql-server-profiler-to-monitor-data-mining-analysis-services---data-mining"></a>使用 SQL Server Profiler 監視資料採礦 (Analysis Services - 資料採礦)
  如果您有必要的權限，可以使用 SQL Server Profiler 來監視資料採礦活動，這些活動會當做傳送給 SQL Server Analysis Services 執行個體的要求來發行。 資料採礦活動可包括模型或結構的處理、預測查詢或內容查詢，或是新模型或結構的建立。  
  
 SQL Server Profiler 會使用 `trace` 監視從多個用戶端傳送的要求，包括 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]、SQL Server Management Studio、Web 服務或是適用於 Excel 的資料採礦增益集，只要這些活動全都使用相同的 SQL Server Analysis Services 執行個體即可。 您必須針對您想要監視的每一個 SQL Server Analysis Services 執行個體建立個別的追蹤。 如需追蹤及如何使用 SQL Server Profiler 的一般資訊，請參閱 [使用 SQL Server Profiler 監視 Analysis Services](../instances/use-sql-server-profiler-to-monitor-analysis-services.md)。  
  
 如需擷取事件類型的特定指引，請參閱[建立 Profiler 追蹤以重新執行 &#40;Analysis Services&#41;](../instances/create-profiler-traces-for-replay-analysis-services.md)。  
  
## <a name="using-traces-to-monitor-data-mining"></a>使用追蹤來監視資料採礦  
 當您在追蹤內擷取資訊時，可以指定該資訊是要儲存到檔案中還是 SQL Server 執行個體的資料表中。 不論您用來儲存資料的方法為何，您都可以使用 SQL Server Profiler 來檢視追蹤及根據事件篩選。 下表列出在預設 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 追蹤內對於資料採礦有興趣的一些事件和子類別。  
  
|EventClass|EventSubclass|描述|  
|----------------|-------------------|-----------------|  
|**查詢開始**<br /><br /> **查詢結束**|**0 - MDXQuery**|包含所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 預存程序呼叫的文字。|  
|**查詢開始**<br /><br /> **查詢結束**|**1 - DMXQuery**|包含資料採礦延伸模組 (DMX) 陳述式的文字和結果。|  
|**進度報告開始**<br /><br /> **進度報告結束**|**34 - DataMiningProgress**|提供有關資料採礦演算法之進度的資訊：例如，如果您正在建立群集模型，進度訊息會告訴您正在建立哪一個候選群集。|  
|**查詢開始**<br /><br /> **查詢結束**|EXECUTESQL|包含所執行之 ransact-SQL 查詢的文字。|  
|**查詢開始**<br /><br /> **查詢結束**|**2-SQLQuery**|包含針對系統資料表形式之結構描述資料列集執行之任何查詢的文字。|  
|**探索開始**<br /><br /> **探索結束**|多個|包含 DMX 函數呼叫或 DISCOVER 陳述式 (封裝在 XMLA 內) 的文字。|  
|**錯誤**|(無)|包含由伺服器傳送給用戶端之錯誤的文字。<br /><br /> 前置 **Error (Data Mining):** 或 **Informational (Data Mining):** (為了回應 DMX 要求所特別產生) 的錯誤訊息。 但是，只檢視這些錯誤訊息是不夠的。 其他錯誤 (例如剖析器產生的錯誤) 可能會與資料採礦相關，但是沒有此前置詞。|  
  
 您也可以藉由檢視追蹤記錄內的命令陳述式，查看用戶端傳送給 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器之複雜陳述式的語法，包括系統預存程序的呼叫。 此資訊對於偵錯很有幫助，或者您也可以使用有效的陳述式當做範本來建立新的預測查詢或模型。 如需您可以透過追蹤擷取之預存程序呼叫的一些範例，請參閱 [叢集模型查詢範例](clustering-model-query-examples.md)。  
  
## <a name="see-also"></a>另請參閱  
 [監視 Analysis Services 實例](../instances/monitor-an-analysis-services-instance.md)   
 [使用 SQL Server 擴充事件 &#40;XEvents&#41; 監視 Analysis Services](../instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
  
