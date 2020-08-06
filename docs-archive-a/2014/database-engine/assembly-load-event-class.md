---
title: Assembly Load 事件類別 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Assembly Load event class
ms.assetid: cfb0b69d-4ce0-4067-a3df-d82775e57886
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: a16659d42355b7999d86aad3aa3e8d1024589ba2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87701965"
---
# <a name="assembly-load-event-class"></a>Assembly Load 事件類別
  在執行載入組件的要求時，會發生 **Assembly Load** 事件類別。  
  
 您可以在想要監視組件載入的追蹤內部加入 **Assembly Load** 事件類別。 這有助於使用 Common Language Runtime (CLR) 的查詢進行疑難排解、執行 CLR 查詢且執行緩慢的伺服器進行疑難排解，或監視伺服器來收集使用者、資料庫、成功或關於組件載入的其他資訊。  
  
## <a name="assembly-load-event-class-data-columns"></a>Assembly Load 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|要求載入的應用程式名稱。|10|是|  
|**ClientProcessID**|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|**int**|由 USE database 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE database 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**DatabaseName**|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|**EventSequence**|**int**|要求中的給定事件順序。|51|否|  
|**GroupID**|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|**HostName**|**nvarchar**|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|**LoginName**|**nvarchar**|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|**LoginSID**|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 **sys.server_principals** 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|Windows 使用者名稱。|6|是|  
|**Exchange Spill**|**int**|組件識別碼。|22|是|  
|**ObjectName**|**nvarchar**|組件的完整名稱。|34|是|  
|**RequestID**|**int**|包含陳述式之要求的識別碼。|49|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SessionLoginName**|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|「成功」|**int**|指出組件載入成功 (1) 或失敗 (0)。|23|是|  
|**TextData**|**ntext**|如果載入成功則為「組件載入成功」；否則為「組件載入失敗」。|1|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../relational-databases/extended-events/extended-events.md)   
 [組件 &#40;Database Engine&#41](../relational-databases/clr-integration/assemblies-database-engine.md)  
  
  
