---
title: MSSQLSERVER_15599 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 15f1b3eb6d97837f1c1c4a9944535cade5b31300
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598946"
---
# <a name="mssqlserver_15599"></a>MSSQLSERVER_15599
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|15599|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|訊息文字|本機暫存物件上不能設定稽核與權限。|  
  
## <a name="explanation"></a>說明  
 為本機或全域暫存物件設定稽核與權限不會有任何作用。 陳述式不會產生錯誤 (作業將回報成功)，但不會有任何作用。  
  
 此行為尚未改變，但從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 起，使用者將會看到此訊息文字警示。  
  
## <a name="user-action"></a>使用者動作  
 無須採取任何動作，但可考慮移除所有嘗試為本機或全域暫存物件設定稽核或權限的陳述式。  
  
  
