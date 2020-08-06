---
title: Broker:Forwarded Message Sent 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Forwarded Message Sent event class
ms.assetid: d0ef74d9-a4ef-4918-aa21-6b267e85569f
author: stevestein
ms.author: sstein
ms.openlocfilehash: fa2748efec393aaa68dd23349d208ae00b64bb5e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699571"
---
# <a name="brokerforwarded-message-sent-event-class"></a>Broker:Forwarded Message Sent 事件類別
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 Service Broker 轉寄訊息時，會產生 Broker:Forwarded Message Sent 事件。  
  
## <a name="brokerforwarded-message-sent-event-class-data-columns"></a>Broker:Forwarded Message Sent 事件類別資料行  
  
|資料行|類型|描述|資料行編號|可篩選|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|`nvarchar`|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|BigintData1|`bigint`|訊息序號。|52|否|  
|ClientProcessID|`int`|主機電腦指派給用戶端應用程式執行中處理序的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|`int`|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database*陳述式，則是預設資料庫的識別碼。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 就會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DBUserName|`nvarchar`|訊息來源服務的 Broker 執行個體識別碼。|40|否|  
|EventClass|`int`|擷取的事件類別類型。 Broker:Forwarded Message Sent 永遠是 139。|27|否|  
|EventSequence|`int`|此事件的序號。|51|否|  
|FileName|`nvarchar`|送出訊息的服務名稱。|36|否|  
|GUID|`uniqueidentifier`|對話的交談識別碼。 此識別碼是以訊息的一部份傳送，並在交談的兩端之間共用。|54|否|  
|HostName|`nvarchar`|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IndexID|`int`|轉寄訊息的躍點剩餘數目。|24|否|  
|IntegerData|`int`|轉寄訊息的片段號碼。|25|否|  
|IsSystem|`int`|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|否|  
|LoginSid|`image`|已登入之使用者的安全性識別碼 (SID)。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NTDomainName|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|`nvarchar`|擁有產生此事件之連接的使用者名稱。|6|是|  
|ObjectId|`int`|在轉寄訊息時，轉寄訊息的存留時間值。|22|否|  
|ObjectName|`nvarchar`|轉寄訊息的訊息識別碼。|34|否|  
|OwnerName|`nvarchar`|將訊息導向的 Broker 識別碼。|37|否|  
|RoleName|`nvarchar`|交談控制代碼的角色。 值為下列其中之一：<br /><br /> 起始端。 此 Broker 起始了交談。<br /><br /> Target。 此 Broker 是交談的目標。|38|否|  
|ServerName|`nvarchar`|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|SPID|`int`|由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指派給用戶端關聯之處理序的伺服器處理序識別碼。|12|是|  
|StartTime|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|Success|`int`|在轉寄處理序期間所耗用的時間量。|23|否|  
|TargetLoginName|`nvarchar`|此執行個體要傳送訊息的網路位址。 請注意這個位址有可能與訊息的最終目的地不同。|42|否|  
|TargetUserName|`nvarchar`|訊息的起始端服務名稱。|39|否|  
|TransactionID|`bigint`|系統指派的交易識別碼。|4|否|  
  
  
