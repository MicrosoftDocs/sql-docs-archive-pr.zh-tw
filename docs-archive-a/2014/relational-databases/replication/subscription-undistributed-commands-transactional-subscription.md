---
title: 訂用帳戶、未散發的命令 (交易式訂用帳戶、SQL Server 2005 和更新版本) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.subscription.performance.f1
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6bbd82b4f4855c99076404d8b621edca11a7e1e4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699445"
---
# <a name="subscription-undistributed-commands-transactional-subscription-sql-server-2005-and-later"></a>訂閱，未散發的命令 (交易式訂閱，SQL Server 2005 和更新的版本)
  **[未散發的命令]** 索引標籤會顯示散發資料庫中尚未傳遞給選取之訂閱者的命令數目，以及傳遞這些命令的估計時間等相關資訊。 如需在散發資料庫中檢視命令的資訊，請參閱 [sp_replshowcmds &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql)。  
  
## <a name="options"></a>選項  
 **在散發資料庫中，等候要套用到此訂閱者的命令數目**  
 散發資料庫中尚未傳遞給選取之訂閱者的命令數目。 由一個 Transact-SQL 資料操作語言 (DML) 陳述式或一個資料定義語言 (DDL) 陳述式組成的命令。  
  
 **依據過去的效能，估計套用這些命令的時間**  
 估計將命令傳遞給訂閱者所需的時間量。 如果此值大於產生快照集並將其套用至訂閱者所需的時間量，則請考慮重新初始化訂閱者。 如需詳細資訊，請參閱 [重新初始化訂閱](reinitialize-subscriptions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](monitor/start-the-replication-monitor.md)   
 [使用複寫監視器監視效能](monitor/monitor-performance-with-replication-monitor.md)   
 [監視複寫](monitoring-replication.md)  
  
  
