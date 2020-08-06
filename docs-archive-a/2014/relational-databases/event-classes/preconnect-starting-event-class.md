---
title: PreConnect:Starting 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- PreConnect:Starting Event Class
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
author: stevestein
ms.author: sstein
ms.openlocfilehash: 67b642d369c73cc144af31f835786613766045f9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597811"
---
# <a name="preconnectstarting-event-class"></a>PreConnect:Starting 事件類別
  PreConnect:Starting 事件類別會指出 LOGON 觸發程序或資源管理員分類函數開始執行。  
  
## <a name="preconnectstarting-event-class-data-columns"></a>PreConnect:Starting 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|`int`|215|27|否|  
|SPID|`int`|引發此事件之伺服器處理序的識別碼。|12|是|  
|EventSubClass|`int`|1 代表使用者定義的分類函數。|21|是|  
|StartTime|`datetime`|使用者定義分類函數啟動的時間。|14|是|  
|ObjectID|`int`|使用者定義之分類物件的識別碼。|22|是|  
|ObjectName|`nvarchar(256)`|使用者定義之分類函數的兩段式名稱。 例如，dbo.classifier。|34|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../extended-events/extended-events.md)   
 [PreConnect： Completed 事件類別](preconnect-completed-event-class.md)   
 [資源管理員](../resource-governor/resource-governor.md)  
  
  
