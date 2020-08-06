---
title: " (ODBC) 的隱含資料指標轉換 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
author: rothja
ms.author: jroth
ms.openlocfilehash: ff8350c71a853e39ff1d35a1f3fba6e8e1944934
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598342"
---
# <a name="implicit-cursor-conversions-odbc"></a>隱含資料指標轉換 (ODBC)
  應用程式可以透過[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)要求資料指標類型，然後執行要求之類型的伺服器資料指標不支援的 SQL 語句。 呼叫**SQLExecute**或**SQLExecDirect**會傳回 SQL_SUCCESS_WITH_INFO 並傳回**SQLGetDiagRec** ：  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 應用程式可以藉由呼叫**SQLGetStmtOption**設定為 SQL_CURSOR_TYPE，來判斷目前正在使用哪一種類型的資料指標。 資料指標類型轉換只適用於一個陳述式。 下一個**SQLExecDirect**或**SQLExecute**將會使用原始的語句資料指標設定來完成。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC&#41;&#40;的資料指標程式設計詳細資料](cursor-programming-details-odbc.md)  
  
  
