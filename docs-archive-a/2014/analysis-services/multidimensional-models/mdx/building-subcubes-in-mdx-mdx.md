---
title: 在 MDX 中建立 Subcube (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- queries [MDX], subcubes
- subcubes [MDX]
- filtered views [MDX]
- MDX [Analysis Services], subcubes
- Multidimensional Expressions [Analysis Services], subcubes
- CREATE SUBCUBE statement
ms.assetid: 5403a62b-99ac-4d83-b02a-89bf78bf0f46
author: minewiskan
ms.author: owend
ms.openlocfilehash: 653b4d30aa86f52179c7b13619ac4347aa65c339
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597417"
---
# <a name="building-subcubes-in-mdx-mdx"></a>在 MDX 中建立 Subcube (MDX)
  Subcube 是 Cube 的子集，呈現篩選後的基礎資料檢視。 將 Cube 限制在 Subcube，可以改善查詢效能。  
  
 若要定義 Subcube，您可以使用 [CREATE SUBCUBE](/sql/mdx/mdx-data-definition-create-subcube) 陳述式，如本主題所述。  
  
## <a name="create-subcube-syntax"></a>CREATE SUBCUBE 語法  
 使用下列語法來建立 Subcube：  
  
```  
CREATE SUBCUBE Subcube_Identifier AS Subcube_Expression  
```  
  
 CREATE SUBCUBE 語法相當簡單。 *Subcube_Identifier* 參數可識別將作為 Subcube 基礎的 Cube。 *Subcube_Expression* 參數可選取將成為 Subcube 的 Cube 部分。  
  
 建立 Subcube 之後，此 Subcube 就會成為所有 MDX 查詢的內容，直到工作階段結束或是執行 [DROP SUBCUBE](/sql/mdx/mdx-data-definition-drop-subcube) 陳述式為止。  
  
### <a name="what-a-subcube-contains"></a>Subcube 包含的項目  
 雖然要使用 CREATE SUBCUBE 陳述式相當簡單，但陳述式本身不會明確地顯示會成為 Subcube 一部份的所有成員。 在定義 Subcube 期間，適用以下規則：  
  
-   如果包含階層的 `(All)` 成員，那個階層的所有成員就會包括在內。  
  
-   如果包含任何成員，那個成員的上階及下階就會包括在內。  
  
-   如果包含層級的每個成員，該階層的所有成員就會包括在內。 如果其他階層的成員不是和該層級的成員並存，則將會予以排除 (例如，未包含客戶的城市等類的不平衡階層)。  
  
-   Subcube 永遠包含 Cube 的每個 `(All)` 成員。  
  
 此外，Subcube 內的彙總值都是以視覺化的方式總計。 例如，Subcube 包含 `USA`、 `WA`及 `OR`。 因為 Subcube 定義的狀態只有 `USA` 及 `{WA,OR}` ，所以 `WA` 的彙總值將會是 `OR` 的總和。 其他狀態都會被忽略。  
  
 此外，明確參考 Subcube 外部的資料格，則會傳回在整個 Cube 內容中評估的資料格值。 例如，您可以建立限制在目前年度的 Subcube。 然後，您可以使用 [ParallelPeriod](/sql/mdx/parallelperiod-mdx) 函數比較目前年度與前一個年度。 即使前一年的值位於子工作子資料集外，值的差異還是會傳回。  
  
 最後，如果原始的內容未被覆寫，就會在子選擇的內容中評估曾在子選擇中評估的集合函數。 如果內容會被覆寫，就會在整個 Cube 的內容中評估集合函數。  
  
## <a name="create-subcube-example"></a>CREATE SUBCUBE 範例  
 下列範例會建立一個 Subcube，將 Budget Cube 限制為只有帳戶 4200 及 4300：  
  
 `CREATE SUBCUBE Budget AS SELECT {[Account].[Account].&[4200], [Account].[Account].&[4300] } ON 0 FROM Budget`  
  
 在為工作階段建立 Subcube 之後，將會對該 Subcube 進行任何後續查詢，而不是對整個 Cube。 例如，您可以執行以下查詢。 此查詢將只會傳回帳戶 4200 及 4300 的成員。  
  
 `SELECT [Account].[Account].Members ON 0, Measures.Members ON 1 FROM Budget`  
  
## <a name="see-also"></a>另請參閱  
 [在查詢中建立 Cube 內容 &#40;MDX&#41;](establishing-cube-context-in-a-query-mdx.md)   
 [MDX 查詢基礎觀念 &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
