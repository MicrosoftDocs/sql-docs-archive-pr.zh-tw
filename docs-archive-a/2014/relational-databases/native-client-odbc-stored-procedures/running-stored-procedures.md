---
title: 執行預存程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- stored procedures [ODBC], running
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], executing
ms.assetid: 866b6dd3-2acd-4dfb-aeca-a0352b2d4c6a
author: rothja
ms.author: jroth
ms.openlocfilehash: 8e5de6a9a13c95b417657a1d108403fa27abe34b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709306"
---
# <a name="running-stored-procedures"></a>執行預存程序
  預存程序是一種儲存在資料庫中的可執行物件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援：  
  
-   預存程序：  
  
     已經先行編譯為單一可執行程序的一或多個 SQL 陳述式。  
  
-   擴充預存程序：  
  
     寫入到擴充預存程序之 SQL Server 開放式資料服務 API 的 C 或 C++ 動態連結程式庫 (DLL)。 開放式資料服務 API 會擴充預存程序的功能以包含 C 或 C++ 程式碼。  
  
 執行陳述式時，在資料來源上呼叫預存程序 (而非直接在用戶端應用程式中執行或準備陳述式) 可以提供：  
  
-   較高的效能  
  
     SQL 陳述式會在建立程序時進行剖析和編譯。 接著，這個負擔會在執行程序時儲存起來。  
  
-   降低的網路負擔  
  
     執行程序而非跨網路傳送複雜查詢可以減少網路流量。 如果 ODBC 應用程式使用 ODBC { CALL } 語法執行預存程序，ODBC 驅動程式會進行額外的最佳化，以排除轉換參數資料的需要。  
  
-   更好的一致性  
  
     如果組織的規則是在中央資源 (例如預存程序) 實作，則這些規則可以進行一次的編碼、測試與偵錯。 接著，各個程式設計師可以使用經過測試的預存程序，而不用開發自己的實作。  
  
-   更好的精確度  
  
     預存程序通常是由具經驗的程式設計師開發，因此這些預存程序會比不同技術層級之程式設計師開發多次的程式碼更有效率，而且錯誤更少。  
  
-   增加的功能  
  
     擴充預存程序可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中未提供的 C 和 C++ 功能。  
  
     如需如何呼叫預存程式的範例，請參閱[&#40;ODBC&#41;處理傳回碼和輸出參數](../native-client-odbc-how-to/running-stored-procedures-process-return-codes-and-output-parameters.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [呼叫預存程序](calling-a-stored-procedure.md)  
  
-   [批次預存程序呼叫](batching-stored-procedure-calls.md)  
  
-   [處理預存程序結果](processing-stored-procedure-results.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [執行預存程式的 how to 主題 &#40;ODBC&#41;](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)  
  
  
