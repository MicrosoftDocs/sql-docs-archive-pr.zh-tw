---
title: SQL Server 2014 中資料庫引擎功能的行為變更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- behavior changes [SQL Server]
- Database Engine [SQL Server], what's new
- Transact-SQL behavior changes
ms.assetid: 65eaafa1-9e06-4264-b547-cbee8013c995
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 9072b851f3512113b23dedc91f8c9b7151136a57
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87700240"
---
# <a name="behavior-changes-to-database-engine-features-in-sql-server-2014"></a>SQL Server 2014 中對於 Database Engine 功能的行為變更
  本主題描述 [!INCLUDE[ssDE](../includes/ssde-md.md)] 中的行為變更。 行為變更會影響 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 功能的運作或互動方式 (相較於舊版的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)])。  
  
## <a name="behavior-changes-in-sssql14"></a><a name="SQL14"></a>中的行為變更[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 在舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，針對包含超過特定長度 (超過 4020 個字元) 之字串的 XML 文件進行查詢，可能會傳回不正確的結果。 在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中，這類查詢會傳回正確的結果。  
  
## <a name="behavior-changes-in-sssql11"></a><a name="Denali"></a>中的行為變更[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="metadata-discovery"></a>中繼資料探索  
 中的改良功能， [!INCLUDE[ssDE](../includes/ssde-md.md)] [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 可讓 SQLDescribeCol 取得比舊版中的 SQLDescribeCol 所傳回的預期結果更精確的描述 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱[中繼資料探索](../relational-databases/native-client/features/metadata-discovery.md)。  
  
 用來判斷回應格式而不實際執行查詢的[SET set fmtonly](/sql/t-sql/statements/set-fmtonly-transact-sql)選項，會取代為[sp_describe_first_result_set &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql)、 [sp_describe_undeclared_parameters &#40;](/sql/relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql)transact-sql&#41;，以及[dm_exec_describe_first_result_set &#40;transact-sql ](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql)&#41;[中 dm_exec_describe_first_result_set_for_object](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql)的 transact-sql &#40;。  
  
### <a name="changes-to-behavior-in-scripting-a-sql-server-agent-task"></a>編寫 SQL Server Agent 工作之指令碼時的行為變更  
從開始 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] ，如果您從現有作業複製腳本來建立新作業，新的作業可能會不小心影響現有的作業。 若要使用現有作業中的腳本建立新作業，請手動刪除參數* \@ schedule_uid*這通常是在現有作業中建立作業排程之區段的最後一個參數。 這將會為新的作業建立新的獨立排程，而不會影響現有的作業。  
  
### <a name="constant-folding-for-clr-user-defined-functions-and-methods"></a>CLR 使用者定義函數和方法的常數摺疊  
從開始 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] ，下列使用者定義的 CLR 物件現在可以折迭：  

-   具決定性、純量值的 CLR 使用者定義函數。  
-   CLR 使用者定義類型的具決定性方法。  
  
 此改進旨在於這些函數或方法都使用相同的引數多次呼叫時提高效能。 但在不具決定性函數或方法因誤標記為具決定性時，此變更可能會導致非預期的結果。 CLR 函數或方法的決定性是由 `IsDeterministic` 或 `SqlFunctionAttribute` 的 `SqlMethodAttribute` 屬性值所指出。  
  
### <a name="behavior-of-stenvelope-method-has-changed-with-empty-spatial-types"></a>空白空間類型之 STEnvelope() 方法的行為已變更  
 具有空白物件之 `STEnvelope` 方法的行為現在與其他 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 空間方法的行為一致。  
  
 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中，以空白物件呼叫 `STEnvelope` 方法時，此方法傳回下列結果：  
  
```sql  
SELECT geometry::Parse('POINT EMPTY').STEnvelope().ToString()  
-- returns POINT EMPTY  
SELECT geometry::Parse('LINESTRING EMPTY').STEnvelope().ToString()  
-- returns LINESTRING EMPTY  
SELECT geometry::Parse('POLYGON EMPTY').STEnvelope().ToString()  
-- returns POLYGON EMPTY  
```  
  
 在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中，以空白物件呼叫 `STEnvelope` 方法時，此方法現在傳回下列結果：  
  
```sql  
SELECT geometry::Parse('POINT EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
SELECT geometry::Parse('LINESTRING EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
SELECT geometry::Parse('POLYGON EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
```  
  
 若要判斷空間物件是否為空白，請呼叫[STIsEmpty &#40;Geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stisempty-geometry-data-type)方法。  
  
### <a name="log-function-has-new-optional-parameter"></a>LOG 函數有新的選擇性參數  
 `LOG`函數現在有選擇性的*基底*參數。 如需詳細資訊，請參閱[LOG &#40;transact-sql&#41;](/sql/t-sql/functions/log-transact-sql)。  
  
### <a name="statistics-computation-during-partitioned-index-operations-has-changed"></a>分割區索引作業期間的統計資料計算已變更  
 並不會在建立或重建分割區索引之後掃描資料表中所有的資料列建立統計資料。 反之，查詢最佳化工具會使用預設的取樣演算法來產生統計資料。 升級具有分割區索引的資料庫之後，可能會注意到這些索引之長條圖資料的差異。 此行為變更可能不會影響查詢效能。 若要在掃描資料表中所有資料列時取得分割區索引的統計資料，使用子句 `FULLSCAN` 時請使用 `CREATE STATISTICS` 或 `UPDATE STATISTICS`。  
  
### <a name="data-type-conversion-by-the-xml-value-method-has-changed"></a>XML value 方法的資料類型轉換已變更  
資料類型之 方法的內部行為已變更。 此方法會針對 XML 執行 XQuery 並傳回指定之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料類型的純量值。 xs 類型必須轉換為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料類型。 以前 `value` 方法會在內部將來源值轉換為 xs:string，然後將 xs:string 轉換為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料類型。 在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中，下列情況下會略過 xs:string 的轉換：  
  
|來源 XS 資料類型|目的地 SQL Server 資料類型|  
|-------------------------|--------------------------------------|  
|byte<br /><br /> short<br /><br /> int<br /><br /> integer<br /><br /> long<br /><br /> unsignedByte<br /><br /> unsignedShort<br /><br /> unsignedInt<br /><br /> unsignedLong<br /><br /> positiveInteger<br /><br /> nonPositiveInteger<br /><br /> negativeInteger<br /><br /> nonNegativeInteger|TINYINT<br /><br /> SMALLINT<br /><br /> int<br /><br /> BIGINT<br /><br /> decimal<br /><br /> NUMERIC|  
|decimal|decimal<br /><br /> NUMERIC|  
|FLOAT|real|  
|double|FLOAT|  
  
 可以略過中繼轉換時，新行為會提高效能。 但在資料類型轉換失敗時，您會看到不同於從中繼 xs:string 值轉換時所引發的錯誤訊息。 例如，如果 value 方法無法將 `int` 值 100000 轉換為 `smallint`，以前的錯誤訊息是：  
  
 `The conversion of the nvarchar value '100000' overflowed an INT2 column. Use a larger integer column.`  
  
 在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]，如果沒有 xs:string 的中繼轉換，錯誤訊息是：  
  
 `Arithmetic overflow error converting expression to data type smallint.`  
  
### <a name="sqlcmdexe-behavior-change-in-xml-mode"></a>XML 模式中的 sqlcmd.exe 行為變更  
 如果您在執行 SELECT * from T FOR XML ... 時，在命令) 上使用 sqlcmd.exe 搭配 XML 模式 (： XML，則會有行為變更。  
  
### <a name="dbcc-checkident-revised-message"></a>DBCC CHECKIDENT 修訂的訊息  
 在中 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] ，DBCC CHECKIDENT 命令所傳回的訊息只有在與重新植入*new_reseed_value*變更目前的識別值一起使用時才會變更。 新訊息是「*正在檢查識別資訊：目前的識別值 ' \<current identity value> '*」。 DBCC 的執行已經完成。 如果 DBCC 印出錯誤訊息，請連絡您的系統管理員」。  
  
 在舊版中，訊息是「*正在檢查識別資訊：目前的識別值 ' \<current identity value> '，目前的資料行值 ' \<current column value> '。DBCC 執行已完成。如果 DBCC 印出錯誤訊息，請洽詢您的系統管理員。* 」 當 `DBCC CHECKIDENT` 指定了 `NORESEED` 、但沒有第二個參數，或沒有重新植入值時，訊息會原封不動。 如需詳細資訊，請參閱 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql)。  
  
### <a name="behavior-of-exist-function-on-xml-datatype-has-changed"></a>XML 資料類型上之 exist() 函數的行為已變更  
 將 `exist()` 具有 null 值的 XML 資料類型與 0 (零) 進行比較時，函數的行為已變更。 請考慮下列範例：  
  
```sql  
DECLARE @test XML;  
SET @test = null;  
SELECT COUNT(1) WHERE @test.exist('/dogs') = 0;  
```  
  
 在舊版中，此比較傳回 1 (true)；現在，此比較傳回 0 (零，false)。  
  
 下列比較尚未變更：  
  
```sql  
DECLARE @test XML;  
SET @test = null;  
SELECT COUNT(1) WHERE @test.exist('/dogs') = 1; -- 0 expected, 0 returned  
SELECT COUNT(1) WHERE @test.exist('/dogs') IS NULL; -- 1 expected, 1 returned  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 中資料庫引擎功能的重大變更](breaking-changes-to-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2014 中已淘汰的資料庫引擎功能](deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2014 中已停止的資料庫引擎功能](discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
