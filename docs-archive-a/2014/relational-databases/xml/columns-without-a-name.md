---
title: 沒有名稱的資料行 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns without
ms.assetid: 440de44e-3a56-4531-b4e4-1533ca933cac
author: rothja
ms.author: jroth
ms.openlocfilehash: 43d1cbce816e4666e6dab52fdffe5850e65740e8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688661"
---
# <a name="columns-without-a-name"></a>沒有名稱的資料行
  任何沒有名稱的資料行都將予以內嵌。 例如，未指定資料行別名的計算資料行或巢狀純量查詢將會產生沒有任何名稱的資料行。 如果此資料行是 `xml` 類型，就會插入該資料類型執行個體的內容。 否則，就會以文字節點的形式插入資料行內容。  
  
```  
SELECT 2+2  
FOR XML PATH  
```  
  
 產生此 XML。 依預設，對於資料列集中的每個資料列，產生的 XML 中會產生 <`row`> 元素。 這與 RAW 模式相同。  
  
 `<row>4</row>`  
  
 下列查詢會傳回三個資料行的資料列集。 沒有名稱的第三個資料行具有 XML 資料。 PATH 模式會插入 xml 類型的執行個體。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ')   
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH ;  
GO  
```  
  
 以下是部份結果：  
  
 `<row>`  
  
 `<ProductModelID>7</ProductModelID>`  
  
 `<Name>HL Touring Frame</Name>`  
  
 `<MI:Location ...LocationID="10" ...></MI:Location>`  
  
 `<MI:Location ...LocationID="20" ...></MI:Location>`  
  
 `...`  
  
 `</row>`  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 PATH 模式](use-path-mode-with-for-xml.md)  
  
  
