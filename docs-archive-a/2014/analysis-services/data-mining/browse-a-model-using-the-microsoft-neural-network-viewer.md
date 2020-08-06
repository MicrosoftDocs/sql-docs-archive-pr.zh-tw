---
title: 使用 Microsoft 類神經網路檢視器流覽模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining model content, viewing
- classification mining model [Analysis Services]
- Microsoft Neural Network Viewer
- regression algorithms [Analysis Services]
- Neural Network Viewer [Analysis Services]
- neural network model [Analysis Services]
ms.assetid: 2343d746-c4f4-499b-9d3c-17d63310a9a3
author: minewiskan
ms.author: owend
ms.openlocfilehash: 77e08955d09b7995e34ac94b75f809a303ca0d2b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607184"
---
# <a name="browse-a-model-using-the-microsoft-neural-network-viewer"></a>使用 Microsoft 類神經網路檢視器瀏覽模型
  中的類 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神經網路檢視器 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會顯示以類神經網路演算法建立的採礦模型 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法建立可分析多個輸入和輸出的分類和迴歸採礦模型，對於開放式分析和瀏覽十分有用。 如需有關這個演算法的詳細資訊，請參閱＜ [Microsoft Neural Network Algorithm](microsoft-neural-network-algorithm.md)＞。  
  
 在您使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路檢視器瀏覽模型時，通常會選擇某個目標屬性和狀態，然後使用該檢視器來查看輸入屬性是如何影響結果。  
  
 例如，假設您知道有關某一類別潛在客戶的下列事實：  
  
-   中年人 (40 至 50 歲)。  
  
-   擁有房子。  
  
-   有兩個仍住在家中的孩子。  
  
 如何將這些屬性與客戶將進行購買的可能性相互關聯？  
  
 透過將購買行為做為目標結果來建立類神經網路模型，您可以瀏覽客戶屬性 (例如高收入) 的多個組合，並且發現哪個屬性組合最有可能影響購買行為。 例如，您可能會發現決定因素是上班通勤距離。  
  
 如果您需要更詳細的檢視資訊，例如表示已發現的每個模式的方程式，則可以切換檢視並且使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般內容樹狀檢視器。 如需詳細資訊，請參閱[使用 Microsoft 一般內容樹狀檢視器瀏覽模型](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)或 [Microsoft 一般內容樹狀檢視器 &#40;資料採礦&#41;](../microsoft-generic-content-tree-viewer-data-mining.md)。  
  
##  <a name="viewer-tabs"></a><a name="BKMK_ViewerTabs"></a>檢視器索引標籤  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中瀏覽採礦模型時，該模型會在適合它的檢視器中，顯示於資料採礦設計師的 **[採礦模型檢視器]** 索引標籤上。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路檢視器會提供下列索引標籤，用來瀏覽類神經網路採礦模型：  
  
-   [輸入](#BKMK_Inputs)  
  
-   [輸出](#BKMK_Outputs)  
  
-   [變數](#BKMK_Characteristics)  
  
###  <a name="inputs"></a><a name="BKMK_Inputs"></a>輸入  
 使用 **[輸入]** 索引標籤選擇模型用來做為輸入的屬性和值。 根據預設，當檢視器開啟時包含所有屬性。 在此預設檢視中，模型會選擇哪些是要顯示的最重要的屬性值。  
  
 若要選取輸入屬性，請按一下 [輸入]**** 方格的 [屬性]**** 資料行內，然後從下拉式清單中選取屬性。 (只有模型所包含的屬性才會包含在清單中)。  
  
 第一個相異值出現在 **[值]** 資料行之下。 按一下預設值會顯示一份清單，它包含相關聯屬性的所有可能狀態。 您可以選取要調查的狀態。 您可以選取任何您想要的屬性，數目不限。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="outputs"></a><a name="BKMK_Outputs"></a>產出  
 使用 **[輸出]** 索引標籤選擇要調查的結果屬性。 您可以選擇任何兩個結果狀態來進行比較，並且假設在建立模型時資料行已定義為可預測屬性。  
  
 使用 **OutputAttribute** 清單來選取屬性。 接著，您可以從 **[值 1]** 和 **[值 2]** 清單中，選取與屬性相關聯的兩個狀態。 輸出屬性的這兩個狀態將會在 **[變數]** 窗格中做比較。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="variables"></a><a name="BKMK_Characteristics"></a>變數  
 [變數]**** 索引標籤中的方格包含下列資料行：[屬性]****、[值]****、[喜好 [值 1]]**** 和 [喜好 [值 2]]****。 依預設，資料行是依 [喜好 [值 1]]**** 的程度來排序。 按一下資料行標題會將排序順序變更為選取的資料行。  
  
 屬性右邊的列會顯示指定的輸入屬性狀態所喜好的輸出屬性狀態。 此橫條的大小會顯示輸出狀態喜好輸入狀態的強烈程度。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 類神經網路演算法](microsoft-neural-network-algorithm.md)   
 [採礦模型檢視器工作和操作說明](mining-model-viewer-tasks-and-how-tos.md)   
 [採礦模型檢視器工作和操作說明](mining-model-viewer-tasks-and-how-tos.md)   
 [資料採礦工具](data-mining-tools.md)   
 [資料採礦模型檢視器](data-mining-model-viewers.md)  
  
  
