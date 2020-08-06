---
title: SQLColumns |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLColumns function
ms.assetid: 69d3af44-8196-43ab-8037-cdd06207b171
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f7acb3dab6a82c5c3cad41191be9ff62a3a3e7e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585377"
---
# <a name="sqlcolumns"></a>SQLColumns
  `SQLColumns`傳回 SQL_SUCCESS *CatalogName*、 *TableName*或*ColumnName*參數的值是否存在。 當這些參數中使用了不正確值時， **SQLFetch**會傳回 SQL_NO_DATA。  
  
> [!NOTE]  
>  若是大數值類型，將會傳回包含 SQL_SS_LENGTH_UNLIMITED 值的所有長度參數。  
  
 `SQLColumns` 可以在靜態伺服器資料指標上執行。 嘗試在可更新的 (動態或索引鍵集) 資料指標上執行 `SQLColumns` 時，將會傳回 SQL_SUCCESS_WITH_INFO，表示資料指標類型已變更。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式藉由接受*CatalogName*參數的兩部分名稱，支援連結伺服器上之資料表的報告資訊： *Linked_Server_Name. Catalog_Name*。  
  
 適用于 ODBC 2。*x*應用程式不在*TableName*中使用萬用字元， `SQLColumns` 會傳回名稱符合*tablename*且由目前使用者擁有之任何資料表的相關資訊。 如果目前使用者沒有任何資料表的名稱符合*tablename*參數，會傳回 `SQLColumns` 其他使用者所擁有的任何資料表的相關資訊，其中資料表名稱符合*tablename*參數。 適用于 ODBC 2。*x*應用程式使用萬用字元，會傳回 `SQLColumns` 名稱符合*TableName*的所有資料表。 適用于 ODBC 3。*x*應用程式會傳回 `SQLColumns` 名稱符合*TableName*的所有資料表，不論擁有者或是否使用萬用字元。  
  
 下表列出結果集傳回的資料行：  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|DATA_TYPE|傳回**VARCHAR (max) **資料類型的 SQL_VARCHAR、SQL_VARBINARY 或 SQL_WVARCHAR。|  
|TYPE_NAME|傳回 Varchar 的 "Varchar"、"Varbinary" 或 "Nvarchar"， ** (max) **、 **Varbinary (max) **和**Nvarchar (max) **資料類型。|  
|COLUMN_SIZE|傳回**Varchar (max) **資料類型的 SQL_SS_LENGTH_UNLIMITED，表示資料行的大小不受限制。|  
|BUFFER_LENGTH|傳回**Varchar (max) **資料類型的 SQL_SS_LENGTH_UNLIMITED，表示緩衝區的大小不受限制。|  
|SQL_DATA_TYPE|傳回**VARCHAR (max) **資料類型的 SQL_VARCHAR、SQL_VARBINARY 或 SQL_WVARCHAR。|  
|CHAR_OCTET_LENGTH|傳回 char 或 binary 資料行的最大長度。 傳回 0 表示大小不受限制。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|傳回定義 XML 結構描述集合名稱所在目錄的名稱。 如果找不到目錄名稱，則此變數包含空字串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|傳回定義 XML 結構描述集合名稱所在結構描述的名稱。 如果找不到結構描述名稱，則此變數包含空字串。|  
|SS_XML_SCHEMACOLLECTION_NAME|傳回 XML 結構描述集合的名稱。 如果找不到名稱，則此變數包含空字串。|  
|SS_UDT_CATALOG_NAME|包含 UDT (使用者定義型別) 之目錄的名稱。|  
|SS_UDT_SCHEMA_NAME|包含 UDT 之結構描述的名稱。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|UDT 的組件完整名稱。|  
  
 若為 Udt，則會使用現有的 TYPE_NAME 資料行來表示 UDT 的名稱。因此，不應該將它的其他資料行加入至 `SQLColumns` 或[SQLProcedureColumns](sqlprocedurecolumns.md)的結果集。 適用於 UDT 資料行或參數的 DATA_TYPE 為 SQL_SS_UDT。  
  
 對於參數的 UDT，如果伺服器傳回或要求此資訊，您可以使用以上定義的新驅動程式專用描述項來取得或設定 UDT 的額外中繼資料屬性。  
  
 當用戶端連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並呼叫 SQLColumns 時，針對目錄輸入參數使用 Null 或萬用字元值，將不會傳回其他目錄的資訊。 系統只會傳回目前目錄的相關資訊。 用戶端可以先呼叫 SQLTables 來判斷所需資料表的所在目錄。 然後，用戶端可以在其對 SQLColumns 的呼叫中，將該目錄值用於目錄輸入參數，以取得該資料表中資料行的相關資訊。  
  
## <a name="sqlcolumns-and-table-valued-parameters"></a>SQLColumns 和資料表值參數  
 SQLColumns 所傳回的結果集會根據 SQL_SOPT_SS_NAME_SCOPE 的設定而定。 如需詳細資訊，請參閱[SQLSetStmtAttr](sqlsetstmtattr.md)。 系統已針對資料表值參數加入下列資料行：  
  
|資料行名稱|資料類型|目錄|  
|-----------------|---------------|--------------|  
|SS_IS_COMPUTED|Smallint|對於 TABLE_TYPE 中的資料行，如果資料行為計算資料行，這是 SQL_TRUE，否則為 SQL_FALSE。|  
|SS_IS_IDENTITY|Smallint|如果資料行是識別資料行，則為 SQL_TRUE，否則為 SQL_FALSE。|  
  
 如需資料表值參數的詳細資訊，請參閱[ODBC&#41;&#40;的資料表值參數](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlcolumns-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLColumns 支援  
 如需日期/時間類型傳回值的相關資訊，請參閱[目錄中繼資料](../native-client-odbc-date-time/metadata-catalog.md)。  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlcolumns-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLColumns 支援  
 `SQLColumns` 支援大型 CLR 使用者定義型別 (UDT)。 如需詳細資訊，請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlcolumns-support-for-sparse-columns"></a>疏鬆資料行的 SQLColumns 支援  
 已將兩個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定資料行加入至 SQLColumns 的結果集：  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|SS_IS_SPARSE|`Smallint`|如果資料行為疏鬆資料行，這是 SQL_TRUE，否則為 SQL_FALSE。|  
|SS_IS_COLUMN_SET|`Smallint`|如果資料行為 `column_set` 資料行，這是 SQL_TRUE，否則為 SQL_FALSE。|  
  
 與 ODBC 規格一致，SS_IS_SPARSE 和 SS_IS_COLUMN_SET 會出現在所有已新增至之前版本的驅動程式特定資料行之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ，以及 odbc 本身所規定的所有資料行之後。  
  
 SQLColumns 所傳回的結果集會根據 SQL_SOPT_SS_NAME_SCOPE 的設定而定。 如需詳細資訊，請參閱[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 如需 ODBC 中的稀疏資料行的詳細資訊，請參閱[&#40;odbc&#41;的稀疏資料行支援](../native-client/odbc/sparse-columns-support-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLColumns 函式](https://go.microsoft.com/fwlink/?LinkId=59336)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
