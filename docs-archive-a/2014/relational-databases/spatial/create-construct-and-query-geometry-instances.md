---
title: 建立、建構及查詢 geometry 執行個體 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- planar spatial data [SQL Server], getting started
- geometry data type [SQL Server], getting started
ms.assetid: c6b5c852-37d2-48d0-a8ad-e43bb80d6514
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 539f3f8bb1d9a1c277d6317cc571cf8bcb281833
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585803"
---
# <a name="create-construct-and-query-geometry-instances"></a>建立、建構及查詢幾何執行個體
  平面空間資料類型 (`geometry`) 代表 Euclidean (平面) 座標系統中的資料。 這種類型在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中是實作為 Common Language Runtime (CLR) 資料類型。  
  
 `geometry` 類型已預先定義，而且可在每一個資料庫中使用。 您可以建立 `geometry` 類型的資料表資料行，並使用與其他 CLR 類型相同的方式來操作 `geometry` 資料。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援的 `geometry` 資料類型 (平面) 符合開放式地理空間協會 (Open Geospatial Consortium，OGC) 的 SQL 簡單特徵規格 1.1.0 版。  
  
 如需有關 OGC 規格的詳細資訊，請參閱下列主題：  
  
-   [OGC 規格，簡單特徵存取第一部 - 常見架構](https://go.microsoft.com/fwlink/?LinkId=93628)  
  
-   [OGC 規格，簡單特徵存取第二部 - SQL 選項](https://go.microsoft.com/fwlink/?LinkId=93629) \(英文\)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援以下列結構描述定義之現有 GML 3.1 標準的子集：[https://schemas.microsoft.com/sqlserver/profiles/gml/SpatialGML.xsd](https://go.microsoft.com/fwlink/?LinkId=230959)。  
  
##  <a name="creating-or-constructing-a-new-geometry-instance"></a><a name="creating"></a> 建立或建構新的 geometry 執行個體  
  
###  <a name="creating-a-new-geometry-instance-from-an-existing-instance"></a><a name="existing"></a> 從現有的執行個體建立新的 geometry 執行個體  
 `geometry` 資料類型提供許多內建方法，您可以使用這些方法來根據現有執行個體建立新的 `geometry` 執行個體。  
  
 **在幾何周圍建立緩衝區**  
 [STBuffer &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stbuffer-geometry-data-type)  
  
 [BufferWithTolerance #40; geometry 資料類型 &#41;](/sql/t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type)  
  
 **建立簡化版本的幾何**  
 [減少 &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/reduce-geometry-data-type)  
  
 **建立幾何的凸面**  
 [STConvexHull &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stconvexhull-geometry-data-type)  
  
 **從兩個幾何的交集建立幾何**  
 [STIntersection &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stintersection-geometry-data-type)  
  
 **從兩個幾何的聯集建立幾何**  
 [STUnion &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stunion-geometry-data-type)  
  
 **從兩個幾何不重疊的點建立幾何**  
 [STDifference &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stdifference-geometry-data-type)  
  
 **從兩個幾何不重疊的點建立幾何**  
 [STSymDifference &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stsymdifference-geometry-data-type)  
  
 **建立位於現有幾何上的任意 Point 執行個體**  
 [STPointOnSurface &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)  
  
  
  
###  <a name="constructing-a-geometry-instance-from-well-known-text-input"></a><a name="wkt"></a> 從已知的文字輸入建構 geometry 執行個體  
 `geometry` 資料類型提供數種內建方法，可從開放式地理空間協會 (Open Geospatial Consortium，OGC) 的 WKT 表示法產生幾何。 WKT 標準是一種文字字串，可允許使用文字格式交換幾何資料。  
  
 **從 WKT 輸入建構任何類型的 geometry 執行個體**  
 [STGeomFromText &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stgeomfromtext-geometry-data-type)  
  
 [剖析 &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/parse-geometry-data-type)  
  
 **從 WKT 輸入建構幾何 Point 執行個體**  
 [STPointFromText &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stpointfromtext-geometry-data-type)  
  
 **從 WKT 輸入建構幾何 MultiPoint 執行個體**  
 [STMPointFromText &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stmpointfromtext-geometry-data-type)  
  
 **從 WKT 輸入建構幾何 LineString 執行個體**  
 [STLineFromText &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stlinefromtext-geometry-data-type)  
  
 **從 WKT 輸入建構幾何 MultiLineString 執行個體**  
 [STMLineFromText &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stmlinefromtext-geometry-data-type)  
  
 **從 WKT 輸入建構幾何 Polygon 執行個體**  
 [STPolyFromText &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stpolyfromtext-geometry-data-type)  
  
 **從 WKT 輸入建構幾何 MultiPolygon 執行個體**  
 [STMPolyFromText &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stmpolyfromtext-geometry-data-type)  
  
 **從 WKT 輸入建構幾何 GeometryCollection 執行個體**  
 [STGeomCollFromText &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stgeomcollfromtext-geometry-data-type)  
  
  
  
###  <a name="constructing-a-geometry-instance-from-well-known-binary-input"></a><a name="wkb"></a> 從已知的二進位輸入建構 geometry 執行個體  
 WKB 是 OGC 指定的一種二進位格式，可允許在用戶端應用程式與 SQL 資料庫之間交換 `geometry` 資料。 下列函數可接受 WKB 輸入來建構幾何：  
  
 **從 WKB 輸入建構任何類型的 geometry 執行個體**  
 [STGeomFromWKB &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stgeomfromwkb-geometry-data-type)  
  
 **從 WKB 輸入建構幾何 Point 執行個體**  
 [STPointFromWKB &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stpointfromwkb-geometry-data-type)  
  
 **從 WKB 輸入建構幾何 MultiPoint 執行個體**  
 [STMPointFromWKB &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stmpointfromwkb-geometry-data-type)  
  
 **從 WKB 輸入建構幾何 LineString 執行個體**  
 [STLineFromWKB &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stlinefromwkb-geometry-data-type)  
  
 **從 WKB 輸入建構幾何 MultiLineString 執行個體**  
 [STMLineFromWKB &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stmlinefromwkb-geometry-data-type)  
  
 **從 WKB 輸入建構幾何 Polygon 執行個體**  
 [STPolyFromWKB &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stpolyfromwkb-geometry-data-type)  
  
 **從 WKB 輸入建構幾何 MultiPolygon 執行個體**  
 [STMPolyFromWKB &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stmpolyfromwkb-geometry-data-type)  
  
 **從 WKB 輸入建構幾何 GeometryCollection 執行個體**  
 [STGeomCollFromWKB &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stgeomcollfromwkb-geometry-data-type)  
  
  
  
###  <a name="constructing-a-geometry-instance-from-gml-text-input"></a><a name="gml"></a> 從 GML 文字輸入建構 geometry 執行個體  
 `geometry`資料類型提供的方法會 `geometry` 從 GML 產生實例，這是幾何物件的 XML 標記法。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可支援 GML 的子集。  
  
 **從 GML 輸入建構任何類型的 geometry 執行個體**  
 [GeomFromGml &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/geomfromgml-geometry-data-type)  
  
  
  
##  <a name="returning-well-known-text-and-well-known-binary-from-a-geometry-instance"></a><a name="returning"></a> 從 geometry 執行個體傳回已知的文字和已知的二進位  
 您可以使用下列方法傳回 WKT 或 WKB 格式的 `geometry` 執行個體：  
  
 **傳回 WKT 表示法的 geometry 執行個體**  
 [STAsText &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stastext-geometry-data-type)  
  
 [ToString &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/tostring-geometry-data-type)  
  
 **傳回 WKT 表示法的 geometry 執行個體 (包含任何 Z 和 M 值)**  
 [AsTextZM &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/astextzm-geometry-data-type)  
  
 **傳回 WKB 表示法的 geometry 執行個體**  
 [STAsBinary &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stasbinary-geometry-data-type)  
  
 **傳回 GML 表示法的 geometry 執行個體**  
 [AsGml &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/asgml-geometry-data-type)  
  
  
  
##  <a name="querying-the-properties-and-behaviors-of-geometry-instances"></a><a name="querying"></a> 查詢 geometry 執行個體的屬性和行為  
 所有 `geometry` 實例都有許多屬性，可以透過提供的方法來抓取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 下列主題定義幾何類型的屬性和行為以及用來查詢每一個類型的方法。  
  
###  <a name="validity-instance-type-and-geometrycollection-information"></a><a name="valid"></a> 有效性、執行個體類型和 GeometryCollection 資訊  
 一旦建構了 `geometry` 執行個體之後，您就可以使用下列方法來判斷它的格式是否正確、傳回執行個體類型，或者如果它是集合執行個體，就會傳回特定的 `geometry` 執行個體。  
  
 **傳回 geometry 類型的執行個體**  
 [STGeometryType &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stgeometrytype-geometry-data-type)  
  
 **判斷 geometry 是否為特定的執行個體類型**  
 [InstanceOf &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/instanceof-geometry-data-type)  
  
 **判斷 geometry 執行個體對於它的執行個體類型而言是否格式正確**  
 [STIsValid &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)  
  
 **將 geometry 執行個體轉換成具有執行個體類型的正確格式 geometry 執行個體**  
 [MakeValid &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/makevalid-geometry-data-type)  
  
 **傳回幾何集合執行個體中的幾何數**  
 [STNumGeometries &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stnumgeometries-geometry-data-type)  
  
 傳回幾何集合執行個體中的特定幾何  
 [STGeometryN &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stgeometryn-geometry-data-type)STGeometryN (geometry 資料類型)  
  
  
  
###  <a name="number-of-points"></a><a name="number"></a> 點數  
 所有非空 `geometry` 的實例都是由*點*組成。 這些點代表幾何繪製所在平面的 X 和 Y 座標。 `geometry`提供許多內建方法來查詢執行個體的點。  
  
 **傳回組成執行個體的點數**  
 [STNumPoints &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type)  
  
 **傳回執行個體中的特定點**  
 [STPointN](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)  
  
 **傳回位於執行個體上的任意點**  
 [STPointOnSurface](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)  
  
 **傳回執行個體的起點**  
 [STStartPoint](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)  
  
 **傳回執行個體的終點**  
 [STEndpoint](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)  
  
 **傳回 Point 執行個體的 X 座標**  
 [STX &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stx-geometry-data-type)  
  
 **傳回 Point 執行個體的 Y 座標**  
 [STY](/sql/t-sql/spatial-geometry/sty-geometry-data-type)  
  
 **傳回 Polygon、CurvePolygon 或 MultiPolygon 執行個體的幾何中心點**  
 [STCentroid](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type)  
  
  
  
###  <a name="dimension"></a><a name="dimension"></a> 維度  
 非空的 `geometry` 執行個體可以是 0 維度、1 維度或 2 維度。 零維度 `geometries` (如 `Point` 和 `MultiPoint`) 沒有長度或區域。 一維度物件 (如 `LineString, CircularString, CompoundCurve` 和 `MultiLineString`) 具有長度。 二維度執行個體 (如 `Polygon`、`CurvePolygon` 和 `MultiPolygon`) 具有區域和長度。 空的執行個體將會報告 -1 的維度，而 `GeometryCollection` 則會報告與其內容類型相依的區域。  
  
 **傳回執行個體的維度**  
 [STDimension](/sql/t-sql/spatial-geometry/stdimension-geometry-data-type)  
  
 **傳回執行個體的長度**  
 [STLength](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)  
  
 **傳回執行個體的區域**  
 [STArea](/sql/t-sql/spatial-geometry/starea-geometry-data-type)  
  
  
  
###  <a name="empty"></a><a name="empty"></a> Empty  
 *空*的 `geometry` 實例沒有任何點。 空的 `LineString, CircularString`、`CompoundCurve` 和 `MultiLineString` 執行個體的長度是零。 空的 `Polygon`、`CurvePolygon` 和 `MultiPolygon` 執行個體的區域是 0。  
  
 **判斷執行個體是否為空的**  
 [STIsEmpty](/sql/t-sql/spatial-geometry/stisempty-geometry-data-type)。  
  
  
  
###  <a name="simple"></a><a name="simple"></a> Simple  
 `geometry`若要讓實例成為*簡單*的，它必須符合這兩項需求：  
  
-   此例項的每一個圖形都不能自己相交 (除了在它的端點上以外)。  
  
-   此例項的兩個圖形不能在非兩者界限內的點上彼此相交。  
  
> [!NOTE]  
>  空的幾何一定是簡單的幾何。  
  
 **判斷執行個體是否為簡單**  
 [STIsSimple](/sql/t-sql/spatial-geometry/stissimple-geometry-data-type)。  
  
  
  
###  <a name="boundary-interior-and-exterior"></a><a name="boundary"></a> 界限、內部和外部  
 實例的*內部* `geometry` 是實例所佔用的空間，而*外部*則是未佔用的空間。  
  
 *「界限」* (Boundary) 是由 OGC 定義如下：  
  
-   `Point` 和 `MultiPoint` 執行個體沒有界限。  
  
-   `LineString` 和 `MultiLineString` 界限是由起點和終點所組成，移除發生偶數次數的點。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 1, 0 0, 1 0, 0 1), (1 1, 1 0))');  
SELECT @g.STBoundary().ToString();  
```  
  
 `Polygon` 或 `MultiPolygon` 執行個體的界限是它的環形集合。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0), (1 1, 1 2, 2 2, 2 1, 1 1))');  
SELECT @g.STBoundary().ToString();  
```  
  
 **傳回執行個體的界限**  
 [STBoundary](/sql/t-sql/spatial-geometry/stboundary-geometry-data-type)  
  
  
  
###  <a name="envelope"></a><a name="envelope"></a> 範圍  
 實例的*信封* `geometry` （也稱為周*框*方塊）是以軸對齊的矩形，由實例的最小值和最大值 (X，Y) 座標所組成。  
  
 **傳回執行個體的範圍**  
 [STEnvelope](/sql/t-sql/spatial-geometry/stenvelope-geometry-data-type)  
  
  
  
###  <a name="closure"></a><a name="closure"></a> 封閉性  
 *封閉式* `geometry` 實例是起始點和結束點相同的圖形。 `Polygon` 執行個體視為封閉式。 `Point` 執行個體視為非封閉式。  
  
 環形是簡單、封閉的 `LineString` 執行個體。  
  
 **判斷執行個體是否為封閉**  
 [STIsClosed](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)  
  
 **判斷執行個體是否為環形**  
 [STIsRing](/sql/t-sql/spatial-geometry/stisring-geometry-data-type)  
  
 **傳回 Polygon 執行個體的外部環形**  
 [STExteriorRing](/sql/t-sql/spatial-geometry/stexteriorring-geometry-data-type)  
  
 **傳回 Polygon 中的內部環形數**  
 [STNumInteriorRing](/sql/t-sql/spatial-geometry/stnuminteriorring-geometry-data-type)  
  
 **傳回 Polygon 的指定內部環形**  
 [STInteriorRingN](/sql/t-sql/spatial-geometry/stinteriorringn-geometry-data-type)  
  
  
  
###  <a name="spatial-reference-id-srid"></a><a name="srid"></a> 空間參考識別碼 (SRID)  
 空間參考識別碼 (SRID) 是用來指定代表 `geometry` 執行個體之座標系統的識別碼。 具有不同 SRID 的兩個執行個體無法進行比較。  
  
 **設定或傳回執行個體的 SRID**  
 [STSrid](/sql/t-sql/spatial-geometry/stsrid-geometry-data-type)  
  
 這個屬性可以修改。  
  
  
  
##  <a name="determining-relationships-between-geometry-instances"></a><a name="rel"></a> 判斷 geometry 執行個體之間的關聯性  
 `geometry` 資料類型提供許多內建方法，您可以使用這些方法來判斷兩個 `geometry` 執行個體之間的關聯性。  
  
 **判斷兩個執行個體是否組成相同的點集合**  
 [STEquals](/sql/t-sql/spatial-geometry/stequals-geometry-data-type)  
  
 **判斷兩個執行個體是否不相交**  
 [STDisjoint](/sql/t-sql/spatial-geometry/stdisjoint-geometry-data-type)  
  
 **判斷兩個執行個體是否相交**  
 [STIntersects](/sql/t-sql/spatial-geometry/stintersects-geometry-data-type)  
  
 **判斷兩個執行個體是否接觸**  
 [STTouches](/sql/t-sql/spatial-geometry/sttouches-geometry-data-type)  
  
 **判斷兩個執行個體是否重疊**  
 [STOverlaps](/sql/t-sql/spatial-geometry/stoverlaps-geometry-data-type)  
  
 **判斷兩個執行個體是否交叉**  
 [STCrosses](/sql/t-sql/spatial-geometry/stcrosses-geometry-data-type)  
  
 **判斷某個執行個體是否在另一個執行個體內**  
 [STWithin](/sql/t-sql/spatial-geometry/stwithin-geometry-data-type)  
  
 **判斷某個執行個體是否包含另一個執行個體**  
 [STContains](/sql/t-sql/spatial-geometry/stcontains-geometry-data-type)  
  
 **判斷某個執行個體是否與另一個執行個體重疊**  
 [STOverlaps](/sql/t-sql/spatial-geometry/stoverlaps-geometry-data-type)  
  
 **判斷兩個執行個體在空間上是否相關**  
 [STRelate](/sql/t-sql/spatial-geometry/strelate-geometry-data-type)  
  
 **判斷兩個 geometry 內點與點之間的最短距離**  
 [STDistance](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type)  
  
  
  
##  <a name="geometry-instances-default-to-zero-srid"></a><a name="defaultsrid"></a> geometry 執行個體預設為零 SRID  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中 `geometry` 執行個體的預設 SRID 是 0。 有了 `geometry` 空間資料，執行計算時並不需要空間執行個體的特定 SRID；因此，執行個體可位於未定義的平面空間內。 若要在 `geometry` 資料類型方法的計算中指示未定義的平面空間，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會使用 SRID 0。  
  
##  <a name="examples"></a><a name="examples"></a> 範例  
 下列兩個範例示範如何加入及查詢幾何資料。  
  
-   第一個範例會建立具有識別資料行及 `geometry` 資料行 `GeomCol1`的資料表。 第三個資料行會將 `geometry` 資料行轉譯成它的開放地理空間協會 (Open Geospatial Consortium，OGC) 已知的文字 (Well-Known Text，WKT) 表示法，並使用 `STAsText()` 方法。 然後會插入兩個資料列：一個資料列包含 `LineString` 的 `geometry`執行個體，另一個資料列包含 `Polygon` 執行個體。  
  
    ```  
    IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
        DROP TABLE dbo.SpatialTable;  
    GO  
  
    CREATE TABLE SpatialTable   
        ( id int IDENTITY (1,1),  
        GeomCol1 geometry,   
        GeomCol2 AS GeomCol1.STAsText() );  
    GO  
  
    INSERT INTO SpatialTable (GeomCol1)  
    VALUES (geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0));  
  
    INSERT INTO SpatialTable (GeomCol1)  
    VALUES (geometry::STGeomFromText('POLYGON ((0 0, 150 0, 150 150, 0 150, 0 0))', 0));  
    GO  
    ```  
  
-   第二個範例使用 `STIntersection()` 方法傳回之前插入之兩個 `geometry` 執行個體相交的點。  
  
    ```  
    DECLARE @geom1 geometry;  
    DECLARE @geom2 geometry;  
    DECLARE @result geometry;  
  
    SELECT @geom1 = GeomCol1 FROM SpatialTable WHERE id = 1;  
    SELECT @geom2 = GeomCol1 FROM SpatialTable WHERE id = 2;  
    SELECT @result = @geom1.STIntersection(@geom2);  
    SELECT @result.STAsText();  
    ```  
  
  
  
## <a name="see-also"></a>另請參閱  
 [空間資料 &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
