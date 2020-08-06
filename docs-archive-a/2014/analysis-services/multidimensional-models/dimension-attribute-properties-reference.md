---
title: 維度屬性屬性參考 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- properties [Analysis Services], attributes
- attributes [Analysis Services], properties
ms.assetid: 7f83d1cb-4732-424f-adc5-2449c1dd1008
author: minewiskan
ms.author: owend
ms.openlocfilehash: e6f76788ae06f9ac9ab5f0b8e5cd106951e9360e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708761"
---
# <a name="dimension-attribute-properties-reference"></a>維度屬性 (attribute) 屬性 (property) 參考
  在中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，有許多屬性可決定維度和維度屬性的運作方式。 下表列出與描述每一項屬性 (Attribute) 的屬性 (Property)。  
  
|屬性|描述|  
|--------------|-----------------|  
|`AttributeHierarchyDisplayFolder`|識別向使用者顯示相關聯屬性階層的資料夾。|  
|`AttributeHierarchyEnabled`|決定是否由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 產生屬性的屬性階層。 如果屬性階層未啟用，則不能在使用者自訂階層中使用該屬性，也不能在多維度運算式 (MDX) 陳述式中參考此屬性階層。|  
|`AttributeHierarchyOptimizedState`|決定套用至屬性階層的最佳化層級。 依預設，屬性階層會 `FullyOptimized`，這表示 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會建立屬性階層的索引，以提升查詢效能。 另一個選項 `NotOptimized` 表示未針對屬性階層建立任何索引。 當屬性階層用於查詢以外的其他目的時，使用 `NotOptimized` 會很有用處，因為此屬性不會建立其他的索引。 屬性階層的其他用途有助於排序另一個屬性。|  
|`AttributeHierarchyOrdered`|決定是否排序相關聯的屬性階層。 預設值是 `True`。 但是，如果屬性階層不會用於查詢，您可將此屬性的值變更為 `False`，以節省處理時間。|  
|`AttributeHierarchyVisible`|決定用戶端應用程式是否可看到屬性階層。 預設值是 `True`。 但是，如果屬性階層不會用於查詢，您可將此屬性的值變更為 `False`，以節省處理時間。|  
|`CustomRollupColumn`|指定用來定義自訂積存公式的資料行。|  
|`CustomRollupPropertiesColumn`|指定包含自訂積存公式之屬性的資料行。|  
|`DefaultMember`|指定定義屬性之預設量值的多維度運算式 (MDX) 運算式。|  
|`Description`|包含屬性的描述。|  
|`DiscretizationBucketCount`|包含要進行離散化的值區數目。|  
|`DiscretizationMethod`|定義用於分隔的方法。|  
|`EstimatedCount`|指定屬性中的估計成員數目。 在您執行彙總設計精靈之前，預設值為零。 您可以讓精靈來計算記錄的數目，或輸入估計的值。 如果您知道成員的數目，且想要節省查詢資料庫以找出該計數所需的時間，請手動輸入值。 如果使用的是實際資料的測試子集，則可使用實際資料的計數，這樣會針對實際資料 (而非測試資料) 最佳化彙總設計。|  
|`GroupingBehavior`|使用者定義的值，可對用戶端應用程式提供有關如何群組屬性的提示。|  
|`ID`|包含維度的唯一識別碼 (ID)。|  
|`InstanceSelection`|提供用戶端應用程式提示，以根據清單中的預期項目數目來如何顯示項目清單。 可用的選項如下：<br /><br /> **None** ：不會對用戶端應用程式提供任何提示。 這是預設值。<br /><br /> **DropDown** ：項目數目夠小，可顯示在下拉式清單中。<br /><br /> **List** ：項目數目對於下拉式 **清單**而言太大，但不需要篩選。<br /><br /> **FilteredList** ：項目數目夠大，因此使用者必須篩選要顯示的項目。<br /><br /> **MandatoryFilter** ：項目數目非常大，一律必須篩選才能顯示。|  
|`IsAggregatable`|指定是否可彙總屬性成員的值。 預設值是 `True`，表示屬性階層包含 (全部) 層級。 如果此屬性的值為 `False`，則屬性階層不會包含 (全部) 層級。|  
|`KeyColumns`|包含表示屬性之索引鍵的一或多個資料行，這是繫結屬性之資料來源檢視的基礎關聯式資料表中的資料行。 除非已指定 `NameColumn` 屬性的值，否則會向使用者顯示每個成員之這個資料行的值。|  
|`MemberNamesUnique`|決定屬性階層中的成員名稱是否必須是唯一的。|  
|`MembersWithData`|供父屬性用來決定是否要在父屬性中顯示非分葉成員的資料成員。 只有當 `Usage` 屬性值設定為 Parent 時，才會使用這個屬性值。 這表示已經定義了父子式階層。 可用的選項如下：<br /><br /> **NonLeafDataHidden** ：會隱藏非分葉資料。<br /><br /> **NonLeafDataVisible** ：可以看見非分葉資料。|  
|`MembersWithDataCaption`|提供父屬性使用的範本字串，以在父屬性中建立系統產生之資料成員的標題。 只有當 `Usage` 屬性值設定為 Parent 時，才會使用這個屬性值。 這表示已經定義了父子式階層。|  
|`Name`|包含屬性的使用者易記名稱。|  
|`NameColumn`|識別可提供向使用者顯示之屬性名稱的資料行，而非屬性之索引鍵資料行中的值。 當屬性成員的索引鍵資料行值已加密 (亦即使用者無法理解)，或當索引鍵資料行是以複合索引鍵為基礎時，就會使用此資料行。 `NameColumn` 屬性不會用於父子式階層中。不過，子成員的 `NameColumn` 屬性會當做父子式階層中的成員名稱使用。|  
|`NamingTemplate`|定義在由父屬性建構的父子式階層中如何命名層級。 只有當 `Usage` 屬性值設定為 Parent 時，才會使用這個屬性值。 這表示已經定義了父子式階層。|  
|`OrderBy`|描述如何排序屬性階層中包含的成員。 預設值為 Name，這會指定屬性成員的排序是根據 `NameColumn` 屬性的值 (如果有的話)。 否則，這項作業會依據索引鍵資料行的值來排序成員。 可用的選項如下：<br /><br /> `NameColumn`依屬性的值排序 `NameColumn` 。<br /><br /> **Key** ：依據屬性成員之索引鍵資料行的值來進行排序。<br /><br /> **AttributeKey** ：依據所指定屬性之成員索引鍵的值來進行排序，這與該屬性必須有屬性關聯性。<br /><br /> **AttributeName** ：依據所指定屬性之成員名稱的值來進行排序，這與該屬性必須有屬性關聯性。|  
|`OrderByAttribute`|識別排序屬性階層之成員時，所要依據的屬性。|  
|`RootMemberIf`|決定如何識別父子式階層的根成員或最上層成員。 只有當 `Usage` 屬性值設定為 Parent 時，才會使用這個屬性值。 這表示已經定義了父子式階層。 預設值是 `ParentIsBlankSelfOrMissing`，表示只有符合針對 `ParentIsBlank`、`ParentIsSelf` 或 `ParentIsMissing` 所描述之一或多個條件的成員，才能視為根成員。 也可使用下列值：<br /><br /> `ParentIsBlank`只有在索引鍵資料行中具有 null、零或空字串的成員會被視為根成員。<br /><br /> `ParentIsSelf`只有本身為父系的成員會被視為根成員。<br /><br /> `ParentIsMissing`只有擁有找不到父代的成員會被視為根成員。|  
|`Type`|包含屬性的類型。 如需詳細資訊，請參閱 [設定屬性類型](attribute-properties-configure-attribute-types.md)。|  
|`UnaryOperatorColumn`|指定提供一元運算子的資料行。 它是 DataItem 類型的繫結，可定義提供一元運算子之資料行的詳細資料。|  
|`Usage`|描述如何使用屬性。<br /><br /> 可用的選項如下：<br /><br /> `Regular`屬性是一般的屬性。 這是預設值。<br /><br /> **Key** ：此屬性是索引鍵屬性。<br /><br /> **Parent** ：此屬性是父屬性。|  
|`ValueColumn`|識別提供屬性值的資料行。 如果已指定屬性的 `NameColumn` 元素，則會使用相同的 `DataItem` 值做為 `ValueColumn` 元素的預設值。 如果未指定屬性的 `NameColumn` 元素，且屬性的 `KeyColumns` 集合包含單一 `KeyColumn` 元素 (代表具有字串資料類型的索引鍵資料行)，則會使用相同的 `DataItem` 值做為 `ValueColumn` 元素的預設值。|  
  
> [!NOTE]  
>  如需如何在 `KeyColumn` 使用 null 值和其他資料完整性問題時設定屬性值的詳細資訊，請參閱[處理 Analysis Services 2005 中的資料完整性問題](https://go.microsoft.com/fwlink/?LinkId=81891)。  
  
> [!NOTE]  
>  當查詢中並未明確包含階層中的成員時，會使用屬性的預設成員來評估運算式。 屬性的預設成員由該屬性的 `DefaultMember` 屬性指定。 只要查詢內包含來自維度的階層，對應到該階層內各層級之屬性的所有預設成員都會忽略。 如果查詢內並未包含維度的階層，則預設成員會用於維度中的所有屬性。 如需預設成員的詳細資訊，請參閱 [定義預設成員](attribute-properties-define-a-default-member.md)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性和屬性階層](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  
