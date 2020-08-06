---
title: 建立資料品質專案 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dqproject.newdqproject.f1
helpviewer_keywords:
- create,data quality project
- data quality project,create
ms.assetid: 19c52d2b-d28e-4449-ab59-5fe0dc326cd9
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 3bab14b34123464450bcf0de7540364fc642343e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687159"
---
# <a name="create-a-data-quality-project"></a>建立資料品質專案
  本主題描述如何使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]來建立資料品質專案。 資料品質專案是用來在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中執行清理或比對活動。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
 您必須擁有要用於資料品質專案的相關知識庫，才能進行清理或比對活動。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 或 dqs_kb_operator 角色，才能建立資料品質專案。  
  
##  <a name="create-a-data-quality-project"></a><a name="Create"></a>建立資料品質專案  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[新增資料品質專案]**。  
  
3.  在 **[新增資料品質專案]** 畫面中：  
  
    1.  在 **[名稱]** 方塊中，輸入新資料品質專案的名稱。  
  
    2.  (選擇性) 在 **[描述]** 方塊中，輸入新資料品質專案的描述。  
  
    3.  在 **[使用知識庫]** 清單中，按一下以選取要用於資料品質專案的知識庫。 右側的 [知識庫詳細資料: <知識庫名稱>]**** 區域會顯示所選知識庫中可用的定義域名稱。  
  
    4.  在 **[選取活動]** 區域中，按一下您想要使用此資料品質專案來執行的活動：  
  
        -   **清理**：若要清理來源資料，請選取此活動。  
  
        -   **比對**：若要執行比對，請選取此活動。 只有當您針對資料品質專案所選取的知識庫包含比對原則時，才能使用此活動。  
  
4.  按一下 **[建立]** ，建立資料品質專案。  
  
##  <a name="follow-up-after-creating-a-data-quality-project"></a><a name="FollowUp"></a>後續操作：建立資料品質專案之後  
 建立資料品質專案之後，系統會顯示可用來執行選取活動的精靈：清理或比對。 如需清理和比對活動的詳細資訊，請參閱[資料清理](../../2014/data-quality-services/data-cleansing.md)和[資料比對](../../2014/data-quality-services/data-matching.md)。  
  
  
