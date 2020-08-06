---
title: 呼叫預存程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- stored procedures [Analysis Services], calling
- MDX queries [Analysis Services]
- CALL statement
ms.assetid: 96a9660d-875b-4ee4-b339-90020b1d9895
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5c9da6edef576a6ab25c183cbc87ff95cc056845
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87700441"
---
# <a name="calling-stored-procedures"></a>呼叫預存程序
  可以在伺服器上，或從用戶端應用程式呼叫預存程序。 在這兩種情況下，預存程序永遠會在伺服器上執行，不論是伺服器或資料庫的內容。 執行預存程序並不需要特殊的權限。 組件將預存程序加入到伺服器或資料庫內容後，任何使用者都可以執行預存程序，只要使用者的角色允許該預存程序執行的動作。  
  
 在 MDX 中呼叫預存程序，與呼叫內建 MDX 函數的方式相同。 對於未採用參數的預存程序，則會使用程序名稱和空白的成對括號，如此處所示：  
  
```  
MyStoredProcedure()  
```  
  
 如果預存程序有一或多個參數，則依序提供以逗號分隔的參數。 下例展示具有三個參數的預存程序範例：  
  
```  
MyStoredProcedure("Parameter1", 2, 800)  
```  
  
## <a name="calling-stored-procedures-in-mdx-queries"></a>在 MDX 查詢中呼叫預存程序  
 在所有 MDX 查詢中，預存程序必須傳回 MDX 運算式所需的句法正確類型。 如果預存程序沒有傳回正確類型，就會發生 MDX 錯誤。 下列範例展示的預存程序會傳回數學運算的集合、成員和結果。  
  
### <a name="returning-a-set"></a>傳回集合  
 下列範例實作名稱為 MySproc 的預存程序，它會傳回一個集合。 在第一個範例中，MySproc 會在 SELECT 運算式中直接傳回集合。 其次的兩個範例中，MySproc 會將集合以 Crossjoin 和 DrilldownLevel 函數之引數的方式傳回。  
  
```  
SELECT MySetProcedure(a,b,c) ON 0 FROM Sales  
SELECT Crossjoin(MySetProcedure(a,b,c)) ON 0 FROM Sales  
SELECT DrilldownLevel(MySetProcedure(a,b,c)) ON 0 FROM Sales  
```  
  
### <a name="returning-a-member"></a>傳回成員  
 下例顯示名稱為 MySproc 的函數，它會傳回一個成員：  
  
```  
SELECT Descendants(MySproc(a,b,c),3) ON 0 FROM Sales  
```  
  
### <a name="returning-the-result-of-a-math-operation"></a>傳回數學運算的結果  
  
```  
SELECT Country.Members on 0, MySproc(Measures.Sales) ON 1 FROM Sales  
```  
  
## <a name="calling-stored-procedures-with-the-call-statement"></a>使用 CALL 陳述式呼叫預存程序  
 使用 MDX `Call` 陳述式，可以在 MDX 查詢內容的外部呼叫預存程序。  
  
 您可使用這個方法具現化預存程序的副作用，或讓應用程式取得預存查詢的結果。 `Call` 陳述式的常見用法，是使用分析管理物件 (AMO) 來執行不會傳回結果的管理功能。 例如，下列命令會呼叫預存程序：  
  
```  
Call MyStoredProcedure(a,b,c)  
```  
  
 在 `Call` 陳述式中，預存程序傳回的唯一支援類型是資料列集。 資料列集的序列化是由 XML for Analysis 定義的。 如果 `Call` 陳述式中的預存程序傳回任何其他的類型，則會被忽略，而且不會以 XML 的方式傳回給呼叫的應用程式。 如需有關 XML for Analysis 資料列集的詳細資訊，請參閱＜XML for Analysis 結構描述資料列集＞。  
  
 如果預存程序傳回 .NET 資料列集，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會將伺服器上的結果轉換成 XML for Analysis 資料列集。 XML for Analysis 資料列集一律由 `Call` 函數中的預存程序傳回。 如果資料集包含的功能無法在 XML for Analysis 資料列集內表示，結果會失敗。  
  
 傳回空值的程序 (例如，Visual Basic 中的副程式) 也可以和 CALL 關鍵字一起使用。 例如，如果您想要在 MDX 陳述式中使用函數 MyVoidFunction()，應使用以下的語法：  
  
```  
CALL(MyVoidFunction)  
```  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型元件管理](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定義預存程式](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
