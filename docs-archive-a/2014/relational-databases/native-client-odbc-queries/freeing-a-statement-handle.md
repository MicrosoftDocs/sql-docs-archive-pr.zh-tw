---
title: 釋放語句控制碼 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d7a1e93d222e2b87058bc878f7eca85313b4108
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585346"
---
# <a name="freeing-a-statement-handle"></a>釋放陳述式控制代碼
  重複使用陳述式控制代碼比卸除陳述式控制代碼然後再配置新的陳述式控制代碼更有效率。 針對陳述式控制代碼執行新的 SQL 陳述式之前，應用程式應該確認目前的陳述式設定是否恰當。 這些包括陳述式屬性、參數繫結，以及結果集繫結。 一般來說，舊 SQL 語句的參數和結果集必須解除系結，方法是使用 SQL_RESET_PARAMS 和 SQL_UNBIND 選項呼叫[SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) ，然後重新系結新的 sql 語句。  
  
 當應用程式完成使用語句時，它會呼叫[SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md)來釋放語句。 請注意， **SQLDisconnect**會自動釋放連接上的所有語句。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行查詢](executing-queries-odbc.md)  
  
  
