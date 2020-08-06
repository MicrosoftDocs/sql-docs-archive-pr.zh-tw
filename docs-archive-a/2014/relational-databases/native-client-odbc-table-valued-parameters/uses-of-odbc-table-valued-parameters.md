---
title: 使用 ODBC 資料表值參數 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), scenarios
- ODBC, table-valued parameters
ms.assetid: f1b73932-4570-4a8a-baa0-0f229d9c32ee
author: rothja
ms.author: jroth
ms.openlocfilehash: 2b128246f7c4ed9a9cec5e28698c743877f9873d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708246"
---
# <a name="uses-of-odbc-table-valued-parameters"></a>使用 ODBC 資料表值參數
  本主題將討論搭配 ODBC 使用資料表值參數的主要使用者案例：  
  
-   完整繫結多資料列緩衝區之下的資料表值參數 (使用記憶體中的所有值，將資料當做 TVP 傳送)  
  
-   以資料流方式傳送資料列的資料表值參數 (使用資料執行中，將資料當做 TVP 傳送)  
  
-   從系統目錄擷取資料表值參數中繼資料  
  
-   針對準備好的陳述式擷取資料表值參數中繼資料  
  
## <a name="table-valued-parameter-with-fully-bound-multirow-buffers-send-data-as-a-tvp-with-all-values-in-memory"></a>完整繫結多資料列緩衝區之下的資料表值參數 (使用記憶體中的所有值，將資料當做 TVP 傳送)  
 當搭配完整繫結的多資料列緩衝區使用時，記憶體中將提供所有參數值。 例如，這對於 OLTP 交易而言就是典型的情況，在這類交易中，資料表值參數可以封裝到單一預存程序中。 如果沒有資料表值參數，這會牽涉到動態產生複雜的多重陳述式批次，或是對伺服器進行多次呼叫。  
  
 資料表值參數本身會使用[SQLBindParameter](https://go.microsoft.com/fwlink/?LinkId=59328)和其他參數來系結。 所有參數都已系結之後，應用程式會在每個資料表值參數上設定參數焦點屬性 SQL_SOPT_SS_PARAM_FOCUS，並針對資料表值參數的資料行呼叫 SQLBindParameter。  
  
 資料表值參數的伺服器類型是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所特有的新類型 SQL_SS_TABLE。 SQL_SS_TABLE 的繫結 C 類型一定必須是 SQL_C_DEFAULT。 資料表值參數繫結的參數不會傳送任何資料；它是用來傳遞資料表中繼資料，以及控制要如何傳遞資料表值參數之組成資料行中的資料。  
  
 資料表值參數的長度會設定為傳送給伺服器的資料列數。 資料表值參數的 SQLBindParameter 的*ColumnSize*參數會指定可以傳送的最大資料列數;這是資料行緩衝區的陣列大小。 *ParameterValuePtr*是參數緩衝區，適用于 SQLBindParameter 中的資料表值參數。 *ParameterValuePtr*及其相關聯的*BufferLength*會在需要時用來傳遞資料表值參數的類型名稱。 此類型名稱不是預存程序呼叫所需，但為 SQL 陳述式所需。  
  
 當資料表值參數類型名稱是在呼叫 SQLBindParameter 時指定時，一定要將它指定為 Unicode 值，即使在以 ANSI 應用程式形式建立的應用程式中也是如此。 當您使用 SQLSetDescField 指定資料表值參數類型名稱時，可以使用符合應用程式建立方式的常值。 ODBC 驅動程式管理員將會執行所有必要的 Unicode 轉換。  
  
 您可以使用 SQLGetDescRec、SQLSetDescRec、SQLGetDescField 和 SQLSetDescField，個別且明確地運算元據表值參數和資料表值參數資料行的中繼資料。 不過，多載 SQLBindParameter 通常更方便，而且在大部分情況下都不需要明確的描述項存取。 這種方法與其他資料類型的 SQLBindParameter 定義一致，不同之處在于，針對資料表值參數，受影響的描述項欄位會稍有不同。  
  
 有時應用程式會搭配動態 SQL 使用資料表值參數，而且必須提供此資料表值參數的類型名稱。 如果是這種情況，而且目前的連接預設架構中未定義資料表值參數，SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME 就必須使用 SQLSetDescField 來設定。 因為資料表類型定義和資料表值參數必須在相同的資料庫中，所以如果應用程式使用資料表值參數，就不能設定 SQL_CA_SS_TYPE_CATALOG_NAME。 否則，SQLSetDescField 會報告錯誤。  
  
 此案例的範例程式碼位於 `demo_fixed_TVP_binding` [使用資料表值參數 &#40;ODBC&#41;](../native-client-odbc-how-to/use-table-valued-parameters-odbc.md)中。  
  
## <a name="table-valued-parameter-with-row-streaming-send-data-as-a-tvp-using-data-at-execution"></a>以資料流方式傳送資料列的資料表值參數 (使用資料執行中，將資料當做 TVP 傳送)  
 在此案例中，應用程式會在要求時提供資料列給驅動程式，然後以資料流方式將資料列傳送給伺服器。 如此就不需要在記憶體中緩衝處理所有資料列。 這是大量插入/更新案例的代表。 資料表值參數會提供參數陣列與大量複製之間某一處的效能點。 也就是說，編寫資料表值參數就跟參數陣列一樣輕鬆，但是資料表值參數在伺服器上提供更大的彈性。  
  
 如同上一節「完整繫結多資料列緩衝區之下的資料表值參數」所討論，資料表值參數和它的資料行會繫結在一起，但是資料表值參數本身的長度指標會設定為 SQL_DATA_AT_EXEC。 驅動程式會以一般方式回應資料執行中參數的 SQLExecute 或 SQLExecuteDirect，也就是藉由傳回 SQL_NEED_DATA。 當驅動程式準備好接受資料表值參數的資料時，SQLParamData 會傳回 SQLBindParameter 中的*ParameterValuePtr*值。  
  
 應用程式會使用 SQLPutData 做為資料表值參數，以指出資料表值參數組成資料行的資料可用性。 針對資料表值參數呼叫 SQLPutData 時， *DataPtr*必須一律為 null，而且*StrLen_or_Ind*必須是0或小於或等於為數據表值參數緩衝區指定的陣列大小， (SQLBindParameter) 的*ColumnSize*參數。 0 表示資料表值參數沒有其他資料列，而且此驅動程式將會繼續處理下一個實際程序參數。 當*StrLen_or_Ind*不是0時，驅動程式將會以與非資料表值參數系結參數相同的方式來處理資料表值參數組成資料行：每個資料表值參數資料行都可以指定其實際的資料長度，SQL_Null_DATA，或可以透過其長度/指標緩衝區來指定執行中的資料。 資料表值參數資料行值可透過重複呼叫 SQLPutData 的方式傳遞，如同平常傳遞字元或二進位值時一樣。  
  
 當所有資料表值參數資料行都已經處理過之後，此驅動程式會回到資料表值參數來進一步處理資料表值參數資料的資料列。 因此，如果是資料執行中的資料表值參數，此驅動程式不會遵循一般的繫結參數循序掃描。 系結資料表值參數將會輪詢，直到*StrLen_Or_IndPtr*等於0的 SQLPutData 呼叫為止，此時驅動程式會略過資料表值參數資料行，並移至下一個實際的預存程式參數。  當 SQLPutData 傳遞大於或等於1的指標值時，驅動程式會依序處理資料表值參數資料行和資料列，直到它具有所有系結的資料列和資料行的值為止。 然後此驅動程式會回到資料表值參數。 在從 SQLParamData 接收資料表值參數的 token，並針對資料表值參數呼叫 SQLPutData (hstmt、Null、n) 之間，應用程式必須針對要傳遞至伺服器的下一個或多個資料列，設定資料表值參數組成資料行資料和指標緩衝區內容。  
  
 此案例的範例程式碼位於 `demo_variable_TVP_binding` [使用資料表值參數 &#40;ODBC&#41;](../native-client-odbc-how-to/use-table-valued-parameters-odbc.md)的常式中。  
  
## <a name="retrieving-table-valued-parameter-metadata-from-the-system-catalog"></a>從系統目錄擷取資料表值參數中繼資料  
 當應用程式針對具有資料表值參數參數的程式呼叫 SQLProcedureColumns 時，會以 SQL_SS_TABLE 傳回 DATA_TYPE，而 TYPE_NAME 是資料表值參數之資料表類型的名稱。 SQLProcedureColumns 傳回的結果集中會加入兩個額外的資料行： SS_TYPE_CATALOG_NAME 會傳回定義資料表值參數之資料表類型的目錄名稱，而 SS_TYPE_SCHEMA_NAME 會傳回架構的名稱，其中定義了資料表值參數的資料表類型。 依照 ODBC 規格規定，SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 會出現在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中所加入的所有驅動程式特有資料行之前，以及 ODBC 本身所託管的所有資料行之後。  
  
 新的資料行不但會針對資料表值參數擴展，也會針對 CLR 使用者定義型別參數擴展。 仍然會擴展 UDT 參數現有的結構描述和目錄資料行，但是讓需要的資料類型擁有共同的結構描述和目錄資料行將會簡化未來的應用程式開發過程  (請注意，XML 結構描述集合會有些不同，而且未包含在這項變更中)。  
  
 應用程式會使用 SQLTables 來判斷資料表類型的名稱，其方式與持續性資料表、系統資料表和視圖相同。 新的資料表類型 TABLE TYPE 已經導入，可讓應用程式識別與資料表值參數相關聯的資料表類型。 資料表類型和一般表格會使用不同的命名空間。 這表示，您可以將相同的名稱用於資料表類型和實際資料表。 為了處理這個情況，已經導入了新的陳述式屬性 SQL_SOPT_SS_NAME_SCOPE。 這個屬性會指定以資料表名稱做為參數的 SQLTables 和其他目錄函數是否應將資料表名稱解讀為實際資料表的名稱或資料表類型的名稱。  
  
 應用程式會使用 SQLColumns 來判斷資料表類型的資料行，其方式與針對持續性資料表相同，但必須先設定 SQL_SOPT_SS_NAME_SCOPE，以指出它是使用資料表類型，而不是實際資料表。 SQLPrimaryKeys 也可以搭配資料表類型使用，再次使用 SQL_SOPT_SS_NAME_SCOPE。  
  
 此案例的範例程式碼位於 `demo_metadata_from_catalog_APIs` [使用資料表值參數 &#40;ODBC&#41;](../native-client-odbc-how-to/use-table-valued-parameters-odbc.md)的常式中。  
  
## <a name="retrieving-table-valued-parameter-metadata-for-a-prepared-statement"></a>針對準備好的陳述式擷取資料表值參數中繼資料  
 在此案例中，應用程式會使用 SQLNumParameters 和 SQLDescribeParam 來抓取資料表值參數的中繼資料。  
  
 IPD 欄位 SQL_CA_SS_TYPE_NAME 是用來擷取資料表值參數的類型名稱。 IPD 欄位 SQL_CA_SS_TYPE_SCHEMA_NAME 和 SQL_CA_SS_TYPE_CATALOG_NAME 是分別用來擷取它的目錄和結構描述。  
  
 資料表類型定義和資料表值參數必須在相同的資料庫中。 如果應用程式在使用資料表值參數時設定 SQL_CA_SS_TYPE_CATALOG_NAME，則 SQLSetDescField 會報告錯誤。  
  
 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME 也可以用來擷取與 CLR 使用者定義型別參數相關聯的目錄和結構描述。 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME 是 CLR UDT 類型的現有類型特有之目錄結構描述屬性的替代方式。  
  
 在此情況下，應用程式會使用 SQLColumns 來抓取資料表值參數的資料行中繼資料，因為 SQLDescribeParam 不會傳回資料表值參數資料行的中繼資料。  
  
 此使用案例的範例程式碼位於 `demo_metadata_from_prepared_statement` [使用資料表值參數 &#40;ODBC&#41;](../native-client-odbc-how-to/use-table-valued-parameters-odbc.md)的常式中。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC&#41;&#40;的資料表值參數](table-valued-parameters-odbc.md)  
  
  
