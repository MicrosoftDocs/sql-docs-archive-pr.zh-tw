---
title: MSSQL_ENG021076 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021076 error
ms.assetid: 612e5c59-ba3e-49c3-a3df-56bac3d850a2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4161428767ce78726436c0cf794f5250140d35b5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87697945"
---
# <a name="mssql_eng021076"></a>MSSQL_ENG021076
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|21076|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|發行項 '%s' 的初始快照集仍然無法使用。|  
  
## <a name="explanation"></a>說明  
 如果在「快照集代理程式」完成快照集的產生之前啟動「散發代理程式」，會引發錯誤 MSSQL_ENG021076。 只有在發行集包含單一發行項時才會引發該錯誤。 如果發行集包含一個以上發行項，則會引發錯誤 MSSQL_ENG021075。 如需詳細資訊，請參閱 [MSSQL_ENG021075](mssql-eng021075.md)。  
  
## <a name="user-action"></a>使用者動作  
 如果在建立訂閱或上次選擇重新初始化訂閱後未啟動發行集的「快照集代理程式」，請啟動「快照集代理程式」，並讓其在啟動「散發代理程式」之前完成。 如需詳細資訊，請參閱[建立和套用快照集](create-and-apply-the-snapshot.md)。  
  
 若快照集代理程式未完成，請檢查快照集代理程式記錄，以便找出錯誤並加以解決。 如需有關在「複寫監視器」中檢視代理程式狀態和錯誤詳細資料的資訊，請參閱[使用複寫監視器來檢視資訊及執行工作](monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
 若錯誤繼續發生，請增加代理程式的記錄，並指定記錄的輸出檔。 視錯誤內容的不同，可提供導致錯誤的步驟和 (或) 其他錯誤訊息。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
