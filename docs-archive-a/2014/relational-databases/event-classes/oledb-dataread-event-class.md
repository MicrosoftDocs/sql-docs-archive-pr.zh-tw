---
title: OLEDB DataRead 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- OLEDB DataRead event class
ms.assetid: fb6869ba-3199-4e32-a650-60a5dda2571e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7911e64ca0e272b95f1c88b705ab9aca9ea75483
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592700"
---
# <a name="oledb-dataread-event-class"></a>OLEDB DataRead 事件類別
  當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 呼叫 OLE DB 提供者以執行分散式查詢和遠端預存程序時，會發生 OLEDB DataRead 事件類別。 請在監看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 何時對 OLE DB 提供者發出資料要求呼叫的追蹤中，包含此事件類別。  
  
 當追蹤中包含 OLEDB DataRead 類別時，所產生的負擔量將會相當高。 建議您僅在短期監視特定問題的追蹤內，使用此事件類別。  
  
## <a name="oledb-dataread-event-class-data-columns"></a>OLEDB DataRead 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|`int`|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|`int`|由 *database* 陳述式所指定的資料庫識別碼；如果沒有針對指定執行個體發出 USE *database*陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|`nvarchar`|正在執行使用者陳述式的資料庫名稱。|35|是|  
|Duration|`bigint`|完成 OLE DB 呼叫事件的時間長度。|13|否|  
|EndTime|`datetime`|事件結束的時間。|15|是|  
|錯誤|`int`|給定事件的錯誤號碼。 通常這是存放在 sys.messages 目錄檢視中的錯誤號碼。|31|是|  
|EventClass|`int`|事件類型 = 121。|27|否|  
|EventSequence|`int`|批次中 OLE DB 事件類別的順序。|51|否|  
|EventSubClass|`int`|事件子類別的類型。<br /><br /> 0=正在啟動<br /><br /> 1=已完成|21|否|  
|GroupID|`int`|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|`nvarchar`|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IsSystem|`int`|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|LinkedServerName|`nvarchar`|連結伺服器的名稱。|45|是|  
|LoginName|`nvarchar`|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\Username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|LoginSid|`image`|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|MethodName|`nvarchar`|呼叫方法的名稱。|47|否|  
|NTDomainName|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|`nvarchar`|Windows 使用者名稱。|6|是|  
|ProviderName|`nvarchar`|OLE DB 提供者的名稱。|46|是|  
|RequestID|`int`|包含陳述式之要求的識別碼。|49|是|  
|SessionLoginName|`nvarchar`|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|`Int`|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|`nvarchar`|在 OLE DB 呼叫中傳送與接收的參數。|1|否|  
|TransactionID|`bigint`|由系統指派給交易的識別碼。|4|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Transact-SQL 中的 OLE Automation 物件](../stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
