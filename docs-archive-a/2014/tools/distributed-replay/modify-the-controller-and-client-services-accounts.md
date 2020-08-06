---
title: 修改控制器與用戶端服務帳戶 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 44a73ddb-18ad-415c-bfbe-126ab2e3290b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 62a054749f1d53323bde5c9d05a1e7632b1dda85
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87703653"
---
# <a name="modify-the-controller-and-client-services-accounts"></a>修改控制器服務帳戶與用戶端服務帳戶
  在本主題中，您將了解如何修改 Distributed Replay Controller 和用戶端服務帳戶，然後重新套用存取控制清單 (ACL)。  
  
### <a name="to-start-or-stop-the-distributed-replay-services-using-computer-management"></a>若要使用電腦管理來啟動或停止 Distributed Replay 服務  
  
1.  在安裝 Distributed Replay 服務的電腦上，於命令提示字元中輸入 `dcomcnfg`。  
  
2.  按兩下 [**服務**]，並在** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay \<service name> **按一下滑鼠右鍵，然後按一下 [**開始**] 或 [**停止**]。  
  
### <a name="to-modify-the-distributed-replay-controller-service"></a>若要修改 Distributed Replay Controller 服務  
  
1.  在控制器電腦上，停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller 服務。  
  
2.  在 [服務]  底下，以滑鼠右鍵按一下 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller]  ，然後選取 [內容]  。  
  
3.  在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller 內容]  視窗的 [登入]  索引標籤上選取 [這個帳戶]  ，輸入或按一下 [瀏覽]  輸入新的登入帳戶，然後按一下 [確定]  。  
  
     **重要**：當您設定 Distributed Replay Controller 時，可以指定要用來執行 Distributed Replay Client 服務的一或多個使用者帳戶。 下列是支援帳戶的清單：  
  
    -   網域使用者帳戶  
  
    -   使用者建立的本機使用者帳戶  
  
    -   系統管理員  
  
    -   虛擬帳戶和 MSA (受管理的服務帳戶)  
  
    -   網路服務、本機系統和系統  
  
     不接受群組帳戶 (本機或網域) 和其他內建帳戶 (例如 Everyone)。  
  
4.  啟動 Distributed Replay Controller 服務。  
  
### <a name="to-modify-the-distributed-replay-client-service"></a>若要修改 Distributed Replay Client 服務  
  
1.  修改 Distributed Replay Client 服務之前，請先確定已在安裝期間指定您要變更的用戶端服務帳戶 (於控制器電腦的 CTLRUSERS 參數中)。 如果未在安裝期間指定您要變更的用戶端服務帳戶，則必須先執行以下步驟：  
  
    1.  停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller 服務。  
  
    2.  在安裝控制器服務的控制器電腦上，於命令提示字元中輸入 `dcomcnfg`。  
  
    3.  在 [元件服務]  視窗中，巡覽至主控台根目錄 -> [元件服務] -> [電腦] -> [我的電腦] -> [DCOM 設定] -> [DReplayController]  。  
  
    4.  以滑鼠右鍵按一下 [DReplayController]  ，然後按一下 [內容]  。  
  
    5.  在 [DReplayController 內容]  視窗的 [安全性]  索引標籤上，按一下 [啟動和啟用權限]  區段中的 [編輯]  。  
  
    6.  將**本機和遠端啟用**權限授與新的用戶端服務登入帳戶，然後按一下 [確定]  。  
  
    7.  按一下 [存取權限]  區段中的 [編輯]  ，將**本機和遠端存取**權限授與新的用戶端服務登入帳戶，然後按一下 [確定]  。  
  
    8.  按一下 [確定]  關閉 [DReplayController 內容]  視窗。  
  
    9. 在控制器電腦上，將已變更的用戶端服務登入帳戶加入 [Distributed COM Users]  群組。  
  
    10. 啟動 SQL Server Distributed Replay Controller 服務。  
  
2.  停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 服務。  
  
3.  在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 內容]  視窗的 [登入]  索引標籤上選取 [這個帳戶]  ，輸入或按一下 [瀏覽]  輸入新的登入帳戶，然後按一下 [確定]  。  
  
4.  啟動 Distributed Replay Client 服務。  
  
  
