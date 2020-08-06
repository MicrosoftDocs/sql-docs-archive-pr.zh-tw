---
title: MSSQLSERVER_9790 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6d6d065d4a0e841da3b5ecb84f902df17dcfd60c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595035"
---
# <a name="mssqlserver_9790"></a>MSSQLSERVER_9790
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|9790|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SB3_XMIT_ERROR_ENTRANCE_BROKER_SINGLE_USER|  
|訊息文字|無法路由內送訊息。 包含路由資訊的系統資料庫 MSDB 正處於單一使用者 (SINGLE USER) 模式。|  
  
## <a name="explanation"></a>說明  
 嘗試分類離線接收的訊息時發生錯誤，因為 MSDB 資料庫處於單一使用者模式中。  
  
## <a name="user-action"></a>使用者動作  
 使用 ALTER DATABASE 命令，將 MSDB 變更為 MULTI USER 模式。  
  
  
