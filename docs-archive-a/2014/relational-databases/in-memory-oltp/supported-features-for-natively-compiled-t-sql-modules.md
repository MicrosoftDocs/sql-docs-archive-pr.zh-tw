---
title: 原生編譯預存程式中支援的結構 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 05515013-28b5-4ccf-9a54-ae861448945b
author: rothja
ms.author: jroth
ms.openlocfilehash: 65e6e794c5858a68c4b2a9b298513911b487cf52
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606311"
---
# <a name="supported-constructs-in-natively-compiled-stored-procedures"></a>原生編譯的預存程序中支援的建構
  本主題包含原生編譯預存程式支援的功能清單 ([CREATE PROCEDURE &#40;transact-sql&#41;](/sql/t-sql/statements/create-procedure-transact-sql)) ：  
  
-   [原生編譯預存程序的程式設計功能](#pncsp)  
  
-   [支援的運算子](#so)  
  
-   [原生編譯預存程序中的內建函數](#bfncsp)  
  
-   [原生編譯預存程序中的查詢介面區](#qsancsp)  
  
-   [稽核](#auditing)  
  
-   [資料表、查詢和聯結提示](#tqh)  
  
-   [排序的限制](#los)  
  
 如需原生編譯預存程序支援的資料類型資訊，請參閱 [Supported Data Types](supported-data-types-for-in-memory-oltp.md)。  
  
 如需有關不支援之建構的完整資訊，請參閱＜ [Migration Issues for Natively Compiled Stored Procedures](migration-issues-for-natively-compiled-stored-procedures.md)＞。 如需不支援功能的詳細資訊，請參閱 [記憶體中的 OLTP 不支援 Transact-SQL 建構](transact-sql-constructs-not-supported-by-in-memory-oltp.md)。  
  
##  <a name="programmability-in-natively-compiled-stored-procedures"></a><a name="pncsp"></a>原生編譯預存程式中的可程式性  
 支援下列功能：  
  
-   BEGIN ATOMIC (在預存程序的外部層級)、LANGUAGE、ISOLATION LEVEL、DATEFORMAT 和 DATEFIRST。  
  
-   將變數宣告為 NULL 或 NOT NULL。 如果變數宣告為 NOT NULL，宣告必須有初始設定式。 如果變數未宣告為 NOT NULL，初始設定式是選擇性的。  
  
-   IF 和 WHILE  
  
-   INSERT/UPDATE/DELETE  
  
     不支援子查詢。 在 WHERE 或 HAVING 子句，支援 AND 和 BETWEEN，但不支援 OR、NOT 和 IN。  
  
-   記憶體最佳化的資料表類型和資料表變數。  
  
-   RETURN  
  
-   SELECT  
  
-   SET  
  
-   TRY/CATCH/THROW  
  
     若要最佳化效能，整個原生編譯預存程序必須使用單一 TRY/CATCH 區塊。  
  
##  <a name="supported-operators"></a><a name="so"></a> 支援的運算子  
 下列為支援的運算子。  
  
-   [&#40;transact-sql&#41;的比較運算子](/sql/t-sql/language-elements/comparison-operators-transact-sql) (例如， \<, > 如果 <，則在條件) 中支援 >、= 和 (=) 。  
  
-   一元運算子 (+、-)。  
  
-   二元運算子 (*、/、+、-、% (模數) )。  
  
     數字和字串都支援加號運算子 (+)。  
  
-   邏輯運算子 (AND、OR、NOT)。 IF 和 WHILE 陳述式支援 OR 和 NOT，但是 WHERE 或 HAVING 子句則不支援。  
  
-   位元運算子 ~、&、| 和 ^  
  
##  <a name="built-in-functions-in-natively-compiled-stored-procedures"></a><a name="bfncsp"></a>原生編譯預存程式中的內建函數  
 記憶體最佳化資料表上的預設條件約束和原生編譯預存程序中，支援下列函數。  
  
-   數學函數：ACOS、ASIN、ATAN、ATN2、COS、COT、DEGREES、EXP、LOG、LOG10、PI、POWER、RADIANS、RAND、SIN、SQRT、SQUARE 和 TAN  
  
-   日期函數：CURRENT_TIMESTAMP, DATEADD, DATEDIFF, DATEFROMPARTS, DATEPART, DATETIME2FROMPARTS, DATETIMEFROMPARTS, DAY, EOMONTH, GETDATE, GETUTCDATE, MONTH, SMALLDATETIMEFROMPARTS, SYSDATETIME, SYSUTCDATETIME 和 YEAR。  
  
-   字串函數：LEN、LTRIM、RTRIM 和 SUBSTRING  
  
-   Identity 函數：SCOPE_IDENTITY  
  
-   NULL 函式：ISNULL  
  
-   Uniqueidentifier 函式：NEWID 和 NEWSEQUENTIALID  
  
-   錯誤函數：ERROR_LINE、ERROR_MESSAGE、ERROR_NUMBER、ERROR_PROCEDURE、ERROR_SEVERITY 和 ERROR_STATE  
  
-   轉換：CAST 和 CONVERT。 不支援 Unicode 和非 Unicode 字元字串 (n(var)char 和 (var)char) 之間的轉換。  
  
-   系統函式：@@rowcount。 原生編譯預存程序內的陳述式會更新 @@rowcount，您可以在原生編譯預存程序中使用 @@rowcount，來判斷該原生編譯預存程序內最後執行之陳述式所影響的資料列數。 不過，@@rowcount 會在原生編譯預存程序開始及結束執行時重設為 0。  
  
##  <a name="query-surface-area-in-natively-compiled-stored-procedures"></a><a name="qsancsp"></a>原生編譯預存程式中的查詢介面區  
 支援下列功能：  
  
-   BETWEEN  
  
-   資料行名稱別名 (使用 AS 或 = 語法)。  
  
-   只有 SELECT 查詢支援 CROSS JOIN 和 INNER JOIN。  
  
-   選取清單中支援運算式，如果使用支援的運算子，則會在[&#40;transact-sql&#41;子句的位置](/sql/t-sql/queries/where-transact-sql)。 如需目前支援的運算子清單，請參閱 [Supported Operators](#so) 。  
  
-   篩選器述詞 IS [NOT] NULL  
  
-   FROM \<memory optimized table>  
  
-   支援[GROUP BY &#40;transact-sql&#41;](/sql/t-sql/queries/select-group-by-transact-sql) ，以及彙總函式 AVG、COUNT、COUNT_BIG、MIN、MAX 和 SUM。 nvarchar、char、varchar、varchar、varbinary 和 binary 類型不支援 MIN 和 MAX。 如果 ORDER BY 清單中的運算式逐字出現在 GROUP BY 清單中，則[order By 子句 &#40;transact-sql&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql)就會受到[Group by &#40;transact-sql&#41;](/sql/t-sql/queries/select-group-by-transact-sql)的支援。 例如，支援 GROUP BY a + b ORDER BY a + b，但不支援 GROUP BY a, b ORDER BY a + b。  
  
-   HAVING，受限於 WHERE 子句相同的運算式限制。  
  
-   INSERT VALUES (每個陳述式一個資料列) 和 INSERT SELECT  
  
-   排序依據<sup>1</sup>  
  
-   未參考資料行的述詞。  
  
-   SELECT、UPDATE 和 DELETE  
  
-   前<sup>1</sup>名  
  
-   SELECT 清單中的變數指派。  
  
-   WHERE .。。和  
  
 <sup>1</sup>原生編譯的預存程式支援 ORDER BY 和 TOP，但有一些限制：  
  
-   不支援 `DISTINCT` 或 `SELECT` 子句中的 `ORDER BY`。  
  
-   不支援 `WITH TIES` 子句中的 `PERCENT` 或 `TOP`。  
  
-   在 `TOP` 子句中使用常數時，`ORDER BY` 與 `TOP` 結合不可大於 8,192。 如果查詢包含聯結或彙總函數，這個限制可能會降低。 (例如，如果有一個聯結 (兩個資料表)，限制為 4,096 個資料列。 如果使用兩個聯結 (三個資料表)，限制為 2,730 個資料列)。  
  
     您可以在變數中儲存資料列數，以取得大於 8,192 的結果。  
  
    ```sql  
    DECLARE @v INT = 9000  
    SELECT TOP (@v) ... FROM ... ORDER BY ...  
    ```  
  
 不過，與使用變數相較，`TOP` 子句中的常數會產生較好的效能。  
  
 這些限制不適用於記憶體最佳化資料表上解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取。  
  
##  <a name="auditing"></a><a name="auditing"></a> 稽核  
 原生編譯預存程序中支援程序層級稽核。 不支援陳述式層級稽核。  
  
 如需有關稽核的詳細資訊，請參閱＜ [建立伺服器稽核和資料庫稽核規格](../security/auditing/create-a-server-audit-and-database-audit-specification.md)＞。  
  
##  <a name="table-query-and-join-hints"></a><a name="tqh"></a>資料表、查詢和聯結提示  
 支援下列功能：  
  
-   在資料表提示語法或查詢的 [OPTION 子句 &#40;Transact-SQL&#41;](/sql/t-sql/queries/option-clause-transact-sql) 中的 INDEX、FORCESCAN 和 FORCESEEK 提示。  
  
-   FORCE ORDER  
  
-   內部迴圈聯結  
  
-   OPTIMIZE FOR  
  
 如需詳細資訊，請參閱[transact-sql&#41;的提示 &#40;](/sql/t-sql/queries/hints-transact-sql)。  
  
##  <a name="limitations-on-sorting"></a><a name="los"></a> 排序的限制  
 在使用 [TOP &#40;Transact-SQL&#41;](/sql/t-sql/queries/top-transact-sql) 和一個 [ORDER BY 子句 &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql) 的查詢中，您可以排序 8000 多個資料列。 但是沒有 [ORDER BY 子句 &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql)，[TOP &#40;Transact-SQL&#41;](/sql/t-sql/queries/top-transact-sql) 最多只能排序 8000 個資料列 (如果有聯結則資料列更少)。  
  
 如果查詢同時使用 [TOP &#40;Transact-SQL&#41;](/sql/t-sql/queries/top-transact-sql) 運算子和一個 [ORDER BY 子句 &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql)，TOP 運算子最多可以指定 8192 個資料列。 如果您指定超過 8192 個資料列，則會收到錯誤訊息：**訊息 41398，層級 16，狀態 1、程序 *\<procedureName>* ，行 *\<lineNumber>* TOP 運算子可傳回最多 8192 個資料列；要求的數目為 *\<number>* 。**  
  
 如果您沒有 TOP 子句，則可以使用 ORDER BY 排序任意數目的資料列。  
  
 如果您未使用 ORDER BY 子句，則可以使用任何整數值搭配 TOP 運算子。  
  
 使用 TOP N = 8192 的範例：編譯  
  
```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8192 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 使用 TOP N > 8192 的範例：無法編譯。  
  
```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8193 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 8192 資料列限制只適用於 `TOP N` ，其中 `N` 是常數，如前面的範例中所示。  如果您需要讓 `N` 大於 8192，可以將值指派給變數，並使用該變數搭配 `TOP`。  
  
 使用變數的範例：編譯  
  
```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    DECLARE @v int = 8193   
    SELECT TOP (@v) ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 **傳回資料列的限制：** 有兩種情況可能會減少 TOP 運算子能夠傳回的資料列數目：  
  
-   在查詢中使用 JOIN。  JOIN 對限制的影響取決於查詢計劃。  
  
-   使用彙總函式或參考彙總 ORDER BY 子句中的函式。  
  
 計算 TOP N 中最差情況下支援之最大值 N 的公式是： `N = floor ( 65536 / number_of_tables * 8 + total_size+of+aggs )`。  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯的預存程序](natively-compiled-stored-procedures.md)   
 [原生編譯預存程序的移轉問題](migration-issues-for-natively-compiled-stored-procedures.md)  
  
  
