---
title: 如何：將資料列插入 Geography 資料行 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 0b6516f7-1fc0-4b01-a2d0-add0571070d5
author: rothja
ms.author: jroth
ms.openlocfilehash: 3a40351ce738dceb5707fcfe8fe15f67883d1ce2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706454"
---
# <a name="how-to-insert-rows-into-geography-column-odbc"></a><span data-ttu-id="457a4-102">如何：將資料列插入 Geography 資料行 (ODBC)</span><span class="sxs-lookup"><span data-stu-id="457a4-102">How to: Insert Rows into Geography Column (ODBC)</span></span>
  <span data-ttu-id="457a4-103">此範例會使用 2 個不同的繫結 (SQLCCHAR 和 SQLCBINARY)，從 WellKnownBinary (WKB) 在具有地理資料行的資料表中插入兩個資料列，</span><span class="sxs-lookup"><span data-stu-id="457a4-103">This sample inserts two rows into a table with a geography column from a WellKnownBinary (WKB) using 2 different bindings (SQLCCHAR and SQLCBINARY).</span></span> <span data-ttu-id="457a4-104">然後再從該資料表選取一個資料列，並使用 ::STAsText() 加以顯示。WKB 是 0x01010000000700ECFAD03A4C4001008000B5DF07C0，而且該應用程式會列印至主控台：POINT(56.4595 -2.9842)。</span><span class="sxs-lookup"><span data-stu-id="457a4-104">Then it selects one row from that table and uses ::STAsText() to display it.The WKB is 0x01010000000700ECFAD03A4C4001008000B5DF07C0 and the application prints to the console: POINT(56.4595 -2.9842).</span></span>  
  
 <span data-ttu-id="457a4-105">此範例不需要 ODBC 資料來源，但依預設，範例會在 SQL Server 的本機執行個體上執行。</span><span class="sxs-lookup"><span data-stu-id="457a4-105">This sample does not require an ODBC data source, but the sample runs, by default, on the local instance of SQL Server.</span></span>  
  
 <span data-ttu-id="457a4-106">此範例不適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的任何 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版本。</span><span class="sxs-lookup"><span data-stu-id="457a4-106">This sample will not work with any version of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] earlier than [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].</span></span>  
  
 <span data-ttu-id="457a4-107">如需空間儲存體的詳細資訊，請參閱[空間資料 &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)。</span><span class="sxs-lookup"><span data-stu-id="457a4-107">For more information about spatial storage, see [Spatial Data &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="457a4-108">範例</span><span class="sxs-lookup"><span data-stu-id="457a4-108">Example</span></span>  
 <span data-ttu-id="457a4-109">第一個 ([!INCLUDE[tsql](../../includes/tsql-md.md)]) 程式碼清單會建立此範例所使用的資料表。</span><span class="sxs-lookup"><span data-stu-id="457a4-109">The first ([!INCLUDE[tsql](../../includes/tsql-md.md)]) code listing creates a table used by this sample.</span></span>  
  
 <span data-ttu-id="457a4-110">使用 odbc32.lib 和 user32.lib 編譯第二個 (C++) 程式碼清單。</span><span class="sxs-lookup"><span data-stu-id="457a4-110">Compile the second (C++) code listing with odbc32.lib and user32.lib.</span></span> <span data-ttu-id="457a4-111">請確認您的 INCLUDE 環境變數包含的目錄內含 sqlncli.h。</span><span class="sxs-lookup"><span data-stu-id="457a4-111">Make sure your INCLUDE environment variable includes the directory that contains sqlncli.h.</span></span>  
  
 <span data-ttu-id="457a4-112">如果您要建立並執行此範例，當做 64 位元作業系統上的 32 位元應用程式，您必須利用 %windir%\SysWOW64\odbcad32.exe，以 ODBC 管理員身分建立 ODBC 資料來源。</span><span class="sxs-lookup"><span data-stu-id="457a4-112">If you will build and run this sample as a 32-bit application on a 64-bit operating system, you must create the ODBC data source with the ODBC Administrator in %windir%\SysWOW64\odbcad32.exe.</span></span>  
  
 <span data-ttu-id="457a4-113">這個範例會連接到電腦的預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。</span><span class="sxs-lookup"><span data-stu-id="457a4-113">This sample connects to your computer's default [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance.</span></span> <span data-ttu-id="457a4-114">若要連接到具名執行個體，請變更 ODBC 資料來源的定義，以便使用下列格式指定執行個體：server\namedinstance。</span><span class="sxs-lookup"><span data-stu-id="457a4-114">To connect to a named instance, change the definition of the ODBC data source to specify the instance using the following format: server\namedinstance.</span></span> <span data-ttu-id="457a4-115">根據預設，[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 會安裝至具名執行個體。</span><span class="sxs-lookup"><span data-stu-id="457a4-115">By default, [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] installs to a named instance.</span></span>  
  
 <span data-ttu-id="457a4-116">第三個 ([!INCLUDE[tsql](../../includes/tsql-md.md)]) 程式碼清單會刪除此範例所使用的資料表。</span><span class="sxs-lookup"><span data-stu-id="457a4-116">The third ([!INCLUDE[tsql](../../includes/tsql-md.md)]) code listing deletes the table used by this sample.</span></span>  
  
```sql
use tempdb  
GO  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'SpatialSample')  
   DROP TABLE SpatialSample  
  
CREATE TABLE SpatialSample (Name varchar(10), Geog Geography)  
GO  
```  
  
```cpp
// compile with: odbc32.lib user32.lib  
#include <windows.h>  
#include <Sqlext.h>  
#include <mbstring.h>  
#include "sqlncli.h"  
#include <string.h>  
#include <stdio.h>  
  
#define MAX_DATA 1024  
#define MYSQLSUCCESS(rc) ( (rc == SQL_SUCCESS) || (rc == SQL_SUCCESS_WITH_INFO) )  
  
SQLCHAR szDSN[] = "Driver={SQL Server Native Client 10.0};Server=.;Database=tempdb;Trusted_Connection=Yes;";  
  
class direxec {  
      RETCODE rc;   // ODBC return code  
      HENV henv;   // Environment  
      HDBC hdbc;   // Connection Handle  
      HSTMT hstmt;   // Statement Handle  
      SQLHDESC hdesc;   // Descriptor handle  
      SQLCHAR szData[MAX_DATA];   // Returned Data Storage  
      SDWORD cbData;   // Output Length of data   
  
      SQLCHAR szConnStrOut[MAX_DATA + 1];  
      SWORD swStrLen;  
  
public:  
      void sqlconn();   // Allocate env, stat and conn  
      void sqldisconn();   // Free pointers to env, stat, conn and disconnect  
      void error_out();   // Display errors  
      void check_rc(RETCODE rc);   // Checks for success of the return code  
      void SqlInsertFromChar();   // Insert a WKB in character form  
      void SqlInsertFromBinary();   // Insert a WKB in binary form   
      void SqlSelectGeogAsText(); // Retrieve the geography as Text.  
};   
  
// Allocate environment handles, connection handle, connect to data source, and allocate statement handle  
void direxec::sqlconn() {  
      // Allocate the environment handle  
      rc = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
      check_rc(rc);  
  
      // Set the ODBC version to version 3  
      rc = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
      check_rc(rc);  
  
      // Allocate the database connection handle  
      rc = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
      check_rc(rc);  
  
      // Connect to the database  
      rc = SQLDriverConnect(hdbc, NULL, szDSN, SQL_NTS, szConnStrOut, MAX_DATA, &swStrLen, SQL_DRIVER_NOPROMPT);  
      check_rc(rc);  
  
      // Allocate the statement handle  
      rc = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
      check_rc(rc);    
  
      // Allocate the descriptor handle  
      rc = rc = SQLAllocHandle(SQL_HANDLE_DESC, hdbc, &hdesc);  
      check_rc(rc);  
}   
  
// Display error message from the DiagRecord  
void direxec::error_out() {  
      // String to hold the SQL State  
      SQLCHAR szSQLSTATE[10];   
  
      // Error code  
      SDWORD nErr;  
  
      // The error message  
      SQLCHAR msg[SQL_MAX_MESSAGE_LENGTH + 1];  
  
      // Size of the message  
      SWORD cbmsg;  
  
      // If hstmt is not null use that for getting the DiagRec  
      if (hstmt)  
            rc = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, 1, szSQLSTATE, &nErr, msg, sizeof(msg), &cbmsg);  
      // else get the diag record from the env  
      else  
            rc = SQLGetDiagRec(SQL_HANDLE_ENV, henv, 1, szSQLSTATE, &nErr, msg, sizeof(msg), &cbmsg);  
  
      // If the rc is successful, show the message using a message box  
      if ( rc == SQL_SUCCESS) {  
            printf((char *)szData, "Error:\nSQLSTATE=%s,Native error=%ld, msg='%s'", szSQLSTATE, nErr, msg);  
            MessageBox(NULL, (const char *)szData, "ODBC Error", MB_OK);  
      }  
}  
  
// Checks the return code.  If failure, displays the error, free the memory and exits the program  
void direxec::check_rc(RETCODE rc) {  
      if (!MYSQLSUCCESS(rc)) {  
            error_out();  
            SQLFreeEnv(henv);  
            SQLFreeConnect(hdbc);  
            exit(-1);  
      }   
}  
  
void direxec::SqlInsertFromBinary() {     
      rc = SQLPrepare(hstmt, (SQLCHAR*) "INSERT INTO SpatialSample(Name,Geog) values('Sample1',Geography::STGeomFromWKB(?,4326))", SQL_NTS);  
      check_rc(rc);  
  
      SQLCHAR szBytes [] = "\x01\x01\x00\x00\x00\x07\x00\xEC\xFA\xD0\x3A\x4C\x40\x01\x00\x80\x00\xB5\xDF\x07\xC0";  
      SQLLEN iDataLength = sizeof(szBytes)-1;  
  
      rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_BINARY, SQL_VARBINARY, 100, 0, szBytes, sizeof(szBytes), &iDataLength);  
      check_rc(rc);  
  
      rc = SQLExecute(hstmt);  
      check_rc(rc);  
}  
  
void direxec::SqlInsertFromChar() {     
      rc = SQLPrepare(hstmt, (SQLCHAR*) "INSERT INTO SpatialSample(Name,Geog) values('Sample2',Geography::STGeomFromWKB(?,4326))", SQL_NTS);  
      check_rc(rc);  
  
      SQLCHAR szBytes [] = "01010000000700ECFAD03A4C4001008000B5DF07C0";  
  
      rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_VARBINARY, 100, 0, szBytes, sizeof(szBytes), NULL);  
      check_rc(rc);  
  
      rc = SQLExecute(hstmt);  
      check_rc(rc);  
}  
  
void direxec::SqlSelectGeogAsText() {  
      rc = SQLFreeStmt(hstmt, SQL_CLOSE);  
      check_rc(rc);   
  
      rc = SQLExecDirect(hstmt, (SQLCHAR*) "SELECT geog.STAsText() FROM SpatialSample", SQL_NTS);  
      check_rc(rc);   
  
      SQLCHAR rgcAsText[MAX_DATA];  
      SQLLEN cbAsText;   
  
      rc = SQLBindCol(hstmt, 1, SQL_C_CHAR, rgcAsText, sizeof(rgcAsText), &cbAsText);  
      check_rc(rc);  
  
      rc = SQLFetch(hstmt);  
      check_rc(rc);  
  
      rgcAsText[cbAsText] = '\0';  
      printf("%s\r\n", (LPSTR)rgcAsText);  
}   
  
int main() {  
      direxec x;  
  
      // Allocate handles, and connect.  
      x.sqlconn();    
  
      // Insert 2 samples into the table  
      x.SqlInsertFromChar();  
      x.SqlInsertFromBinary();  
  
      // Select 1 row from the table and display the geography as text  
      x.SqlSelectGeogAsText();  
}  
```  
  
```sql
use tempdb  
GO  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'SpatialSample')  
   DROP TABLE SpatialSample  
GO  
```  
  
  