---
title: Deprecation Announcement 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- deprecation [SQL Server], events announced stage
- Deprecation Announcement event class
ms.assetid: 46fc578f-3c97-477f-879c-8a1b2cfd9d58
author: stevestein
ms.author: sstein
ms.openlocfilehash: c622d4d0c39d685b7808c6c4cf1bebbe7f455b12
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87701143"
---
# <a name="deprecation-announcement-event-class"></a>Deprecation Announcement 事件類別
  當您使用的功能將從 **未來版本中移除，但不會從下一個主要版本中移除時，就會發生** Deprecation Announcement [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]事件類別。 為了使應用程式的使用壽命達到最久，請避免使用會造成 **Deprecation Announcement** 事件類別或 **Deprecation Final Support** 事件類別的功能。  
  
## <a name="deprecation-announcement-event-class-data-columns"></a>Deprecation Announcement 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|`int`|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|`int`|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 如果在追蹤中擷取到 `ServerName` 資料行，而且伺服器可以使用，則 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 會顯示資料庫名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|`nvarchar`|正在執行使用者陳述式的資料庫名稱。|35|是|  
|EventClass|`int`|事件類型 = 125。|27|否|  
|EventSequence|`int`|要求中的給定事件順序。|51|否|  
|HostName|`nvarchar`|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IntegerData2|`int`|所執行之陳述式的結束位移 (以位元組為單位)。|55|是|  
|IsSystem|`int`|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|LoginName|`nvarchar`|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|LoginSid|`image`|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NTDomainName|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|`nvarchar`|Windows 使用者名稱。|6|是|  
|ObjectID|`int`|已被取代功能的識別碼。|22|是|  
|ObjectName|`nvarchar`|已被取代功能的名稱。|34|是|  
|Offset|`int`|預存程序或批次內之陳述式的起始位移。|61|是|  
|RequestID|`int`|包含陳述式之要求的識別碼。|49|是|  
|ServerName|`nvarchar`|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|SessionLoginName|`nvarchar`|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到，並以 Login2 的身分 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行語句，則會 `SessionLoginName` 顯示 Login1 並 `LoginName` 顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|`int`|事件發生所在之工作階段的識別碼。|12|是|  
|SqlHandle|`image`|可用於識別 SQL 批次或預存程序的二進位控制代碼。|63|是|  
|StartTime|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|`ntext`|與追蹤中所擷取的事件類別有關的文字值。|1|是|  
|TransactionID|`bigint`|由系統指派給交易的識別碼。|4|是|  
|XactSequence|`bigint`|描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Deprecation Final Support 事件類別](deprecation-final-support-event-class.md)   
 [SQL Server 2014 中已被取代的 Database Engine 功能](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)  
  
  
