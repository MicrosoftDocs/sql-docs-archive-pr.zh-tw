---
title: 記錄傳送監視器設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.logshipping.settings.monitor.f1
ms.assetid: 45e2ba7d-b3aa-4643-9451-bcb991572314
author: stevestein
ms.author: sstein
ms.openlocfilehash: 162fdc1b8b0ef850a7e58d1380c533426e16539c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709545"
---
# <a name="log-shipping-monitor-settings"></a>記錄傳送監視器設定
  使用此頁面來設定和修改記錄傳送監視伺服器的屬性。  
  
 如需記錄傳送概念的說明，請參閱 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)。  
  
## <a name="options"></a>選項。  
 **監視伺服器執行個體**  
 顯示目前設定為記錄傳送組態的監視伺服器之伺服器執行個體的名稱。  
  
 **[連接]**  
 選擇和連接到做為監視伺服器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 用來連接的帳戶必須是次要伺服器執行個體上的系統管理員 (sysadmin) 固定伺服器角色的成員。  
  
 **藉由模擬作業的 Proxy 帳戶**  
 連接到監視伺服器執行個體時，讓記錄傳送模擬 SQL Server Agent Proxy 帳戶。 備份、複製與還原處理序必須能夠連接到監視伺服器，才能更新記錄傳送作業的狀態。  
  
 **使用下列的 SQL Server 登入**  
 連接到監視伺服器執行個體時，允許記錄傳送使用特定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 備份、複製與還原處理序必須能夠連接到監視伺服器，才能更新記錄傳送作業的狀態。 如果您想要記錄傳送使用特定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，請選擇此選項，然後指定登入與密碼。  
  
 **在此時間後刪除記錄**  
 指定記錄傳送記錄資訊於刪除之前，在監視伺服器上保存的時間量。  
  
 **作業名稱**  
 指出超過備份或還原臨界值時，記錄傳送用來引發警示的 SQL Server Agent 警示作業的名稱。 第一次建立此作業時，您可以在方塊中輸入新的名稱。  
  
 **[排程]**  
 指出 SQL Server Agent 警示作業的目前排程。  
  
 **編輯**  
 修改 SQL Server Agent 警示作業參數。  
  
 **停用此作業**  
 暫停 SQL Server Agent 警示作業。  
  
  
