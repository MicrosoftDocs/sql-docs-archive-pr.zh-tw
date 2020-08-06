---
title: 管理 (開啟、解除鎖定、重新命名和刪除資料品質專案) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dqproject.opendqproject.f1
helpviewer_keywords:
- data quality project,delete
- data quality project,rename
- data quality project,unlock
- data quality project,open
ms.assetid: de8a2b04-4673-4beb-b4cf-96a28cdf3a93
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 216c95937676954c509890b879abdee8f55b778c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599675"
---
# <a name="manage-open-unlock-rename-and-delete-a-data-quality-project"></a>管理 (開啟、解除鎖定、重新命名和刪除) 資料品質專案
  此主題描述如何使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 管理資料品質專案，例如開啟、解除鎖定、重新命名和刪除資料品質專案。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 限制事項  
  
-   您無法開啟另一個使用者所建立且已鎖定的專案。  
  
-   您無法解除鎖定、重新命名或刪除另一個使用者所建立的資料品質專案。  
  
-   您不能刪除已鎖定的資料品質專案。 您必須先解除鎖定，然後才能刪除。  
  
-   您只能解除鎖定由您建立的資料品質專案。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
 您至少必須有一個資料品質專案可供管理。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 或 dqs_kb_operator 角色，才能管理資料品質專案。  
  
##  <a name="open-a-data-quality-project"></a><a name="Open"></a> 開啟資料品質專案  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[開啟資料品質專案]**。 **[開啟專案]** 畫面隨即出現。  
  
     或者，您也可以按一下 **[最近使用的資料品質專案]** 區域底下所列出的資料品質專案，直接將它開啟。  
  
3.  在 **[開啟專案]** 畫面中，按一下來選取您想要開啟的資料品質專案，然後按 **[下一步]**。  
  
4.  隨即以上次活動關閉時的相同狀態來開啟資料品質專案。 資料品質專案具有以下狀態：  
  
    -   針對 [**清理**] 活動，資料品質專案可以具有下列狀態： [**清理-對應**]、[**清理-** 清理]、[**清理-管理和查看結果**] 和 [**清理-匯出**]。  
  
    -   針對比**對活動，** 資料品質專案可以具有下列狀態：比**對對應**、比對**對應、比**對-**生存**和比**對匯出**。  
  
##  <a name="unlock-a-data-quality-project"></a><a name="Unlock"></a> 解除鎖定資料品質專案  
 當您建立資料品質專案時，它處於已鎖定狀態，以防止其他使用者使用或修改。 如果您希望其他使用者使用您的資料品質專案，在您完成工作之後必須解除鎖定資料品質專案。 鎖定的專案會顯示鎖定符號。  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[開啟資料品質專案]**。 **[開啟專案]** 畫面隨即出現。  
  
3.  在 **[開啟專案]** 畫面中，以滑鼠右鍵按一下您所建立且已鎖定的資料品質專案，然後按一下快速鍵功能表中的 **[解除鎖定]** 。 專案會顯示綠色核取記號，表示專案已解除鎖定。  
  
##  <a name="rename-a-data-quality-project"></a><a name="Rename"></a> 重新命名資料品質專案  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[開啟資料品質專案]**。 **[開啟專案]** 畫面隨即出現。  
  
3.  在 **[開啟專案]** 畫面中，以滑鼠右鍵按一下您所建立的資料品質專案，然後按一下快速鍵功能表中的 **[重新命名]** 。  
  
4.  此資料品質專案名稱就可以在 **[名稱]** 資料行中編輯。 輸入新的名稱，然後按下 Enter。  
  
##  <a name="delete-a-data-quality-project"></a><a name="Delete"></a> 刪除資料品質專案  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[開啟資料品質專案]**。 **[開啟專案]** 畫面隨即出現。  
  
3.  在 **[開啟專案]** 畫面中，以滑鼠右鍵按一下您所建立且解除鎖定的資料品質專案，然後按一下快速鍵功能表中的 **[刪除]** 。  
  
4.  確認訊息隨即出現。 按一下 [是] 。  
  
  
