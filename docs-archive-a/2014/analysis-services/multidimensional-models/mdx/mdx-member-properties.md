---
title: 使用 MDX) 的成員屬性 (|Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DIMENSION PROPERTIES keyword
- Properties function
- member properties [MDX]
- members [MDX], properties
ms.assetid: 26b5ad08-3799-4a5e-89f3-dca25e637d45
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5b7fdf989fc23ea70be7d7863f5d4c6ac0b61d8a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87698620"
---
# <a name="using-member-properties-mdx"></a>使用成員屬性 (MDX)
  成員屬性包含每個 Tuple 中每個成員的基本資訊。 此基本資訊包括成員名稱、父層級、子系數目等等。 指定層級上的所有成員都能使用成員屬性。 就組織而言，會將成員屬性視為儲存在單一維度上，且以維度方式組織的資料。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，成員屬性稱為屬性關聯性。 如需詳細資訊，請參閱 [屬性關聯性](../../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)。  
  
 成員屬性不是 *「內建」* 就是 *「自訂」*：  
  
 內建成員屬性  
 當維度與層級提供其他內建維度與層級成員屬性 (如成員識別碼) 時，所有成員都會支援內建成員屬性 (例如，格式化的成員值)。  
  
 如需詳細資訊，請參閱[內建成員屬性 &#40;MDX&#41;](mdx-member-properties-intrinsic-member-properties.md)。  
  
 使用者自訂成員屬性  
 成員通常會擁有與之相關的其他屬性。 例如，Products 層級可能會為每項產品提供 SKU、SRP、Weight 與 Volume 屬性。 這些屬性不是成員，但包含了有關 Products 層級上成員的其他資訊。  
  
 如需詳細資訊，請參閱[使用者自訂成員屬性 &#40;MDX&#41;](mdx-member-properties-user-defined-member-properties.md)。  
  
 內建和使用者自訂成員屬性都可以透過使用 `PROPERTIES` 關鍵字或[properties](/sql/mdx/properties-mdx)函數來抓取。  
  
## <a name="using-the-properties-keyword"></a>使用 PROPERTIES 關鍵字  
 `PROPERTIES` 關鍵字可以指定成員屬性，以供指定的座標軸維度使用。 `PROPERTIES`關鍵字會內嵌在 `<axis specification>` MDX [SELECT](/sql/mdx/mdx-data-manipulation-select)語句的子句中：  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
```  
  
 `<axis_specification>` 子句包含一個選擇性的 `<dim_props>` 子句，如以下語法所示：  
  
```  
<axis_specification> ::= <set> [<dim_props>] ON <axis_name>  
```  
  
> [!NOTE]  
>  如需 `<set>` 和 `<axis_name>` 值的詳細資訊，請參閱[指定查詢座標軸的內容 &#40;MDX&#41;](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)。  
  
 `<dim_props>` 子句可讓您使用 `PROPERTIES` 關鍵字，查詢維度、層級與成員屬性。 以下語法顯示 `<dim_props>` 子句的格式：  
  
```  
<dim_props> ::= [DIMENSION] PROPERTIES <property> [,<property>...]  
```  
  
 `<property>` 語法的解析會依據您查詢的屬性而有所不同：  
  
-   可區分內容的內建成員屬性，必須在前面加上維度或層級的名稱。 但是，不區分內容的內建成員屬性，就無法以維度或層級名稱來限定。 如需如何搭配使用關鍵字與內建成員屬性的詳細資訊 `PROPERTIES` ，請參閱[內部成員屬性 &#40;MDX&#41;](mdx-member-properties-intrinsic-member-properties.md)。  
  
-   使用者自訂成員屬性應該在前面加上所屬層級的名稱。 如需如何搭配使用 `PROPERTIES` 關鍵字與使用者定義成員屬性的詳細資訊，請參閱[&#40;MDX&#41;的使用者自訂成員屬性](mdx-member-properties-user-defined-member-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立和使用屬性值 &#40;MDX&#41;](../../creating-and-using-property-values-mdx.md)  
  
  
