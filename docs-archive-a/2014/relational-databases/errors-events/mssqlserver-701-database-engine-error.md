---
title: MSSQLSERVER_701 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 701 (Database Engine error)
ms.assetid: 3b975000-63a1-43c2-a40f-89d0a8a36bef
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 542535223d3e394c72079092411add143de61545
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594084"
---
# <a name="mssqlserver_701"></a>MSSQLSERVER_701
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|701|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|NOSYSMEM|  
|訊息文字|系統記憶體不足，無法執行此查詢。|  
  
## <a name="explanation"></a>說明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法配置足夠的記憶體來執行查詢。 有各種原因會造成此錯誤，包括作業系統設定、實體記憶體可用性或目前工作負載的記憶體限制。 在大部分情況下，交易失敗並非造成此錯誤的原因。  
  
 診斷查詢 (例如 DBCC 陳述式) 可能會因為伺服器記憶體不足而失敗。  
  
 等候記憶體資源來執行資源集區 'default' 中的查詢時發生逾時。  
  
## <a name="user-action"></a>使用者動作  
 如果您未使用資源管理員，我們建議您對整個伺服器狀態和負載進行驗證，或者檢查資源集區或工作負載群組設定。  
  
 下列清單概述有助於疑難排解記憶體錯誤的一般步驟：  
  
1.  確認是否有其他應用程式或服務正在耗用此伺服器的記憶體。 重新設定比較不重要的應用程式或服務，以降低其記憶體耗用量。  
  
2.  開始收集以下內容的效能監視器計數：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **：緩衝區管理員**、**SQL Server：記憶體管理員**。  
  
3.  檢查下列 SQL Server 記憶體組態參數：  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
     注意不尋常的設定， 並且視需要加以更正。 說明增加的記憶體需求。 預設值列於《SQL Server 線上叢書》中的＜設定伺服器組態選項＞。  
  
4.  當您看到這些錯誤訊息時，請觀察 DBCC MEMORYSTATUS 輸出以及它變更的方式。  
  
5.  檢查工作負載 (例如，並行工作階段的數目以及目前正在執行的查詢數)。  
  
 下列動作可以為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供更多可用的記憶體：  
  
-   如果有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外的應用程式正在耗用資源，請嘗試停止執行這些應用程式或考慮在不同的伺服器上執行這些應用程式。 這將會移除外部的記憶體壓力。  
  
-   如果已經設定 **max server memory,** ，請增加其設定值。  
  
 執行下列 DBCC 命令，以便釋放數個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體快取。  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
 如果仍繼續發生該問題，您必須進一步研究，而且可能必須降低工作負載。  
  
  
