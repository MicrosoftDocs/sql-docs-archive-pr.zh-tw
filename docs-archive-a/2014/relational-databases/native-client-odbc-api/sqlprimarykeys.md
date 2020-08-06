---
title: SQLPrimaryKeys |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
author: rothja
ms.author: jroth
ms.openlocfilehash: 67a932996ccbf52f5ab21fd6aa62381184ebc510
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606263"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
  資料表可能會有一個或多個資料行可以做為唯一的資料列識別碼，而不含 PRIMARY KEY 條件約束建立的資料表則會將空的結果集傳回給 SQLPrimaryKeys。 ODBC 函數[SQLSpecialColumns](sqlspecialcolumns.md)會報告沒有主鍵之資料表的資料列識別碼候選項。  
  
 SQLPrimaryKeys 會傳回 SQL_SUCCESS *CatalogName*、 *SchemaName*或*TableName*參數的值是否存在。 當這些參數中使用無效值時，SQLFetch 會傳回 SQL_NO_DATA。  
  
 SQLPrimaryKeys 可以在靜態伺服器資料指標上執行。 嘗試在可更新的 (動態或索引鍵集) 資料指標上執行 SQLPrimaryKeys 時，將會傳回 SQL_SUCCESS_WITH_INFO，表示資料指標類型已變更。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式藉由接受*CatalogName*參數的兩部分名稱，支援連結伺服器上之資料表的報告資訊： *Linked_Server_Name. Catalog_Name*。  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys 和資料表值參數  
 如果 SQL_SOPT_SS_NAME_SCOPE 語句屬性的值 SQL_SS_NAME_SCOPE_TABLE_TYPE，而不是其預設值 SQL_SS_NAME_SCOPE_TABLE，則 SQLPrimaryKeys 會傳回資料表類型之主鍵資料行的相關資訊。 如需 SQL_SOPT_SS_NAME_SCOPE 的詳細資訊，請參閱[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 如需資料表值參數的詳細資訊，請參閱[ODBC&#41;&#40;的資料表值參數](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLPrimaryKeys 函式](https://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
