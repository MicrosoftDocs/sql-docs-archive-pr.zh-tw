---
title: 定義 Cube |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8aa4ac2d-857f-4048-baa0-0f314e207cf6
author: minewiskan
ms.author: owend
ms.openlocfilehash: 354a05840dd2e091f956454858edd5c75c8c4bdd
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584776"
---
# <a name="defining-a-cube"></a>定義 Cube
  「Cube 精靈」可協助您定義 Cube 的量值群組和維度。 在下列工作中，您將使用「Cube 精靈」來建立 Cube。  
  
### <a name="to-define-a-cube-and-its-properties"></a>若要定義 Cube 及其屬性  
  
1.  在方案總管中，以滑鼠右鍵按一下 [Cube]****，然後按一下 [新增 Cube]****。 [Cube 精靈] 隨即出現。  
  
2.  在 [歡迎使用 Cube 精靈]**** 頁面上，按一下 [下一步]****。  
  
3.  在 [選取建立方法]**** 頁面上，確認已選取 [使用現有的資料表]**** 選項，然後按一下 [下一步]****。  
  
4.  在 [選取量值群組資料表]**** 頁面上，確認已選取 [Adventure Works DW 2012]**** 資料來源檢視。  
  
5.  按一下 [建議]****，讓 Cube 精靈建議用來建立量值群組的資料表。  
  
     此精靈會檢查這些資料表並建議使用 [InternetSales]**** 當作量值群組資料表。 量值群組資料表 (也稱為事實資料表) 包含您感興趣的量值，例如銷售的單位數。  
  
6.  按 [下一步] 。  
  
7.  在 [選取量值]**** 頁面上，檢閱 [網際網路銷售]**** 量值群組中的所選取量值，再清除下列量值的核取方塊：  
  
    -   **升級索引鍵**  
  
    -   **貨幣索引鍵**  
  
    -   **銷售領域索引鍵**  
  
    -   **修訂號碼**  
  
     根據預設，此精靈會選取事實資料表中所有未連結到維度的數值資料行當做量值。 不過，這 4 個資料行不是實際量值。 前 3 個是連結事實資料表與維度資料表的索引鍵值，它們不使用於這個 Cube 的初始版本。  
  
8.  按 [下一步] 。  
  
9. 在 [選取現有維度]**** 頁面上，確定已選取您先前建立的 [Date]**** 維度，然後按一下 [下一步]****。  
  
10. 在 [選取新維度]**** 頁面上，選取要建立的新維度。 若要執行這項操作，請確認已選取 [Customer]****、[Geography]**** 和 [Product]**** 核取方塊，然後清除 [InternetSales]**** 核取方塊。  
  
11. 按 [下一步] 。  
  
12. 在 [**正在完成嚮導]** 頁面上，將 cube 的名稱變更為 `Analysis Services Tutorial` 。 在 [預覽] 窗格中，您可以看見 [InternetSales]**** 量值群組及其量值。 此外，您也可以看見 [Date]****、[Customer]**** 和 [Product]**** 維度。  
  
13. 按一下 [完成]**** 以完成程序。  
  
     在方案總管的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程專案中，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 會出現在 [Cube]**** 資料夾內，而 [Customer] 和 [Product] 資料庫維度則出現在 [維度]**** 資料夾內。 另外，在開發環境中心，[Cube 結構] 索引標籤會顯示 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube。  
  
14. 在 [Cube 結構] 索引標籤的工具列上，將 [顯示比例]**** 層級變更為 50%，這樣就可以更容易看到 Cube 中的維度資料表和事實資料表。 請注意，事實資料表是黃色，維度資料表是藍色。  
  
15. 在 [檔案] 功能表上，按一下 [全部儲存]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [將屬性加入至維度](lesson-2-3-adding-attributes-to-dimensions.md)  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的 cube](multidimensional-models/cubes-in-multidimensional-models.md)   
 [多維度模型中的維度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
