---
title: 使用自動擷取搭配 ODBC 資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
author: rothja
ms.author: jroth
ms.openlocfilehash: e3d9374cf9ceab4a7e73cc0059783486f2bf9c41
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598343"
---
# <a name="using-autofetch-with-odbc-cursors"></a>使用自動擷取搭配 ODBC 資料指標
  當連接到的實例時 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式會在使用任何伺服器資料指標類型時支援自動擷取選項。 使用自動擷取，開啟游標的**SQLExecute**或**SQLExecDirect**函式也會有隱含的[SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md) (SQL_FIRST) 函數。 構成第一個資料列集的資料列會當做陳述式執行的一部分而傳回至繫結的應用程式變數，如此就不需要再一次透過網路往返伺服器。 啟用自動擷取選項時，不支援[SQLGetData](../../native-client-odbc-api/sqlgetdata.md) ;結果集資料行必須系結至程式變數。  
  
 應用程式會藉由將驅動程式特定的 SQL_SOPT_SS_CURSOR_OPTIONS 陳述式屬性設定為 SQL_CO_AF 來要求自動擷取。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC&#41;&#40;的資料指標程式設計詳細資料](cursor-programming-details-odbc.md)  
  
  
