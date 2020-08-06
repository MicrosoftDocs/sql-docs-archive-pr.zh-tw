---
title: Database Mail 訊息物件 | Microsoft 文件
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], host databases
- Database Mail [SQL Server], messaging objects
- mail host databases [SQL Server]
- host databases [Database Mail]
ms.assetid: 5aa2886e-1db1-4066-85df-57ccf4538c54
author: stevestein
ms.author: sstein
ms.openlocfilehash: d284d3ef1d0ac349dea95b1a6a134cb2429e6e4c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709606"
---
# <a name="database-mail-messaging-objects"></a>Database Mail 訊息物件
  **msdb** 資料庫是 Database Mail 主機資料庫。 這個資料庫包含 Database Mail 的預存程序和訊息物件。 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 包含 [Database Mail 組態精靈]，用以啟用 Database Mail、建立和管理設定檔及帳戶，以及設定 Database Mail 選項。  
  
##  <a name="objects-in-msdb-database"></a><a name="ComponentsAndConcepts"></a>**msdb** 資料庫中的物件  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 必須在 **msdb** 資料庫中加以啟用。 不過，Database Mail 不會使用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 網路。 因此，使用者並不需要建立 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 端點來使用 Database Mail。 外部 Database Mail 處理序會使用標準 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接來與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]進行通訊。  
  
 啟用 Database Mail 時，Database Mail 會公開 **msdb** 資料庫中的下列物件。  
  
 這些物件是郵件主機資料庫中的 Database Mail 介面。 所安裝的其他物件則可執行上列物件所提供的功能。 不過，那些物件會保留給內部使用。  
  
|名稱|類型|描述|  
|----------|----------|-----------------|  
|[sysmail_allitems &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-allitems-transact-sql)|`View`|列出提交至 Database Mail 的所有訊息。|  
|[sysmail_event_log &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-event-log-transact-sql)|`View`|列出關於 [Database Mail External Program](database-mail-external-program.md)行為的訊息。|  
|[sysmail_faileditems &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-faileditems-transact-sql)|`View`|關於 Database Mail 無法傳送之訊息的資訊。|  
|[sysmail_mailattachments &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql)|`View`|關於 Database Mail 訊息之附加檔案的資訊。|  
|[sysmail_sentitems &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-sentitems-transact-sql)|`View`|關於使用 Database Mail 傳訊之訊息的資訊。|  
|[sysmail_unsentitems &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql)|`View`|關於 Database Mail 目前嘗試傳送之訊息的資訊。|  
|[sp_send_dbmail &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql)|`Stored Procedure`|使用 Database Mail 來傳送電子郵件訊息。|  
|[sysmail_delete_log_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql)|`Stored Procedure`|刪除 Database Mail 記錄檔中的訊息。|  
|[sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql)|`Stored Procedure`|刪除 Database Mail 佇列中的郵件項目。|  
|[sysmail_help_status_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-help-status-sp-transact-sql)|`Stored Procedure`|指示 Database Mail 是否已啟動。|  
|[sysmail_start_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql)|`Stored Procedure`|啟動外部程式所使用的 Service Broker 物件。 根據預設會啟動這些物件。|  
|[sysmail_stop_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql)|`Stored Procedure`|停止外部程式所使用的 Service Broker 物件。|  
  

  
## <a name="see-also"></a>另請參閱  
 [Database Mail](database-mail.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
