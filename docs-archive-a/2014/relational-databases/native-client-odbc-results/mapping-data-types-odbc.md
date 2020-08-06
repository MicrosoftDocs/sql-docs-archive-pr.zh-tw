---
title: " (ODBC) 對應資料類型 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [ODBC]
- result sets [ODBC], data types
- ODBC data types, mapping
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], mapping
- sql_variant data type
- SQL Server Native Client ODBC driver, data types
ms.assetid: 4ba0924d-9fca-4c48-aced-0a8d817b3dde
author: rothja
ms.author: jroth
ms.openlocfilehash: 545e738afb6b3283b2ff2f3830921da8ed13202f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709334"
---
# <a name="mapping-data-types-odbc"></a>對應資料類型 (ODBC)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 資料類型對應至 ODBC sql 資料類型。 下列章節討論 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 資料類型和它們所對應的 ODBC SQL 資料類型。 這些章節也討論 ODBC SQL 資料類型及其對應的 ODBC C 資料類型，以及支援的和預設的轉換。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**時間戳記**資料類型會對應至 SQL_BINARY 或 SQL_VARBINARY 的 ODBC 資料類型，因為**timestamp**資料行中的值不是**datetime**值，而是**BINARY (8) **或**VARBINARY (8) **值，指出資料列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上的活動順序。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式遇到奇數位元組的 SQL_C_WCHAR (Unicode) 值，則尾端的奇數位元組會被截斷。  
  
## <a name="dealing-with-sql_variant-data-type-in-odbc"></a>處理 ODBC 中的 sql_variant 資料類型  
 **sql_variant** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 除了大型物件 (lob) （例如**text**、 **Ntext**和**image**）以外，SQL_variant 資料類型資料行可以包含其中的任何資料類型。 例如，資料行可能包含某些資料列的**Smallint**值、其他資料列的**浮點**值，以及餘數中的**char/Nchar**值。  
  
 **Sql_variant**資料類型類似于 Microsoft Visual Basic 中的**variant**資料類型??。  
  
### <a name="retrieving-data-from-the-server"></a>從伺服器擷取資料  
 ODBC 沒有 variant 類型的概念，會限制在中使用**SQL_variant**資料類型與 ODBC 驅動程式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，如果指定了 binding，則**SQL_variant**資料類型必須系結至其中一個已記載的 ODBC 資料類型。 **SQL_CA_SS_VARIANT_TYPE**，NATIVE Client ODBC 驅動程式特定的新屬性會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL_variant**資料行中實例的資料類型傳回給使用者。  
  
 如果未指定系結，則可以使用[SQLGetData](../native-client-odbc-api/sqlgetdata.md)函數來判斷實例在**SQL_variant**資料行中的資料類型。  
  
 若要取得**SQL_variant**資料，請遵循下列步驟。  
  
1.  呼叫**SQLFetch** ，以定位至抓取的資料列。  
  
2.  呼叫**SQLGetData**，並指定類型的 SQL_C_BINARY，並將資料長度指定為0。 這會強制驅動程式讀取**SQL_variant**標頭。 標頭會在**SQL_variant**資料行中提供該實例的資料類型。 **SQLGetData**會傳回值的大小 (以位元組) 。  
  
3.  藉由指定**SQL_CA_SS_VARIANT_TYPE**做為其屬性值來呼叫[SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md) 。 此函式會將**SQL_variant**資料行中實例的 C 資料類型傳回至用戶端。  
  
 下列程式碼片段顯示前述的步驟。  
  
```  
while ((retcode = SQLFetch (hstmt))==SQL_SUCCESS)  
{  
    if (retcode != SQL_SUCCESS && retcode != SQL_SUCCESS_WITH_INFO)  
    {  
        SQLError (NULL, NULL, hstmt, NULL,   
                    &lNativeError,szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    retcode = SQLGetData (hstmt, 1, SQL_C_BINARY,   
                                pBuff,0,&Indicator);//Figure out the length  
    if (retcode != SQL_SUCCESS_WITH_INFO && retcode != SQL_SUCCESS)  
    {  
        SQLError (NULL, NULL, hstmt, NULL, &lNativeError,   
                    szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    printf_s ("Byte length : %d ",Indicator); //Print out the byte length  
  
    int iValue = 0;  
    retcode = SQLColAttribute (hstmt, 1, SQL_CA_SS_VARIANT_TYPE, NULL,   
                                        NULL,NULL,&iValue);  //Figure out the type  
    printf_s ("Sub type = %d ",iValue);//Print the type, the return is C_type of the column]  
  
// Set up a new binding or do the SQLGetData on that column with   
// the appropriate type  
}  
```  
  
 如果使用者使用[SQLBindCol](../native-client-odbc-api/sqlbindcol.md)建立系結，驅動程式會讀取中繼資料和資料。 驅動程式會接著將資料轉換為繫結中指定的適當 ODBC 類型。  
  
### <a name="sending-data-to-the-server"></a>將資料傳送到伺服器  
 **SQL_SS_VARIANT** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是 Native Client ODBC 驅動程式特定的新資料類型，會用於傳送至**SQL_variant**資料行的資料。 使用參數將資料傳送至伺服器時 (例如，插入 TableName 值 (?,? ) # A3， [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md)是用來指定包含 C 類型和對應類型的參數資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式會將 C 資料類型轉換成其中一個適當的**SQL_variant**子類型。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;處理結果](processing-results-odbc.md)  
  
  
