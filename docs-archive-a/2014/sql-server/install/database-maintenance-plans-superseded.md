---
title: 已取代資料庫維護計畫 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- suspended database maintenance plans
- database maintenance plans [SQL Server Agent]
- maintenance plans [SQL Server Agent]
ms.assetid: efac127c-6c81-4c7a-a6c4-9aae5d15545d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 3aea75cc4ecc94ccbaeb1f35cecd0b18ff3a65ff
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584988"
---
# <a name="database-maintenance-plans-superseded"></a>已取代資料庫維護計畫
    
## <a name="component"></a>元件  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式  
  
## <a name="description"></a>描述  
 現有的資料庫維護計劃已經升級，而且仍會繼續運作。 但是，您將無法使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來建立新的資料庫維護計劃。 若要在 [物件總管] 中檢視維護計畫，請展開 [管理]，然後再展開 [舊版]。 您可以從任何資料庫維護計畫的內容功能表中選取 [**遷移**]，將現有的資料庫維護計畫遷移至新的格式。 因為新維護計畫功能並非直接取代資料庫維護計畫，所以移轉後，某些功能可能會遺失。 移轉資料庫維護計畫並不會刪除舊計畫，所以您可以測試維護計畫的功能後，再移除舊計畫。  
  
 資料庫維護計畫不再支援下列功能：  
  
-   記錄傳送  
  
-   [**資料庫完整性檢查**] 工作的 [**嘗試修復任何次要問題**] 選項  
  
## <a name="corrective-action"></a>更正動作  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 禁止在資料庫維護計劃中包含記錄傳送。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜記錄傳送＞。  
  
  
