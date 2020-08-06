---
title: ODBC 中的交易 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, transactions
- transactions [ODBC]
- ODBC, transactions
ms.assetid: c5a87fa5-827a-4e6f-a0d9-924bac881eb0
author: rothja
ms.author: jroth
ms.openlocfilehash: 386b248edfdb6e0ac5eb97b3aeb6c0bbc505a5a0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593354"
---
# <a name="transactions-in-odbc"></a>ODBC 中的交易
  ODBC 中的交易會在連接層級進行管理。 當應用程式完成交易時，它會認可或回復透過該連接之所有陳述式控制代碼完成的所有工作。 若要認可或回復交易，應用程式應該呼叫[SQLEndTran](../../native-client-odbc-api/sqlendtran.md) ，而不是提交 COMMIT 或 ROLLBACK 語句。  
  
 應用程式會呼叫[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) ，以便在管理交易的兩個 ODBC 模式之間切換：  
  
-   自動認可模式  
  
     每個陳述式都會在成功完成時自動認可。 當您在自動認可模式下執行時，不需要其他任何交易管理函數。  
  
-   手動認可模式  
  
     所有執行的語句都會包含在相同的交易中，直到藉由呼叫**SQLEndTran**特別停止為止。  
  
 自動認可模式是 ODBC 的預設交易模式。 建立連線時，它會處於自動認可模式，直到呼叫**SQLSetConnectAttr** ，藉由設定自動認可模式來切換為手動認可模式。 當應用程式關閉自動認可時，傳送到資料庫的下一個陳述式會啟動交易。 然後，交易會維持有效，直到應用程式使用 SQL_COMMIT 或 SQL_ROLLBACK 選項呼叫**SQLEndTran**為止。 **SQLEndTran**啟動下一個交易之後，傳送至資料庫的命令。  
  
 如果應用程式從手動認可模式切換到自動認可模式，驅動程式會認可目前在連接上開啟的所有交易。  
  
 ODBC 應用程式不應使用 Transact-SQL 交易陳述式 (例如，BEGIN TRANSACTION、COMMIT TRANSACTION 或 ROLLBACK TRANSACTION)，因為這可能會在驅動程式上造成未定的行為。 ODBC 應用程式應該在自動認可模式中執行，而不是使用任何交易管理函數或語句，或在手動認可模式下執行，並使用 ODBC **SQLEndTran**函數來認可或回復交易。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行交易](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
  
