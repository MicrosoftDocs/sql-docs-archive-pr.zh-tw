---
title: 範例：指定 ELEMENT 指示詞及實體編碼 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ELEMENT directive
- entity encoding [XML]
ms.assetid: 50cda5c1-7293-4080-93b3-872e3b8d484e
author: rothja
ms.author: jroth
ms.openlocfilehash: 4ba4e419d31aa7c02cc2dc8f19a3350c233f042b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686862"
---
# <a name="example-specifying-the-element-directive-and-entity-encoding"></a>範例：指定 ELEMENT 指示詞及實體編碼
  此範例說明 **ELEMENT** 與 **XML** 指示詞之間的相異處。 **ELEMENT** 指示詞會將資料實體化，但 **XML** 指示詞則否。 已將 \<Summary> 元素指派給查詢中的 XML `<Summary>This is summary description</Summary>`。  
  
 請考量這項查詢：  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID  as [ProductModel!1!ProdModelID],  
        Name            as [ProductModel!1!Name],  
        NULL            as [Summary!2!SummaryDescription!ELEMENT]  
FROM    Production.ProductModel  
WHERE   ProductModelID=19  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        NULL,  
       '<Summary>This is summary description</Summary>'  
FROM   Production.ProductModel  
WHERE  ProductModelID=19  
FOR XML EXPLICIT  
```  
  
 以下是結果。 摘要描述會在結果中實體化。  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription><Summary>This is summary description</Summary></SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 現在，如果您在資料行名稱 **中指定** XML `Summary!2!SummaryDescription!XML`指示詞，而非 **ELEMENT** 指示詞，您將會收到未實體化的摘要描述。  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
      <Summary>This is summary description</Summary>  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 以下查詢不會指派靜態的 XML 值，而是使用 **xml** 類型的 **query()** 方法，擷取 **xml** 類型之 CatalogDescription 資料行的產品型號摘要描述。 因為已知結果將為 **xml** 類型，所以不會套用實體化。  
  
```  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID  as [ProductModel!1!ProdModelID],  
        Name            as [ProductModel!1!Name],  
        NULL            as [Summary!2!SummaryDescription]  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        Name,  
       (SELECT CatalogDescription.query('  
            declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
          /pd:ProductDescription/pd:Summary'))  
FROM     Production.ProductModel  
WHERE    CatalogDescription is not null  
ORDER BY [ProductModel!1!ProdModelID],Tag  
FOR XML EXPLICIT  
```  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 EXPLICIT 模式](use-explicit-mode-with-for-xml.md)  
  
  
