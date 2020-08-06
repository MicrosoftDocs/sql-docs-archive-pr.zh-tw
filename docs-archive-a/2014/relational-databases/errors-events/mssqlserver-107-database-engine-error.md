---
title: MSSQLSERVER_107 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 107 (Database Engine error)
ms.assetid: f33f514c-56aa-42e2-841b-e91244da90e2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b9388bbda6f00b1aafd02caee1b6a7b8387564f9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598446"
---
# <a name="mssqlserver_107"></a>MSSQLSERVER_107
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|107|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|P_NOCORRMATCH|  
|訊息文字|資料行前置詞 '%.*ls' 與用於查詢中的資料表名稱或別名名稱不符。|  
  
## <a name="explanation"></a>說明  
 查詢的選取清單包含以不正確方式使用資料行前置詞限定的星號 (*)。 這項錯誤可能會在下列情況下傳回：  
  
-   資料行前置詞沒有對應至用於查詢中的任何資料表或別名名稱。 例如，下列陳述式會使用別名名稱 (`T1`) 當做資料行前置詞，但是此別名並未定義於 FROM 子句中。  
  
    ```  
    SELECT T1.* FROM dbo.ErrorLog;  
    ```  
  
-   當您在 FROM 子句中提供資料表的別名名稱時，資料表名稱就會指定為資料行前置詞。 例如，下列陳述式會使用資料表名稱 `ErrorLog` 當做資料行前置詞。不過，資料表具有在 FROM 子句中定義的別名 (`T1`)。  
  
    ```  
    SELECT ErrorLog.* FROM dbo.ErrorLog AS T1;  
    ```  
  
     如果已經在 FROM 子句中提供資料表名稱的別名，您就只能使用此別名當做資料表中資料行的前置詞。  
  
## <a name="user-action"></a>使用者動作  
 針對在查詢之 FROM 子句中指定的資料表名稱或別名名稱，比對資料行前置詞。 例如，您可以依照下列方式更正上述陳述式：  
  
```  
SELECT T1.* FROM dbo.ErrorLog AS T1;  
```  
  
 或  
  
```  
SELECT ErrorLog.* FROM dbo.ErrorLog;  
```  
  
## <a name="see-also"></a>另請參閱  
 [MSSQLSERVER_4104](mssqlserver-4104-database-engine-error.md)  
  
  
