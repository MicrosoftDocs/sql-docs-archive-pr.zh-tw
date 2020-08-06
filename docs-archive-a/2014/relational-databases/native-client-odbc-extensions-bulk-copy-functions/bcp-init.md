---
title: bcp_init |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_init
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_init function
ms.assetid: 6a25862c-7f31-4873-ab65-30f3abde89d2
author: rothja
ms.author: jroth
ms.openlocfilehash: 72d48b2a07e425e0863084c700c4de93d2776739
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594060"
---
# <a name="bcp_init"></a>bcp_init
  初始化大量複製作業。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_init (  
HDBC   
hdbc  
,  
LPCTSTR   
szTable  
,  
LPCTSTR   
szDataFile  
,  
LPCTSTR   
szErrorFile  
,  
INT   
eDirection  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *szTable*  
 這是要來回複製之資料庫資料表的名稱。 此名稱也可以包含資料庫名稱或擁有者名稱。 例如， **gracie. 標題**、 **pubs.。標題**、 **gracie**和**標題**都是合法的資料表名稱。  
  
 如果*eDirection*為 DB_OUT， *szTable*也可以是資料庫檢視的名稱。  
  
 如果 DB_OUT *eDirection* ，而且在呼叫[bcp_exec](bcp-exec.md)之前使用[bcp_control](bcp-control.md)來指定 SELECT 語句， **bcp_init**_szTable_必須設定為 Null。  
  
 *szDataFile*  
 這是要來回複製之使用者檔案的名稱。 如果要使用[bcp_sendrow](bcp-sendrow.md)直接從變數複製資料，請將*SZDATAFILE*設定為 Null。  
  
 *szErrorFile*  
 這是錯誤檔案的名稱，該檔案會以進度訊息、錯誤訊息，以及因為任何原因而無法從使用者檔案複製到資料表之任何資料列的複本。 如果將 Null 當做*szErrorFile*傳遞，則不會使用任何錯誤檔案。  
  
 *eDirection*  
 這是複製的方向，DB_IN 或 DB_OUT。 DB_IN 表示從程式變數或使用者檔案複製到資料表。 DB_OUT 表示從資料庫資料表複製到使用者檔案。 您必須利用 DB_OUT 指定使用者檔案名稱。  
  
## <a name="returns"></a>傳回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 呼叫任何其他大量複製函數之前，請先呼叫**bcp_init** 。 **bcp_init**會針對工作站和之間的資料大量複製，執行必要的初始化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 必須提供已啟用 ODBC 連接控制碼的**bcp_init**函式，以便搭配大量複製函數使用。 若要啟用控制碼，請在已配置但未連接的連接控制碼上，使用[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)搭配 SQL_COPT_SS_BCP 設定為 SQL_BCP_ON。 嘗試在已連接的控制代碼上指派屬性會導致錯誤。  
  
 當指定資料檔案時， **bcp_init**會檢查資料庫來源或目標資料表的結構，而不是資料檔案。 **bcp_init**會根據資料庫資料表、VIEW 或 SELECT 結果集中的每個資料行，指定資料檔案的資料格式值。 這個指定包括每個資料行的資料類型、資料中是否有長度或 null 指標和結束字元位元組字串，以及固定長度資料類型的寬度。 **bcp_init**設定這些值，如下所示：  
  
-   指定的資料類型為資料行在資料庫資料表、檢視或 SELECT 結果集中的資料類型。 資料類型會由 sqlncli.h 中所指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生資料類型列舉。 資料本身會以其電腦格式表示。 也就是說，來自**integer**資料類型之資料行的資料會根據建立資料檔案的電腦，以四個位元組的序列來表示。  
  
-   如果資料庫資料類型的長度是固定的，資料檔案資料的長度也是固定的。 處理資料的大量複製函式 (例如， [bcp_exec](bcp-exec.md)) 剖析資料列，該資料列必須要有資料檔中的資料長度，與資料庫資料表、VIEW 或 SELECT 資料行清單中所指定之資料的長度相同。 例如，定義為**char (13) **之資料庫資料行的資料，在檔案中的每個資料列都必須以13個字元表示。 如果資料庫資料行允許使用 Null 值，固定長度的資料前置詞可以是 Null 指標。  
  
-   定義結束字元位元組順序時，結束字元位元組順序的長度會設定為 0。  
  
-   複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，資料檔案對於資料庫資料表中的每個資料行都必須有資料。 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複製時，來自資料庫資料表、檢視或 SELECT 結果集中所有資料行的資料都會複製到資料檔案中。  
  
-   複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，資料行在資料檔案中的序數位置必須與資料行在資料庫資料表中的序數位置相同。 從複製時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ， **bcp_exec**會根據資料庫資料表中資料行的序數位置來放置資料。  
  
-   如果資料庫資料類型的長度可變 (例如， **Varbinary (22) **) 或者，如果資料庫資料行可以包含 null 值，資料檔案中的資料就會以長度/null 指標作為前置詞。 指標的寬度會根據資料類型和大量複製的版本而改變。  
  
 若要變更針對資料檔案指定的資料格式值，請呼叫[bcp_columns](bcp-columns.md)並[bcp_colfmt](bcp-colfmt.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的大量複製可以針對不包含索引的資料表進行最佳化，方法是，將資料庫復原模式設定為 SIMPLE 或 BULK_LOGGED。 如需詳細資訊，請參閱大量匯入和[ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql)[中最低限度記錄的必要條件](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)。  
  
 如果沒有使用任何資料檔案，您必須呼叫[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)來指定記憶體中每個資料行之為的格式和位置，然後使用 bcp_sendrow 將資料列複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 [bcp_sendrow](bcp-sendrow.md)  
  
## <a name="example"></a>範例  
 此範例顯示如何利用格式檔案使用 ODBC bcp_init 函數。  
  
 編譯與執行 C++ 程式碼之前，您需要執行下列動作：  
  
-   建立成為 Test 的 ODBC 資料來源。 您可以讓此資料來源與任何資料庫產生關聯。  
  
-   在資料庫上執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)]：  
  
    ```  
    CREATE TABLE BCPDate (cola int, colb datetime);  
    ```  
  
-   在您執行應用程式的目錄中，加入稱為 Bcpfmt.fmt 的檔案，並將其加入至檔案中：  
  
    ```  
    8.0  
    2  
    1SQLCHAR04"\t"1colaSQL_Latin1_General_Cp437_Bin  
    2SQLCHAR08"\r\n"2colbSQL_Latin1_General_Cp437_Bin  
    ```  
  
-   在您執行應用程式的目錄中，加入稱為 Bcpodbc.bcp 的檔案，並將其加入至檔案中：  
  
    ```  
    1  
    2  
    ```  
  
 現在，您可以編譯及執行 C++ 程式碼。  
  
```  
// compile with: odbc32.lib sqlncli11.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
SQLHENV henv = SQL_NULL_HENV;  
HDBC hdbc1 = SQL_NULL_HDBC;   
  
void Cleanup() {  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
   SDWORD cRows;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle, set BCP mode, and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLSetConnectAttr(hdbc1, SQL_COPT_SS_BCP, (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetConnectAttr(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security. Create SQL Server DSN using Windows NT authentication.  
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Initialize the bulk copy.  
   retcode = bcp_init(hdbc1, "BCPDate", "BCPODBC.bcp", NULL, DB_IN);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_init(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Read the format file.  
   retcode = bcp_readfmt(hdbc1, "BCPFMT.fmt");  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_readfmt(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the bulk copy.  
   retcode = bcp_exec(hdbc1, &cRows);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_exec(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("Number of rows bulk copied in = %d.\n", cRows);  
  
   // Cleanup  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
