---
title: 專案版本對話方塊 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isprojectprop.versions.f1
ms.assetid: a48a387c-2e70-45bc-be2e-26e57a9bb2c4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 998dd194c2a056121fd6f7a404e75c7080b85aa1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705362"
---
# <a name="project-versions-dialog-box"></a>專案版本對話方塊
  使用 **[專案版本]** 對話方塊檢視專案版本，以及還原舊版。  
  
 您也可以在 [catalog.object_versions &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-object-versions-ssisdb-database) 檢視中檢視舊版，並使用 [catalog.restore_project &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database) 預存程序還原舊版。  
  
 **您想要做什麼事？**  
  
-   [開啟 [專案版本] 對話方塊](#open_dialog)  
  
-   [還原專案版本](#restore)  
  
##  <a name="open-the-project-versions-dialog-box"></a><a name="open_dialog"></a> 開啟 [專案版本] 對話方塊  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接至 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 伺服器。  
  
     亦即連接到主控 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 資料庫的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 執行個體。  
  
2.  在 [物件總管] 中，展開樹狀目錄以顯示 **[Integration Services 目錄]** 節點。  
  
3.  展開 **[Integration Services 目錄]** 節點以顯示 **[SSISDB]** 節點。  
  
4.  **[SSISDB]** 節點包含一個或多個資料夾，且每個資料夾包含一個或多個專案。 展開包含您感興趣之專案的資料夾。  
  
5.  以滑鼠右鍵按一下專案，然後按一下 [版本]  。  
  
 在 [專案版本]  對話方塊中，[版本]  資料表會顯示已經在伺服器上部署之專案版本的清單、版本部署的日期和時間、版本還原的日期和時間 (如果已還原)、版本描述，以及版本識別碼。 目前使用中的版本會以資料表之 **[目前]** 資料行中的核取記號表示。  
  
##  <a name="restore-a-project-version"></a><a name="restore"></a> 還原專案版本  
 若要還原舊版專案，請在 **[版本]** 資料表中選取版本，然後按一下 **[還原至選取的版本]** 。 專案便會還原到選取的版本，而且該版本會以 **[版本]** 資料表之 **[目前]** 資料行中的核取記號表示。  
  
  
