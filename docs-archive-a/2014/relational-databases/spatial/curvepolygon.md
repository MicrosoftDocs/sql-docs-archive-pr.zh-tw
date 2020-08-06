---
title: CurvePolygon | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e000a1d8-a049-4542-bfeb-943fd6ab3969
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: b90fdbd9a0bc80dfc6a82416d0193b2951fe13ef
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585802"
---
# <a name="curvepolygon"></a>CurvePolygon
  `CurvePolygon` 是由一個外部週框環形以及零或多個內部環形所定義的拓撲封閉介面。  
  
> [!IMPORTANT]  
>  如需中引進的空間功能（包括子類型）的詳細描述和範例，請下載技術白皮書 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] `CurvePolygon` ： [SQL Server 2012 中的新空間功能](https://go.microsoft.com/fwlink/?LinkId=226407)。  
  
 下列準則會定義實例的屬性 `CurvePolygon` ：  
  
-   `CurvePolygon` 執行個體的界限是由外部環形和所有內部環形所定義。  
  
-    執行個體的內部是外部環形與所有內部環形之間的空間。  
  
  執行個體與  執行個體不同之處在於， 執行個體可能會包含下列圓弧線段： 和 。  
  
## <a name="compoundcurve-instances"></a>CompoundCurve 執行個體  
 下圖顯示了有效的 `CurvePolygon` 圖形：  
  
### <a name="accepted-instances"></a>已接受的執行個體  
 若要讓系統接受 `CurvePolygon` 執行個體，它必須是空的，或僅包含已接受的圓弧環形。 已接受的圓弧環形符合下列需求。  
  
1.  是已接受的 `LineString`、`CircularString` 或 `CompoundCurve` 執行個體。 如需有關已接受之執行個體的詳細資訊，請參閱 [LineString](linestring.md)、 [CircularString](circularstring.md)，和 [CompoundCurve](compoundcurve.md)。  
  
2.  至少具有四個點。  
  
3.  開始和結束點都具有相同的 X 和 Y 座標。  
  
    > [!NOTE]  
    >  已忽略 Z 和 M 值。  
  
 下列範例會顯示已接受的 `CurvePolygon` 執行個體。  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON EMPTY';  
DECLARE @g2 geometry = 'CURVEPOLYGON((0 0, 0 0, 0 0, 0 0))';  
DECLARE @g3 geometry = 'CURVEPOLYGON((0 0 1, 0 0 2, 0 0 3, 0 0 3))'  
DECLARE @g4 geometry = 'CURVEPOLYGON(CIRCULARSTRING(1 3, 3 5, 4 7, 7 3, 1 3))';  
DECLARE @g5 geography = 'CURVEPOLYGON((-122.3 47, 122.3 -47, 125.7 -49, 121 -38, -122.3 47))';  
```  
  
 `@g3` 即使起點和終點的 Z 值不同仍會接受，因為會忽略 Z 值。 即使 `geography` 類型執行個體無效，仍會接受 `@g5`。  
  
 下列範例會擲回 `System.FormatException`。  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON((0 5, 0 0, 0 0, 0 0))';  
DECLARE @g2 geometry = 'CURVEPOLYGON((0 0, 0 0, 0 0))';  
```  
  
 `@g1` 不被接受，因為起點和終點的 Y 值不相同。 `@g2` 不被接受，因為環形未包含足夠的點。  
  
### <a name="valid-instances"></a>有效的執行個體  
 若要讓 `CurvePolygon` 執行個體有效，外部與內部環形都必須符合下列準則：  
  
1.  它們只能在單一正切點接觸。  
  
2.  它們不得彼此相交。  
  
3.  每個環形至少必須包含四個點。  
  
4.  每個環形都必須是可接受的曲線類型。  
  
 根據 `CurvePolygon` 執行個體是 `geometry` 或 `geography` 資料類型而定，它們也必須符合特定準則。  
  
#### <a name="geometry-data-type"></a>Geometry 資料類型  
 有效的 **geometryCurvePolygon** 執行個體必須具有下列屬性：  
  
1.  所有內部環形都必須包含在外部環形中。  
  
2.  可以具有多個內部環形，但是某個內部環形不得包含另一個內部環形。  
  
3.  所有環形都不得跨越它本身或其他環形。  
  
4.  環形只能在單一正切點接觸 (環形接觸的點數必須是有限的)。  
  
5.  多邊形的內部必須連接在一起。  
  
 下列範例會顯示有效的 **geometryCurvePolygon** 執行個體。  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON EMPTY';  
DECLARE @g2 geometry = 'CURVEPOLYGON(CIRCULARSTRING(1 3, 3 5, 4 7, 7 3, 1 3))';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
 CurvePolygon 執行個體與 Polygon 執行個體具有相同的有效性規則，不過 CurvePolygon 執行個體可接受新的圓弧線段類型。 如需有效或無效執行個體的其他範例，請參閱 [Polygon](polygon.md)。  
  
#### <a name="geography-data-type"></a>Geography 資料類型  
 有效的 **geographyCurvePolygon** 執行個體必須具有下列屬性：  
  
1.  多邊形的內部是使用左側規則來連接。  
  
2.  所有環形都不得跨越它本身或其他環形。  
  
3.  環形只能在單一正切點接觸 (環形接觸的點數必須是有限的)。  
  
4.  多邊形的內部必須連接在一起。  
  
 下列範例會顯示有效的 geography CurvePolygon 執行個體。  
  
```  
DECLARE @g geography = 'CURVEPOLYGON((-122.3 47, 122.3 47, 125.7 49, 121 38, -122.3 47))';  
SELECT @g.STIsValid();  
```  
  
## <a name="examples"></a>範例  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-curvepolygon"></a>A. 使用空的 CurvePolygon 來具現化 Geometry 執行個體  
 這個範例會示範如何建立空的 `CurvePolygon` 執行個體：  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON EMPTY');  
```  
  
### <a name="b-declaring-and-instantiating-a-geometry-instance-with-a-curvepolygon-in-the-same-statement"></a>B. 在相同的陳述式中使用 CurvePolygon 來宣告和具現化 Geometry 執行個體  
 這個程式碼片段會示範如何在相同的陳述式中使用 `CurvePolygon` 來宣告和初始化 geometry 執行個體：  
  
```sql  
DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))'  
```  
  
### <a name="c-instantiating-a-geography-instance-with-a-curvepolygon"></a>C. 使用 CurvePolygon 來具現化 Geography 執行個體  
 這個程式碼片段會示範如何使用 `geography` 來宣告和初始化 `CurvePolygon` 執行個體：  
  
```sql  
DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
```  
  
### <a name="d-storing-a-curvepolygon-with-only-an-exterior-bounding-ring"></a>D. 儲存只有一個外部週框環形的 CurvePolygon  
 這個範例會示範如何將簡單的圓形儲存在 `CurvePolygon` 執行個體中 (只用一個外部週框環形來定義圓形)：  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))');  
SELECT @g.STArea() AS Area;  
```  
  
### <a name="e-storing-a-curvepolygon-containing-interior-rings"></a>E. 儲存包含內部環形的 CurvePolygon  
 這個範例會在 `CurvePolygon` 執行個體中建立甜甜圈 (外部週框環形與內部環形都用來定義甜甜圈)：  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 4, 4 0, 8 4, 4 8, 0 4), CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))');  
SELECT @g.STArea() AS Area;  
```  
  
 這個範例會顯示使用內部環形時有效的 `CurvePolygon` 執行個體與無效的執行個體：  
  
```sql  
DECLARE @g1 geometry, @g2 geometry;  
SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 5, 5 0, 0 -5, -5 0, 0 5), (-2 2, 2 2, 2 -2, -2 -2, -2 2))');  
IF @g1.STIsValid() = 1  
  BEGIN  
     SELECT @g1.STArea();  
  END  
SET @g2 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 5, 5 0, 0 -5, -5 0, 0 5), (0 5, 5 0, 0 -5, -5 0, 0 5))');  
IF @g2.STIsValid() = 1  
  BEGIN  
     SELECT @g2.STArea();  
  END  
SELECT @g1.STIsValid() AS G1, @g2.STIsValid() AS G2;  
```  
  
 @g1 和 @g2 都會使用相同的外部週框環形：半徑為 5 的圓形，而且它們都使用正方形代表內部環形。  不過，執行個體 @g1 有效，但執行個體 @g2 卻無效。  @g2 無效的原因是，內部環形會將外部環形所限定的內部空間分割成四個不同的區域。  下圖將顯示所發生的情況：  
  
## <a name="see-also"></a>另請參閱  
 [多邊形](polygon.md)   
 [CircularString](circularstring.md)   
 [CompoundCurve](compoundcurve.md)   
 [geometry 資料類型方法參考](/sql/t-sql/spatial-geometry/spatial-types-geometry-transact-sql)   
 [geography 資料類型方法參考](/sql/t-sql/spatial-geography/spatial-types-geography)   
 [空間資料類型概觀](spatial-data-types-overview.md)  
  
  
