---
title: SQLDescribeCol |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDescribeCol function
ms.assetid: ffbf34c6-8268-434f-829a-82009a6cda59
author: rothja
ms.author: jroth
ms.openlocfilehash: bc7ca9602e433f5e9ad26c39117e216eb0cc9564
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705118"
---
# <a name="sqldescribecol"></a>SQLDescribeCol
  針對執行的語句， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式不需要查詢伺服器來描述結果集中的資料行。 在此情況下， `SQLDescribeCol` 並不會造成伺服器往返。 如同[SQLColAttribute](sqlnumresultcols.md)， `SQLDescribeCol` 在已備妥但未執行的語句上呼叫，會產生伺服器往返。  
  
 當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或陳述式批次傳回多個結果資料列集時，按序數參考的資料行有可能源自於個別的資料表，或是參考結果集中完全不同的資料行。 `SQLDescribeCol`應針對每個集合呼叫。 當結果集變更時，應用程式應該在提取資料列結果以前先重新繫結資料值。 如需有關處理多個結果集傳回的詳細資訊，請參閱[SQLMoreResults](sqlmoreresults.md)。  
  
 當已備妥的 SQL 陳述式批次產生多個結果集時，只有第一個結果集會報告資料行屬性。  
  
 對於大數值資料類型，在*DataTypePtr*中傳回的值是 SQL_VARCHAR、SQL_VARBINARY 或 SQL_NVARCHAR。 *ColumnSizePtr*中的 SQL_SS_LENGTH_UNLIMITED 值表示大小為「無限制」。  
  
 從開始，database engine 的改進 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 可讓 SQLDescribeCol 取得預期結果的更精確描述。 這些更精確的結果可能與舊版的 SQLDescribeCol 所傳回的值不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱[中繼資料探索](../native-client/features/metadata-discovery.md)。  
  
## <a name="sqldescribecol-support-for-enhanced-date-and-time-features"></a>SQLDescribeCol 對增強型日期和時間功能的支援  
 針對日期/時間類型所傳回的值如下：  
  
||*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|---------------------|------------------------|  
|Datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqldescribecol-support-for-large-clr-udts"></a>SQLDescribeCol 對於大型 CLR UDT 的支援  
 `SQLDescribeCol` 支援大型 CLR 使用者定義型別 (UDT)。 如需詳細資訊，請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLDescribeCol 函式](https://go.microsoft.com/fwlink/?LinkID=59338)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
