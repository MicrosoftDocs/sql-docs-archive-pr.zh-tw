---
title: SQLCloseCursor |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
author: rothja
ms.author: jroth
ms.openlocfilehash: 770a67432868516e5023d1cf0ff819501b4c130e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709382"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
  **SQLCloseCursor**會將[SQLFreeStmt](sqlfreestmt.md)取代為 SQL_CLOSE 的*選項*值。 在收到**SQLCloseCursor**時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會捨棄暫止的結果集資料列。 請注意， **SQLCloseCursor**不會改變語句的資料行和參數系結 (是否有任何) 。  
  
## <a name="see-also"></a>另請參閱  
 [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
