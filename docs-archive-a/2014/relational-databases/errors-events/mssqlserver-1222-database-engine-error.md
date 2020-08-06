---
title: MSSQLSERVER_1222 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1222 (Database Engine error)
ms.assetid: c5b1c2f4-f591-4cc1-aa17-204636a27f29
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ac3fe9314386836633a11f17d6775c75019de93a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584556"
---
# <a name="mssqlserver_1222"></a>MSSQLSERVER_1222
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|1222|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LK_TIMEOUT|  
|訊息文字|鎖定要求的逾時期間已過。|  
  
## <a name="explanation"></a>說明  
 其他交易鎖定必要資源的時間比這項查詢可以等候的時間還長。  
  
## <a name="user-action"></a>使用者動作  
 執行下列工作來減少問題：  
  
1.  如果可以的話，請找出鎖定必要資源的交易。 使用 **sys.dm_os_waiting_tasks** 和 **sys.dm_tran_locks** 動態管理檢視。  
  
2.  如果交易仍然鎖定資源，請依適當情況結束該交易。  
  
3.  重新執行查詢。  
  
 如果這項錯誤經常發生，請變更鎖定逾時期限，或請修改造成問題的交易，以縮短這些交易鎖定資源的時間。  
  
  
