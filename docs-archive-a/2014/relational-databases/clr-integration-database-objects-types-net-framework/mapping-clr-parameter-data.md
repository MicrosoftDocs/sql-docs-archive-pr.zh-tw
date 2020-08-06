---
title: 對應 CLR 參數資料 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlBinary data type
- SqlInt16 data type
- SqlMoney data type
- SqlString data type
- SqlSingle data type
- data types [CLR integration]
- SqlInt64 data type
- SqlDateTime data type
- SqlXml data type
- SqlBoolean data type
- SqlDecimal data type
- SqlBytes data type
- mapping data types [CLR integration]
- SqlChars data type
- SqlInt32 data type
ms.assetid: 89b43ee9-b9ad-4281-a4bf-c7c8d116daa2
author: rothja
ms.author: jroth
ms.openlocfilehash: 7025c5180eac793534961af63df9ac701c95c03f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709638"
---
# <a name="mapping-clr-parameter-data"></a>對應 CLR 參數資料
  下表列出 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型、其在 common language runtime 中的對等專案， ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 命名空間中的 clr) `System.Data.SqlTypes` ，以及其在 .NET Framework 中的原生 CLR 對應項 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
||||  
|-|-|-|  
|**SQL Server 資料類型**|類型 (在 System.Data.SqlTypes 或 Microsoft.SqlServer.Types 中)|**CLR 資料類型 (.NET Framework)**|  
|`bigint`|`SqlInt64`|**Int64、Nullable\<Int64>**|  
|`binary`|`SqlBytes, SqlBinary`|`Byte[]`|  
|`bit`|`SqlBoolean`|**布林值，可為 Null\<Boolean>**|  
|`char`|無|無|  
|`cursor`|無|無|  
|`date`|`SqlDateTime`|**DateTime，Nullable\<DateTime>**|  
|`datetime`|`SqlDateTime`|**DateTime，Nullable\<DateTime>**|  
|`datetime2`|無|**DateTime，Nullable\<DateTime>**|  
|`DATETIMEOFFSET`|`None`|**DateTimeOffset，Nullable\<DateTimeOffset>**|  
|`decimal`|`SqlDecimal`|**十進位、可為 Null\<Decimal>**|  
|`float`|`SqlDouble`|**Double、Nullable\<Double>**|  
|`geography`|`SqlGeography`<br /><br /> `SqlGeography`定義在 Microsoft.SqlServer.Types.dll 中，這會與 SQL Server 一起安裝，而且可以從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能套件](https://www.microsoft.com/download/details.aspx?id=53164)下載。|無|  
|`geometry`|`SqlGeometry`<br /><br /> `SqlGeometry`定義在 Microsoft.SqlServer.Types.dll 中，這會與 SQL Server 一起安裝，而且可以從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能套件](https://www.microsoft.com/download/details.aspx?id=53164)下載。|無|  
|`hierarchyid`|`SqlHierarchyId`<br /><br /> `SqlHierarchyId`定義在 Microsoft.SqlServer.Types.dll 中，這會與 SQL Server 一起安裝，而且可以從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能套件](https://www.microsoft.com/download/details.aspx?id=53164)下載。|無|  
|`image`|無|無|  
|`int`|`SqlInt32`|**Int32，Nullable\<Int32>**|  
|`money`|`SqlMoney`|**十進位、可為 Null\<Decimal>**|  
|`nchar`|`SqlChars, SqlString`|`String, Char[]`|  
|`ntext`|無|無|  
|`numeric`|`SqlDecimal`|**十進位、可為 Null\<Decimal>**|  
|`nvarchar`|`SqlChars, SqlString`<br /><br /> `SQLChars` 比較適合資料傳輸和存取，而 `SQLString` 比較適合執行 String 作業。|`String, Char[]`|  
|`nvarchar(1), nchar(1)`|`SqlChars, SqlString`|**Char、String、Char []、Nullable\<char>**|  
|`real`|`SqlSingle` (`SqlSingle` 的範圍，但大於 `real`)|**單一、可為 Null\<Single>**|  
|`rowversion`|無|`Byte[]`|  
|`smallint`|`SqlInt16`|**Int16，Nullable\<Int16>**|  
|`smallmoney`|`SqlMoney`|**十進位、可為 Null\<Decimal>**|  
|`sql_variant`|無|`Object`|  
|`table`|無|無|  
|`text`|無|無|  
|`time`|無|**TimeSpan、可為 Null\<TimeSpan>**|  
|`timestamp`|無|無|  
|`tinyint`|`SqlByte`|**Byte、Nullable\<Byte>**|  
|`uniqueidentifier`|`SqlGuid`|**Guid，可為 Null\<Guid>**|  
|`User-defined type(UDT)`|無|繫結到相同組件或相依組件中之使用者定義型別的相同類別。|  
|**varbinary**|`SqlBytes, SqlBinary`|`Byte[]`|  
|`varbinary(1), binary(1)`|`SqlBytes, SqlBinary`|**byte、Byte []、Nullable\<byte>**|  
|`varchar`|無|無|  
|`xml`|`SqlXml`|無|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>利用 Out 參數自動轉換資料類型  
 CLR 方法可以利用 `out` 修飾詞 (Microsoft Visual C#) 或 `<Out()> ByRef` (Microsoft Visual Basic) 標示輸入參數，以便將資訊傳回到呼叫程式碼或程式。如果輸入參數在 `System.Data.SqlTypes` 命名空間中為 CLR 資料類型，而且呼叫程式會將其對等的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型指定為輸入參數，當 CLR 方法傳回資料類型時，會自動進行類型轉換。  
  
 例如，下列 CLR 預存程序所擁有的 `SqlInt32` CLR 資料類型輸入參數會以 `out` (C#) 或 `<Out()> ByRef` (Visual Basic) 標示：  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ ... }  
```  
  
```vb  
<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( <Out()> ByRef value As SqlInt32)  
...  
End Sub  
```  
  
 在資料庫中建置與建立組件之後，就會使用下列 Transact-SQL，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立預存程序，這會將 `int` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型指定為 OUTPUT 參數：  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 呼叫 CLR 預存程序時，`SqlInt32` 資料類型會自動轉換為 `int` 資料類型，並傳回到呼叫程式。  
  
 不過，並非所有 CLR 資料類型都可以透過 out 參數，自動轉換為其對等的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 下表列出這些例外。  
  
|||  
|-|-|  
|**CLR 資料類型 (SQL Server)**|**SQL Server 資料類型**|  
|`Decimal`|SMALLMONEY|  
|`SqlMoney`|SMALLMONEY|  
|`Decimal`|money|  
|`DateTime`|smalldatetime|  
|`SQLDateTime`|smalldatetime|  
  
## <a name="change-history"></a>變更記錄  
  
|更新的內容|  
|---------------------|  
|已在對應資料表中加入 `SqlGeography`、`SqlGeometry` 和 `SqlHierarchyId` 類型。|  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](sql-server-data-types-in-the-net-framework.md)  
  
  
