---
title: FLOOR (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- largest integer less than or equal to expression
- FLOOR function [SSIS]
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b638c9a7215d120c562e416cdecee463f031ad2a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595205"
---
# <a name="floor-ssis-expression"></a>FLOOR (SSIS 運算式)
  傳回小於或等於數值運算式的最大整數。  
  
## <a name="syntax"></a>語法  
  
```  
  
FLOOR(numeric_expression)  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 有效的數值運算式。  
  
## <a name="result-types"></a>結果類型  
 引數運算式的數值資料類型。 結果是計算值的整數部分，與 *numeric_expression*具有相同的資料類型。  
  
## <a name="remarks"></a>備註  
 如果引數為 Null，則 FLOOR 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 這些範例會將 FLOOR 函數套用至正值、負值和零值。  
  
```  
FLOOR(123.45)  
```  
  
 傳回 123.00  
  
```  
FLOOR(-123.45)  
```  
  
 傳回 -124.00  
  
```  
FLOOR(0.00)  
```  
  
 傳回 0.00  
  
## <a name="see-also"></a>另請參閱  
 [CEILING &#40;SSIS 運算式&#41;](ceiling-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  
