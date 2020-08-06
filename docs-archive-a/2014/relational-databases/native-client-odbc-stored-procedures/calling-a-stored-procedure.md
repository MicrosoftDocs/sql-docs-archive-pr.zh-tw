---
title: 呼叫預存程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- ODBC, stored procedures
- stored procedures [ODBC], calling
- SQL Server Native Client ODBC driver, stored procedures
- ODBC CALL escape sequence
- escape sequences [SQL Server]
- CALL statement
ms.assetid: d13737f4-f641-45bf-b56c-523e2ffc080f
author: rothja
ms.author: jroth
ms.openlocfilehash: c6fa704e45e4e85b479ae8a40a3e567bea1ec5e9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709318"
---
# <a name="calling-a-stored-procedure"></a>呼叫預存程序
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式同時支援 ODBC 呼叫 escape 序列和 [!INCLUDE[tsql](../../includes/tsql-md.md)] [EXECUTE](/sql/t-sql/language-elements/execute-transact-sql)語句來執行預存程式; odbc 呼叫 escape 序列是慣用的方法。 使用 ODBC 語法可讓應用程式擷取預存程序的傳回碼，而且會最佳化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式，使用最初開發的通訊協定，在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦之間傳送遠端程序 (RPC) 呼叫。 此 RPC 通訊協定會排除在伺服器上完成的許多參數處理與陳述式剖析，藉以增加效能。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用具有 ODBC (的具名引數來呼叫預存程式時，如需詳細資訊，請參閱[依名稱 (具名引數) ](https://go.microsoft.com/fwlink/?LinkID=209721)) 系結參數。參數名稱必須以 ' \@ ' 字元開頭。 這是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定的限制。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會比 Microsoft Data Access Components (MDAC) 更嚴格地強制執行此限制。  
  
 用來呼叫程序的 ODBC CALL 逸出序列為：  
  
 {[**？ =**]**呼叫**_procedure_name_[ ( [*參數*] [**，**[*parameter*]] ... ) ]}  
  
 其中*procedure_name*會指定程式的名稱，而*參數*會指定程式參數。 只有使用 ODBC CALL 逸出序列的陳述式才會支援具名參數。  
  
 程序可以有零或多個參數。 它也可以傳回值 (如語法開頭的選用參數標記 ?= 所指示)。 如果參數是輸入參數或輸入/輸出參數，則可以是常值或參數標記。 如果參數是輸出參數，它必須是參數標記，因為輸出不明。 參數標記必須與[SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)系結，才能執行程序呼叫語句。  
  
 輸入和輸入/輸出參數可以從程序呼叫省略。 如果呼叫包含括號但沒有任何參數的程序，驅動程式會引導資料來源使用第一個參數的預設值。 例如：  
  
 {**call** _procedure_name_ ** ( ) **}  
  
 如果程序沒有任何參數，該程序可能會失敗。 如果呼叫沒有括號的程序，驅動程式不會傳送任何參數值。 例如：  
  
 {**call** _procedure_name_}  
  
 在程序呼叫中可以針對輸入和輸入/輸出參數指定常值。 例如，程序 InsertOrder 有五個輸入參數。 以下對 InsertOrder 的呼叫會省略第一個參數、提供第二個參數的常值，然後將參數標記用於第三、第四和第五個參數 (參數會循序編號，從 1 這個值開始)。  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}  
```  
  
 請注意，如果省略了某個參數，將它與其他參數分隔的逗號仍然必須出現。 如果省略了輸入或輸入/輸出參數，程序就會使用參數的預設值。 指定輸入或輸入/輸出參數預設值的其他方法是，將繫結至參數之長度/指標緩衝區的值設定成 SQL_DEFAULT_PARAM，或使用 DEFAULT 關鍵字。  
  
 如果省略了輸入/輸出參數，或者如果有提供參數的常值，驅動程式就會捨棄輸出值。 同樣地，如果省略了程序傳回值的參數標記，驅動程式就會捨棄傳回值。 最後，如果應用程式指定的程序傳回值參數不會傳回值，驅動程式會將繫結至參數之長度/指標緩衝區的值設定為 SQL_NULL_DATA。  
  
## <a name="delimiters-in-call-statements"></a>CALL 陳述式中的分隔符號  
 依預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式也支援 ODBC { CALL } 逸出序列專屬的相容性選項。 驅動程式會接受 CALL 陳述式以及只有單一一組分隔完整預存程序名稱的雙引號：  
  
```  
{ CALL "master.dbo.sp_who" }  
```  
  
 依預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式也接受遵循 ISO 規則，並將每個分隔符號括在雙引號中的 CALL 陳述式：  
  
```  
{ CALL "master"."dbo"."sp_who" }  
```  
  
 不過，利用預設值執行時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式不支援使用引號識別碼的形式與包含 ISO 標準未指定為合法識別碼之字元的識別碼。 例如，驅動程式無法使用引號識別碼的 CALL 語句來存取名為 **"My. Proc"** 的預存程式：  
  
```  
{ CALL "MyDB"."MyOwner"."My.Proc" }  
```  
  
 這個陳述式會由驅動程式解譯為：  
  
```  
{ CALL MyDB.MyOwner.My.Proc }  
```  
  
 伺服器會引發錯誤，指出名為**MyDB**的連結伺服器不存在。  
  
 此問題在使用有括號的識別碼時不存在，因為此陳述式會正確解譯：  
  
```  
{ CALL [MyDB].[MyOwner].[My.Table] }  
```  
  
## <a name="see-also"></a>另請參閱  
 [執行預存程序](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
