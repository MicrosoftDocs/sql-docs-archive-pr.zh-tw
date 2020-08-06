---
title: 管理 Text 和 Image 資料行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- data types [ODBC], mapping
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 7b543556-ff36-4d35-ac08-de96223d92cd
author: rothja
ms.author: jroth
ms.openlocfilehash: e9d7d5b0f48c68e8ac911f5e274c9afdb8cfe17d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709294"
---
# <a name="managing-text-and-image-columns"></a>管理 Text 和 Image 資料行
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**text**、 **Ntext**和**image**資料 (也稱為 long 資料) 是字元或二進位字串資料類型，可以保存太大的資料值，使其無法納入**char**、 **Varchar**、 **binary**或**Varbinary**資料行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Text**資料類型會對應至 ODBC SQL_LONGVARCHAR 資料類型;**Ntext**對應至 SQL_WLONGVARCHAR;和**影像**會對應到 SQL_LONGVARBINARY。 某些資料項目 (例如長篇的文件或大型的點陣圖) 可能太大，而無法適當地儲存到記憶體中。 若要從連續部分取出長資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式可讓應用程式呼叫[SQLGetData](../native-client-odbc-api/sqlgetdata.md)。 若要在連續的部分傳送長資料，應用程式可以呼叫[SQLPutData](../native-client-odbc-api/sqlputdata.md)。 在執行時間傳送資料所使用的參數就是所謂的資料執行中參數。  
  
 應用程式實際上可以撰寫或取出任何類型的資料， (不只是使用**SQLPutData**或**SQLGetData**的長資料) ，雖然只有**字元**和**二進位**資料可以在部分中傳送或取出。 不過，如果資料夠小，而無法放入單一緩衝區，通常就沒有理由使用**SQLPutData**或**SQLGetData**。 針對參數或資料行建立單一緩衝區更為容易。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [繫結與未繫結的 Text 和 Image 資料行](bound-vs-unbound-text-and-image-columns.md)  
  
-   [已記錄與未記錄的修改](logged-vs-unlogged-modifications.md)  
  
-   [資料執行中和 Text、ntext 或 Image 資料行](data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
