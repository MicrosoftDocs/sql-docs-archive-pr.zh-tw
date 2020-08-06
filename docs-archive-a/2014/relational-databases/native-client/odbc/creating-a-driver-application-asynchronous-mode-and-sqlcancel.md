---
title: 非同步模式和 SQLCancel |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- asynchronous operations [SQL Server Native Client]
- SQLCancel function
- SQLSetConnectAttr function
- SQL Server Native Client, asynchronous operations
- ODBC functions
- ODBC applications, asynchronous operations
- SQL Server Native Client ODBC driver, asynchronous mode
ms.assetid: f31702a2-df76-4589-ac3b-da5412c03dc2
author: rothja
ms.author: jroth
ms.openlocfilehash: 9071c6821e6edeb577b639223e42899d2927bced
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598302"
---
# <a name="asynchronous-mode-and-sqlcancel"></a>非同步模式和 SQLCancel
  某些 ODBC 函數可以透過同步或非同步方式來操作。 應用程式可以針對陳述式控制代碼或連接控制代碼來啟用非同步作業。 如果針對連接控制代碼來設定此選項，它會影響連接控制代碼上的所有陳述式控制代碼。 應用程式會使用以下陳述式來啟用或停用非同步作業：  
  
```  
SQLSetConnectAttr(hdbc, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
SQLSetConnectAttr(hdbc, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_OFF, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_OFF, SQL_IS_INTEGER);  
```  
  
 當應用程式在同步模式下呼叫 ODBC 函數時，此驅動程式要等到被通知伺服器已經完成命令之後，才會將控制權送回應用程式。  
  
 當以非同步方式操作時，此驅動程式會立即將控制權送回應用程式，即使是在傳送命令給伺服器以前。 此驅動程式會將傳回碼設定為 SQL_STILL_EXECUTING。 然後應用程式可以執行其他工作。  
  
 當應用程式測試是否完成命令時，它會使用相同的驅動程式參數來進行相同的函數呼叫。 如果此驅動程式尚未收到伺服器的回應，它將會再次傳回 SQL_STILL_EXECUTING。 應用程式必須定期測試命令，直到程式碼為 SQL_STILL_EXECUTING 以外的項目為止。 當應用程式取得某個其他傳回碼 (甚至是 SQL_ERROR) 時，它可以判斷出命令已經完成。  
  
 有時命令會持續一段很長的時間未處理。 如果應用程式需要取消命令而不等待回復，則可以使用與未處理的命令相同的語句控制碼呼叫**SQLCancel**來完成此動作。 這是唯一應該使用**SQLCancel**的時間。 有些程式設計人員會在透過結果集處理部分方式時使用**SQLCancel** ，並想要取消其餘的結果集。 [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md)或[SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md)應該用來取消未完成的結果集的其餘部分，而不是**SQLCancel**。  
  
## <a name="see-also"></a>另請參閱  
 [建立 SQL Server Native Client ODBC 驅動程式應用程式](creating-a-driver-application.md)  
  
  
