---
title: 將定義域匯出為 .dqs 檔案 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eba10d3d-b5c4-447b-8a30-fa07996cb28e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 5d23e9efa2b3224aab5623201a54d1af56e49e09
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592856"
---
# <a name="export-a-domain-to-a-dqs-file"></a>將定義域匯出成 .dqs 檔案
  此主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中將定義域匯出至 .dqs 檔案。 您可以將定義域或整個知識庫匯出到資料檔。 如需匯出知識庫的資訊，請參閱[將知識庫匯出為 .dqs 檔案](../../2014/data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)。  
  
 將某個知識庫中的定義域匯出到 .dqs 資料檔，然後將它匯入另一個知識庫將會簡化知識產生程序，以節省時間與精力。 這樣可讓您將定義域和定義域的知識與其他人分享。  
  
 您可以匯出單一定義域或複合定義域。 包含單一定義域的 .dqs 檔案包括所有定義域資料，其中包括定義域屬性、值和規則，但不包括附加的參考資料資訊。 含有複合定義域的 .dqs 檔案包括所有複合定義域資料，其中包括複合定義域內所容納之定義域的所有定義域資料，以及複合定義域屬性、關聯和規則，但不包括參考資料資訊。 匯入 .dqs 檔之後，如有必要，您必須將定義域或複合定義域再次附加至適當的參考資料服務。 已發行和未發行的資料都會匯出。  
  
 匯出程序所建立的 .dqs 資料檔已經過加密，因此無法檢視內容。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
 若要將定義域匯出到 .dqs 資料檔，您必須已經建立及選取單一定義域或是包含多個單一定義域的複合定義域。 您不需要擁有匯出目標的 .dqs 檔案，系統會為您建立一個檔案。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能將定義域匯出到 .dqs 資料檔。  
  
##  <a name="export-a-domain-to-a-dqs-file"></a><a name="Export"></a>將網域匯出至 dqs 檔案  
 您可以從任何 [定義域管理] 頁面匯出。 您可以從使用者介面的控制項或是 [定義域清單] 窗格之內容功能表的命令中取得匯出命令。  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，於 [定義域管理] 活動中開啟知識庫。  
  
3.  在 **[定義域管理]** 頁面 (包含任何選取的索引標籤) 中，於 **[定義域]** 清單中選取單一定義域或複合定義域。  
  
4.  按一下定義域清單上方的 **[匯出知識庫資料]** 圖示，然後按一下 **[匯出定義域]**。 另外，您也可以用滑鼠右鍵按一下 **[定義域]** 清單中的定義域，指向 **[匯出]**，然後按一下 **[匯出定義域]**。  
  
5.  在 [匯出到資料檔]**** 對話方塊中，移至您想要用來儲存檔案的資料夾、為檔案命名或是保留預設名稱、將 [DQS 資料檔 (\*.dqs)]**** 保留為 [檔案類型]****，然後按一下 [儲存]****。  
  
6.  在 **[匯出定義域]** 對話方塊中，確認此對話方塊中的狀態行指出已完成匯出。 按一下 [確定]  。  
  
##  <a name="follow-up-after-exporting-a-domain-to-a-dqs-file"></a><a name="FollowUp"></a>後續操作：將定義域匯出至 dqs 檔案之後  
 在您將定義域匯出到 .dqs 檔案之後，您可以將此定義域匯入另一個知識庫中。  
  
  
