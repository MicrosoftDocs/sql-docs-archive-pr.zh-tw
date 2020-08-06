---
title: " (ODBC) 的快速順向資料指標 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
- forward-only cursors
- cursors [ODBC], fast forward-only
- ODBC cursors, fast forward-only
ms.assetid: 0707d07e-fc95-42ed-9280-b7e508ac8c62
author: rothja
ms.author: jroth
ms.openlocfilehash: de8d82a0c72ad51741a3785fba2910f691028cba
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598349"
---
# <a name="fast-forward-only-cursors-odbc"></a>快速順向資料指標 (ODBC)
  當連接到的實例時 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式支援順向、唯讀資料指標的效能優化。 快速順向資料指標是由驅動程式和伺服器以非常類似於預設結果集的方式在內部實作。 除了具有高效能以外，快速順向資料指標還具有下列特性：  
  
-   不支援[SQLGetData](../../native-client-odbc-api/sqlgetdata.md) 。 結果集資料行必須繫結至程式變數。  
  
-   偵測到資料指標的結尾時，伺服器就會自動關閉資料指標。 應用程式仍然必須呼叫[SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md)或[SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) (SQL_CLOSE) ，但驅動程式不需要將關閉要求傳送至伺服器。 這樣可節省透過網路與伺服器之間的往返。  
  
 應用程式會使用驅動程式特有的陳述式屬性 SQL_SOPT_SS_CURSOR_OPTIONS 來要求快速順向資料指標。 設定為 SQL_CO_FFO 時，就會啟用快速順向資料指標，但不啟用自動擷取。 設定為 SQL_CO_FFO_AF 時，則會一併啟用自動擷取選項。 如需自動擷取的詳細資訊，請參閱搭配[ODBC 資料指標使用自動擷取](using-autofetch-with-odbc-cursors.md)。  
  
 包含自動擷取的快速順向資料指標可用來透過與伺服器之間的一次往返，擷取小型結果集。 在這些步驟中， *n*是要傳回的資料列數目：  
  
1.  將 SQL_SOPT_SS_CURSOR_OPTIONS 設定為 SQL_CO_FFO_AF。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 設定為*n* + 1。  
  
3.  將結果資料行系結至*n* + 1 個元素的陣列 (在) 實際提取*n* + 1 個數據列時，都是安全的。  
  
4.  使用**SQLExecDirect**或**SQLExecute**開啟資料指標。  
  
5.  如果傳回狀態為 SQL_SUCCESS，則呼叫**SQLFreeStmt**或**SQLCloseCursor**來關閉資料指標。 資料列的所有資料都將位於繫結的程式變數中。  
  
 透過這些步驟， **SQLExecDirect**或**SQLExecute**會傳送已啟用自動擷取選項的資料指標開啟要求。 在收到來自用戶端的單一要求時，伺服器會：  
  
-   開啟資料指標。  
  
-   建立結果集並將資料列傳送至用戶端。  
  
-   由於資料列集大小設定為結果集的資料列數目加上 1，所以伺服器會偵測資料指標的結尾並關閉資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC&#41;&#40;的資料指標程式設計詳細資料](cursor-programming-details-odbc.md)  
  
  
