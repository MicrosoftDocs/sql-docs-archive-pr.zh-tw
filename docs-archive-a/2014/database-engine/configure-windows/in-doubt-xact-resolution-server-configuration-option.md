---
title: 不能肯定的交易解析伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- distributed transactions [SQL Server], unresolved transactions
- unresolved transactions
- in-doubt xact resolution option
ms.assetid: 3426fd32-cad2-4f2f-8ca9-e0296cc12703
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6b8db57ef2a4ee85d65e8c25de28ff7ada7994e1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688226"
---
# <a name="in-doubt-xact-resolution-server-configuration-option"></a>不能肯定的交易解析伺服器組態選項
  使用 [不能肯定的交易解析] 選項，可控制 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) 無法解析之交易的預設結果。 無法解析交易的原因，可能與 MS DTC 停機，或在復原時出現未知的交易結果等狀況有關。  
  
 下表列出解析不確定的交易時，可能出現的結果值。  
  
|結果值|描述|  
|-------------------|-----------------|  
|0|無假設結果。 如果 MS DTC 有無法解析的不確定交易，復原即會失敗。|  
|1|假設為認可。 任何 MS DTC 不確定的交易都假設為已認可。|  
|2|假設為中止。 任何 MS DTC 不確定的交易都假設為已中止。|  
  
 若要將停機時間降到最低，系統管理員可將此選項設為「假設為認可」或「假設為中止」，如以下範例所示。  
  
```  
sp_configure 'show advanced options', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'in-doubt xact resolution', 2 -- presume abort  
GO  
RECONFIGURE  
GO  
sp_configure 'show advanced options', 0  
GO  
RECONFIGURE  
GO  
  
```  
  
 或者，系統管理員也可以採用預設值 (無假設結果) 並允許復原失敗，以便記錄 DTC 失敗，如以下範例所示。  
  
```  
sp_configure 'show advanced options', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'in-doubt xact resolution', 1 -- presume commit  
GO  
reconfigure  
GO  
ALTER DATABASE pubs SET ONLINE -- run recovery again  
GO  
sp_configure 'in-doubt xact resolution', 0 -- back to no assumptions  
GO  
sp_configure 'show advanced options', 0  
GO  
RECONFIGURE  
GO  
  
```  
  
 [不能肯定的交易解析] 選項屬於進階選項。 如果您要使用 **sp_configure** 系統預存程序來變更此設定，只有在 [顯示進階選項] 設為 1 時，才能變更 [不能肯定的交易解析]。 設定會立即生效，伺服器不必重新啟動。  
  
> [!NOTE]  
>  在與分散式交易相關的所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上，讓此選項的組態都維持一致，將有助於避免資料不一致。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
