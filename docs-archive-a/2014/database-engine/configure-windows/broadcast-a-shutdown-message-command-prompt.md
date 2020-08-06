---
title: 廣播關機訊息 (命令提示字元) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, stopping
- named instances [SQL Server], broadcasting shutdown messages
- shutdown message broadcast
- broadcasting shutdown message
- command prompt [SQL Server], broadcasting shutdown messages
- default instances [SQL Server], broadcasting shutdown messages
- stopping SQL Server
ms.assetid: 9f20ccd5-d952-431d-ba12-339911af9430
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 540baada4a78d7b5caf54cbabb9196ce5a79780e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87701881"
---
# <a name="broadcast-a-shutdown-message-command-prompt"></a>廣播關機訊息 (命令提示字元)
  本主題描述如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中使用 **net send** 命令廣播關機訊息。 在訊息中包含要停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的時間，讓使用者能夠完成其工作。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-broadcast-a-shutdown-message"></a>若要廣播關閉訊息  
  
1.  在命令提示字元下，輸入：  
  
     **net send /users "message"**  
  
     **/users** 選項可指定將訊息傳送給連接到伺服器的所有使用者。  
  
> [!NOTE]  
>  **net send** 命令需要 Messenger 服務同時在傳送與接收電腦上執行。 Windows Server 2003 預設會停用 Messenger 服務。 如需有關 **net send**的詳細資訊，請參閱 Windows 文件。  
  
 在您的網路上，使用電子郵件或電話來連絡使用者可能會更加適合。 若要判斷目前有哪些使用者連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請使用活動監視器。 如需活動監視器的相關資訊，請參閱[活動監視器](../../relational-databases/performance-monitor/activity-monitor.md)和[開啟活動監視器 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)。  
  
## <a name="see-also"></a>另請參閱  
 [啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務](start-stop-pause-resume-restart-sql-server-services.md)  
  
  
