---
title: " (ODBC) 的日期時間資料類型轉換 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC]
- bindings [ODBC]
- ODBC, bindings and conversions
ms.assetid: 66b9d282-c88d-40e5-93c2-fd5499a74458
author: rothja
ms.author: jroth
ms.openlocfilehash: 142e4388cb87055ddbc6faa7d5b1a92a627738c2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598334"
---
# <a name="datetime-data-type-conversions-odbc"></a>datetime 資料類型轉換 (ODBC)
  下列轉換已由 ODBC 定義，或為一致的 ODBC 延伸模組。 每個提供者所提供的轉換取決於提供者所服務的社群，因此在提供者之間通常會發生不一致。 方括號中的值是選擇性的。  
  
-   datetime 字串的格式為 'yyyy-mm-dd[ hh:mm:ss[.9999999][ plus/minus hh:mm]]'  
  
-   time 字串的格式是 'hh:mm:ss[.9999999]'  
  
-   date 字串的格式為 'yyyy-mm-dd'  
  
 字串的轉換在空白和欄位寬度上允許彈性。 如需詳細資訊，請參閱[資料類型支援 ODBC 日期和時間改善](data-type-support-for-odbc-date-and-time-improvements.md)的「資料格式：字串和常值」一節。  
  
 下面是一般轉換規則：  
  
-   如果沒有任何時間存在，但是接收者可以儲存時間，則時間會設定為零。  
  
-   如果沒有任何日期存在，但是接收者可以儲存日期，則會使用目前的日期。  
  
-   如果在資料類型中沒有用戶端所使用的時區存在，但是伺服器可以儲存時區，則會將日期儲存在用戶端的時區中。 請注意，這與伺服器行為不同。  
  
-   如果在伺服器類型中沒有時區存在，但是用戶端類型擁有時區，則會先將時間轉換為 UTC，然後再儲存在伺服器上。  
  
-   如果有時間存在，但是接收者無法儲存時間，則會忽略時間元件。  
  
-   如果有日期存在，但是接收者無法儲存日期，則會忽略日期元件。  
  
-   如果在從 C 轉換為 SQL 時發生秒或毫秒的截斷，就會產生包含 SQLSTATE 22008 以及「日期時間欄位溢位」訊息的診斷記錄。  
  
-   如果在從 SQL 轉換為 C 時發生秒或毫秒的截斷，就會產生包含 SQLSTATE 01S07 以及「小數位數截斷」訊息的診斷記錄。  
  
## <a name="in-this-section"></a>本節內容  
 [從 C 轉換成 SQL](datetime-data-type-conversions-from-c-to-sql.md)  
 列出當您從 C 類型轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期/時間類型時應該考量的問題。  
  
 [從 SQL 轉換成 C](datetime-data-type-conversions-from-sql-to-c.md)  
 列出當您從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期/時間類型轉換成 C 類型時應該考量的問題。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC&#41;&#40;的日期和時間改善](date-and-time-improvements-odbc.md)  
  
  
