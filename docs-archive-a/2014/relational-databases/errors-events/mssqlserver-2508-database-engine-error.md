---
title: MSSQLSERVER_2508 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2508 (Database Engine error)
ms.assetid: c37d40e5-c665-4d66-a727-5cb845634fcc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 11dd1c72c8cae868b7ebcb02e72ef0db81aeafe2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699640"
---
# <a name="mssqlserver_2508"></a>MSSQLSERVER_2508
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2508|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_OUT_OF_DATE_PAGE_OR_ROW_COUNT|  
|訊息文字|物件 "%.\*ls"，索引識別碼 %d，分割區識別碼 %I64d，配置單位識別碼 %I64d (類型 %.\*ls) 的 %.*ls 計數不正確。 請執行 DBCC UPDATEUSAGE。|  
  
## <a name="explanation"></a>說明  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 版本中，資料表和索引資料列計數值與頁數計數值可能會變得不正確。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 之前的版本中建立的資料庫可能包含不正確的計數。 DBCC CHECKDB 已經增強為可以偵測到這些錯誤，而且會在遇到錯誤時傳回這則警告訊息。  
  
## <a name="user-action"></a>使用者動作  
 針對指定的物件或索引，或針對包含此物件的資料庫執行 DBCC UPDATEUSAGE，以便更正無效的計數。  
  
  
