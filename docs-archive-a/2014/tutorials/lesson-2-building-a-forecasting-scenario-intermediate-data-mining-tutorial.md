---
title: 第2課：建立預測案例 (中繼資料採礦教學課程) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time series [Analysis Services]
- data mining [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 9a988156-c900-4c22-97fa-f6b0c1aea9e2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c81d5846df0a37c2b4182cb92fea86ce6f3417a7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584919"
---
# <a name="lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial"></a>第 2 課：建立預測案例 (中繼資料採礦教學課程)
  您是 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]的銷售分析師，奉命預測下一年度產品的銷售狀況。 您特別奉命比較不同區域和產品線的預測狀況。 另外，您也受要求判斷不同產品的銷售情況是否會隨著年度時段而有所不同。  
  
 為了找到所要求的資訊，在這個課程中，您將摘要說明公司每月的銷售資料，而且您要依照三個地區摘要這些銷售數字：歐洲、北美和太平洋地區。  
  
 完成這個課程的工作之後，您將能夠回答下列問題：  
  
-   不同自行車型號的銷售情況隨著時間改變的情況如何？  
  
-   這三個區域的銷售模式之間是否有差異？  
  
-   是否能夠預測銷售旺季？  
  
 這一課可以分成兩個部分完成：  
  
-   第一部分介紹如何建立和使用時序模型的基本知識。  
  
-   第二部分將逐步引導您依據所有區域建立一般的時間序列模型。 您可以使用此一般模型進行*交叉預測*。  
  
 若要完成本課程中所列的工作（如下所示），您將使用在 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] [第1課：建立中繼資料採礦方案 &#40;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)中建立的資料來源，&#41;。  
  
> [!WARNING]  
>  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 範例資料庫中的日期已在此版本中更新。 如果您使用舊版 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]，可以在這些步驟後建立模型，但您可能會看到不同的結果。  
  
 **建立簡單的預測模型**  
  
-   [加入資料來源視圖以進行預測 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial.md)  
  
-   [建立預測結構和模型 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [&#40;中繼資料採礦教學課程修改預測結構&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
-   [自訂及處理預測模型 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
-   [&#40;中繼資料採礦教學課程中探索預測模型&#41;](../../2014/tutorials/exploring-the-forecasting-model-intermediate-data-mining-tutorial.md)  
  
-   [&#40;中繼資料採礦教學課程建立時間序列預測&#41;](../../2014/tutorials/creating-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
 **建立一般預測模型以供交叉預測**  
  
-   [&#40;中繼資料採礦教學課程的先進時間序列預測&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
-   [使用更新的資料 &#40;中繼資料採礦教學課程的時間序列預測&#41;](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
-   [使用取代資料 &#40;中繼資料採礦教學課程的時間序列預測&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
-   [比較預測模型 &#40;中繼資料採礦教學課程的預測&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [加入資料來源視圖以進行預測 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial.md)  
  
 [瞭解時間序列模型的需求 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="all-lessons"></a>所有課程  
 [第1課：建立中繼資料採礦解決方案 &#40;元資料採礦教學課程&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 第 2 課：預測案例 (中繼資料採礦教學課程)  
  
 [第 3 課：建立購物籃狀況 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 [第4課：建立時序群集案例 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 [第五課：建立類神經網路和羅吉斯迴歸模型 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [基本資料採礦教學課程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [元資料採礦教學課程 &#40;Analysis Services-資料採礦&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Microsoft 時間序列演算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
