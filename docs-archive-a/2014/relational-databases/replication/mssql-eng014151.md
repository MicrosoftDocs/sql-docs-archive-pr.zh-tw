---
title: MSSQL_ENG014151 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014151 error
ms.assetid: 54b45e70-46b3-4c7a-a5bf-06f6dd028ceb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d2796451f6f681cfb0ce529ed44a946c34135649
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585302"
---
# <a name="mssql_eng014151"></a>MSSQL_ENG014151
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|14151|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|複寫 -%s：代理程式 %s 失敗。 %s|  
  
## <a name="explanation"></a>說明  
 任何複寫代理程式的失敗均會導致錯誤。 訊息結尾處的文字視失敗的內容而定。  
  
## <a name="user-action"></a>使用者動作  
 此錯誤在許多情況下都會出現；請視需要使用下列方法：  
  
-   重新啟動失敗的代理程式，查看現在執行是否已無錯誤。 如需詳細資訊，請參閱[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 與[複寫代理程式可執行檔概念](concepts/replication-agent-executables-concepts.md)。  
  
-   請檢查代理程式記錄和作業記錄是否同時發生其他錯誤。 如需有關在「複寫監視器」中檢視代理程式狀態和錯誤詳細資料的資訊，請參閱[使用複寫監視器來檢視資訊及執行工作](monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
-   確認在由代理程式存取的電腦之間是否使用基本連接，然後使用類似 [sqlcmd Utility](../../tools/sqlcmd-utility.md)的公用程式連接到各台電腦。 連接時，請使用代理程式建立連接的相同帳戶。 如需各代理程式帳戶所需權限的詳細資訊，請參閱＜ [Replication Agent Security Model](security/replication-agent-security-model.md)＞。  
  
-   如果在建立或套用快照集時發生錯誤，則請檢查快照集目錄中的檔案以找到錯誤。  
  
-   若錯誤繼續發生，請增加代理程式的記錄，並指定記錄的輸出檔。 視錯誤內容的不同，可提供導致錯誤的步驟和 (或) 其他錯誤訊息。  
  
## <a name="see-also"></a>另請參閱  
 [複寫代理程式管理](agents/replication-agent-administration.md)   
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)   
 [Replication Distribution Agent](agents/replication-distribution-agent.md)   
 [Replication Log Reader Agent](agents/replication-log-reader-agent.md)   
 [Replication Merge Agent](agents/replication-merge-agent.md)   
 [複寫佇列讀取器代理程式](agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](agents/replication-snapshot-agent.md)  
  
  
