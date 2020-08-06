---
title: 定義帳戶智慧 (維度 Wizard) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.accountintelligencetypemapping.f1
ms.assetid: cbcff072-3a7e-4e98-858f-1b4265461561
author: minewiskan
ms.author: owend
ms.openlocfilehash: 90871e2299d1531db1b678b1f4b16ddd7f1db767
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598054"
---
# <a name="define-account-intelligence-dimension-wizard"></a>定義帳戶智慧 (維度精靈)
  使用 **[定義帳戶智慧]** 頁面，即可將 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體上定義的帳戶類型，對應至維度屬性上所定義的帳戶類型，這些帳戶類型與維度中的 **[帳戶類型]** 屬性類型相關聯。  
  
> [!NOTE]  
>   只有在您已選取 **[選取維度類型]** 頁面上的 **[標準維度]** ，而且已將維度屬性對應至 **[指定維度類型]** 頁面上的 **[Account Type]** 屬性類型時，才會顯示此頁面。  
  
## <a name="options"></a>選項  
 **來源資料表帳戶類型**  
 顯示已指派給 [指定維度索引鍵和類型]**** 頁面中的 [帳戶類型]**** 屬性類型之維度屬性中所含的值。  
  
 **內建帳戶類型**  
 選取在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體上定義，且對應至來源資料表帳戶類型的帳戶類型。  
  
 下表列出在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體上定義的帳戶類型。  
  
|值|描述|  
|-----------|-----------------|  
|**資產**|擁有之事物在特定時間點的價值。|  
|**餘額**|某項目在特定時間點的計數。|  
|**費用**|花費之事物的價值。|  
|**Flow**|事物的累加計數。|  
|**Income**|收到之事物的價值。|  
|**負債**|所欠之事物在特定時間點的價值。|  
|**統計**|某項目的計算比率，或者無法彙總之項目的計數。|  
  
## <a name="see-also"></a>另請參閱  
 [維度嚮導 F1 說明](dimension-wizard-f1-help.md)   
 [維度 &#40;Analysis Services 多維資料&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多維度模型中的維度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
