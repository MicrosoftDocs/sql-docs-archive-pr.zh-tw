---
title: MSSQLSERVER_10534 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10534 (Database Engine error)
ms.assetid: e65bb118-99d5-4fdb-b1d5-0ec70f0a677b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 793bb0bf5048e30624d9566f65e7c6752bd14386
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699739"
---
# <a name="mssqlserver_10534"></a>MSSQLSERVER_10534
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10534|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_INVALID_PARAMS|  
|訊息文字|無法建立計畫指南 '%.\*ls'，因為指定的 `@params` 值無效。 請以 *parameter_name parameter_type* 格式指定值，或指定 NULL。|  
  
## <a name="explanation"></a>說明  
 針對 `@params` 指定的值無效。  
  
## <a name="user-action"></a>使用者動作  
 請以 *parameter_name parameter_type* 格式指定值，或指定 NULL。  
  
## <a name="see-also"></a>另請參閱  
 [計劃指南](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
