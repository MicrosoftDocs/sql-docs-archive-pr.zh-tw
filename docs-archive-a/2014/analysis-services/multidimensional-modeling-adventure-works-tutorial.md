---
title: 多維度模型化 (的艾德作品教學課程) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tutorials [Analysis Services]
- Analysis Services, tutorials
ms.assetid: db55e226-601a-4026-8651-573195555a59
author: minewiskan
ms.author: owend
ms.openlocfilehash: cd2e8f856d36cab045e6cbc4d34f7cfeffac3c3c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598034"
---
# <a name="multidimensional-modeling-adventure-works-tutorial"></a>多維度模型化 (Adventure Works 教學課程)
  歡迎使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程。 這個教學課程描述如何使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 來開發和部署 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案，所有範例都使用虛構公司 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 。  
  
## <a name="what-you-will-learn"></a>學習內容  
 在本教學課程中，您將學會下列作業：  
  
-   如何在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]專案中定義資料來源、資料來源檢視、維度、屬性、屬性關聯性、階層和 Cube。  
  
-   如何透過將 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案部署至 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]執行個體，檢視 Cube 和維度資料，以及如何處理已部署的物件，以便使用基礎資料來源中的資料擴展這些物件。  
  
-   如何在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案中修改量值、維度、階層、屬性和量值群組，以及如何將累加變更部署到開發伺服器上已部署的 Cube。  
  
-   如何在 Cube 內定義計算、關鍵效能指標 (KPI)、動作、檢視方塊、翻譯和安全性角色。  
  
 案例描述隨附此教學課程，讓您可以更了解這些課程的內容。 如需詳細資訊，請參閱＜ [Analysis Services Tutorial Scenario](analysis-services-tutorial-scenario.md)＞。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要完成這個教學課程的所有課程，您將需要範例資料、範例專案檔及軟體。 如需如何尋找及安裝這個教學課程之必要條件的指示，請參閱＜ [Install Sample Data and Projects for the Analysis Services Multidimensional Modeling Tutorial](install-sample-data-and-projects.md)＞。  
  
 另外還要具備下列權限才能順利完成這個教學課程：  
  
-   您必須是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 電腦上 Administrators 本機群組的成員，或是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]執行個體中伺服器管理角色的成員。  
  
-   您必須具有 **AdventureWorksDW2012** 範例資料庫的「讀取」權限。 這個範例資料庫對 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本有效。  
  
## <a name="lessons"></a>課程  
 這個教學課程包括下列課程。  
  
|課程|預估完成時間|  
|------------|--------------------------------|  
|[第1課：在 Analysis Services 專案中定義資料來源視圖](lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md)|15 分鐘|  
|[第2課：定義和部署 Cube](lesson-2-defining-and-deploying-a-cube.md)|30 分鐘|  
|[第3課：修改量值、屬性和階層](lesson-3-modifying-measures-attributes-and-hierarchies.md)|45 分鐘|  
|[第4課：定義 Advanced 屬性和維度屬性](lesson-4-defining-advanced-attribute-and-dimension-properties.md)|120 分鐘|  
|[第5課：定義維度和量值群組之間的關聯性](lesson-5-defining-relationships-between-dimensions-and-measure-groups.md)|45 分鐘|  
|[第6課：定義計算](lesson-6-defining-calculations.md)|45 分鐘|  
|[第 7 課：定義關鍵效能指標 &#40;KPI&#41;](lesson-7-defining-key-performance-indicators-kpis.md)|30 分鐘|  
|[第8課：定義動作](lesson-8-defining-actions.md)|30 分鐘|  
|[第9課：定義觀點和翻譯](lesson-9-defining-perspectives-and-translations.md)|30 分鐘|  
|[第10課：定義系統管理角色](lesson-10-defining-administrative-roles.md)|15 分鐘|  
  
> [!NOTE]  
>  您將在此教學課程中建立的 Cube 資料庫是簡化的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多維度模型專案版本，此專案是 Adventure Works 範例資料庫的一部分，可在 codeplex 網站下載。 已簡化「艾德作品多維度資料庫」的教學課程版本，將焦點放在您想要立即改善的特定技能。 完成此教學課程之後，請考慮自行瀏覽多維度模型專案，以更了解 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多維度模型。  
  
## <a name="next-step"></a>後續步驟  
 若要開始本教學課程，請繼續進行第一課： [Lesson 1: Defining a Data Source View within an Analysis Services Project](lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md)。  
  
  
