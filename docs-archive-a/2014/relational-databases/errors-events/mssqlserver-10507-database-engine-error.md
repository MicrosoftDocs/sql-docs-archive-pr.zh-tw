---
title: MSSQLSERVER_10507 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10507 (Database Engine error)
ms.assetid: cd83fa81-ac37-4eda-a3c3-17610b051de2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a80e48948c03b370c07742fabbb3cf8eb3e74315
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706542"
---
# <a name="mssqlserver_10507"></a>MSSQLSERVER_10507
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10507|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_STMT_DOES_NOT_MATCH|  
|訊息文字|無法建立計畫指南 '%.\*ls'，因為 `@stmt` 和 `@module_or_batch` 或是 `@plan_handle` 和 `@statement_start_offset` 所指定的陳述式不符合指定的模組或批次中的任何陳述式。 請將值修改為與模組或批次中的陳述式相符。|  
  
## <a name="explanation"></a>說明  
 指定之模組或批次中的陳述式無法與指定的陳述式或陳述式位移值相符。  
  
## <a name="user-action"></a>使用者動作  
 請將指定的參數值修改為與模組或批次中的陳述式相符。  
  
## <a name="see-also"></a>另請參閱  
 [計劃指南](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
