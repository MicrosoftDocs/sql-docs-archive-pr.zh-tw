---
title: 資料類型使用方式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data types
- ODBC data types, about ODBC data types
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC]
- SQL Server Native Client ODBC driver, data types
- data types [ODBC], about data types
ms.assetid: 4f19b0d6-94ac-4a98-a121-57d38787864c
author: rothja
ms.author: jroth
ms.openlocfilehash: 8333f45fd9e3b742b3765efaee5ae7a865161bc2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708270"
---
# <a name="data-type-usage"></a>資料類型使用方式
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式，並 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 強加下列資料類型的使用。  
  
|資料類型|限制|  
|---------------|----------------|  
|日期常值|日期常值，當儲存在 SQL_TYPE_TIMESTAMP 資料行 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**或**Smalldatetime**) 的資料類型時，其時間值為12：00： 00.000 A.M。|  
|**money**和**smallmoney**|只有**money**和**smallmoney**資料類型的整數部分很重要。 如果在資料類型轉換期間截斷 SQL **money**資料的小數部分， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會傳回警告，而不是錯誤。|  
|SQL_BINARY (可為 Null)|連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 版和更早版本時，如果 SQL_BINARY 資料行可為 Null，則儲存在資料來源中的資料就不會以零進行填補。 抓取這類資料行的資料時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會在右側以零填補。 不過，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所執行的作業 (例如串連) 中建立的資料就沒有此類填補。<br /><br /> 此外，當資料是放在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 或更早版本之執行個體的此類資料行中，且資料太長而無法放入資料行時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會從右側截斷資料。 **注意：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式支援連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 和更早版本。|  
|SQL_CHAR (截斷)|如果是連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 和更早版本的執行個體，而且資料是放在 SQL_CHAR 資料行中，則在資料太長無法放入資料行時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在未提供警告的情況下從右側截斷資料。 **注意：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式支援連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 和更早版本。|  
|SQL_CHAR (可為 Null)|當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 和更早版本時，如果 SQL_CHAR 資料行可為 Null，則儲存在資料來源中的資料就不會以空白進行填補。 抓取這類資料行的資料時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會在右側以空白填補。 不過，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所執行的作業 (例如串連) 中建立的資料就沒有此類填補。 **注意：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式支援連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 和更早版本。|  
|SQL_LONGVARBINARY、SQL_LONGVARCHAR、SQL_WLONGVARCHAR|當連接到實例6時，會完全支援 SQL_LONGVARBINARY、SQL_LONGVARCHAR 或 SQL_WLONGVARCHAR 資料類型 (使用 WHERE 子句) 會影響多個資料列的資料行更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。*x*和更新版本。 當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*的實例時，會出現 S1000 錯誤「部分插入/更新」。 文字或影像資料行的插入/更新未成功」。 **注意：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式支援連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 和更早版本。|  
|字串函數參數|字串函數的*string_exp*參數必須是 SQL_CHAR 或 SQL_VARCHAR 的資料類型。 字串函數中不支援 SQL_LONG_VARCHAR 資料類型。 *Count*參數必須小於或等於8000，因為 SQL_CHAR 和 SQL_VARCHAR 資料類型受限於8000個字元的最大長度。|  
|時間常值|時間常值（當儲存在 SQL_TIMESTAMP 資料行中， ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**或**Smalldatetime**) 的資料類型時，其日期值為1900年1月1日。|  
|**timestamp**|只有 Null 值可以手動插入**timestamp**資料行。 不過，由於**時間戳記**資料行是由自動更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，所以會覆寫 Null 值。|  
|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Tinyint**資料類型不帶正負號。 在預設的情況下， **Tinyint**資料行系結至資料類型 SQL_C_UTINYINT 的變數。|  
|別名資料類型|當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*的實例時，ODBC 驅動程式會將 Null 新增至未明確宣告資料行 null 屬性的資料行定義。 因此會忽略儲存在別名資料類型定義中的 Null 屬性。<br /><br /> 當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*的實例時，具有具有**char**或**binary**基底資料類型且未宣告 null 屬性之別名資料類型的資料行，會建立為**Varchar**或**Varbinary**資料類型。 [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md)、 [SQLColumns](../native-client-odbc-api/sqlcolumns.md)和[SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md)會傳回 SQL_VARCHAR 或 SQL_VARBINARY 做為這些資料行的資料類型。 從這些資料行所擷取的資料不會進行填補。 **注意：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式支援連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 和更早版本。|  
|LONG 資料類型|同時限制 SQL_LONGVARBINARY 和 SQL_LONGVARCHAR 資料類型的*資料執行中*參數。|  
|大型值類型|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式會在接受或傳回 ODBC SQL 資料類型的 api 中，分別** () **、 **Varbinary (max) **和**Nvarchar (max) **類型，SQL_VARCHAR 和 SQL_VARBINARY SQL_WVARCHAR 的最大值。|  
|使用者定義型別 (UDT)|UDT 資料行會對應為 SQL_SS_UDT。 如果 UDT 資料行使用 UDT 的 ToString() 或 ToXMLString() 方法或是透過 CAST/CONVERT 函數而明確地對應到 SQL 陳述式中的其他類型，則結果集內的資料行類型會反映出此資料行轉換成的實際類型。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式只能以二進位形式系結至 UDT 資料行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只支援 SQL_SS_UDT 和 SQL_C_BINARY 資料類型之間的轉換。|  
|XML|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動將 XML 轉換為 Unicode 文字。 XML 類型會對應為 SQL_SS_XML。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;處理結果](processing-results-odbc.md)  
  
  
