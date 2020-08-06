---
title: 變更採礦模型中資料行的離散化 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- discretization [Analysis Services]
- mining structures [Analysis Services], how-to topics
- discretized columns [data mining]
- bucketing problems [Analysis Services]
ms.assetid: 3c49862b-595d-4fa4-b890-e2e1bde1d74f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 25b20d6428afac5c1492fdc74aafd4d0c010159d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599277"
---
# <a name="change-the-discretization-of-a-column-in-a-mining-model"></a>變更採礦模型中的資料行離散化
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]自動離散化值-也就是說，它會在某些情況下，將資料在數值資料行中。 例如，如果您的資料包含連續數值資料，而且您要建立決策樹模型，則連續資料的每一個資料行都將會自動分類收納 (視資料的分佈而定)。 如果您想要控制資料離散化的方式，您必須在採礦結構資料行上，變更可控制資料在模型內之使用方式的屬性。  
  
 如需如何在採礦模型中設定屬性的一般資訊，請參閱 [採礦模型資料行](mining-model-columns.md)。  
  
### <a name="to-display-the-properties-for-a-mining-model-column"></a>顯示採礦模型資料行的屬性  
  
1.  在資料採礦設計師的 [採礦模型]**** 索引標籤上，以滑鼠右鍵按一下包含採礦模型名稱的資料行標頭，或是方格中包含採礦演算法名稱的資料列，然後選取 [屬性]****。  
  
     **[屬性]** 視窗會顯示在整體上與採礦模型相關聯的屬性。  
  
2.  在靠近螢幕左邊的 **[結構]** 資料行中，按一下包含您想要離散化之連續數值資料的資料行。  
  
     **[屬性]** 視窗會變更，以便只顯示與該資料行有關聯的屬性。  
  
### <a name="to-change-the-discretization-method"></a>變更離散化方法  
  
1.  在 [**挖掘屬性**] 視窗中，按一下 [**內容**] 旁邊的文字方塊，然後 `Discretized` 從下拉式清單中選取。  
  
     <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 和 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 屬性現在就會啟用。  
  
2.  在 [**屬性**] 視窗中，按一下旁邊的文字方塊， <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 然後選取下列其中一個值： `Automatic` 、 `EqualAreas` 或 `Cluster` 。  
  
    > [!NOTE]  
    >  如果 [資料行使用方式] 設定為，則資料 `Ignore` 行的 [**屬性**] 視窗是空白的。  
  
     您在設計師中選取其他元素時，新值就會生效。  
  
3.  在 [**屬性**] 視窗中，按一下旁邊的文字方塊 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> ，然後輸入數值。  
  
    > [!NOTE]  
    >  如果您變更這些屬性，就必須重新處理此結構，連同您想要使用新設定的任何模型。  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型工作和使用說明](mining-model-tasks-and-how-tos.md)  
  
  
