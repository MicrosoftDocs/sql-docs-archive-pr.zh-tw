---
title: SP:Completed 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SP:Completed event class
ms.assetid: 7636a433-5d32-4562-8f5a-694f8e2beeca
author: stevestein
ms.author: sstein
ms.openlocfilehash: 50a4fc1d3fdc5feacd13e516cfe3b5ddd02277bc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592047"
---
# <a name="spcompleted-event-class"></a>SP:Completed 事件類別
  SP:Completed 事件類別指出預存程序已完成執行。  
  
## <a name="spcompleted-event-class-data-columns"></a>SP:Completed 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|`int`|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|`int`|執行預存程序之資料庫的識別碼。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|`nvarchar`|執行預存程序之資料庫的名稱。|35|是|  
|Duration|`bigint`|事件所花費的時間量 (以百萬分之一秒為單位)。|13|是|  
|EndTime|`datetime`|事件結束的時間。 此資料行不會因啟動的事件類別 (如 SQL:BatchStarting 或 SP:Starting) 而擴展。|15|是|  
|EventClass|`int`|事件類型 = 43。|27|否|  
|EventSequence|`int`|要求中的給定事件順序。|51|否|  
|GroupID|`int`|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|`nvarchar`|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IsSystem|`int`|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|LineNumber|`int`|顯示呼叫這個預存程序之執行陳述式的行號。|5|是|  
|LoginName|`nvarchar`|使用者的登入名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|LoginSid|`image`|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NestLevel|`int`|預存程序的巢狀層級。|29|是|  
|NTDomainName|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|`nvarchar`|Windows 使用者名稱。|6|是|  
|ObjectID|`int`|系統指派的預存程序識別碼。|22|是|  
|ObjectName|`nvarchar`|正在參考之物件的名稱。|34|是|  
|ObjectType|`int`|已呼叫的預存程序類型。 這個值會對應到 sys.objects 目錄檢視中的類型資料行。 針對各值，請參閱 [ObjectType 追蹤事件資料行](objecttype-trace-event-column.md)。|28|是|  
|RequestID|`int`|包含陳述式之要求的識別碼。|49|是|  
|RowCounts|`bigint`|在此預存程序中所有陳述式的資料列數目。|48|是|  
|ServerName|`nvarchar`|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|SessionLoginName|`nvarchar`|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SourceDatabaseID|`int`|物件所存在之資料庫的識別碼。|62|是|  
|SPID|`int`|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|`ntext`|預存程序呼叫的文字。|1|是|  
|TransactionID|`bigint`|由系統指派給交易的識別碼。|4|是|  
|XactSequence|`bigint`|描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
