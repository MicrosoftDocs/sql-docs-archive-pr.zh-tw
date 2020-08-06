---
title: 如何管理本機 CDC 服務 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f9be649-cd93-40c1-bc48-0480106f207c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 437590d4b91f2fc80d5bb8a90251bf0dc7c8e18a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686462"
---
# <a name="how-to-manage-a-local-cdc-service"></a>如何管理本機 CDC 服務
  此程序描述如何使用 CDC 服務組態主控台來管理特定的 CDC 服務。  
  
### <a name="to-manage-a-specific-cdc-service"></a>若要管理特定的 CDC 服務  
  
1.  從 **[開始]** 功能表，選取 **[Oracle CDC 服務組態]** 。  
  
2.  從 CDC 服務組態主控台的左窗格中，展開 **[本機 CDC 服務]** 。  
  
3.  選取您想要使用的 CDC 服務。  
  
     您也可以用滑鼠右鍵按一下您想要使用的 CDC 服務，並選取所要的動作。  
  
     **OR**  
  
     從 CDC 服務組態主控台的左窗格選取 **[本機 CDC 服務]** ，然後從 CDC 服務組態主控台的中間區段選取您想要使用的服務。  
  
     您也可以用滑鼠右鍵按一下您想要使用的 CDC 服務，並選取所要的動作。  
  
4.  當您使用 CDC 服務時，可以執行以下工作。  
  
    -   **刪除服務**  
  
         從 CDC 服務組態主控台右側的 **[動作]** 窗格中，按一下 **[刪除]** 刪除此服務。  
  
         您也可以用滑鼠右鍵按一下您想要刪除的 CDC 服務，然後選取 [刪除]  。  
  
         **注意**：如果當您刪除此服務時，它正在執行中，在刪除此服務之前會先將它停止。  
  
         若要刪除 Oracle CDC Windows 服務定義，此程式需要關聯 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中 MSXDBCDC 資料庫的更新存取權。 當您按一下 **[確定]** 刪除此服務時，此程式會嘗試刪除 MSXDBCDC 資料庫中的 Oracle CDC 服務登錄。 如果它因為缺少權限而失敗，畫面上會出現一個對話方塊，提示使用者輸入具有 MSXDBCDC 資料庫之更新存取權的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
         如需有關您必須在 [連接到 SQL Server] 對話方塊中輸入之資料的詳細資訊，請參閱＜ [Manage an Oracle CDC Service](manage-an-oracle-cdc-service.md) ＞和＜ [Connection to SQL Server for Delete](connection-to-sql-server-for-delete.md)＞。  
  
    -   **編輯 CDC 服務屬性**  
  
         從 CDC 服務組態主控台右側的 **[動作]** 窗格中，按一下 **[屬性]** 。  
  
         您也可以用滑鼠右鍵按一下您要編輯屬性的 CDC 服務，然後選取 [屬性]  。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Oracle CDC 服務](manage-an-oracle-cdc-service.md)  
  
  
