---
title: 將多個資料區連結至相同的資料集 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 90c94a91-8fb2-42cb-b998-563691f30d2d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d282636b58352f0ffad1083077bdab9769bd6fdc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707085"
---
# <a name="linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs"></a>將多個資料區連結至相同的資料集 (報表產生器及 SSRS)
  您可以將多個資料區域加入到報表中，以便從相同的報表資料集提供資料的不同檢視。 例如，您可能想要在資料表中顯示資料，也要以視覺方式顯示在圖表中。 若要這樣做，您必須將相同的運算式和範圍用於適當的篩選運算式、排序運算式與群組運算式。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 若要使用圖表和資料表或矩陣顯示相同的資料，了解資料表和形狀圖、矩陣和區域、長條圖和直條圖之間的相似處很有協助。 包含單一資料列群組的資料表可以當做圓形圖輕鬆顯示。 當您加入多個資料列群組時，可以選擇不同類型的圖表，讓巢狀群組的顯示達到最佳的效果。 將巢狀資料列群組加入到圓形圖會增加圓形圖中的配量數目。 您必須決定父群組與子群組結合之群組執行個體的數目是否太多，而無法顯示在單一圓形圖中。 對於在圓形圖上顯示為小配量的多個群組值，您可以設定屬性，讓低於特定臨界值的所有值都顯示為一個圓形圖配量。 如需詳細資訊，請參閱 [收集圓形圖上的小配量 &#40;報表產生器及 SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)。  
  
 包含多個資料列群組的資料表可以顯示為包含多個類別目錄群組的直條圖。 如需詳細資訊，請參閱[在矩陣和圖表上顯示相同的資料 &#40;報表產生器&#41;](display-the-same-data-on-a-matrix-and-a-chart-report-builder.md)。 如需呈現相同報表資料集之不同檢視的資料表和圖表範例，請參閱＜AdventureWorks 報表範例＞中的「Product Line Sales 報表」。 資料表和圖表都會連結到此報表中的相同資料集，因此，當您在排序 Top Employees 資料表中，按一下 Employee Name 的互動式排序按鈕時，Top Employees 圖表也會自動顯示新的排序順序。 如需下載這個範例報表及其他項目的詳細資訊，請參閱 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][報表產生器與報表設計師範例報表](https://go.microsoft.com/fwlink/?LinkId=198283)：  
  
 包含多個資料列和資料行群組的矩陣可以同時搭配類別目錄和數列群組使用區域圖、橫條圖或直條圖，以最佳的方式顯示。 將相同的群組運算式用於矩陣上的資料行群組和圖表上的類別目錄群組，並將相同的群組運算式用於矩陣上的資料列群組和圖表上的數列群組。 您必須記住，群組執行個體的數目會影響圖表的可讀性。 因此，您可以根據範圍值定義群組，藉以減少報表中群組執行個體的數目。 如需詳細資訊，請參閱 [群組運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器和 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [列出 &#40;報表產生器和 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [巢狀資料區 &#40;報表產生器及 SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md)  
  
  
