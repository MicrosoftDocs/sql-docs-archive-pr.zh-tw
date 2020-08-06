---
title: 使用 Microsoft 關聯規則檢視器流覽模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- mining models [Analysis Services], associations
- mining model content, viewing
- rules [Data Mining]
- Association Rules Viewer [Analysis Services]
- market basket analysis [Analysis Services]
- associations [Analysis Services]
- Microsoft Association Rules Viewer
- dependencies [Analysis Services]
ms.assetid: 538fc01b-8eb1-467a-9b66-3cd57cf7489f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 75bcefde30cb81cc00d8ad971756c68dedf670ed
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606529"
---
# <a name="browse-a-model-using-the-microsoft-association-rules-viewer"></a>使用 Microsoft 關聯規則檢視器瀏覽模型
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]中的關聯規則檢視器 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會顯示以關聯分析演算法建立的採礦模型 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯演算法是用於建立資料採礦模型的關聯演算法，這些模型可用於購物籃分析。 如需有關這個演算法的詳細資訊，請參閱＜ [Microsoft Association Algorithm](microsoft-association-algorithm.md)＞。  
  
 以下是使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯演算法的主要原因：  
  
-   若要尋找描述交易中通常出現在一起之項目的項目集。  
  
-   若要探索依據現有的項目預測交易中其他項目存在與否的規則。  
  
> [!NOTE]  
>  若要檢視有關此模型中所用的方程式及所探索之模式的詳細資訊，請使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般內容樹狀檢視器。 如需詳細資訊，請參閱[使用 Microsoft 一般內容樹狀檢視器瀏覽模型](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)或 [Microsoft 一般內容樹狀檢視器 &#40;資料採礦&#41;](../microsoft-generic-content-tree-viewer-data-mining.md)。  
  
 如需如何建立、瀏覽，以及使用關聯採礦模型的逐步解說，請參閱[第 3 課︰建立購物籃狀況 &#40;中繼資料採礦教學課程&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)。  
  
##  <a name="viewer-tabs"></a><a name="BKMK_ViewerTabs"></a>檢視器索引標籤  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中瀏覽採礦模型時，該模型會在適合它的檢視器中，顯示於資料採礦設計師的 **[採礦模型檢視器]** 索引標籤上。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯規則檢視器包括下列索引標籤：  
  
-   [項目集](#BKMK_Itemsets)  
  
-   [規則](#BKMK_Rules)  
  
-   [相依性網路](#BKMK_Dependency)  
  
 每一個索引標籤會包含 **[顯示完整名稱]** 核取方塊，您可以使用它在規則或項目集內顯示或隱藏從中產生項目集的資料表。  
  
###  <a name="itemsets"></a><a name="BKMK_Itemsets"></a>專案集  
 **[項目集]** 索引標籤會顯示被模型識別為經常湊在一起的項目集清單。 索引標籤會顯示具有下列資料行的方格： **[案例數]**、 **[大小]** 和 **[項目集]**。 如需有關案例數的詳細資訊，請參閱＜ [Microsoft Association Algorithm](microsoft-association-algorithm.md)＞。 **[大小]** 資料行會顯示項目集內的項目數目。 **[項目集]** 資料行會顯示模型探索的實際項目集。 您可以使用 **[顯示]** 清單來控制項目集的格式，您可以將它設定為下列選項：  
  
-   **顯示屬性名稱和值**  
  
-   **只顯示屬性值**  
  
-   **只顯示屬性名稱**  
  
 您可以使用 **[最小案例數]** 和 **[項目集大小下限]**，來篩選索引標籤中所顯示的項目集數目。 您可以使用 **[篩選項目集]** 和輸入必須存在的項目集特性，來進一步限制所顯示的項目集數目。 例如，若您輸入「Water Bottle = existing」，您就可以將項目集限制為僅包含水壺的那些項目集。 **[篩選項目集]** 選項也會顯示您先前已用過的篩選清單。  
  
 您可以按一下資料行標題來排序方格中的資料列。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="rules"></a><a name="BKMK_Rules"></a>條  
 **[規則]** 索引標籤會顯示關聯演算法探索的規則。 **[規則]** 索引標籤有一個方格包含下列資料行： **[機率]**、 **[重要性]** 和 **[規則]**。 機率是描述發生規則之結果的可能性。 重要性是設計來測量規則的效益。 雖然規則發生的機率很高，但規則的效益本身可能不重要。 重要性資料行會描述這方面。 例如，若每一個項目集包含屬性的特定狀態，則預測狀態的規則只是一般規則，即使機率很高也一樣。 重要性愈高，規則就愈重要。  
  
 您可以使用 [**最小**機率] 和 [**最低重要性**] 來篩選規則，類似于您可以在 [**專案集**] 索引標籤上執行的篩選。您也可以使用 [**篩選規則**]，根據其包含的屬性狀態來篩選規則。  
  
 您可以按一下資料行標題來排序方格中的資料列。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="dependency-net"></a><a name="BKMK_Dependency"></a>相依性網路  
 **[相依性網路]** 索引標籤包含相依性網路檢視器。 檢視器中的每一個節點代表一個項目，例如「state = WA」。 節點之間的箭頭代表項目之間的關聯。 根據演算法探索的規則，箭頭的方向會指出項目之間的關聯。 例如，如果檢視器包含三個專案： A、B 和 C，而 C 是由 A 和 B 預測，則如果您選取節點 C，則兩個箭頭會指向節點 C-A 到 C，B 到 C。  
  
 檢視器左邊的滑桿會有篩選的作用，與規則的機率相關。 降低滑桿只顯示最強的連結。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 關聯分析演算法](microsoft-association-algorithm.md)   
 [採礦模型檢視器工作和操作說明](mining-model-viewer-tasks-and-how-tos.md)   
 [採礦模型檢視器工作和操作說明](mining-model-viewer-tasks-and-how-tos.md)   
 [資料採礦工具](data-mining-tools.md)   
 [資料採礦模型檢視器](data-mining-model-viewers.md)  
  
  
