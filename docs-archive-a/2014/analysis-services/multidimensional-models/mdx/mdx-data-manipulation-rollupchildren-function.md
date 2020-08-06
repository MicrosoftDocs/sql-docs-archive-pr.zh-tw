---
title: 使用 RollupChildren 函數 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- queries [MDX], RollupChildren function
- RollupChildren function
- custom member properties [MDX]
- IIf function
ms.assetid: 03c624d4-f277-451d-9995-623a07ea2f86
author: minewiskan
ms.author: owend
ms.openlocfilehash: 341468d521cebe1fda33d73ea999f3b6571cb01e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705601"
---
# <a name="working-with-the-rollupchildren-function-mdx"></a>使用 RollupChildren 函數 (MDX)
  多維度運算式 (MDX) [RollupChildren](/sql/mdx/rollupchildren-mdx) [Script for Search 和 Replace] 函式會匯總成員的子系，並將不同的一元運算子套用至每個子系，並傳回此 rollup 的值做為數位。 一元運算子可由與子成員相關的成員屬性提供，或者可能是字串運算式直接將運算子提供給函數。  
  
## <a name="rollupchildren-function-examples"></a>RollupChildren 函數範例  
 要說明使用多維度運算式 (MDX) 陳述式的 `RollupChildren` 函數是很簡單，但此函數對 MDX 查詢的影響相當廣泛。  
  
 `RollupChildren` 函數會對為了對現有的 Cube 資料，執行選擇性分析而設計 MDX 查詢的產生影響。 例如，下表包含 Net Sales 父成員的子成員清單，以及在括號中顯示它們的一元運算子 (以 `UNARY_OPERATOR` 成員屬性代表)。  
  
|父成員|子成員|  
|-------------------|------------------|  
|Net Sales|Domestic Sales (+)<br /><br /> Domestic Returns (-)<br /><br /> Foreign Sales (+)<br /><br /> Foreign Returns (-)|  
  
 Net Sales 父成員目前是淨銷售量的總和減去國內外總銷售量值，而國內外退貨量則當做積存減去。  
  
 但是，您想要外加 10% 以簡單、快速地預測國內外銷售總額，而不理會國內外的退貨量。 若要計算此值，您能以下其中一個方式使用 `RollupChildren` 函數：利用自訂成員屬性，或利用`IIf` 函數。  
  
### <a name="using-a-custom-member-property"></a>使用自訂成員屬性  
 如果將會經常執行積存計算作業，其中一個方法是建立一個成員屬性，儲存供每個子系當做特定函數使用的運算子。 下表顯示有效的一元運算子，而且描述了預期的結果。  
  
|運算子|結果|  
|--------------|------------|  
|+|總計 = 總計 + 目前的子系|  
|-|總計 = 總計 - 目前的子系|  
|*|總計 =總計 * 目前的子系|  
|/|總計 =總計 / 目前的子系|  
|~|子系不會被用在積存中。 子系的值會被忽略。|  
  
 例如，您可以建立一個稱為 `SALES_OPERATOR` 的成員屬性，將以下的一元運算子指派給此成員屬性，如下表所示。  
  
|父成員|子成員|  
|-------------------|------------------|  
|Net Sales|Domestic Sales (+)<br /><br /> Domestic Returns (~)<br /><br /> Foreign Sales (+)<br /><br /> Foreign Returns (~)|  
  
 有了這個新的成員屬性，以下 MDX 陳述式就可以快速且有效地執行銷售總額估計作業 (忽略國內外退貨量)：  
  
```  
RollupChildren([Net Sales], [Net Sales].CurrentMember.Properties("SALES_OPERATOR")) * 1.1  
```  
  
 當呼叫此函數時，就會使用成員屬性中儲存的運算子，將每個子系的值套用到總計。 國內外退貨量會被忽略，而且 `RollupChildren` 函數所傳回的積存總計會乘以 1.1。  
  
### <a name="using-the-iif-function"></a>使用 IIf 函數  
 如果範例作業不是常見的，或作業只套用至一個 MDX 查詢，則[IIf](/sql/mdx/iif-mdx)函式可與函數搭配使用， `RollupChildren` 以提供相同的結果。 以下的 MDX 查詢可以提供跟先前 MDX 範例一樣的結果，但不需要使用自訂的成員屬性就可以做到。  
  
```  
RollupChildren([Net Sales], IIf([Net Sales].CurrentMember.Properties("UNARY_OPERATOR") = "-", "~", [Net Sales].CurrentMember.Properties("UNARY_OPERATOR))) * 1.1  
```  
  
 MDX 陳述式會檢查子成員的一元運算子。 如果一元運算子用於減法 (如同在處理國內外退貨量成員的情況下)，則 `IIf` 函數會取代波狀符號 (~) 一元運算子。 否則，`IIf` 函數會使用子成員的一元運算子。 最後，傳回的積存總計會乘以 1.1，做為國內外銷售總額的預測值。  
  
## <a name="see-also"></a>另請參閱  
 [操作資料 &#40;MDX&#41;](mdx-data-manipulation-manipulating-data.md)  
  
  
