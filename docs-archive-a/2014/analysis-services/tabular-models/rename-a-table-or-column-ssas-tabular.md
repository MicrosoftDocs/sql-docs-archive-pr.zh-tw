---
title: " (SSAS 表格式) 重新命名資料表或資料行 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.renametableorcolumn.f1
ms.assetid: 88061a39-c5aa-403d-a52b-7fdb365fc235
author: minewiskan
ms.author: owend
ms.openlocfilehash: d3a2e9a9f41434e64f9ec5ea2180861b459e8f97
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706801"
---
# <a name="rename-a-table-or-column-ssas-tabular"></a>重新命名資料表或資料行 (SSAS 表格式)
  您可以在匯入程序期間，於 **[資料表匯入精靈]** 的 **[選取資料表和檢視表]** 頁面中輸入 **[易記名稱]** 來變更資料表的名稱。 如果在 **[資料表匯入精靈]** 的 **[指定 SQL 查詢]** 頁面上指定查詢來匯入資料，也可以變更資料表和資料行名稱。  
  
 在您將資料加入至模型之後，資料表的名稱 (或標題) 會出現在模型設計師底部的資料表索引標籤上。 您可以變更資料表的名稱，為它提供一個更適合的名稱。 您也可以在將資料加入到模型之後重新命名資料行。 如果您是從多個來源匯入資料，並想要確保不同資料表中的資料行具有容易區分的名稱時，這個選項特別重要。  
  
### <a name="to-rename-a-table"></a>重新命名資料表  
  
1.  在模型設計師中，以滑鼠右鍵按一下包含您要重新命名之資料表的索引標籤，然後按一下 **[重新命名]**。  
  
2.  輸入新的名稱。  
  
    > [!NOTE]  
    >  您可以使用 **[編輯資料表屬性]** 對話方塊，編輯資料表的其他屬性，包括連接資訊和資料行對應。 不過，您無法在此對話方塊中變更名稱。  
  
### <a name="to-rename-a-column"></a>重新命名資料行  
  
1.  在模型設計師中，按兩下您要重新命名之資料行的標頭，或以滑鼠右鍵按一下標頭，然後從內容功能表中選取 **[重新命名資料行]** 。  
  
2.  輸入新的名稱。  
  
## <a name="naming-requirements-for-columns-and-tables"></a>資料行和資料表的命名需求  
 下列文字和字元無法用於資料表或資料行的名稱：  
  
-   開頭或尾端空白  
  
-   控制字元  
  
-   下列字元 (在 Analysis Services 物件的名稱中無效) ：.、; '：/ \\*|?&% $！ + = ( # A3 [] {}<>  
  
-   Analysis Services 保留關鍵字，包括多維度運算式 (MDX) 和資料採礦延伸模組 (DMX) 的函數名稱與運算子。  
  
## <a name="effect-of-renaming-on-existing-tables-columns-and-calculations"></a>重新命名對於現有的資料表、資料行和計算的影響  
 每當您變更資料表的名稱時，您都會變更基礎資料表物件的名稱，其中可能包含多個資料行或量值。 因此，資料表中的任何資料行以及使用資料表的任何關聯性都必須更新，才能使用其定義中的新名稱。 在某些情況下，這個更新作業將會自動發生。 量值並不會自動更新。  
  
 此外，如果計算使用重新命名之資料表或是使用重新命名之資料表中的資料行，則也必須更新這些計算，而且從這些計算衍生的資料也必須重新整理及重新計算。 根據受到影響之資料表和計算的數目而定，完成這個程序可能需要一點時間。 因此，重新命名資料表的最佳時機是匯入期間，或是在您開始建立複雜關聯性和計算之前。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SSAS 表格式&#41;的資料表和資料行](tables-and-columns-ssas-tabular.md)   
 [從 PowerPivot 匯入 &#40;SSAS 表格式&#41;](import-from-power-pivot-ssas-tabular.md)   
 [從 Analysis Services 匯入 &#40;SSAS 表格式&#41;](import-from-analysis-services-ssas-tabular.md)  
  
  
