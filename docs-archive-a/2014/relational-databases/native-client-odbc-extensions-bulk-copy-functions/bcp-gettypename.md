---
title: bcp_gettypename |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_gettypename
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_gettypename function
ms.assetid: 65f036d1-f60e-4b8a-97b3-76fccf0dfed4
author: rothja
ms.author: jroth
ms.openlocfilehash: b2d92498b9d863fa2cb700ec4d88868c0984c4d4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594061"
---
# <a name="bcp_gettypename"></a>bcp_gettypename
  傳回指定之 BCP 類型 Token 的 SQL 類型名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_gettypename (  
INT   
token  
,  
DBBOOL   
fIsMaxType  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *token*  
 指出 BCP 類型 Token 的值。  
  
 *欄位*  
 指出要求的 Token 是否為最大值類型。  
  
## <a name="returns"></a>傳回  
 包含對應到 BCP 類型之 SQL 類型名稱的字串。 如果指定無效的 BCP 類型，則傳回空字串。  
  
## <a name="remarks"></a>備註  
 BCP 類型 Token 是在 sqlncli.h 標頭檔和 sqlncli11.lib 程式庫中定義的。  
  
 以下的資料表會指定可能的 BCP 類型 (不論它們是否為最大類型) 以及預期的輸出。  
  
|BCP 類型名稱|MaxType|輸出|  
|-------------------|-------------|------------|  
|`SQLDECIMAL`|之前或之後|**decimal**|  
|`SQLNUMERIC`|之前或之後|**numeric**|  
|`SQLINT1`|之前或之後|**tinyint**|  
|`SQLINT2`|之前或之後|**smallint**|  
|`SQLINT4`|之前或之後|**int**|  
|`SQLMONEY`|之前或之後|**money**|  
|`SQLFLT8`|之前或之後|**float**|  
|`SQLDATETIME`|之前或之後|**datetime**|  
|`SQLBITN`|之前或之後|**bit-null**|  
|`SQLBIT`|之前或之後|**bit**|  
|`SQLBIGCHAR`|否|**char**|  
|`SQLCHARACTER`|否|**char**|  
|`SQLBIGVARCHAR`|否|**varchar**|  
|`SQLVARCHAR`|否|**varchar**|  
|`SQLTEXT`|之前或之後|**text**|  
|`SQLBIGBINARY`|否|**binary**|  
|`SQLBINARY`|否|**二進位**|  
|`SQLBIGVARBINARY`|否|**Varbinary**|  
|`SQLVARBINARY`|否|**Varbinary**|  
|`SQLIMAGE`|之前或之後|**影像**|  
|`SQLINTN`|之前或之後|**int-null**|  
|`SQLDATETIMN`|之前或之後|**datetime-null**|  
|`SQLMONEYN`|之前或之後|**money-null**|  
|`SQLFLTN`|之前或之後|**float-null**|  
|`SQLAOPSUM`|之前或之後|**要求**|  
|`SQLAOPAVG`|之前或之後|**Avg**|  
|`SQLAOPCNT`|之前或之後|**Count**|  
|`SQLAOPMIN`|之前或之後|**分鐘**|  
|`SQLAOPMAX`|之前或之後|**讀數**|  
|`SQLDATETIM4`|之前或之後|**smalldatetime**|  
|`SQLMONEY4`|之前或之後|**Smallmoney**|  
|`SQLFLT4`|之前或之後|**即時**|  
|`SQLUNIQUEID`|之前或之後|**uniqueidentifier**|  
|`SQLNCHAR`|否|**Nchar**|  
|`SQLNVARCHAR`|否|**Nvarchar**|  
|`SQLNTEXT`|之前或之後|**Ntext**|  
|`SQLVARIANT`|之前或之後|**sql_variant**|  
|`SQLINT8`|之前或之後|**Bigint**|  
|`SQLCHARACTER`|是|**varchar(max)**|  
|`SQLBIGCHAR`|是|**varchar(max)**|  
|`SQLBIGVARCHAR`|是|**varchar(max)**|  
|`SQLVARCHAR`|是|**varchar(max)**|  
|`SQLBINARY`|是|**varbinary(max)**|  
|`SQLBIGBINARY`|是|**varbinary(max)**|  
|`SQLBIGVARBINARY`|是|**varbinary(max)**|  
|`SQLVARBINARY`|是|**varbinary(max)**|  
|`SQLNCHAR`|是|**nvarchar(max)**|  
|`SQLNVARCHAR`|是|**nvarchar(max)**|  
|`SQLXML`|是|**XML**|  
|`SQLUDT`|之前或之後|**Udt**|  
  
## <a name="bcp_gettypename-support-for-enhanced-date-and-time-features"></a>bcp_gettypename 支援增強的日期和時間功能  
 適用于日期/時間類型的 token 參數值會在[&#40;OLE DB 和 ODBC&#41;的增強型日期和時間類型的大量複製變更](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)中，描述于資料表中的 "Type in sqlncli. h" 資料行。 傳回值位於 "File storage type" 資料行的對應資料列中。  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
