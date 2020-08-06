---
title: 90或更新版本相容性模式中的 views 不允許使用 FOR BROWSE |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], FOR BROWSE clause
- FOR BROWSE clause
ms.assetid: 8f49b1c1-d877-4c46-b988-f8cdd8ac0925
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 251e0ae2ff6f19dfcff3b0f8056f6697c1bfc40d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598177"
---
# <a name="for-browse-is-not-allowed-in-views-in-90-or-later-compatibility-modes"></a>在 90 或 90 之後的相容性模式中，檢視內不允許有 FOR BROWSE
  Upgrade Advisor 偵測到在檢視中使用 FOR BROWSE 子句。 當資料庫相容性模式設定為 80 時，檢視中允許有 FOR BROWSE 子句 (並且會忽略)。 當資料庫相容性模式設定為 90 或之後時，檢視中就不允許有 FOR BROWSE 子句。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 當您升級時，使用者資料庫會維持其相容性模式。 將資料庫相容性模式變更為 90 或之後以前，請從檢視定義中移除 FOR BROWSE 子句。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜sp_dbcmptlevel＞。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
