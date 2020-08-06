---
title: " (維度 Wizard) 中指定來源資訊 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensionmaintable.f1
ms.assetid: 0538b490-5185-49e1-a783-4ce3539a0de5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 99bbaac0bdf24a18dcde455e779f056b98106dc4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598550"
---
# <a name="specify-source-information-dimension-wizard"></a>指定來源資訊 (維度精靈)
  使用 **[選取主維度資料表]** 頁面，即可針對要建立的維度，選取資料來源檢視、主維度資料表、索引鍵資料行和成員名稱資料行。  
  
 **開啟維度精靈**  
  
-   在方案總管**** 的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案的 [維度]**** 資料夾，然後按一下 [新增維度]****。  
  
## <a name="options"></a>選項  
 **資料來源視圖**  
 選取資料來源檢視。  
  
 **主資料表**  
 從選取的資料來源檢視中選取資料表，用來作為維度的主資料表。  
  
 **索引鍵資料行**  
 從 [主資料表]**** 指定的資料表中選取索引鍵資料行，作為維度的索引鍵屬性。  
  
> [!NOTE]  
>  可以選取一個以上的資料行。 如果資料表包含複合主索引鍵，請選取複合主索引鍵包含的所有資料行。 索引鍵資料行的順序很重要。  
  
 **名稱資料行**  
 從 [主資料表]**** 指定的資料表中選取資料行，此資料行提供維度的成員名稱。 使用複合索引鍵時，必須指定名稱資料行。 若要針對複合索引鍵建立名稱資料行，我們建議您在串連指定之索引鍵資料行的資料來源檢視中建立具名計算。 使用單一索引鍵時，名稱資料行是選擇性的。  
  
## <a name="see-also"></a>另請參閱  
 [維度嚮導 F1 說明](dimension-wizard-f1-help.md)   
 [維度 &#40;Analysis Services 多維資料&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多維度模型中的維度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
