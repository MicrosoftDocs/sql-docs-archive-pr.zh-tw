---
title: MSSQLSERVER_10502 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10502 (Database Engine error)
ms.assetid: 26d9b64d-4299-4b55-92d0-0a32a3688c0a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: eeec3a3adf318cadc96501938f8a5565f1c07670
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585488"
---
# <a name="mssqlserver_10502"></a>MSSQLSERVER_10502
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10502|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_DUP_FOUND|  
|訊息文字|無法建立計畫指南 '%.*ls'，因為 @stmt 和 @module_or_batch 或是 @plan_handle 和 @statement_start_offset 所指定的陳述式與資料庫中現有的計畫指南 '%.\*ls' 相符。 請卸除現有計畫指南後，再建立新的計畫指南。|  
  
## <a name="explanation"></a>說明  
 指定之陳述式的計畫指南已存在。  
  
## <a name="user-action"></a>使用者動作  
 請卸除現有計畫指南後，再建立新的計畫指南。  
  
## <a name="see-also"></a>另請參閱  
 [計劃指南](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
