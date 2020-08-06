---
title: 使用巢狀 AUTO 模式查詢產生同層級 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- queries [XML in SQL Server], nested AUTO mode
- nested AUTO mode query
ms.assetid: 748d9899-589d-4420-8048-1258e9e67c20
author: rothja
ms.author: jroth
ms.openlocfilehash: 20362942bdd0f7e7537433b664e5e63461ded499
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87710421"
---
# <a name="generate-siblings-with-a-nested-auto-mode-query"></a>使用巢狀 AUTO 模式查詢產生同層級
  以下範例示範如何使用巢狀 AUTO 模式查詢產生同層級。 其他產生這類 XML 的唯一方式是使用 EXPLICIT 模式。 但是，這可能會相當繁雜。  
  
## <a name="example"></a>範例  
 此查詢會建構提供銷售訂單資訊的 XML。 這包括下列項目：  
  
-   銷售訂單標頭資訊、 `SalesOrderID`、 `SalesPersonID`和 `OrderDate`。 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 會將這些資訊儲存在 `SalesOrderHeader` 資料表中。  
  
-   銷售訂單詳細資訊。 這包括一或多項已訂購的產品、單價及訂購的數量。 此項資訊是儲存在 `SalesOrderDetail` 資料表中。  
  
-   銷售人員資訊。 這是承接訂單的銷售人員。 `SalesPerson` 資料表提供 `SalesPersonID`。 對於此查詢，您必須將此資料表聯結到 `Employee` 資料表，才能找到銷售人員的名稱。  
  
 下述的兩個相異 `SELECT` 查詢會產生外觀上有些許不同的 XML。  
  
 第一個查詢會產生 XML，而 <`SalesPerson`> 及 <`SalesOrderHeader`> 會顯示為 <`SalesOrder`> 的同層級子系：  
  
```  
SELECT   
      (SELECT top 2 SalesOrderID, SalesPersonID, CustomerID,  
         (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
           from Sales.SalesOrderDetail  
            WHERE  SalesOrderDetail.SalesOrderID =   
                   SalesOrderHeader.SalesOrderID  
            FOR XML AUTO, TYPE)  
        FROM  Sales.SalesOrderHeader  
        WHERE SalesOrderHeader.SalesOrderID = SalesOrder.SalesOrderID  
        for xml auto, type),  
        (SELECT *   
         FROM  (SELECT SalesPersonID, EmployeeID  
              FROM Sales.SalesPerson, HumanResources.Employee  
              WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As   
                     SalesPerson  
         WHERE  SalesPerson.SalesPersonID = SalesOrder.SalesPersonID  
       FOR XML AUTO, TYPE)  
FROM (SELECT SalesOrderHeader.SalesOrderID, SalesOrderHeader.SalesPersonID  
      FROM Sales.SalesOrderHeader, Sales.SalesPerson  
      WHERE SalesOrderHeader.SalesPersonID = SalesPerson.SalesPersonID  
     ) as SalesOrder  
ORDER BY SalesOrder.SalesOrderID  
FOR XML AUTO, TYPE  
```  
  
 在上一個查詢中，最外層 `SELECT` 陳述式會執行下列動作：  
  
-   查詢 `SalesOrder` 子句中指定的資料列集 `FROM`。 結果是具有一或多個 <`SalesOrder`> 元素的 XML。  
  
-   指定 `AUTO` 模式和 `TYPE` 指示詞。 `AUTO`模式會將查詢結果轉換為 XML，而指示詞會 `TYPE` 以類型傳回結果 `xml` 。  
  
-   包括以逗號分隔的兩個巢狀 `SELECT` 陳述式。 第一個巢狀 `SELECT` 陳述式會擷取銷售訂單資訊、標頭及詳細資料，而第二個巢狀 `SELECT` 陳述式會擷取銷售人員資訊。  
  
    -   擷取 `SELECT` 、 `SalesOrderID`與 `SalesPersonID`的 `CustomerID` 陳述式本身，包含另一個會傳回銷售訂單詳細資訊的巢狀 `SELECT ... FOR XML` 陳述式 (具有 `AUTO` 模式與 `TYPE` 指示詞)。  
  
 擷取銷售人員資訊的 `SELECT` 陳述式，會查詢以 `SalesPerson`子句建立的資料列集 `FROM` 。 為了要使 `FOR XML` 查詢能夠運作，您必須對以 `FROM` 子句產生的匿名資料列集提供名稱。 在此情況下，提供的名稱為 `SalesPerson`。  
  
 以下是部份結果：  
  
```  
<SalesOrder>  
  <Sales.SalesOrderHeader SalesOrderID="43659" SalesPersonID="279" CustomerID="676">  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="776" OrderQty="1" UnitPrice="2024.9940" />  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="777" OrderQty="3" UnitPrice="2024.9940" />  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="778" OrderQty="1" UnitPrice="2024.9940" />  
  </Sales.SalesOrderHeader>  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</SalesOrder>  
...  
```  
  
 以下查詢會產生相同的銷售訂單資訊，<`SalesPerson`> 在產生的 XML 中還會顯示為 <`SalesOrderDetail`> 的同層級：  
  
```  
<SalesOrder>  
    <SalesOrderHeader ...>  
          <SalesOrderDetail .../>  
          <SalesOrderDetail .../>  
          ...  
          <SalesPerson .../>  
    </SalesOrderHeader>  
  
</SalesOrder>  
<SalesOrder>  
  ...  
</SalesOrder>  
```  
  
 此查詢如下：  
  
```  
SELECT SalesOrderID, SalesPersonID, CustomerID,  
             (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
              from Sales.SalesOrderDetail  
              WHERE SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
              FOR XML AUTO, TYPE),  
              (SELECT *   
               FROM  (SELECT SalesPersonID, EmployeeID  
                    FROM Sales.SalesPerson, HumanResources.Employee  
                    WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
               WHERE  SalesPerson.SalesPersonID = SalesOrderHeader.SalesPersonID  
         FOR XML AUTO, TYPE)  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderID=43659 or SalesOrderID=43660  
FOR XML AUTO, TYPE  
```  
  
 以下是結果：  
  
```  
<Sales.SalesOrderHeader SalesOrderID="43659" SalesPersonID="279" CustomerID="676">  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="776" OrderQty="1" UnitPrice="2024.9940" />  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="777" OrderQty="3" UnitPrice="2024.9940" />  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="778" OrderQty="1" UnitPrice="2024.9940" />  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</Sales.SalesOrderHeader>  
<Sales.SalesOrderHeader SalesOrderID="43660" SalesPersonID="279" CustomerID="117">  
  <Sales.SalesOrderDetail SalesOrderID="43660" ProductID="762" OrderQty="1" UnitPrice="419.4589" />  
  <Sales.SalesOrderDetail SalesOrderID="43660" ProductID="758" OrderQty="1" UnitPrice="874.7940" />  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</Sales.SalesOrderHeader>  
```  
  
 因為 `TYPE` 指示詞會以 `xml` 類型傳回查詢結果，所以您可以使用不同的 `xml` 資料類型方法查詢產生的 XML。 如需詳細資訊，請參閱 [XML 資料類型方法](/sql/t-sql/xml/xml-data-type-methods)。 在下列查詢中，請注意下列項目：  
  
-   先前的查詢已加入 `FROM` 子句中。 查詢結果會以資料表傳回。 請注意新增的 `XmlCol` 別名。  
  
-   `SELECT` 子句會對 `XmlCol` 子句中傳回的 `FROM` 指定 XQuery。 `query()` 資料類型的 `xml` 方法則用來指定 XQuery。 如需詳細資訊，請參閱 [query&#40;&#41; 方法 &#40;xml 資料類型&#41;](/sql/t-sql/xml/query-method-xml-data-type)。  
  
    ```  
    SELECT XmlCol.query('<Root> { /* } </Root>')  
    FROM (  
    SELECT SalesOrderID, SalesPersonID, CustomerID,  
                 (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
                  from Sales.SalesOrderDetail  
                  WHERE SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
                  FOR XML AUTO, TYPE),  
                  (SELECT *   
                   FROM  (SELECT SalesPersonID, EmployeeID  
                        FROM Sales.SalesPerson, HumanResources.Employee  
                        WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
                   WHERE  SalesPerson.SalesPersonID = SalesOrderHeader.SalesPersonID  
             FOR XML AUTO, TYPE)  
    FROM Sales.SalesOrderHeader  
    WHERE SalesOrderID='43659' or SalesOrderID='43660'  
    FOR XML AUTO, TYPE ) as T(XmlCol)  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [使用巢狀 FOR XML 查詢](use-nested-for-xml-queries.md)  
  
  
