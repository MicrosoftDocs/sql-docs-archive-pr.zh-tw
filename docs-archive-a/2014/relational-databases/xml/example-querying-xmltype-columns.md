---
title: 範例：查詢 XMLType 資料行 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, querying XML example
ms.assetid: d9f3710d-7a2e-4abe-9c02-3e3c0df4d620
author: rothja
ms.author: jroth
ms.openlocfilehash: 0eedfa5a5a265f3715a76a6ca80d489bbec199bd
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585174"
---
# <a name="example-querying-xmltype-columns"></a>範例：查詢 XMLType 資料行
  下列查詢包含 `xml` 類型的資料行。 此查詢會從 `xml` 類型之 `Instructions` 資料行的第一個位置，擷取產品型號識別碼、名稱和製造步驟。  
  
## <a name="example"></a>範例  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name,  
   Instructions.query('  
declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
   /MI:root/MI:Location[1]/MI:step  
')   
FROM Production.ProductModel  
FOR XML RAW ('ProductModelData')  
GO  
```  
  
 以下為結果。 請注意，此資料表只儲存某些產品型號的製造指示。 製造步驟會當做結果中 <`ProductModelData`> 元素的子元素傳回。  
  
```  
<ProductModelData ProductModelID="5" Name="HL Mountain Frame" />  
<ProductModelData ProductModelID="6" Name="HL Road Frame" />  
<ProductModelData ProductModelID="7" Name="HL Touring Frame">  
    <MI:step> ... </MI:step>  
    <MI:step> ... </MI:step>  
 </ProductModelData>  
```  
  
 如果查詢對 XQuery 傳回的 XML 指定資料行名稱 (如下列 `SELECT` 陳述式所指定)，則製造步驟會包在具有指定之名稱的元素中。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name,  
   Instructions.query('  
declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
   /MI:root/MI:Location[1]/MI:step  
') as ManuSteps  
FROM Production.ProductModel  
FOR XML RAW ('ProductModelData')  
go  
```  
  
 以下是結果：  
  
```  
<ProductModelData ProductModelID="5" Name="HL Mountain Frame" />  
<ProductModelData ProductModelID="6" Name="HL Road Frame" />  
<ProductModelData ProductModelID="7" Name="HL Touring Frame">  
  <ManuSteps>  
    <MI:step ... </MI:step>  
    <MI:step ... </MI:step>  
  </ManuSteps>  
</ProductModelData>  
```  
  
 下列查詢指定了 `ELEMENTS` 指示詞。 因此，傳回的結果會是元素中心的。 與 `XSINIL` 指示詞一起指定的 `ELEMENTS` 選項會傳回 <`ManuSteps`> 元素，即使資料列集內相對應的資料行是 NULL 也一樣。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name,  
   Instructions.query('  
declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
   /MI:root/MI:Location[1]/MI:step  
') as ManuSteps  
FROM Production.ProductModel  
FOR XML RAW ('ProductModelData'), root('MyRoot'), ELEMENTS XSINIL  
go  
```  
  
 以下是結果：  
  
```  
<MyRoot xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
   ...  
  <ProductModelData>  
    <ProductModelID>6</ProductModelID>  
    <Name>HL Road Frame</Name>  
    <ManuSteps xsi:nil="true" />  
  </ProductModelData>  
  <ProductModelData>  
    <ProductModelID>7</ProductModelID>  
    <Name>HL Touring Frame</Name>  
    <ManuSteps>  
      <MI:step ... </MI:step>  
      <MI:step ...</MI:step>  
       ...  
    </ManuSteps>  
  </ProductModelData>  
</MyRoot>  
```  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 RAW 模式](use-raw-mode-with-for-xml.md)  
  
  
