---
title: 篩選運算子 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 27914c8b-8951-4b7d-914d-1cbf528dd248
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: decd9f7ecac15f897eeada6b8943bdd194aca30c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699928"
---
# <a name="filter-operators-master-data-services"></a>篩選運算子 (Master Data Services)
  篩選成員清單時，可以使用下列運算子。  
  
> [!NOTE]  
>  當您依據多個準則進行篩選時，所有準則都必須為 True，才能傳回結果。 例如，SquareFeet = 2000 **AND** Division <> 123。  
  
## <a name="filter-operators"></a>篩選運算子  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**等於**|傳回與指定準則完全相同的屬性值。 例如，若要以 **Mountain-100**篩選，必須輸入 **Mountain-100**。|  
|**不等於**|傳回與指定準則不是完全相同的屬性值。 篩選準則必須與您要排除於結果之外的屬性值完全相同。 例如，若要排除與 **Mountain-100**相符的結果，必須輸入 **Mountain-100**。<br /><br /> 注意：當您針對某個屬性套用具有 "Is not equal" 子句的篩選條件時，其屬性為 NULL 的成員將會通過篩選條件，並在資料庫設定中 SET ANSI_NULLS 設為 ON 時傳回。 若要停止此行為，請在資料庫設定中，將 SET ANSI_NULLS 變成 OFF。 當 SET ANSI_NULLS 設定為 OFF 時，如果資料值為 NULL，則所有資料針對 Null 值所做的比較都會評估為 TRUE，且結果是成員不會通過 "Is not equal" 子句。 如需詳細資訊，請參閱 [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql)。|  
|**類似**|使用 Transact-SQL 的 LIKE 運算子來篩選結果。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [LIKE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/like-transact-sql)。|  
|**不類似**|使用 Transact-SQL 的 NOT 運算子來篩選結果。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [NOT &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/not-transact-sql)。|  
|**大於**|傳回大於指定準則的屬性值。 例如，若要傳回以大於 **F**之字母開頭的屬性值，請輸入 **F**。|  
|**小於**|傳回小於指定準則的屬性值。 例如，若要傳回以小於 **F**之字母開頭的屬性值，請輸入 **F**。|  
|**大於或等於**|傳回大於或等於指定準則的屬性值。 例如，若要傳回以數字 **3** 或大於 3 開頭的屬性值，請輸入 **3**。|  
|**小於或等於**|傳回小於或等於指定準則的屬性值。 例如，若要傳回以數字 **3** 或小於 **3**開頭的屬性值，請輸入 3。|  
|**相符項**|使用模糊查閱索引來篩選結果。<br /><br /> 使用 [相似度層級]**** 欄位來指定屬性值必須符合所指定之篩選準則的程度 (預設為 30%)。 在 [演算法]**** 清單方塊中選取下列其中一項：<br /><br /> **Levenshtein**：以編輯 (例如新增或刪除) 次數為基礎的距離，這是某個字串要比對另一個字串所需的距離。 這是預設值。 不需要任何額外的參數。<br /><br /> **Jaccard**：嘗試比對多個字串時最適合的指標。 此搜尋支援其他內含項目偏差的參數 (請參閱下面)。<br /><br /> **Jaro-Winkler**：最適用於尋找重複人名的距離。 此方法比其他任何方法傳回的結果還多。 不支援內含項目偏差。<br /><br /> **最長的常見子序列**：可根據子序列（模式中的字母順序顯示）來運作，雖然它們可以分開 (例如，"MSR" 是 "MaSteR" ) 的子序列。 此搜尋支援其他內含項目偏差的參數 (請參閱下面)。<br /><br /> <br /><br /> 針對 [Jaccard]**** 或 [最長的通用子序列]**** 演算法，新增 [內含項目偏差]****。 [內含項目偏差]**** 是以介於 0 和 1 之間的小數位數百分比提供的長度臨界值，預設值為 .62。 臨界值較低時，會增加傳回的可能符合項目數目。|  
|**不符合**|使用模糊查閱索引來篩選結果。 使用 [相似度層級]**** 欄位來指定屬性值不可符合所指定篩選準則的程度。|  
|**包含模式**|使用 .NET Framework 規則運算式，以指定模式篩選結果。 如需正則運算式的詳細資訊，請參閱 MSDN Library 中的[正則運算式語言元素](https://go.microsoft.com/fwlink/?LinkId=164401)。|  
|**不包含模式**|使用 .NET Framework 規則運算式，篩選與指定之模式不相符的結果。 如需正則運算式的詳細資訊，請參閱 MSDN Library 中的[正則運算式語言元素](https://go.microsoft.com/fwlink/?LinkId=164401)。|  
|**為 Null**|傳回是 Null 的屬性值。 當您選取 [是 NULL]**** 運算子時，會停用 [準則]**** 欄位。|  
|**不是 Null**|傳回不是 Null 的屬性值。 當您選取 [不是 NULL]**** 運算子時，會停用 [準則]**** 欄位。|  
  
  
