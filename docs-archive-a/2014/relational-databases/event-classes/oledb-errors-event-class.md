---
title: OLEDB Errors 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- OLEDB Errors event class
ms.assetid: 0ce1e906-5d92-42f2-ab38-8771ad5ca008
author: stevestein
ms.author: sstein
ms.openlocfilehash: 97918f1be9c5256fe05c873841ceca98fff3917f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593408"
---
# <a name="oledb-errors-event-class"></a>OLEDB Errors 事件類別
  對 OLE DB 提供者的呼叫若傳回錯誤，[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中就會發生 OLEDB Errors 事件類別。 在追蹤中包含此事件類別，以檢視 OLE DB 提供者的失敗 HRESULT。  
  
 當追蹤中包含 OLEDB Errors 事件類別時，效能負擔需視追蹤期間資料庫發生 OLE DB 提供者錯誤的頻率決定。 如果經常發生這類錯誤，追蹤可能會嚴重妨礙效能。  
  
## <a name="oledb-errors-event-class-data-columns"></a>OLEDB Errors 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|`int`|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|`int`|由 USE *database*語句所指定的資料庫識別碼，或者如果沒有針對指定實例發出 use database 語句，則是預設的*資料庫*。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|`nvarchar`|正在執行使用者陳述式的資料庫名稱。|35|是|  
|錯誤|`int`|由提供者傳回的 HRESULT。|31|是|  
|EventClass|`int`|事件類別 = 61。|27|否|  
|EventSequence|`int`|批次中 OLE DB 事件類別的順序。|51|否|  
|GroupID|`int`|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|`nvarchar`|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IsSystem|`int`|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|LinkedServerName|`nvarchar`|連結伺服器的名稱。|45|是|  
|LoginName|`nvarchar`|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\Username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|LoginSid|`image`|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|MethodName|`nvarchar`|OLE DB 方法的名稱。|47|是|  
|NTDomainName|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|`nvarchar`|Windows 使用者名稱。|6|是|  
|ProviderName|`nvarchar`|OLE DB 提供者的名稱。|46|是|  
|RequestID|`int`|包含陳述式之要求的識別碼。|49|是|  
|SessionLoginName|`nvarchar`|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|`int`|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|`nvarchar`|在 OLE DB 呼叫中傳送與接收的參數。|1|否|  
|TransactionID|`bigint`|由系統指派給交易的識別碼。|4|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Transact-SQL 中的 OLE Automation 物件](../stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
