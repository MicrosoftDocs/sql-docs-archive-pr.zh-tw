---
title: " (ODBC) 呼叫預存程式 |Microsoft Docs"
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
author: rothja
ms.author: jroth
ms.openlocfilehash: d98d623dbbb4701bb59c95df502d0063d528d0d6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595938"
---
# <a name="call-stored-procedures-odbc"></a>呼叫預存程序 (ODBC)
  當 SQL 語句使用 ODBC CALL escape 子句來呼叫預存程式時，Microsoft SQL Server 驅動程式會使用遠端預存程序呼叫 (RPC) 機制，將此程式傳送至 SQL Server。 RPC 要求會略過 SQL Server 中大部分的陳述式剖析和參數處理，也比使用 Transact-SQL EXECUTE 陳述式來得快。  
  
 如需示範這項功能的範例應用程式，請參閱[處理 &#40;ODBC&#41;的傳回碼和輸出參數](running-stored-procedures-process-return-codes-and-output-parameters.md)。  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>將程序當做 RPC 執行  
  
1.  建構使用 ODBC CALL 逸出序列的 SQL 陳述式。 此陳述式會針對每個輸入、輸入/輸出和輸出參數，以及程序傳回值 (若有) 使用參數標記：  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  針對每個輸入、輸入/輸出和輸出參數呼叫[SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) ，如果有任何) ，則 (程式傳回值。  
  
3.  使用[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)執行語句。  
  
> [!NOTE]  
>  如果應用程式使用 Transact-SQL EXECUTE 語法 (相對於 ODBC CALL 逸出序列) 來提交程序，則 SQL Server ODBC 驅動程式會將程序呼叫當做 SQL 陳述式 (而不是 RPC) 傳遞到 SQL Server。 此外，如果使用 Transact-SQL EXECUTE 陳述式，則不會傳回輸出參數。  
  
## <a name="see-also"></a>另請參閱  
 [執行預存程式的 how to 主題 &#40;ODBC&#41;](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)   
 [批次處理預存程序呼叫](../native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [執行預存程式](../native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [呼叫預存程式](../native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [程序](../native-client-odbc-queries/executing-statements/procedures.md)  
  
  
