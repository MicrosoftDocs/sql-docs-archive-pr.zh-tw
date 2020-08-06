---
title: 批次處理 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- batches [Analysis Services]
ms.assetid: ba4dcf72-0667-41d0-816b-ab8ff9a7d9cb
author: minewiskan
ms.author: owend
ms.openlocfilehash: c777339f41f5f9029e4d03d47cc7f682e00032b8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585647"
---
# <a name="batch-processing-analysis-services"></a>批次處理 (Analysis Services)
  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，您可以使用 [批次] 命令，以單一要求將多個處理命令傳送至伺服器。 批次處理讓您可以控制要處理的物件和處理順序。 此外，批次可以當做一系列獨立的作業來執行，或是做為交易執行，其中若有一個處理序失敗，就會造成整個批次全部回復。  
  
 批次處理透過合併及縮短認可變更所需的時間，來提高資料可用性。 當您完整處理維度時，任何使用該維度的分割區都會標示為尚未處理。 因此，包含尚未處理之分割區的 Cube 都無法瀏覽。 您可以同時處理維度和受影響的分割區，藉由批次處理作業的方式處理解決這種狀況。 將批次處理工作當做交易執行，可確保包含在交易中的所有物件保持可供查詢，直到所有處理完成為止。 當交易認可有所變更時，受影響的物件上會遭到鎖定，讓物件暫時無法使用，但是認可變更所使用的整體時間會比您個別處理物件還短。  
  
 本主題中的程序示範完整處理維度和分割區的步驟。 批次處理也可以包含其他處理選項，如累加式處理。 若要讓這些程序正確運作，必須使用至少包含兩個維度和一個分割區的現有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。  
  
 這個主題包括下列各節：  
  
 [SQL Server Data Tools 中的批次處理](#bkmk_ssdt)  
  
 [在 Management Studio 中使用 XMLA 執行批次處理](#bkmk_xmla)  
  
##  <a name="batch-processing-in-sql-server-data-tools"></a><a name="bkmk_ssdt"></a> SQL Server 資料工具中的批次處理  
 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中處理物件之前，必須先部署包含該物件的專案。 如需詳細資訊，請參閱[部署 Analysis Services 專案 &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)。  
  
1.  開啟 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]。  
  
2.  開啟已部署的專案。  
  
3.  在 [方案總管] 中，已部署的專案之下，展開 **[維度]** 資料夾。  
  
4.  按住 Ctrl 鍵，並按一下 **[維度]** 資料夾中列出的每個維度。  
  
5.  以滑鼠右鍵按一下選取的維度，然後按一下 [處理]****。  
  
6.  按住 Ctrl 鍵，並按一下 **[物件清單]** 中列出的每個維度。  
  
7.  以滑鼠右鍵按一下選取的維度，然後選取 [完整處理]****。  
  
8.  若要自訂批次處理作業，請按一下 **[變更設定]**。  
  
9. 在 **[處理選項]** 下標示下列設定：  
  
    -   將 **[處理順序]** 設定為 **[循序]**，並將 **[交易模式]** 設定為 **[一筆交易]**。  
  
    -   將 **[回寫資料表選項]** 設定為 **[使用現有的]**。  
  
    -   在 **[受影響的物件]** 下，選取 **[處理受影響的物件]** 核取方塊。  
  
10. 按一下 [**維度索引鍵錯誤**] 索引標籤。請確認已選取 [**使用預設錯誤**設定]。  
  
11. 按一下 **[確定]** ，關閉 **[變更設定]** 畫面。  
  
12. 在 **[處理物件]** 畫面中按一下 **[執行]** ，以啟動處理作業。  
  
13. 當 **[狀態]** 方塊顯示 **[處理成功]** 時，按一下 **[關閉]**。  
  
14. 按一下 **[處理物件]** 畫面上的 **[關閉]** 。  
  
##  <a name="batch-processing-using-xmla-in-management-studio"></a><a name="bkmk_xmla"></a>在 Management Studio 中使用 XMLA 的批次處理  
 您可以建立執行批次處理的 XMLA 指令碼。 首先在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中為每個物件產生 XMLA 指令碼，然後將它們結合為可以互動方式執行或在排程工作內執行的單一 XMLA 查詢。  
  
 如需逐步指示，請參閱 **使用 SQL Server Agent 排程 SSAS 管理工作** 中的 [範例 2](../instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型物件處理](processing-a-multidimensional-model-analysis-services.md)  
  
  
