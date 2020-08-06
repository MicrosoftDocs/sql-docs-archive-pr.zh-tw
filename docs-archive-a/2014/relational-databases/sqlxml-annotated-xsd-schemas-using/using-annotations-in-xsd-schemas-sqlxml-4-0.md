---
title: 使用 XSD 架構中的批註 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, about annotated XSD schemas
- annotations [SQLXML]
- relationships [SQLXML]
- relationships [SQLXML], hierarchical relationships
- hierarchical relationships [SQLXML]
- mapping schema [SQLXML], scenarios for using
ms.assetid: 78f318a4-7a36-473b-9852-a4bae6940ce5
author: rothja
ms.author: jroth
ms.openlocfilehash: e2be94aa5815593d7a5a2e0c00bcd8849e81484e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595898"
---
# <a name="using-annotations-in-xsd-schemas-sqlxml-40"></a>在 XSD 結構描述中使用註釋 (SQLXML 4.0)
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 中，XSD 結構描述語言以類似 XML-Data Reduced (XDR) 結構描述語言所推出之註解的方式支援註解。 在 XSD 中有 XDR 不支援的其他註解。  
  
 這些註解可以在 XSD 結構描述內，用於指定 XML 到關聯式的對應。 這包括 XSD 結構描述中的元素和屬性到資料庫中的資料表 (檢視) 和資料行之間的對應。  
  
 如果您沒有指定註解，就會使用預設對應。 根據預設，包含複雜類型的 XSD 元素會對應到指定之資料庫中的資料表 (檢視) 名稱，而包含簡單類型的元素或屬性會對應到具有相同名稱的資料行，做為元素或屬性。  
  
 這些批註也可以用來指定 XML 中的階層式關聯性，因此代表資料庫中的關聯性，因為 XSD 架構只是關聯式資料的 XML 視圖。  
  
 本節提供您可搭配 XSD 結構描述一起使用之註解的描述以及其使用方式的範例。  
  
> [!NOTE]  
>  本節中的所有範例都會根據每個範例中所描述的註解式 XSD 結構描述，指定簡單的 XPath 查詢。 同時會假設您熟悉 XPath 語言。  
  
## <a name="in-this-section"></a>本節內容  
 [&#40;SQLXML 4.0&#41;的 XSD 注釋](xsd-annotations-sqlxml-4-0.md)  
 列出您可以搭配 XSD 結構描述使用的註解、其描述，以及適用於 XDR 的相等註解。  
  
 [XSD 元素和屬性對資料表和資料行的預設對應 &#40;SQLXML 4.0&#41;](default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
 說明預設對應，並提供與預設對應相關之工作的範例。  
  
 [XSD 元素和屬性對資料表和資料行的明確對應 &#40;SQLXML 4.0&#41;](explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns.md)  
 說明與 `sql:relation` 和 `sql:field` 註解的明確對應，並提供範例。  
  
 [使用 sql： relationship 指定關聯性 &#40;SQLXML 4.0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
 描述及提供 `sql:relationship` 註解的範例。  
  
 [在 sql： relationship 上指定 sql：反向屬性 &#40;SQLXML 4.0&#41;](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)  
 描述 `sql:inverse` 註解。  
  
 [使用 sql： is-常數建立常數元素 &#40;SQLXML 4.0&#41;](creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)  
 描述及提供 `sql:is-constant` 註解的範例。  
  
 [使用 sql：對應 &#40;SQLXML 4.0&#41;，從產生的 XML 檔排除架構元素](excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)  
 描述及提供 `sql:mapped` 註解的範例。  
  
 [使用 sql： limit-field 和 sql： limit-value &#40;SQLXML 4.0&#41;篩選值](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 描述及提供 `sql:limit-field` 和 `sql:limit-value` 註解的範例。  
  
 [使用 sql：索引鍵-欄位來識別索引鍵資料行 &#40;SQLXML 4.0&#41;](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)  
 描述及提供 `sql:key-fields` 註解的範例。  
  
 [使用 targetNamespace 屬性來指定目標命名空間 &#40;SQLXML 4.0&#41;](specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
 描述並提供**targetNamespace**屬性的範例。  
  
 [使用 sql： prefix 建立有效的 ID、IDREF 和 IDREFS 類型屬性 &#40;SQLXML 4.0&#41;](creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)  
 描述及提供 `sql:prefix` 註解的範例。  
  
 [資料類型強制型轉和 sql： datatype 注釋 &#40;SQLXML 4.0&#41;](data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)  
 描述及提供 `sql:datatype` 註解的範例。  
  
 [將 XSD 資料類型對應到 XPath 資料類型 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md)  
 提供比較 XSD、XDR 與 XPath 資料類型的資料表，並列出相關的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 轉換。  
  
 [使用 sql： use-CDATA 建立 CDATA 區段 &#40;SQLXML 4.0&#41;](creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)  
 描述及提供 `sql:use-data` 註解的範例。  
  
 [使用 sql： &#40;SQLXML 4.0&#41;要求對 BLOB 資料的 URL 參考](requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)  
 描述及提供 `sql:encode` 註解的範例。  
  
 [使用 sql：溢位欄位來抓取未使用的資料 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 描述及提供 `sql:overflow-field` 註解的範例。  
  
 [使用 sql:hide 來隱藏項目和屬性](hiding-elements-and-attributes-by-using-sql-hide.md)  
 描述及提供 `sql:hide` 註解的範例。  
  
 [使用 sql:identity 和 sql:guid 註解](using-the-sql-identity-and-sql-guid-annotations.md)  
 描述及提供 `sql:identity` 和 `sql:guid` 註解的範例。  
  
 [使用 sql:max-depth 來指定遞迴關聯性的深度](specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)  
 描述及提供 `sql:max-depth` 註解的範例。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SQLXML 4.0&#41;的批註式架構安全性考慮](../sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)  
  
  
