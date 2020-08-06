---
title: 日期和時間以及結構描述資料列集 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], schema rowsets
ms.assetid: 8c35e86f-0597-4ef4-b2b8-f643e53ed4c2
author: rothja
ms.author: jroth
ms.openlocfilehash: 71a54cd1d40101b48a0e02fc4b6a6343b04fe185
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707481"
---
# <a name="date-and-time-and-schema-rowsets"></a>日期和時間與架構資料列集
  本主題提供有關 COLUMNS 資料列集和 PROCEDURE_PARAMETERS 資料列集的資訊。 這項資訊與 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中引進的 OLE DB 日期和時間增強功能相關。  
  
## <a name="columns-rowset"></a>COLUMNS 資料列集  
 系統會傳回日期/時間類型的下列資料行值：  
  
|資料行類型|DATA_TYPE|COLUMN_FLAGS、DBCOLUMFLAGS_SS_ISVARIABLESCALE|DATETIME_PRECISION|  
|-----------------|----------------|------------------------------------------------------|-------------------------|  
|date|DBTYPE_DBDATE|清除|0|  
|time|DBTYPE_DBTIME2|設定|0..7|  
|smalldatetime|DBTYPE_DBTIMESTAMP|清除|0|  
|Datetime|DBTYPE_DBTIMESTAMP|清除|3|  
|datetime2|DBTYPE_DBTIMESTAMP|設定|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|設定|0..7|  
  
 在 COLUMN_FLAGS 中，DBCOLUMNFLAGS_ISFIXEDLENGTH 對 date/time 類型永遠為 true，而且下列旗標永遠為 false：  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 剩餘的旗標 (DBCOLUMNFLAGS_ISNULLABLE、DBCOLUMNFLAGS_MAYBENULL、DBCOLUMNFLAGS_WRITE 和 DBCOLUMNFLAGS_WRITEUNKNOWN) 可以根據資料行的定義方式來設定。  
  
 在 COLUMN_FLAGS 中會提供新旗標 DBCOLUMNFLAGS_SS_ISVARIABLESCALE，以允許應用程式判斷資料行的伺服器類型，其中 DATA_TYPE 是 DBTYPE_DBTIMESTAMP。 DATETIME_PRECISION 也必須用來識別伺服器類型。  
  
 只有連接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本的伺服器時，DBCOLUMNFLAGS_SS_ISVARIABLESCALE 才有效。 連接到下層伺服器時，不會定義 DBCOLUMNFLAGS_SS_ISFIXEDSCALE。  
  
## <a name="procedure_parameters-rowset"></a>PROCEDURE_PARAMETERS 資料列集  
 DATA_TYPE 包含與 COLUMNS 結構描述資料列集相同的值，而 TYPE_NAME 包含伺服器類型。  
  
 已經加入新的資料行 SS_DATETIME_PRECISION，以傳回與 DATETIME_PRECISION 資料行相同的類型，類似 COLUMNS 資料列集。  
  
## <a name="provider_types-rowset"></a>PROVIDER_TYPES 資料列集  
 系統會傳回日期/時間類型的下列資料列：  
  
|類型 -><br /><br /> 資料行|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_DBDATE|DBTYPE_DBTIME2|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULL|級別|NULL|NULL|級別|級別|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|可搜尋|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|0|NULL|NULL|0|0|  
|MAXIMUM_SCALE|NULL|7|NULL|NULL|7|7|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|除非下列其中之一是 true，否則為 VARIANT_TRUE：<br /><br /> -是連接到下層伺服器的用戶端。<br />-資料類型相容性連接屬性會指定等於80的相容性層級。|除非下列其中之一是 true，否則為 VARIANT_TRUE：<br /><br /> -是連接到下層伺服器的用戶端。<br />-資料類型相容性連接屬性會指定等於80的相容性層級。|VARIANT_TRUE|  
|IS_FIXEDLENGTH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
  
 OLE DB 只會定義數值和十進位類型的 MINIMUM_SCALE 和 MAXIMUM_SCALE，因此，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 對於 time、datetime2 和 datetimeoffset 這些資料行的用法不是標準的。  
  
## <a name="see-also"></a>另請參閱  
 [中繼資料 &#40;OLE DB&#41;](../../database-engine/dev-guide/metadata-ole-db.md)  
  
  
