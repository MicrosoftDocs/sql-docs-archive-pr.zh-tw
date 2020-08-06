---
title: 了解資料庫引擎錯誤 | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server], about errors
- errors [SQL Server], Database Engine
- errors [SQL Server]
- Database Engine [SQL Server], errors
ms.assetid: ddaca9d3-956f-46a5-8cd3-a7a15ec75878
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: aa8747066433488a8517d2931ad51f082075a66f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596693"
---
# <a name="understanding-database-engine-errors"></a>了解 Database Engine 錯誤
  下表描述 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 所引發錯誤的屬性。  
  
|屬性|描述|  
|---------------|-----------------|  
|錯誤號碼|每一則錯誤訊息都有唯一的錯誤號碼。|  
|錯誤訊息字串|錯誤訊息包含錯誤原因的診斷資訊。 許多錯誤訊息都有用來插入資訊 (例如產生錯誤的物件名稱) 的替代變數。|  
|Severity|嚴重性指出錯誤的嚴重程度。 嚴重性低 (例如 1 或 2) 的錯誤是參考訊息或低階警告。 嚴重性高的錯誤指出應該儘快處理的問題。 如需有關嚴重性的詳細資訊，請參閱 [Database Engine 錯誤嚴重性](database-engine-error-severities.md)。|  
|State|對於 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，程式碼的多個點都可能會產生某些錯誤訊息。 例如，在許多不同情況下，都有可能產生 1105 錯誤。 每個產生錯誤的特定狀況，都會指派唯一的狀態碼。<br /><br /> 檢視內含已知問題之資訊的資料庫時 (例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知識庫)，可以使用狀態碼來判斷所記錄的問題與您遇到的錯誤是否相同。 例如，如果知識庫文件描述狀態為 2 的 1105 錯誤，而您收到之 1105 錯誤訊息的狀態為 3，則錯誤原因可能不是文件中所報告的原因。<br /><br /> [!INCLUDE[msCoName](../../includes/msconame-md.md)] 支援工程師也可以使用錯誤中的狀態碼，來找出原始程式碼中引發錯誤碼的位置。 這項資訊可能會提供如何診斷問題的其他想法。|  
|程序名稱|這是發生錯誤之預存程序或觸發程序的名稱。|  
|行號|指出批次、預存程序、觸發程序或函數中的哪個陳述式產生錯誤。|  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體中的所有系統和使用者自訂的錯誤訊息都包含在 **sys.messages** 目錄檢視中。 您可以使用 RAISERROR 陳述式，將使用者自訂的錯誤傳回給應用程式。  
  
 所有資料庫 API，例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] **SQLClient** 命名空間、ActiveX Data Objects (ADO)、OLE DB 和開放式資料庫連線 (ODBC)，都會報告基本錯誤屬性。 這項資訊包括錯誤號碼和訊息字串。 不過，並非所有 API 都會報告所有其他錯誤屬性。  
  
 您可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼中，使用相關聯之 CATCH 區塊範圍內的 ERROR_LINE、ERROR_MESSAGE、ERROR_NUMBER、ERROR_PROCEDURE、ERROR_SEVERITY 和 ERROR_STATE 等函數，來取得在 TRY…CATCH 建構的 TRY 區塊範圍內出現之錯誤的相關資訊。 如需詳細資訊，請參閱 [TRY...CATCH &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/try-catch-transact-sql)。  
  
## <a name="examples"></a>範例  
 下列範例會查詢 `sys.messages` 目錄檢視，以傳回 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中具有英文文字 (`1033`) 之所有系統和使用者自訂錯誤訊息的清單。  
  
```  
SELECT  
    message_id,  
    language_id,  
    severity,  
    is_event_logged,  
    text  
  FROM sys.messages  
  WHERE language_id = 1033;  
```  
  
 如需詳細資訊，請參閱 [sys.messages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages)。  
  
## <a name="see-also"></a>另請參閱  
 [sys.messages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages)   
 [RAISERROR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/raiserror-transact-sql)   
 [@@ERROR &#40;Transact-SQL&#41;](/sql/t-sql/functions/error-transact-sql)   
 [TRY...CATCH &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/try-catch-transact-sql)   
 [ERROR_LINE &#40;Transact-SQL&#41;](/sql/t-sql/functions/error-line-transact-sql)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](/sql/t-sql/functions/error-message-transact-sql)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](/sql/t-sql/functions/error-number-transact-sql)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/functions/error-procedure-transact-sql)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](/sql/t-sql/functions/error-severity-transact-sql)   
 [ERROR_STATE &#40;Transact-SQL&#41;](/sql/t-sql/functions/error-state-transact-sql)  
  
  
