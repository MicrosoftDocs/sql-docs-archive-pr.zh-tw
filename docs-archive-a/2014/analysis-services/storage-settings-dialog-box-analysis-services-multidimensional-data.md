---
title: '[儲存設定] 對話方塊 (Analysis Services-多維度資料) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.f1
- sql12.asvs.cubeeditor.cubebuilder.measuregroupstoragesettings.f1
ms.assetid: 80c41c71-226c-45fe-b9cf-af824b592fe1
author: minewiskan
ms.author: owend
ms.openlocfilehash: a2ec48f97e7d0a86f64f53e41f5c5df1c0728fff
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706822"
---
# <a name="storage-settings-dialog-box-analysis-services---multidimensional-data"></a>儲存設定對話方塊 (Analysis Services - 多維度資料)
  使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的 [儲存設定]**** 對話方塊，即可設定維度、Cube、量值群組或資料分割的主動式快取、儲存和通知設定。 您可藉由下列方式在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中顯示 [儲存設定]**** 對話方塊：  
  
-   **...** `ProactiveCaching` 在的 [**屬性**] 視窗中，針對維度、cube、量值群組或資料分割的屬性值，按一下省略號按鈕 (...) [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 。  
  
-   在 Cube 設計師**** 的 [資料分割]**** 索引標籤中展開量值群組，然後按一下 [儲存設定]****。  
  
-   展開量值群組並在 Cube 設計師**** 的 [資料分割]**** 索引標籤中，為該量值群組選取方格中的資料分割，然後按一下 [儲存設定]****。  
  
-   展開量值群組並在 Cube 設計師**** 的 [資料分割]**** 索引標籤中，為該量值群組選取方格中的資料分割，然後在 Cube 設計師**** 的 [資料分割]**** 索引標籤中，按一下 [工具列]**** 窗格中的 [儲存設定]****。  
  
## <a name="options"></a>選項  
  
|詞彙|定義|值|  
|----------|----------------|------------|  
|**標準設定**|選取以啟用 [標準設定滑桿]****，並使用儲存模式與主動式快取功能的預先定義設定。||  
|**標準設定滑桿**|設定為下列預先定義的設定之一：<br /><br /> **即時 ROLAP**<br /><br /> 選取以使用下列儲存與主動式快取設定：|ROLAP 儲存模式<br /><br /> 啟用主動式快取<br /><br /> 卸除過期的快取，延遲期間為 0 秒<br /><br /> 使物件立刻回到線上|  
||**即時 HOLAP**<br /><br /> 選取以使用下列儲存與主動式快取設定：|HOLAP 儲存模式<br /><br /> 啟用主動式快取<br /><br /> 卸除過期的快取，延遲期間為 0 秒<br /><br /> 資料變更時更新快取，無回應間隔為 0 秒，沒有無回應覆寫間隔<br /><br /> 使物件立刻回到線上|  
||**低度延遲 MOLAP**<br /><br /> 選取以使用下列儲存與主動式快取設定：|MOLAP 儲存模式<br /><br /> 啟用主動式快取<br /><br /> 卸除過期的快取，延遲期間為 30 分鐘<br /><br /> 資料變更時更新快取，無回應間隔為 10 秒，無回應覆寫間隔為 10 分鐘<br /><br /> 使物件立刻回到線上|  
||**中度延遲 MOLAP**<br /><br /> 選取以使用下列儲存與主動式快取設定：|MOLAP 儲存模式<br /><br /> 啟用主動式快取<br /><br /> 卸除過期的快取，延遲期間為 4 小時<br /><br /> 資料變更時更新快取，無回應間隔為 10 秒，無回應覆寫間隔為 10 分鐘<br /><br /> 使物件立刻回到線上|  
||**自動 MOLAP**<br /><br /> 選取以使用下列儲存與主動式快取設定：|MOLAP 儲存模式<br /><br /> 啟用主動式快取<br /><br /> 資料變更時更新快取，無回應間隔為 0 秒，沒有無回應覆寫間隔|  
||**已排程 MOLAP**<br /><br /> 選取以使用下列儲存與主動式快取設定：|MOLAP 儲存模式<br /><br /> 啟用主動式快取<br /><br /> 定期更新快取，重建間隔為 1 天|  
||**MOLAP**<br /><br /> 選取以使用下列儲存與主動式快取設定：|MOLAP 儲存模式|  
|**自訂設定**|選取以明確地設定儲存模式、主動式快取和通知選項。||  
|**選項**|按一下以顯示 [儲存選項]**** 對話方塊，以明確地設定儲存模式、主動式快取和通知選項。 如需 [儲存選項]**** 對話方塊的詳細資訊，請參閱[儲存選項對話方塊 &#40;Analysis Services - 多維度資料&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)。||  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 的設計工具和對話方塊 &#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [主動式快取 &#40;分割區&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 [Cube 儲存體 &#40;Analysis Services-多維度資料&#41;](multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)  
  
  
