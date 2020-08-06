---
title: 指定查詢準則 (基於使用方式的優化 Wizard) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.usagebasedoptimizationwizard.specifyquerycriteria.f1
ms.assetid: 3193adc2-af9f-4234-a4cc-dea0c280a724
author: minewiskan
ms.author: owend
ms.openlocfilehash: f3b93034a089ff3121155e35de4cec96846824a9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593620"
---
# <a name="specify-query-criteria-usage-based-optimization-wizard"></a>指定查詢準則 (基於使用方式的最佳化精靈)
  使用 **[指定查詢準則]** 頁面選擇一個或多個篩選選項來識別要最佳化的查詢。  
  
> [!NOTE]  
>  如果 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 無法連接到查詢記錄，此頁面就會停用。  
  
## <a name="options"></a>選項  
 **查詢記錄統計資料**  
 顯示所選取資料分割的查詢記錄中，所儲存之查詢的相關資訊。 其中會顯示下列項目：  
  
|詞彙|定義|  
|----------|----------------|  
|**查詢總計**|顯示所選取資料分割的查詢記錄中，所儲存的查詢總數。|  
|**相異查詢**|顯示所選取資料分割的查詢記錄中，所儲存的相異查詢數目。|  
|**相異使用者**|顯示所選取資料分割的查詢記錄中，與所儲存之查詢相關聯的相異使用者總數。|  
|**平均回應時間**|顯示所選取資料分割的查詢記錄中，所儲存之查詢的平均回應時間。|  
  
 **開始日期**  
 依據開始日期和時間篩選查詢記錄中的查詢。 在下拉式清單中選擇或輸入日期。  
  
> [!NOTE]  
>   如果未選取 **[結束日期]** ，則會考量查詢記錄中，符合此選項指定的日期和時間或之後的所有查詢。  
  
 **結束日期**  
 依據結束日期和時間篩選查詢記錄中的查詢。 在下拉式清單中選擇或輸入日期。  
  
> [!NOTE]  
>   如果未選取 **[開始日期]** ，則會考量查詢記錄中，符合在此選項指定的日期和時間或之前的所有查詢。  
  
 **使用者**  
 依據指定的使用者集合篩選查詢記錄中的查詢。 按一下省略符號 (**...**) 按鈕，即可顯示 [使用者選取]**** 對話方塊，並選擇用來篩選查詢的使用者。 如需 [使用者選取]**** 對話方塊的詳細資訊，請參閱[使用者選取對話方塊 &#40;Analysis Services - 多維度資料&#41;](user-selection-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **最常使用查詢**  
 依據所選取資料分割最常執行之相異查詢的最高百分比，篩選查詢記錄中的查詢。 選擇或在文字方塊輸入百分比值。  
  
## <a name="see-also"></a>另請參閱  
 [基於使用方式的優化嚮導 F1 說明](usage-based-optimization-wizard-f1-help.md)   
 [Analysis Services 的 &#40;多維度資料的嚮導&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
