---
title: MSSQLSERVER_3961 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f55be9288b3c2e559633d0f67709829466fc8815
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599517"
---
# <a name="mssqlserver_3961"></a>MSSQLSERVER_3961
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|3961|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|XACT_METADATA_INVALID|  
|訊息文字|資料庫 '%.*ls' 中的快照集隔離交易失敗，因為這個交易啟動之後，另一個並行交易的 DDL 陳述式修改了此陳述式存取的物件。  因為中繼資料並未建立版本，因此不允許此情況發生。 如果與快照集隔離混合，中繼資料的並行更新可能會導致不一致的問題。|  
  
## <a name="explanation"></a>說明  
 如果您要查詢快照隔離下的中繼資料，而且有並行 DDL 陳述式會更新在快照隔離下受到存取的中繼資料，就會發生此錯誤。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援中繼資料的版本控制。 基於這個理由，可在快照隔離下執行的明確交易之中執行的 DDL 作業會受到限制。 根據定義，隱含交易是單一陳述式，即便使用 DDL 陳述式，也能強制執行快照集隔離的語意。 在 BEGIN TRANSACTION 陳述式之後，不允許在快照隔離下執行下列 DDL 陳述式：ALTER TABLE、CREATE INDEX、CREATE XML INDEX、ALTER INDEX、DROP INDEX、DBCC REINDEX、ALTER PARTITION FUNCTION、ALTER PARTITION SCHEME 或是任何通用語言執行平台 (CLR) DDL 陳述式。 在隱含交易內使用快照集隔離時，這些陳述式會受到允許。 根據定義，隱含交易是單一陳述式，即便使用 DDL 陳述式，也能強制執行快照集隔離的語意。  
  
## <a name="user-action"></a>使用者動作  
 將快照隔離等級變更為非快照隔離等級，例如在查詢中繼資料之前認可的讀取。  
  
  
