---
title: SQLMoreResults |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLMoreResults function
ms.assetid: f65698c3-7291-480d-9dab-58b13feb7771
author: rothja
ms.author: jroth
ms.openlocfilehash: 58f306d585640dfb07c3a62aa1d885a4bf8ba56a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606279"
---
# <a name="sqlmoreresults"></a>SQLMoreResults
  **SQLMoreResults**可讓應用程式取得多組結果資料列。 包含 COMPUTE 子句或是已提交之 ODBC 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式批次的 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 陳述式會造成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式產生多個結果集。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許建立伺服器資料指標來處理任一案例中的結果。 因此，開發人員必須確保 ODBC 陳述式正在封鎖中。 開發人員必須用完傳回的資料或是取消 ODBC 陳述式，然後才能處理連接上其他作用中陳述式的資料。  
  
> [!NOTE]  
>  只有在連接至 [!INCLUDE[tsql](../../includes/tsql-md.md)] 之前的伺服器版本時，才支援包含 COMPUTE 子句的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SELECT 陳述式。  
  
 開發人員可以判斷結果集資料行和資料列的屬性，這些資料行和資料列是由 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 陳述式的 COMPUTE 子句所產生。 如需詳細資訊，請參閱[SQLColAttribute](sqlcolattribute.md)。  
  
 使用結果集中的 unfetched 資料列來呼叫**SQLMoreResults**時，會遺失這些資料列，並提供下一個結果資料列集的資料列資料。  
  
## <a name="examples"></a>範例  
  
```  
void GetComputedRows  
    (  
    SQLHSTMT hStmt  
    )   
    {  
    SQLUSMALLINT    nCols;  
    SQLUSMALLINT    nCol;  
    PODBCSETINFO    pODBCSetInfo = NULL;  
    SQLRETURN       sRet;  
    UINT            nRow;  
    SQLINTEGER      nComputes = 0;  
    SQLINTEGER      nSet;  
    BYTE*           pValue;  
  
    // If SQLNumResultCols failed, then some error occurred in  
    //  statement execution. Exit.  
    if (!SQL_SUCCEEDED(SQLNumResultCols(hStmt, (SQLSMALLINT*) &nCols)))  
        {  
        goto EXIT;  
        }  
  
    // Determine the presence of COMPUTE clause result sets. The SQL  
    //  Server Native Client ODBC driver uses column attributes to report multiple  
    //  sets. The column number must be less than or equal to the   
    //  number of columns returned. You are guaranteed to have at least  
    //  one, so use '1' for the SQLColAttribute ColumnNumber  
    //  parameter.  
    SQLColAttribute(hStmt, 1, SQL_CA_SS_NUM_COMPUTES,  
        NULL, 0, NULL, (SQLPOINTER) &nComputes);  
  
    // Create a result info structure pointer array, one element for  
    //  the normal result rows and one for each compute result set.  
    //  Initialize the array to NULL pointers.  
    pODBCSetInfo = new ODBCSETINFO[1 + nComputes];  
  
    // Process the result sets...  
    nSet = 0;  
    while (TRUE)  
        {  
        // If required, get the column information for the result set.  
        if (pODBCSetInfo[nSet].pODBCColInfo == NULL)  
            {  
            if (pODBCSetInfo[nSet].nCols == 0)  
                {  
                SQLNumResultCols(hStmt, (SQLSMALLINT*) &nCols);  
                pODBCSetInfo[nSet].nCols = nCols;  
                }  
  
            if (GetColumnsInfo(hStmt, pODBCSetInfo[nSet].nCols,  
                &(pODBCSetInfo[nSet].pODBCColInfo)) == SQL_ERROR)  
                {  
                goto EXIT;  
                }  
            }  
  
        // Get memory for bound return values if required.  
        if (pODBCSetInfo[nSet].pRowValues == NULL)  
            {  
            CreateBindBuffer(&(pODBCSetInfo[nSet]));  
            }  
  
        // Rebind columns each time the result set changes.  
        myBindCols(hStmt, pODBCSetInfo[nSet].nCols,  
            pODBCSetInfo[nSet].pODBCColInfo,  
            pODBCSetInfo[nSet].pRowValues);  
  
        // Set for ODBC row array retrieval. Fast retrieve for all  
        //  sets. COMPUTE row sets have only a single row, but  
        //  normal rows can be retrieved in blocks for speed.  
        SQLSetStmtAttr(hStmt, SQL_ATTR_ROW_BIND_TYPE,  
            (void*) pODBCSetInfo[nSet].nResultWidth, SQL_IS_UINTEGER);  
        SQLSetStmtAttr(hStmt, SQL_ATTR_ROW_ARRAY_SIZE,  
            (void*) pODBCSetInfo[nSet].nRows, SQL_IS_UINTEGER);  
        SQLSetStmtAttr(hStmt, SQL_ATTR_ROWS_FETCHED_PTR,  
            (void*) &nRowsFetched, sizeof(SQLINTEGER));  
  
        while (TRUE)  
            {  
            // In ODBC 3.x, SQLFetch supports arrays of bound rows or  
            //  columns. SQLFetchScroll (or ODBC 2.x SQLExtendedFetch)  
            //  is not necessary to support fastest retrieval of   
            //  data rows.  
            if (!SQL_SUCCEEDED(sRet = SQLFetch(hStmt)))  
                {  
                break;  
                }  
  
            for (nRow = 0; nRow < (UINT) nRowsFetched; nRow++)  
                {  
                for (nCol = 0; nCol < pODBCSetInfo[nSet].nCols;  
                        nCol++)  
                    {  
                    // Processing row and column values...  
                    }  
                }  
            }  
  
        // sRet is not SQL_SUCCESS and is not SQL_SUCCESS_WITH_INFO.  
        //  If it's SQL_NO_DATA, then continue. If it's an  
        //  error state, stop.  
        if (sRet != SQL_NO_DATA)  
            {  
            break;  
            }  
  
        // If there's another set waiting, determine the result set  
        //  indicator. The indicator is 0 for regular row sets or an  
        //  ordinal indicating the COMPUTE clause responsible for the  
        //  set.  
        if (SQLMoreResults(hStmt) == SQL_SUCCESS)  
            {  
            sRet = SQLColAttribute(hStmt, 1, SQL_CA_SS_COMPUTE_ID,  
                NULL, 0, NULL, (SQLPOINTER) &nSet);  
            }  
        else  
            {  
            break;  
            }  
        }  
  
EXIT:  
    // Clean-up anything dynamically allocated and return.  
    return;  
    }  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQLMoreResults 函式](https://go.microsoft.com/fwlink/?LinkId=59357)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
