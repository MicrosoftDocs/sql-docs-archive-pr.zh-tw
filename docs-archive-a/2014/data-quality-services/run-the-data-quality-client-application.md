---
title: 執行 Data Quality Client 應用程式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.browseforservers.f1
- sql12.dqs.connecttoserver.f1
ms.assetid: 0b2aa202-7ab2-4c9d-b0f1-802588053a1e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 45372ce22fd1b18f0ec13f7a7fd76a369b78dfd6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709970"
---
# <a name="run-the-data-quality-client-application"></a>執行 Data Quality Client 應用程式
  您可以執行 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)]，然後登入 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]，藉以使用 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] (DQS)。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
 您必須執行 DQSInstaller.exe 檔案，才可以完成 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 的安裝。 如需詳細資訊，請參閱 [執行 DQSInstaller.exe 完成 Data Quality Server 安裝](install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您必須擁有授與 DQS_MAIN 資料庫的其中一個 DQS 角色 (dqs_adminstrator、dqs_kb_editor 或 dqs_kb_operator)，才能登入 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]。  
  
##  <a name="run-data-quality-client"></a><a name="Run"></a>執行 Data Quality Client  
 若要在已安裝 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 的電腦上執行此用戶端，請依照以下方式繼續進行：  
  
1.  按一下 [開始]****，並指向 [所有程式]****，然後依序按一下 [[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]]****、[Data Quality Services]**** 及 [Data Quality Client]****。  
  
2.  在 [連線至伺服器] 對話方塊中：  
  
    1.  指定您想要讓 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式連接的目標伺服器。 若要連接到本機電腦上的 **，請選取** [(LOCAL)] [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 。 您也可以按一下向下箭號，然後選取 **\<Browse network for more servers>** 以連接到不同的伺服器 (或依名稱) 連接到本機伺服器。 此時會顯示 **[瀏覽伺服器]** 對話方塊。 您可以在 **[本機伺服器]** 索引標籤或 **[網路伺服器]** 索引標籤中選取伺服器。  
  
    2.  如果您想要加密 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 與 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 之間的資料傳輸，請按一下 [選項]****，然後選取 [加密連接]**** 核取方塊。  
  
3.  按一下 [ **連接**]。  
  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面隨即出現。 如需詳細資訊，請參閱 [Data Quality Client 首頁畫面](../../2014/data-quality-services/data-quality-client-home-screen.md)。  
  
  
