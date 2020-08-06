---
title: 父子式維度中的一元運算子 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- UnaryOperatorColumn property
- attributes [Analysis Services], unary operators
- unary operators
ms.assetid: b8ef549c-5458-458a-bf1a-fd743a1417fd
author: minewiskan
ms.author: owend
ms.openlocfilehash: db07b99fd52ed4a126b7e69864652b9a164ae29b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87698629"
---
# <a name="unary-operators-in-parent-child-dimensions"></a>父子式維度中的一元運算子
  在中包含父子式關聯性的維度中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，您可以指定一元 (或自訂匯總) 運算子資料行，以決定父屬性之所有非匯出成員的自訂匯總。 只要評估父成員的值時，就會將一元運算子套用至成員。 父屬性 ( **Usage** =Parent) 上的**UnaryOperatorColumn**，會在包含一元運算子的資料來源檢視中指定資料表的資料行。 儲存在此資料行之自訂積存運算子的值，會套用到屬性的每個成員。  
  
 您可以在資料來源檢視的維度資料表上，建立和指定具名計算做為一元運算子資料行。 最簡單的運算式 (例如 '+') 會針對所有成員傳回相同的運算子。 但是您可以使用任何運算式，只要它會針對每個成員傳回運算子。  
  
 您可以在父屬性上手動變更 **UnaryOperatorColumn** 屬性設定，或使用 [商業智慧精靈] 的 [定義自訂彙總] 增強功能取代與維度之成員相關聯的預設彙總。 如需如何使用 [商業智慧精靈] 來執行此組態的詳細資訊，請參閱 [將自訂彙總加入維度中](bi-wizard-add-a-custom-aggregation-to-a-dimension.md)。  
  
 父屬性上之 **UnaryOperatorColumn** 屬性的預設值為 (無)，會停用自訂積存運算子。 下表列出一元運算子，並描述其套用到層級時的行為。  
  
|一元運算子|描述|  
|--------------------|-----------------|  
|+ (加號)|成員的值加入到該成員發生前之同層級成員的彙總值中。 如果沒有為屬性定義任何一元運算子資料行，這會是預設運算子。|  
|- (減號) |從成員發生前之同層級成員的彙總值中減掉該成員的值。|  
|* (星號)|成員的值乘以該成員發生前之同層級成員的彙總值。|  
|/ (斜線)|成員的值除以該成員發生前之同層級成員的彙總值。|  
|~ (波狀符號)|忽略成員的值。|  
  
 空白值以及資料表中找不到的其他任何值，都與加號 (+) 一元運算子一樣地處理。 由於並無運算子優先順序，因此儲存在一元運算子資料行的成員順序就決定其評估順序。 若要變更評估順序，請建立新的屬性，將其 [類型]**** 屬性設定為 [順序]****，然後在其 [來源資料行]**** 屬性中指派對應到此評估順序的序號。 您也必須根據該屬性來排序此屬性的成員。 如需如何使用 [商業智慧精靈] 來排序屬性之成員的資訊，請參閱 [定義維度的排序方式](bi-wizard-define-the-ordering-for-a-dimension.md)。  
  
 您可以使用 **UnaryOperatorColumn** 屬性指定具名計算，以傳回一元運算子作為屬性之所有成員的常值字元。 這可能和在具名計算中輸入常值字元 (例如 `'*'` ) 一樣簡單。 這會針對屬性的所有成員，使用乘法運算子 (星號 (*)) 來取代預設運算子 (加號 (+))。 如需詳細資訊，請參閱[在資料來源檢視中定義具名計算 &#40;Analysis Services&#41;](define-named-calculations-in-a-data-source-view-analysis-services.md)。  
  
 在維度設計師的 [瀏覽器]**** 索引標籤中，您可以檢視階層中每個成員旁邊的一元運算子。 當您使用可寫入的維度時，也可以變更一元運算子。 如果維度是不可寫入的，您必須使用工具直接修改資料來源。  
  
## <a name="see-also"></a>另請參閱  
 [維度屬性屬性參考](dimension-attribute-properties-reference.md)   
 [父子式維度中的自訂 Rollup 運算子](parent-child-dimension-attributes-custom-rollup-operators.md)   
 [在維度設計師中啟動商業智慧精靈](database-dimensions-bi-wizard-in-dimension-designer.md)  
  
  
