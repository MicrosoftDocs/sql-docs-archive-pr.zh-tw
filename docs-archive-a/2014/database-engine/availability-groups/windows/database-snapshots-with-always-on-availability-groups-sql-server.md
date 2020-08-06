---
title: 具有 AlwaysOn 可用性群組 (SQL Server) 的資料庫快照集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 7432da1c-ce2f-4cd9-af41-54c97744166b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e1e4307653b5b8150d71019a373ee073d15123f9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705438"
---
# <a name="database-snapshots-with-alwayson-availability-groups-sql-server"></a>資料庫快照集與 AlwaysOn 可用性群組 (SQL Server)
  您可以在可用性群組的主要或次要資料庫上建立資料庫快照集。 複本角色必須是不在 RESOLVING 狀態的 PRIMARY 或 SECONDARY。  
  
 當您建立資料庫快照集時，建議資料庫同步處理狀態為 SYNCHRONIZING 或 SYNCHRONIZED。 但是，當資料庫同步處理狀態為 NOT SYNCHRONIZING 時，可以建立資料庫快照集。  
  
 如果次要複本與主要複本中斷連接 (DISCONNECTED)，則此次要複本上的資料庫快照集應該繼續執行。  
  
 某些 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 情況會導致來源資料庫及其資料庫快照集重新啟動，暫時中斷使用者連接。 這些情況如下：  
  
-   主要複本變更角色，無論是因為目前主要複本離線並且在相同伺服器執行個體上恢復連線狀態，還是因為可用性群組容錯移轉。  
  
-   資料庫進入次要角色。  
  
 如果裝載資料庫快照集的可用性複本容錯移轉，資料庫快照集會保留在其建立所在的伺服器執行個體上。 使用者可以在容錯移轉後繼續使用快照集。如果效能是您的環境中的顧慮，我們建議您只在設定為手動容錯移轉模式的次要複本所裝載的次要資料庫上建立資料庫快照集。  如果您曾經將可用性群組手動容錯移轉到此次要複本，則可以在其他次要複本上建立一組新的資料庫快照集，將用戶端重新導向至這些新的資料庫快照集，並且從目前主要資料庫上卸除所有資料庫快照集。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [資料庫快照集 &#40;SQL Server&#41;](../../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
