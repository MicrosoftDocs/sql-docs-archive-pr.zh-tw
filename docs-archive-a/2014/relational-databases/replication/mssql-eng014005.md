---
title: MSSQL_ENG014005 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014005 error
ms.assetid: f168f0d6-cb11-45d4-9781-c374d7f388ee
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d820fd26cceee72b0d08204d6f6ce73a76508e9c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585310"
---
# <a name="mssql_eng014005"></a>MSSQL_ENG014005
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|14005|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|無法卸除發行集。 有它的訂閱存在。|  
  
## <a name="explanation"></a>說明  
 您已嘗試卸除具有一個或多個關聯訂閱的發行集。 發行集僅在沒有關聯的訂閱時方可卸除。  
  
## <a name="user-action"></a>使用者動作  
 先卸除訂閱，然後再卸除發行集。 如果使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 卸除發行集，您可以選擇在卸除發行集之前自動卸除所有關聯的訂閱。 如果使用預存程序，則必須先明確地卸除訂閱。 如需相關資訊，請參閱 [Delete a Push Subscription](delete-a-push-subscription.md) 及 [Delete a Pull Subscription](delete-a-pull-subscription.md)。  
  
 如果發行集不存在訂閱，或者在建立發行集時出現此錯誤，可能有之前的訂閱在移除時未完全清除。 在資料庫上執行 [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)，以移除與複寫相關的所有物件與設定。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
