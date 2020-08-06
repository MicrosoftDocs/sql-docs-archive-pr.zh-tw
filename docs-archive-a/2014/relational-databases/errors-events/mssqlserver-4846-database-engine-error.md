---
title: MSSQLSERVER_4846 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 4846 (Database Engine error)
ms.assetid: a455e809-1883-4c7d-b3e3-835ee5bfe258
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 923137645aae72476fb4b2ae33f0cbbf3e81c2a3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87698242"
---
# <a name="mssqlserver_4846"></a>MSSQLSERVER_4846
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|4846|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|BULKPROV_MEMORY|  
|訊息文字|大量資料提供者無法配置記憶體。|  
  
## <a name="explanation"></a>說明  
 記憶體配置失敗。  
  
## <a name="user-action"></a>使用者動作  
 請遵循下列一般步驟以疑難排解記憶體錯誤：  
  
1.  確認是否有其他應用程式或服務正在耗用此伺服器的記憶體。 重新設定比較不重要的應用程式或服務，以降低其記憶體耗用量。  
  
2.  開始收集下列項目的效能監視器計數：**SQL Server：緩衝區管理員**、**SQL Server：記憶體管理員**。  
  
3.  檢查下列 SQL Server 記憶體組態參數：  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
     注意不尋常的設定， 並且視需要加以更正。 說明 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的記憶體需求。 預設值列於《SQL Server 線上叢書》中的＜設定伺服器組態選項＞。  
  
4.  當您看到這些錯誤訊息時，請觀察 DBCC MEMORYSTATUS 輸出以及它變更的方式。  
  
5.  檢查工作負載 (例如，並行工作階段的數目以及目前正在執行的查詢數)。  
  
 下列動作可以為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供更多可用的記憶體：  
  
-   如果有 SQL Server 以外的應用程式正在耗用資源，請嘗試停止執行這些應用程式或考慮在不同的伺服器上執行這些應用程式。 這將會移除外部的記憶體壓力。  
  
-   如果已經設定 **max server memory,** ，請增加其設定值。  
  
 執行下列 DBCC 命令，以便釋放數個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體快取。  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
 如果仍繼續發生該問題，您必須進一步研究，而且可能必須降低工作負載。  
  
  
