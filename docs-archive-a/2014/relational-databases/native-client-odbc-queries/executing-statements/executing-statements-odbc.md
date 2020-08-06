---
title: " (ODBC) 執行語句 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
author: rothja
ms.author: jroth
ms.openlocfilehash: 3066a09cb1f5e63105ca3ffe2441f19e4bbe0101
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585355"
---
# <a name="executing-statements-odbc"></a>執行陳述式 (ODBC)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式提供各種方式來執行資料庫中的 SQL 語句 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ：  
  
-   直接執行  
  
-   準備執行  
  
 直接執行牽涉到建立包含語句的字元字串 [!INCLUDE[tsql](../../../includes/tsql-md.md)] ，並提交它以使用**SQLExecDirect**函數執行。 準備執行則包括建立含有 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式的字元字串，然後在兩個階段中執行此字串。 第一個階段會使用[SQLPrepare 函數](https://go.microsoft.com/fwlink/?LinkId=59360)函式來剖析並編譯中語句的執行計畫 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 。 第二個階段會使用**SQLExecute**函數來執行先前已備妥的執行計畫。 這樣會省下每次執行時的剖析和編譯負擔。 應用程式通常會使用備妥的執行來重複執行相同且參數化的 SQL 陳述式。  
  
 直接和準備執行都可以執行單一 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式或 SQL 陳述式批次，也可以呼叫預存程序。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [直接執行](direct-execution.md)  
  
-   [備妥的執行](prepared-execution.md)  
  
-   [程序](procedures.md)  
  
-   [陳述式的批次](batches-of-statements.md)  
  
-   [ISO 選項的作用](effects-of-iso-options.md)  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行查詢](../executing-queries-odbc.md)  
  
  
