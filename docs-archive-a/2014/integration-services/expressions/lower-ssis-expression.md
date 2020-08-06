---
title: LOWER (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting uppercase to lowercase
- LOWER function
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: 109328e1-5604-40ff-895e-f2e7c13fff41
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 180be8f3cfb5a15eb0fcd6ddd3d63b09fe874af5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595202"
---
# <a name="lower-ssis-expression"></a>LOWER (SSIS 運算式)
  傳回將大寫字元轉換為小寫字元之後的字元運算式。  
  
## <a name="syntax"></a>語法  
  
```  
  
LOWER(character_expression)  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 是轉換成小寫字元的字元運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_WSTR  
  
## <a name="remarks"></a>備註  
 LOWER 只適用於 DT_WSTR 資料類型。 如果 *character_expression* 引數是字串常值或具有 DT_STR 資料類型的資料行，則該引數會在 LOWER 執行其作業前隱含轉換成 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)和[轉換 &#40;SSIS 運算式&#41;](cast-ssis-expression.md)。  
  
 如果引數為 Null，則 LOWER 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會將字串常值轉換成小寫字元。 傳回結果為 "new york"。  
  
```  
LOWER("New York")  
```  
  
 此範例會將 **Color** 輸入資料行中的所有字元轉換成小寫字元，除了第一個字元以外。 如果 Color 是 YELLOW，則傳回結果為 "Yellow"。 如需詳細資訊，請參閱 [SUBSTRING &#40;SSIS 運算式&#41;](substring-ssis-expression.md)。  
  
```  
LOWER(SUBSTRING(Color, 2, 15))  
```  
  
 此範例會將 **CityName** 變數中的值轉換成小寫字元。  
  
```  
LOWER(@CityName)  
```  
  
## <a name="see-also"></a>另請參閱  
 [UPPER &#40;SSIS 運算式&#41;](upper-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  
