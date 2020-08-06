---
title: SQLSetStmtAttr |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSetStmtAttr function
ms.assetid: 799c80fd-c561-4912-8562-9229076dfd19
author: rothja
ms.author: jroth
ms.openlocfilehash: 725a7917f817af44f17f8da06d484171cbe9a25d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595964"
---
# <a name="sqlsetstmtattr"></a>SQLSetStmtAttr
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式不支援混合式 (索引鍵集/動態) 資料指標模型。 如果設定的值不等於 0，使用 SQL_ATTR_KEYSET_SIZE 設定索引鍵值大小的嘗試將會失敗。  
  
 應用程式會在所有語句上設定 SQL_ATTR_ROW_ARRAY_SIZE，以宣告**SQLFetch**或[SQLFetchScroll](sqlfetchscroll.md)函式呼叫所傳回的資料列數目。 在表示伺服器資料指標的陳述式上，驅動程式會使用 SQL_ATTR_ROW_ARRAY_SIZE 決定伺服器所產生之資料列區塊的大小以滿足來自資料指標的提取要求。 在動態資料指標的區塊大小內，如果交易隔離等級足以確保可重複讀取已認可的交易，資料列成員資格與排序是固定的。 在此值指出的區塊之外，資料指標是完全動態的。 伺服器資料指標區塊大小是完全動態的，而且可以在提取處理的任何點變更。  
  
## <a name="sqlsetstmtattr-and-table-valued-parameters"></a>SQLSetStmtAttr 和資料表值參數  
 SQLSetStmtAttr 可以用來設定應用程式參數描述元中的 SQL_SOPT_SS_PARAM_FOCUS (APD) ，然後再存取資料表值參數資料行的描述項欄位。  
  
 如果嘗試將 SQL_SOPT_SS_PARAM_FOCUS 設定為不是資料表值參數之參數的序數，則 SQLSetStmtAttr 會傳回 SQL_ERROR 並使用 SQLSTATE = HY024 和訊息「不正確屬性值」來建立診斷記錄。 當傳回 SQL_ERROR 時，SQL_SOPT_SS_PARAM_FOCUS 不會變更。  
  
 將 SQL_SOPT_SS_PARAM_FOCUS 設定為 0 會還原參數之描述項記錄的存取權。  
  
 SQLSetStmtAttr 也可以用來設定 SQL_SOPT_SS_NAME_SCOPE。 如需詳細資訊，請參閱本主題稍後的「SQL_SOPT_SS_NAME_SCOPE」一節。  
  
 如需詳細資訊，請參閱備妥之[語句的資料表值參數中繼資料](../native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)。  
  
 如需資料表值參數的詳細資訊，請參閱[ODBC&#41;&#40;的資料表值參數](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlsetstmtattr-support-for-sparse-columns"></a>疏鬆資料行的 SQLSetStmtAttr 支援  
 SQLSetStmtAttr 可以用來設定 SQL_SOPT_SS_NAME_SCOPE。 如需詳細資訊，請參閱本主題稍後的 SQL_SOPT_SS_NAME_SCOPE 一節。如需稀疏資料行的詳細資訊，請參閱[&#40;ODBC&#41;的稀疏資料行支援](../native-client/odbc/sparse-columns-support-odbc.md)。  
  
## <a name="statement-attributes"></a>陳述式屬性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式也支援下列驅動程式專屬的陳述式屬性。  
  
### <a name="sql_sopt_ss_cursor_options"></a>SQL_SOPT_SS_CURSOR_OPTIONS  
 SQL_SOPT_SS_CURSOR 屬性會指定驅動程式是否會在資料指標上使用驅動程式專屬的效能選項。 設定這些選項時，不允許[SQLGetData](sqlgetdata.md) 。 預設值為 SQL_CO_OFF。 *Valueptr 是*值的類型是 SQLLEN。  
  
|*Valueptr 是*值|描述|  
|----------------------|-----------------|  
|SQL_CO_OFF|預設值： 停用快速順向、唯讀資料指標和自動擷取，可讓您在順向、唯讀資料指標上**SQLGetData** 。 當 SQL_SOPT_SS_CURSOR_OPTIONS 設定為 SQL_CO_OFF 時，資料指標類型將不會變更。 也就是說，快速順向資料指標仍是快速順向資料指標。 若要變更資料指標類型，應用程式現在必須使用/SQL_ATTR_CURSOR_TYPE 設定不同的資料指標類型 `SQLSetStmtAttr` 。|  
|SQL_CO_FFO|啟用快速順向、唯讀資料指標，在順向、唯讀資料指標上停用**SQLGetData** 。|  
|SQL_CO_AF|在任何資料指標類型上啟用自動擷取選項。 當針對語句控制碼設定此選項時， **SQLExecute**或**SQLExecDirect**會產生隱含的**SQLFetchScroll** (SQL_FIRST) 。 資料指標會開啟，而且第一個批次的資料列會在伺服器的單一往返中傳回。|  
|SQL_CO_FFO_AF|使用自動擷取選項啟用快速順向資料指標。 這在同時指定 SQL_CO_AF 和 SQL_CO_FFO 時相同。|  
  
 設定這些選項時，如果伺服器偵測到已經提取最後一個資料列，則會自動關閉資料指標。 應用程式仍然必須呼叫[SQLFreeStmt](sqlfreestmt.md) (SQL_CLOSE) 或[SQLCloseCursor](sqlclosecursor.md)，但驅動程式不需要將關閉通知傳送至伺服器。  
  
 如果選取清單包含**text**、 **Ntext**或**image**資料行，則快速順向資料指標會轉換成動態資料指標，並允許**SQLGetData** 。  
  
### <a name="sql_sopt_ss_defer_prepare"></a>SQL_SOPT_SS_DEFER_PREPARE  
 SQL_SOPT_SS_DEFER_PREPARE 屬性會決定是否要立即準備或延後語句，直到執行**SQLExecute**、 [SQLDescribeCol](sqldescribecol.md)或[SQLDescribeParam](sqldescribeparam.md)為止。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 和先前版本中，會忽略此屬性 (沒有延遲準備)。 *Valueptr 是*值的類型是 SQLLEN。  
  
|*Valueptr 是*值|描述|  
|----------------------|-----------------|  
|SQL_DP_ON|預設值： 呼叫[SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360)函式之後，將會延遲語句準備，直到呼叫**SQLExecute**或中繼屬性作業 (**SQLDescribeCol**或**SQLDescribeParam**) 執行為止。|  
|SQL_DP_OFF|一旦執行**SQLPrepare** ，就會準備語句。|  
  
### <a name="sql_sopt_ss_regionalize"></a>SQL_SOPT_SS_REGIONALIZE  
 SQL_SOPT_SS_REGIONALIZE 屬性用於決定陳述式層級的資料轉換。 將日期、時間和貨幣值轉換為字元字串時，此屬性會使驅動程式遵從用戶端的地區設定。 此轉換僅能從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生資料類型轉換成字元字串。  
  
 *Valueptr 是*值的類型是 SQLLEN。  
  
|*Valueptr 是*值|描述|  
|----------------------|-----------------|  
|SQL_RE_OFF|預設值： 此驅動程式不會使用用戶端地區設定，將日期、時間和貨幣資料轉換成字元字串資料。|  
|SQL_RE_ON|將日期、時間和貨幣資料轉換成字元字串資料時，此驅動程式會使用用戶端地區設定。|  
  
 地區轉換設定適用於貨幣、數值、日期和時間資料類型。 此轉換設定只有在貨幣、數值、日期或時間值轉換為字元字串時，才會套用到輸出轉換。  
  
> [!NOTE]  
>  當 SQL_SOPT_SS_REGIONALIZE 陳述式選項開啟時，驅動程式會針對目前的使用者使用地區設定的登錄設定。 如果應用程式是透過呼叫**SetThreadLocale**，則驅動程式不接受目前線程的地區設定。  
  
 變更資料來源的地區行為可能會導致應用程式失敗。 剖析日期字串並預期日期字串如 ODBC 定義之方式顯示的應用程式，可能會受到變更此值的負面影響。  
  
### <a name="sql_sopt_ss_textptr_logging"></a>SQL_SOPT_SS_TEXTPTR_LOGGING  
 SQL_SOPT_SS_TEXTPTR_LOGGING 屬性會在包含**文字**或**影像**資料的資料行上，切換作業的記錄。 *Valueptr 是*值的類型是 SQLLEN。  
  
|*Valueptr 是*值|描述|  
|----------------------|-----------------|  
|SQL_TL_OFF|停用在**文字**和**影像**資料上執行之作業的記錄。|  
|SQL_TL_ON|預設值： 啟用在**文字**和**影像**資料上執行之作業的記錄。|  
  
### <a name="sql_sopt_ss_hidden_columns"></a>SQL_SOPT_SS_HIDDEN_COLUMNS  
 SQL_SOPT_SS_HIDDEN_COLUMNS 屬性會在結果集中公開 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SELECT FOR BROWSE 陳述式內隱藏的資料行。 此驅動程式預設不會公開這些資料行。 *Valueptr 是*值的類型是 SQLLEN。  
  
|*Valueptr 是*值|描述|  
|----------------------|-----------------|  
|SQL_HC_OFF|預設值： FOR BROWSE 資料行會從結果集隱藏起來。|  
|SQL_HC_ON|公開 FOR BROWSE 資料行。|  
  
### <a name="sql_sopt_ss_querynotification_msgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 屬性會傳回查詢通知要求的訊息文字。  
  
### <a name="sql_sopt_ss_querynotification_options"></a>SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
 SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS 屬性會指定用於查詢通知要求的選項。 這些是使用 `name=value` 語法在字串中指定，如下所示。 應用程式會負責建立此服務以及在佇列外部讀取通知。  
  
 查詢通知選項字串的語法為：  
  
 `service=<service-name>[;(local database=<database>|broker instance=<broker instance>)]`  
  
 例如：  
  
 `service=mySSBService;local database=mydb`  
  
### <a name="sql_sopt_ss_querynotification_timeout"></a>SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
 SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT 屬性會指定查詢通知維持作用中的秒數。 預設值是 432000 秒 (5 天)。 *Valueptr 是*值的類型是 SQLLEN。  
  
### <a name="sql_sopt_ss_param_focus"></a>SQL_SOPT_SS_PARAM_FOCUS  
 SQL_SOPT_SS_PARAM_FOCUS 屬性會指定後續 SQLBindParameter、SQLGetDescField、SQLSetDescField、SQLGetDescRec 和 SQLSetDescRec 呼叫的焦點。  
  
 SQL_SOPT_SS_PARAM_FOCUS 的類型是 SQLULEN。  
  
 預設值為 0，表示這些呼叫處理的參數會對應到 SQL 陳述式中的參數標記。 設定為資料表值參數的參數號碼時，這些呼叫會處理該資料表值參數的資料行。 設定為非資料表值參數之參數號碼的值時，這些呼叫會傳回錯誤 IM020：「參數焦點沒有參考資料表值參數」。  
  
### <a name="sql_sopt_ss_name_scope"></a>SQL_SOPT_SS_NAME_SCOPE  
 SQL_SOPT_SS_NAME_SCOPE 屬性會指定後續目錄函數呼叫的名稱範圍。 SQLColumns 所傳回的結果集會根據 SQL_SOPT_SS_NAME_SCOPE 的設定而定。  
  
 SQL_SOPT_SS_NAME_SCOPE 的類型是 SQLULEN。  
  
|*Valueptr 是*值|描述|  
|----------------------|-----------------|  
|SQL_SS_NAME_SCOPE_TABLE|預設值：<br /><br /> 使用資料表值參數時，指出應該傳回實際資料表的中繼資料。<br /><br /> 使用「稀疏資料行」功能時，SQLColumns 只會傳回不是 sparse 成員的資料行 `column_set` 。|  
|SQL_SS_NAME_SCOPE_TABLE_TYPE|表示應用程式需要資料表類型 (而非實際資料表) 的中繼資料 (目錄函數應該傳回資料表類型的中繼資料)。 然後，應用程式會傳遞資料表值參數的 TYPE_NAME 做為*TableName*參數。|  
|SQL_SS_NAME_SCOPE_EXTENDED|使用「稀疏資料行」功能時，SQLColumns 會傳回所有資料行，而不論 `column_set` 成員資格為何。|  
|SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET|使用「稀疏資料行」功能時，SQLColumns 只會傳回屬於 sparse 成員的資料行 `column_set` 。|  
|SQL_SS_NAME_SCOPE_DEFAULT|等於 SQL_SS_NAME_SCOPE_TABLE。|  
  
 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 分別與*CatalogName*和*SchemaName*參數搭配使用，以識別資料表值參數的目錄和架構。 當應用程式完成擷取資料表值參數的中繼資料時，必須將 SQL_SOPT_SS_NAME_SCOPE 社回 SQL_SS_NAME_SCOPE_TABLE 的預設值。  
  
 當 SQL_SOPT_SS_NAME_SCOPE 設定為 SQL_SS_NAME_SCOPE_TABLE 時，連結伺服器的查詢會失敗。 使用包含伺服器元件的目錄呼叫 SQLColumns 或 SQLPrimaryKeys 將會失敗。  
  
 如果嘗試將 SQL_SOPT_SS_NAME_SCOPE 設定為無效值，會傳回 SQL_ERROR，並產生包含 SQLSTATE HY024 與「屬性值無效」訊息的診斷記錄。  
  
 如果 SQL_SOPT_SS_NAME_SCOPE 具有 SQL_SS_NAME_SCOPE_TABLE 以外的值，則會呼叫其他 then SQLTables、SQLColumns 或 SQLPrimaryKeys 的目錄函式，SQL_ERROR 傳回。 此時會產生包含 SQLSTATE HY010 與「函數順序錯誤 (SQL_SOPT_SS_NAME_SCOPE 未設定為 SQL_SS_NAME_SCOPE_TABLE)」訊息的診斷記錄。  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetStmtAttr 函式](https://go.microsoft.com/fwlink/?LinkId=59355)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
