---
title: Showplan Statistics Profile 事件類別 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Showplan Statistics Profile event class
ms.assetid: fa9e1330-a217-491c-ad7c-2c1c4015d1bb
author: stevestein
ms.author: sstein
ms.openlocfilehash: 393f30252d2689deb63d1bd540d6db3673f84f73
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606849"
---
# <a name="showplan-statistics-profile-event-class"></a>Showplan Statistics Profile 事件類別
  當 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行 SQL 陳述式時，會發生 Showplan Statistics Profile 事件類別。 包含的資訊是 Showplan XML Statistics Profile 事件類別中可用資訊的子集。  
  
 Showplan Statistics Profile 事件類別會顯示完整的編譯時間資料；包含 Showplan Statistics Profile 的追蹤會造成顯著的效能負擔。 若要減少此問題，此事件類別請限用於追蹤對特定問題的短期監視。  
  
 如果追蹤中包含 Showplan Statistics Profile 事件類別，則必須選取 BinaryData 資料行。 否則，此事件類別的資訊將不會顯示在追蹤結果中。  
  
## <a name="showplan-statistics-profile-event-class-data-columns"></a>Showplan Statistics Profile 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|BinaryData|`image`|查詢的預估成本。|2|否|  
|ClientProcessID|`int`|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|`int`|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|`nvarchar`|正在執行使用者陳述式的資料庫名稱。|35|是|  
|EventClass|`int`|事件類型 = 98。|27|否|  
|EventSequence|`int`|要求中的給定事件順序。|51|否|  
|GroupID|`int`|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|`nvarchar`|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IntegerData|`int`|傳回的資料列預估總數。|25|是|  
|IsSystem|`int`|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|LineNumber|`int`|顯示包含錯誤的行號。|5|是|  
|LoginName|`nvarchar`|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|LoginSID|`image`|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|否|  
|NestLevel|`int`|代表 @@NESTLEVEL 所傳回之資料的整數。|29|是|  
|NTDomainName|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|ObjectID|`int`|系統指派給物件的識別碼。|22|是|  
|ObjectName|`nvarchar`|正在參考之物件的名稱。|34|是|  
|ObjectType|`int`|代表參與事件之物件類型的值。 此值對應至 sys.objects 中的類型資料行。 針對各值，請參閱 [ObjectType 追蹤事件資料行](objecttype-trace-event-column.md)。|28|是|  
|RequestID|`int`|包含陳述式之要求的識別碼。|49|是|  
|ServerName|`nvarchar`|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|SessionLoginName|`nvarchar`|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|`int`|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|TransactionID|`bigint`|由系統指派給交易的識別碼。|4|是|  
|XactSequence|`bigint`|用來描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [執行程序邏輯和實體運算子參考](../showplan-logical-and-physical-operators-reference.md)   
 [Showplan XML Statistics Profile 事件類別](showplan-xml-statistics-profile-event-class.md)  
  
  
