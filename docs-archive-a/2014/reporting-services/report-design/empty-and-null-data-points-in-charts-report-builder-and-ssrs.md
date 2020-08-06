---
title: 圖表中的空白和 Null 資料點 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: faddd29d-4cc1-4c2c-8e29-d3d9918fe22a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3f0826a202969b432e53b3c57ddfe80680ba99e7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686825"
---
# <a name="empty-and-null-data-points-in-charts-report-builder-and-ssrs"></a>圖表中的空白和 Null 資料點 (報表產生器及 SSRS)
  如果您要在圖表中顯示包含空白或 Null 值的欄位，圖表外觀可能不如您預期。 圖表會根據指定的圖表類型，以不同的方式處理空白值：  
  
-   如果圖表類型是線性圖表類型 (橫條圖、直條圖、散佈圖、折線圖、區域圖、範圍圖)，則空白值會在圖表中顯示為空格或「間距」。 如果想要指出空點，必須加入空點預留位置。 如需詳細資訊，請參閱[將空點加入圖表 &#40;報表產生器和 SSRS&#41;](add-empty-points-to-a-chart-report-builder-and-ssrs.md)。  
  
-   如果圖表類型是連續的線性圖表類型 (區域圖、橫條圖、直條圖、折線圖、散佈圖)，則空白的資料點會加入到圖表以維持數列的連續性。  
  
-   如果圖表類型是非線性圖表類型 (極座標圖、圓形圖、環圈圖、漏斗圖或金字塔圖)，則圖表會省略空白值的顯示。  
  
-   形狀圖圖表類型中會省略 Null 值。  
  
 具有空資料點的圖表範例可從範例報表取得。 如需下載這個範例報表及其他項目的詳細資訊，請參閱 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][報表產生器與報表設計師範例報表](https://go.microsoft.com/fwlink/?LinkId=198283)：  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="removing-empty-or-null-values"></a>移除空白或 Null 值  
 若要避免重要資料不易辨認，請考慮從資料集移除空白值。 若要篩選 Null 值，可以在查詢中使用 NOT IS NULL 子句。 或者也可以加入篩選運算式，指定您只要顯示不等於零的值。 如需詳細資訊，請參閱 [加入資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)。  
  
## <a name="fields-with-no-values-in-a-chart"></a>圖表中沒有值的欄位  
 如果在傳回的資料集中欄位未包含任何值，則圖表會顯示沒有資料點的空白圖表，但會加入數列名稱 (通常為欄位名稱) 做為圖例項目。  
  
 這項行為與傳回資料集中有零個資料列的情況不同，後者可能會發生在當報表已進行參數化，而選取的值傳回空白結果集時。 如果資料集查詢傳回零個資料列，則系統會在執行階段會顯示訊息，指出沒有可以顯示的資料。 您可以在 [屬性]  窗格中修改報表的 NoDataMessage 標題，以自訂這個訊息。 如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器和 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [將圖表格式化 &#40;報表產生器和 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [將圖表新增至報表 &#40;報表產生器和 SSRS&#41;](add-a-chart-to-a-report-report-builder-and-ssrs.md)   
 [疑難排解圖表 &#40;報表產生器及 SSRS&#41;](troubleshoot-charts-report-builder-and-ssrs.md)  
  
  
