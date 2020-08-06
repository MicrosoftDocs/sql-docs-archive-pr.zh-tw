---
title: 篩選方程式範例 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- filtering data [Reporting Services], filter equation examples
ms.assetid: 66bec93d-7c3b-4d4a-8cb6-7a7bb2f34ec6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9b4d7c7c561c9185c141190e26f37bc29fe52eb6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594393"
---
# <a name="filter-equation-examples-report-builder-and-ssrs"></a>篩選方程式範例 (報表產生器及 SSRS)
  若要建立篩選，您必須指定一個或多個篩選方程式。 篩選方程式包含運算式、資料類型、運算子和值。 本主題提供常用的篩選範例。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="filter-examples"></a>篩選範例  
 下表說明使用不同資料類型和不同運算子的篩選方程式範例。 比較的範圍是由定義篩選的報表項目所決定。 例如，如果是資料集上所定義的篩選， **TOP % 10** 就是資料集中前百分之 10 的值；如果是群組上所定義的篩選， **TOP % 10** 就是群組中前百分之 10 的值。  
  
|簡單運算式|資料類型|運算子|值|描述|  
|-----------------------|---------------|--------------|-----------|-----------------|  
|`[SUM(Quantity)]`|`Integer`|`>`|`7`|包含大於 7 的資料值。|  
|`[SUM(Quantity)]`|`Integer`|`TOP N`|`10`|包含前 10 大資料值。|  
|`[SUM(Quantity)]`|`Integer`|`TOP %`|`20`|包含前百分之 20 的資料值。|  
|`[Sales]`|`Text`|`>`|`=CDec(100)`|包含所有大於 $100 之 System.Decimal 類型 (SQL "money" 資料類型) 的值。|  
|`[OrderDate]`|`DateTime`|`>`|`2008-01-01`|包含從 2008 年 1 月 1 日到目前的所有日期。|  
|`[OrderDate]`|`DateTime`|`BETWEEN`|`2008-01-01`<br /><br /> `2008-02-01`|包含從 2008 年 1 月 1 日 (含) 算起的日期。|  
|`[Territory]`|`Text`|`LIKE`|`*east`|所有以 "east" 結尾的領域名稱。|  
|`[Territory]`|`Text`|`LIKE`|`%o%th*`|所有在名稱開頭包含 North 和 South 的領域名稱。|  
|`=LEFT(Fields!Subcat.Value,1)`|`Text`|`IN`|`B, C, T`|所有以字母 B、C 或 T 為開頭的子類別目錄值。|  
  
## <a name="see-also"></a>另請參閱  
 [報表參數 &#40;報表產生器和報表設計師&#41;](report-parameters-report-builder-and-report-designer.md)   
 [新增資料集篩選、資料區域篩選和群組篩選 &#40;報表產生器和 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [運算式中的資料類型 &#40;報表產生器和 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [運算式用於報表 &#40;報表產生器和 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  
