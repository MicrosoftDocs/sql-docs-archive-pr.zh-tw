---
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f26211da21829a0a898dfb36ff9fefd453c7ad44
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699652"
---
# <a name="mssqlserver_21871"></a>MSSQLSERVER_21871
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|21871|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum21871|  
|訊息文字|尚未重新導向資料庫 %s 的發行者 %s。|  
  
## <a name="explanation"></a>說明  
 `sp_validate_replica_hosts_as_publishers` 會檢查散發資料庫中的 MSredirected_publishers 資料表是否存在已識別發行者和發行者資料庫的項目。  找不到任何項目時，`sp_validate_replica_hosts_as_publishers` 就會傳回錯誤 21871。  
  
## <a name="user-action"></a>使用者動作  
 `sp_validate_replica_hosts_as_publishers` 只與重新導向的發行者有關。 如果發行者資料庫是可用性群組的成員，請使用 `sp_redirect_publisher` 預存程序，讓發行者和發行者資料庫與可用性群組的可用性群組接聽程式名稱產生關聯。  
  
  
