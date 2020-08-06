---
title: 對 OLE DB 日期和時間改善的資料類型支援 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], data type support
- OLE DB, date/time improvements
ms.assetid: d40e3fd6-9057-4371-8236-95cef300603e
author: rothja
ms.author: jroth
ms.openlocfilehash: 834583fdec63a8f613e623c239f9c3a1c9398950
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706414"
---
# <a name="data-type-support-for-ole-db-date-and-time-improvements"></a>對 OLE DB 日期和時間改善的資料類型支援
  本主題提供有關支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期/時間資料類型之 OLE DB ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client) 類型的資訊。  
  
## <a name="data-type-mapping-in-rowsets-and-parameters"></a>資料列集和參數中的資料類型對應  
 OLE DB 提供兩種新的資料類型來支援新的伺服器類型：DBTYPE_DBTIME2 和 DBTYPE_DBTIMESTAMPOFFSET。 下表顯示完整伺服器類型的對應：  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型|OLE DB 資料類型|值|  
|-----------------------------------------|----------------------|-----------|  
|Datetime|DBTYPE_DBTIMESTAMP|135 (oledb.h)|  
|smalldatetime|DBTYPE_DBTIMESTAMP|135 (oledb.h)|  
|date|DBTYPE_DBDATE|133 (oledb.h)|  
|time|DBTYPE_DBTIME2|145 (sqlncli) |  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|146 (sqlncli) |  
|datetime2|DBTYPE_DBTIMESTAMP|135 (oledb.h)|  
  
## <a name="data-formats-strings-and-literals"></a>資料格式：字串和常值  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型|OLE DB 資料類型|用於用戶端轉換的字串格式|  
|-----------------------------------------|----------------------|------------------------------------------|  
|Datetime|DBTYPE_DBTIMESTAMP|'yyyy-mm-dd hh:mm:ss[.999]'<br /><br /> 針對 Datetime，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最多支援三個小數秒位數。|  
|smalldatetime|DBTYPE_DBTIMESTAMP|'yyyy-mm-dd hh:mm:ss'<br /><br /> 此資料類型的精確度為一分鐘。 輸出時，秒數元件為零，而在輸入時，將會由伺服器捨去。|  
|date|DBTYPE_DBDATE|'yyyy-mm-dd'|  
|time|DBTYPE_DBTIME2|'hh:mm:ss[.9999999]'<br /><br /> 您最多可以使用七位數選擇性地指定小數秒。|  
|datetime2|DBTYPE_DBTIMESTAMP|'yyyy-mm-dd hh:mm:ss[.fffffff]'<br /><br /> 您最多可以使用七位數選擇性地指定小數秒。|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|'yyyy-mm-dd hh:mm:ss[.fffffff] +/-hh:mm'<br /><br /> 您最多可以使用七位數選擇性地指定小數秒。|  
  
 日期/時間常值的逸出序列沒有變更。  
  
 結果中的小數秒會使用點 (.) 而非冒號 (:)。  
  
 傳回到應用程式的字串值一律為適用於給定資料行的相同長度。 年、月、日、時、分和秒元件會以前置零填補以符合最大寬度。 在日期和時間之間將有一個空格，而在時間和時區位移之間也將有一個空格。 時區位移一律置於一個符號之後。 當位移為零時，此符號為加號 (+)。 在符號和位移值之間將沒有任何空格。 如果需要，小數秒將會以尾端零填補，最多填補到針對資料行定義的有效位數，但沒有其他東西。 對於 datetime 資料行，將有三個小數秒位數。 對於 smalldatetime 資料行，則沒有小數秒的位數，而且秒數將永遠為零。  
  
 應用程式從字串值進行的轉換將更具彈性，而且將允許元件值小於最大寬度。 年可以是 1-4 位數。 月、日、時、分和秒可以是 1 或 2 位數。 在日期/時間和時間/時區位移之間可以有一個任意空格。 包含零小時和零分鐘的位移符號可以是加號或減號。 小數秒允許使用尾端零，最多可達 9 位數。 時間元件可以利用一個小數點 (沒有小數秒位數) 結束。  
  
 空字串不是有效的日期/時間常值，而且它不代表 NULL 值。 嘗試將空字串轉換為日期/時間值時，將會導致 SQLState 22018 的錯誤，而且會出現「轉換規格的字元值無效」訊息。  
  
## <a name="data-formats-data-structures"></a>資料格式：資料結構  
 在以下描述的 OLE DB 專屬結構中，OLE DB 符合與 ODBC 相同的限制。 這些是取自西曆：  
  
-   月份的範圍由 1 至 12。  
  
-   日期欄位範圍為 1 至該月份的天數，而且如果是潤年，則必須與年和月欄位一致。  
  
-   小時的範圍由 0 至 23。  
  
-   分鐘的範圍由 0 至 59。  
  
-   秒數的範圍從 0 至 59。 這可讓最多兩個潤秒與恆星時間保持同步。  
  
 下列現有 OLE DB 結構的實作已經經過修改，支援新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期和時間資料類型。 不過，定義尚未變更。  
  
-   DBTYPE_DATE (這是一個自動化 DATE 類型。 這在內部表示為 `double`。 整數部分為自 1899 年 12 月 30 日起的天數，而分數部分則為一天的分數部分。 此類型的精確度為 1 秒，因此，有效的小數位數為 0)。  
  
-   DBTYPE_DBDATE  
  
-   DBTYPE_DBTIME  
  
-   DBTYPE_DBTIMESTAMP (分數欄位會由 OLE DB 定義為十億分之一秒 (奈秒) 的數字，而範圍為 0-999,999,999)  
  
-   DBTYPE_FILETIME  
  
### <a name="dbtype_dbtime2"></a>DBTYPE_DBTIME2  
 此結構在 32 位元和 64 位元作業系統上會填補到 12 個位元組。  
  
```  
typedef struct tagDBTIME2 {  
    USHORT hour;  
    USHORT minute;  
    USHORT second;  
    ULONG fraction;  
    } DBTIME2;  
```  
  
### <a name="dbtype_-dbtimestampoffset"></a>DBTYPE_ DBTIMESTAMPOFFSET  
  
```  
typedef struct tagDBTIMESTAMPOFFSET {  
    SHORT year;  
    USHORT month;  
    USHORT day;  
    USHORT hour;  
    USHORT minute;  
    USHORT second;  
    ULONG fraction;  
    SHORT timezone_hour;  
    SHORT timezone_minute;  
    } DBTIMESTAMPOFFSET;  
```  
  
 如果 `timezone_hour` 是負數，`timezone_minute` 必須為負數或零。 如果 `timezone_hour` 是正數，`timezone minute` 必須為正數或零。 如果 `timezone_hour` 為零，`timezone minute` 可以容納介於 -59 和 +59 之間的值。  
  
### <a name="ssvariant"></a>SSVARIANT  
 此結構現在包含新的結構 DBTYPE_DBTIME2 和 DBTYPE_DBTIMESTAMPOFFSET，而且可以針對適當的類型加入小數秒小數位數。  
  
```  
struct SSVARIANT {  
   SSVARTYPE vt;  
   DWORD dwReserved1;  
   DWORD dwReserved2;  
   union {  
// ...  
      DBTIMESTAMP tsDateTimeVal;  
      DBDATE dDateVal;  
      struct _Time2Val {  
         DBTIME2 tTime2Val;  
         BYTE bScale;  
      } Time2Val;  
      struct _DateTimeVal {  
         DBTIMESTAMP tsDateTimeVal;  
         BYTE bScale;  
      } DateTimeVal;  
      struct _DateTimeOffsetVal {   
         DBTIMESTAMPOFFSET tsoDateTimeOffsetVal;  
         BYTE bScale;  
      } DateTimeOffsetVal;  
// ...  
   };  
};  
```  
  
 此外，與 SSVARIANT 類型編碼 (可判斷列舉的類型) 相關聯的列舉將會擴充如下：  
  
```  
enum SQLVARENUM {  
// ...  
   // Datetime  
   VT_SS_DATETIME      = DBTYPE_DBTIMESTAMP,  
   VT_SS_SMALLDATETIME = 206,  
  
   VT_SS_DATE = DBTYPE_DBDATE,  
   VT_SS_TIME2 = DBTYPE_DBTIME2,  
   VT_SS_DATETIME2 = 212  
   VT_SS_DATETIMEOFFSET = DBTYPE_DBTIMESTAMPOFFSET  
};  
```  
  
 如果基礎結構描述更新為使用 `sql_variant` 而非 `datetime`，將需要更新移轉至使用 `datetime2` 並依賴 `datetime` 限制有效位數之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的應用程式。  
  
 SSVARIANT 的存取巨集也已經透過加入下列項目來擴充：  
  
```  
#define V_SS_DATETIME2(X)       V_SS_UNION(X, DateTimeVal)  
#define V_SS_TIME2(X)           V_SS_UNION(X, Time2Val)  
#define V_SS_DATE(X)            V_SS_UNION(X, dDateVal)  
#define V_SS_DATETIMEOFFSET(X)  V_SS_UNION(X, DateTimeOffsetVal)  
```  
  
## <a name="data-type-mapping-in-itabledefinitioncreatetable"></a>ITableDefinition::CreateTable 中的資料類型對應  
 下列類型對應會搭配 ITableDefinition::CreateTable 所使用的 DBCOLUMNDESC 結構使用：  
  
|OLE DB 資料類型 (*wType*)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型|注意|  
|----------------------------------|-----------------------------------------|-----------|  
|DBTYPE_DBDATE|date||  
|DBTYPE_DBTIMESTAMP|`datetime2`(p)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會檢查 DBCOLUMDESC *bScale*成員，以判斷小數秒數有效位數。|  
|DBTYPE_DBTIME2|`time`(p)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會檢查 DBCOLUMDESC *bScale*成員，以判斷小數秒數有效位數。|  
|DBTYPE_DBTIMESTAMPOFFSET|`datetimeoffset`(p)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會檢查 DBCOLUMDESC *bScale*成員，以判斷小數秒數有效位數。|  
  
 當應用程式在*wType*中指定 DBTYPE_DBTIMESTAMP 時，它可以藉 `datetime2` 由在*pwszTypeName*中提供類型名稱來覆寫的對應。 如果 `datetime` 指定了， *bScale*必須是3。 如果 `smalldatetime` 指定了， *bScale*必須是0。 如果*bScale*與*wType*和*pwszTypeName*不一致，則會傳回 DB_E_BADSCALE。  
  
## <a name="see-also"></a>另請參閱  
 [日期和時間改善 &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
