---
title: MSSQLSERVER_1461 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6667728b2cc134632ddc538b662d73533ee4d6ef
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598952"
---
# <a name="mssqlserver_1461"></a>MSSQLSERVER_1461
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|1461|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBM_SAFETY_MISMATCH|  
|訊息文字|在各伺服器上偵測到資料庫 "%.*ls" 的不同資料庫鏡像安全性層級。 將會使用 FULL 安全性層級。|  
  
## <a name="explanation"></a>說明  
 由於主體和鏡像資料庫上的交易安全性設定不一致，因此，當修改交易安全性層級時，鏡像連接會中斷。 將會使用完整交易安全性的預設安全性設定。 工作階段將以高安全性模式執行。  
  
## <a name="user-action"></a>使用者動作  
 若要將交易安全性設為關閉，請在主體資料庫上重新執行 ALTER DATABASE *database_name* SET PARTNER SAFETY OFF 陳述式。  
  
  
