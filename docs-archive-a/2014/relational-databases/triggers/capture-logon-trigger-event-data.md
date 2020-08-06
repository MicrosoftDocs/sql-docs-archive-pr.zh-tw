---
title: 擷取登入觸發程序事件資料 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e05b1ab4-c10b-402a-9591-f6ec1e3db8c0
author: rothja
ms.author: jroth
ms.openlocfilehash: b11323702d7468d07783b4d1c763dba691479d9c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606153"
---
# <a name="capture-logon-trigger-event-data"></a>擷取登入觸發程序事件資料
  若要擷取有關 LOGON 事件的 XML 資料，以用於登入觸發程序內部，請使用 [EVENTDATA](/sql/t-sql/functions/eventdata-transact-sql) 函式。 LOGON 事件會傳回下列事件資料結構描述：  
  
 `<EVENT_INSTANCE>`  
  
 `<EventType>event_type</EventType>`  
  
 `<PostTime>post_time</PostTime>`  
  
 `<SPID>spid</SPID>`  
  
 `<ServerName>server_name</ServerName>`  
  
 `<LoginName>login_name</LoginName>`  
  
 `<LoginType>login_type</LoginType>`  
  
 `<SID>sid</SID>`  
  
 `<ClientHost>client_host</ClientHost>`  
  
 `<IsPooled>is_pooled</IsPooled>`  
  
 `</EVENT_INSTANCE>`  
  
 `<EventType>`  
 包含 `LOGON`。  
  
 `<PostTime>`  
 包含要求建立工作階段的時間。  
  
 `<SID>`  
 包含所指定登入名稱的安全識別碼 (SID) 之 Base 64 編碼二進位資料流。  
  
 `<ClientHost>`  
 包含建立連接的來源用戶端之主機名稱。 如果用戶端和伺服器名稱相同，這個值會是 '`<local_machine>`'。 否則會是用戶端的 IP 位址。  
  
 `<IsPooled>`  
 如果是利用連接共用來重複使用連接，這會是 `1` 。 否則，這個值便為 `0`。  
  
  
