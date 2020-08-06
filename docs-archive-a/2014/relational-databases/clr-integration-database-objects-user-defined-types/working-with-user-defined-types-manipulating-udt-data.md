---
title: 操作 UDT 資料 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- data deletions [CLR integration]
- data insertions [CLR integration]
- CONVERT function
- data updates [CLR integration]
- comparing data
- updating data [CLR integration]
- removing data
- IsByteOrdered property
- variables [CLR integration]
- data manipulation [CLR integration]
- user-defined types [CLR integration], data manipulation
- deleting data
- UDTs [CLR integration], data manipulation
- invoking UDT methods
- inserting data
ms.assetid: 51b1a5f2-7591-4e11-bfe2-d88e0836403f
author: rothja
ms.author: jroth
ms.openlocfilehash: 75810a2ffd92130e45025f742d43ba7917d73992
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87698308"
---
# <a name="manipulating-udt-data"></a>操作 UDT 資料
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 在修改使用者定義型別 (UDT) 資料行中的資料時，不會提供 INSERT、UPDATE 或 DELETE 陳述式的特定語法。 [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 或 CONVERT 函數可用來將原生資料類型轉換為 UDT 類型。  
  
## <a name="inserting-data-in-a-udt-column"></a>將資料插入 UDT 資料行  
 下列語句會將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 三個範例資料列插入至**Points**資料表。 **Point**資料類型是由會公開為 UDT 屬性的 X 和 Y 整數值所組成。 您必須使用 CAST 或 CONVERT 函數，將以逗號分隔的 X 和 Y 值轉換為**Point**類型。 前兩個語句使用 CONVERT 函式，將字串值轉換為**Point**類型，而第三個語句則使用 CAST 函數：  
  
```  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '3,4'));  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '1,5'));  
INSERT INTO dbo.Points (PointValue) VALUES (CAST ('1,99' AS Point));  
```  
  
## <a name="selecting-data"></a>選取資料  
 下列 SELECT 陳述式選取 UDT 的二進位值。  
  
```  
SELECT ID, PointValue FROM dbo.Points  
```  
  
 若要查看以可讀取格式顯示的輸出，請呼叫 `ToString` **Point** UDT 的方法，將值轉換為其字串表示。  
  
```  
SELECT ID, PointValue.ToString() AS PointValue   
FROM dbo.Points;  
```  
  
 如此會產生下列結果。  
  
```  
IDPointValue  
----------  
13,4  
21,5  
31,99  
```  
  
 您還可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 及 CONVERT 函數，以取得相同的結果。  
  
```  
SELECT ID, CAST(PointValue AS varchar)   
FROM dbo.Points;  
  
SELECT ID, CONVERT(varchar, PointValue)   
FROM dbo.Points;  
```  
  
 **Point** UDT 會將其 X 和 Y 座標公開為屬性，然後您就可以個別選取。 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式分別選取 X 及 Y 座標：  
  
```  
SELECT ID, PointValue.X AS xVal, PointValue.Y AS yVal   
FROM dbo.Points;  
```  
  
 X 及 Y 屬性傳回的整數值將顯示在結果集中。  
  
```  
IDxValyVal  
----------  
134  
215  
3199  
```  
  
## <a name="working-with-variables"></a>使用變數  
 使用變數時，可利用 DECLARE 陳述式將變數指派給 UDT 類型。 下列陳述式使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] SET 陳述式指派值，並在變數上呼叫 UDT 的 `ToString` 方法以顯示結果。  
  
```  
DECLARE @PointValue Point;  
SET @PointValue = (SELECT PointValue FROM dbo.Points  
    WHERE ID = 2);  
SELECT @PointValue.ToString() AS PointValue;  
```  
  
 結果集顯示變數值：  
  
```  
PointValue  
----------  
-1,5  
```  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式使用 SELECT (而非 SET) 進行變數指派時，可取得同樣的結果：  
  
```  
DECLARE @PointValue Point;  
SELECT @PointValue = PointValue FROM dbo.Points  
    WHERE ID = 2;  
SELECT @PointValue.ToString() AS PointValue;  
```  
  
 使用 SELECT 與 SET 進行變數指派的差異在於，SELECT 可讓您在一個 SELECT 陳述式中指派多個變數，而 SET 語法要求每個變數指派都具有自己的 SET 陳述式。  
  
## <a name="comparing-data"></a>比較資料  
 定義類別時如果已將 `IsByteOrdered` 屬性設為 `true`，則可使用比較運算子比較 UDT 中的值。 如需詳細資訊，請參閱[建立使用者定義型](creating-user-defined-types.md)別。  
  
```  
SELECT ID, PointValue.ToString() AS Points   
FROM dbo.Points  
WHERE PointValue > CONVERT(Point, '2,2');  
```  
  
 如果值本身可比較，則可以比較 UDT 的內部值，無論 `IsByteOrdered` 設定為何。 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式選取 X 大於 Y 的資料列：  
  
```  
SELECT ID, PointValue.ToString() AS PointValue   
FROM dbo.Points  
WHERE PointValue.X < PointValue.Y;  
```  
  
 如這個搜尋相符 PointValue 的查詢所示，您還可以將變數與比較運算子搭配使用。  
  
```  
DECLARE @ComparePoint Point;  
SET @ComparePoint = CONVERT(Point, '3,4');  
SELECT ID, PointValue.ToString() AS MatchingPoint   
FROM dbo.Points  
WHERE PointValue = @ComparePoint;  
```  
  
## <a name="invoking-udt-methods"></a>叫用 UDT 方法  
 您也可在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中叫用 UDT 中定義的方法。 **Point**類別包含三個方法： `Distance` 、 `DistanceFrom` 和 `DistanceFromXY` 。 如需定義這三種方法的程式代碼清單，請參閱[編碼使用者定義類型](creating-user-defined-types-coding.md)。  
  
 下列的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式會呼叫 `PointValue.Distance` 方法：  
  
```  
SELECT ID, PointValue.X AS [Point.X],   
    PointValue.Y AS [Point.Y],  
    PointValue.Distance() AS DistanceFromZero   
FROM dbo.Points;  
```  
  
 結果會顯示在資料 `Distance` 行中：  
  
```  
IDXYDistance  
------------------------  
1345  
2155.09901951359278  
319999.0050503762308  
```  
  
 `DistanceFrom`方法接受**Point**資料類型的引數，並顯示從指定點到 PointValue 的距離：  
  
```  
SELECT ID, PointValue.ToString() AS Pnt,  
   PointValue.DistanceFrom(CONVERT(Point, '1,99')) AS DistanceFromPoint  
FROM dbo.Points;  
```  
  
 結果顯示資料表中每個資料列之 `DistanceFrom` 方法的結果：  
  
```  
ID PntDistanceFromPoint  
---------------------  
13,495.0210502993942  
21,594  
31,990  
```  
  
 `DistanceFromXY` 方法將個別點視為引數：  
  
```  
SELECT ID, PointValue.X as X, PointValue.Y as Y,   
PointValue.DistanceFromXY(1, 99) AS DistanceFromXY   
FROM dbo.Points  
```  
  
 結果集與 `DistanceFrom` 方法相同。  
  
## <a name="updating-data-in-a-udt-column"></a>更新 UDT 資料行中的資料  
 若要更新 UDT 資料行中的資料，請使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE 陳述式。 您還可以使用 UDT 的方法，以更新物件的狀態。 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式會更新資料表中的單一資料列：  
  
```  
UPDATE dbo.Points  
SET PointValue = CAST('1,88' AS Point)  
WHERE ID = 3  
```  
  
 您也可個別更新 UDT 項目。 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式僅更新 Y 座標：  
  
```  
UPDATE dbo.Points  
SET PointValue.Y = 99  
WHERE ID = 3  
```  
  
 如果已定義位元組順序的 UDT 設為 `true`，則 [!INCLUDE[tsql](../../includes/tsql-md.md)] 可以評估 WHERE 子句中的 UDT 資料行。  
  
```  
UPDATE dbo.Points  
SET PointValue = '4,5'  
WHERE PointValue = '3,4';  
```  
  
### <a name="updating-limitations"></a>更新限制  
 不可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 一次更新多個屬性。 例如，下列 UPDATE 陳述式失敗並發生錯誤，因為同一資料行名稱不可在一個 UPDATE 陳述式中使用兩次。  
  
```  
UPDATE dbo.Points  
SET PointValue.X = 5, PointValue.Y = 99  
WHERE ID = 3  
```  
  
 若要個別更新每個點，您需要在 Point UDT 組件中建立 Mutator 方法。 然後，可以叫用 Mutator 方法，以更新 [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE 陳述式中的物件，如下所示：  
  
```  
UPDATE dbo.Points  
SET PointValue.SetXY(5, 99)  
WHERE ID = 3  
```  
  
## <a name="deleting-data-in-a-udt-column"></a>刪除 UDT 資料行中的資料  
 若要刪除 UDT 中的資料，請使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] DELETE 陳述式。 下列陳述式會刪除資料表中符合 WHERE 子句中所指定準則的所有資料列。 如果在 DELETE 陳述式中省略 WHERE 子句，將刪除資料表中的所有資料列。  
  
```  
DELETE FROM dbo.Points  
WHERE PointValue = CAST('1,99' AS Point)  
```  
  
 若要移除 UDT 資料行中的值，同時又不變更其他資料列值，請使用 UPDATE 陳述式。 此範例將 PointValue 設為 Null。  
  
```  
UPDATE dbo.Points  
SET PointValue = null  
WHERE ID = 2  
```  
  
## <a name="see-also"></a>另請參閱  
 [在 SQL Server 中使用使用者定義型別](working-with-user-defined-types-in-sql-server.md)  
  
  
