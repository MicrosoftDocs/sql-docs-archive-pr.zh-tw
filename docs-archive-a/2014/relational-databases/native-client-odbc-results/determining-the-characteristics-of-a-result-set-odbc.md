---
title: 判斷結果集 (ODBC) 的特性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], characteristics
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- SQLDescribeCol function
- metadata [ODBC]
- SQLColAttribute function
- SQLNumResultCols function
ms.assetid: 90be414c-04b3-46c0-906b-ae7537989b7d
author: rothja
ms.author: jroth
ms.openlocfilehash: 5957092cdddfbcbce904d9a6483914672565d337
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594043"
---
# <a name="determining-the-characteristics-of-a-result-set-odbc"></a>決定結果集的特性 (ODBC)
  中繼資料是描述其他資料的資料。 例如，結果集中繼資料會描述結果集的特性，例如，結果集中的資料行數目、這些資料行的資料類型、其名稱、有效位數，以及 Null 屬性。  
  
 ODBC 會透過其目錄 API 函數提供中繼資料給應用程式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式會將許多 ODBC API 目錄函數實作為對應目錄程式的呼叫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 應用程式需要大部分結果集作業的中繼資料。 例如，應用程式會使用資料行的資料類型來決定要繫結到該資料行的變數種類。 它會使用字元資料行的位元組長度來決定從該資料行顯示資料必須擁有的空格數目。 應用程式決定資料行之中繼資料的方式取決於應用程式的類型。  
  
 垂直應用程式通常會使用預先定義的資料表，並針對這些資料表執行預先定義的作業。 此類應用程式的結果集中繼資料甚至會在撰寫應用程式前定義，並受到開發人員的控制，因此可以將程式碼寫入應用程式。 例如，如果次序識別碼資料行在資料來源中定義為 4 位元組整數，應用程式永遠可以將 4 位元組整數繫結至該資料行。 當中繼資料在應用程式中寫入程式碼時，應用程式所使用的資料表變更通常意味著應用程式的程式碼變更。  
  
 在泛型應用程式，尤其是支援隨選查詢的應用程式中，應用程式所建立之結果集的中繼資料在執行階段前通常不明。  
  
 若要決定結果集的特性，應用程式可以呼叫：  
  
-   [SQLNumResultCols](../native-client-odbc-api/sqlnumresultcols.md)以判斷要求傳回的資料行數目。  
  
-   [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md)或[SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md) ，用來描述結果集中的資料行。  
  
 設計良好的應用程式撰寫時會假設結果集不明，並使用這些函數傳回的資訊來繫結結果集中的資料行。 準備並執行陳述式之後，應用程式可以隨時呼叫這些函數。 不過，為了達到最佳效能，應用程式應該在執行語句之後呼叫**SQLColAttribute**、 **SQLDescribeCol**和**SQLNumResultCols** 。  
  
 針對中繼資料，您可以擁有多個並行呼叫。 在 ODBC 目錄 API 實作之下的系統目錄程序可以在使用靜態伺服器資料指標時，由 ODBC 驅動程式呼叫。 這可讓應用程式並行處理 ODBC 目錄函數的多個呼叫。  
  
 如果應用程式多次使用特定一組中繼資料，在第一次取得中繼資料時，可能會從私用變數的快取資訊中獲益。 這樣可以防止稍後針對相同資訊呼叫 ODBC 目錄函數，這會強迫驅動程式往返伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;處理結果](processing-results-odbc.md)  
  
  
