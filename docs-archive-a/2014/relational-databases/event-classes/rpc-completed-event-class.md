---
title: RPC:Completed 事件類別 | Microsoft 文件
ms.custom: ''
ms.date: 12/04/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- RPC:Completed event class
ms.assetid: 0d526201-94c9-4e4c-afb1-4213df1815ba
author: stevestein
ms.author: sstein
ms.openlocfilehash: a16d34ca8865174d9d05dc08f01402a9d87187b4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584536"
---
# <a name="rpccompleted-event-class"></a>RPC:Completed 事件類別
  RPC:Completed 事件類別表示已經完成遠端程序呼叫。  
  
## <a name="rpccompleted-event-class-data-columns"></a>RPC:Completed 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|BinaryData|`image`|這是一個二進位值，會隨著追蹤所擷取的事件類別而不同。|2|是|  
|ClientProcessID|`int`|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|CPU|`int`|事件使用的 CPU 時間量。 自 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始以毫秒為單位。 舊版中的單位是毫秒。|18|是|  
|DatabaseID|`int`|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|`nvarchar`|正在執行使用者陳述式的資料庫名稱。|35|是|  
|Duration|`bigint`|事件花費的時間量。 自 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]開始以毫秒為單位。 舊版中的單位是毫秒。|13|是|  
|EndTime|`datetime`|遠端程序呼叫的結束時間。|15|是|  
|錯誤|`int`|給定事件的錯誤號碼。<br /><br /> 0=確定<br /><br /> 1=錯誤<br /><br /> 2=中止<br /><br /> 3=已略過|31|是|  
|EventClass|`int`|事件類別 = 10。|27|否|  
|EventSequence|`int`|要求中的給定事件順序。|51|否|  
|GroupID|`int`|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|`nvarchar`|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IsSystem|`int`|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|LoginName|`nvarchar`|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|LoginSid|`image`|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NTDomainName|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|`nvarchar`|Windows 使用者名稱。|6|是|  
|ObjectName|`nvarchar`|正在參考之物件的名稱。|34|是|  
|讀取|`bigint`|遠端程序呼叫所發出的分頁讀取數。|16|是|  
|RequestID|`int`|包含陳述式之要求的識別碼。|49|是|  
|RowCounts|`bigint`|RPC 批次中資料列的數目。|48|是|  
|ServerName|`nvarchar`|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26||  
|SessionLoginName|`nvarchar`|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|`int`|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|`ntext`|遠端程序呼叫的文字。|1|是|  
|TransactionID|`bigint`|由系統指派給交易的識別碼。|4|是|  
|寫入|`bigint`|遠端程序呼叫所發出的分頁寫入數。|17|是|  
|XactSequence|`bigint`|描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
