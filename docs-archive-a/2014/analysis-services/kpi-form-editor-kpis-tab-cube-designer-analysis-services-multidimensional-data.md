---
title: KPI 表單編輯器 (Kpi 索引標籤、Cube 設計工具)  (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpidefinitionpane.f1
ms.assetid: 45c6453a-bbe2-4ca5-836e-c7ef11cfcb65
author: minewiskan
ms.author: owend
ms.openlocfilehash: 3c88d6fcec60634f37ddad8b6d0f5cb2124fa1cc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592951"
---
# <a name="kpi-form-editor-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>KPI 表單編輯器 (KPI 索引標籤，Cube 設計工具) (Analysis Services - 多維度資料)
  在 Cube 設計師的 [KPI]**** 索引標籤上，使用 [KPI 表單編輯器]**** 窗格來建立或修改選取的關鍵效能指標 (KPI)。  
  
> [!NOTE]  
>  此窗格只會以表單檢視方式顯示。  
  
## <a name="options"></a>選項。  
 **名稱**  
 鍵入 KPI 的名稱。  
  
 **相關聯的量值群組**  
 選取與 KPI 相關聯的量值群組。 用戶端應用程式可以使用此資訊，來決定當使用者瀏覽此 KPI 時可以使用的維度。  
  
 **值運算式**  
 展開即可檢視或編輯 KPI 值的多維度運算式 (MDX) 運算式。  
  
 鍵入會傳回 KPI 值的 MDX 運算式。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
 **目標運算式**  
 展開即可檢視或編輯 KPI 目標值的 MDX 運算式。  
  
 鍵入當 KPI 執行時會傳回 KPI 目標值的 MDX 運算式。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
 **狀態**  
 展開即可編輯 [狀態圖形]**** 和 [狀態運算式]**** 選項。  
  
 **狀態圖形**  
 選取用戶端應用程式在圖形表單中用來代表狀態值的圖形。  
  
> [!NOTE]  
>  用戶端應用程式可以支援選取的圖形，或使用適當的替代項目來取代。  
  
 **狀態運算式**  
 鍵入當 KPI 執行時會傳回 KPI 狀態值的 MDX 運算式。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
 建議此運算式傳回介於-1 和1之間的十進位數。 較低的數字代表負值狀況，而較高的數字代表正值狀況。  
  
> [!NOTE]  
>  低於-1 和以上的值是可能的，但協力廠商用戶端應用程式可能無法正確地加以解讀。  
  
 **趨勢**  
 展開即可編輯 [趨勢圖形]**** 和 [趨勢運算式]**** 選項。  
  
 **趨勢圖形**  
 選取用戶端應用程式在圖形表單中用來代表趨勢值的圖形。  
  
> [!NOTE]  
>  用戶端應用程式可以支援選取的圖形，或使用適當的替代項目來取代。  
  
 **趨勢運算式**  
 鍵入會傳回 KPI 趨勢值的 MDX 運算式。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
 趨勢運算式可以根據給定商務內容中任何有意義、以時間為基礎的準則。 建議此運算式傳回介於-1 和1之間的十進位數。 較低的數字代表經過一段時間的負值趨勢，而較高的數字代表經過一段時間的正值趨勢。  
  
> [!NOTE]  
>  低於-1 和以上的值是可能的，但協力廠商用戶端應用程式可能無法正確地加以解讀。  
  
 **其他屬性**  
 展開即可檢視 [顯示資料夾]****、[父 KPI]****、[目前時間成員]****、[加權]**** 和 [描述]**** 選項。  
  
 **顯示資料夾**  
 鍵入用戶端應用程式用於顯示用途所使用的 KPI 分類。  
  
 在顯示資料夾中使用反斜線 (\\) 來分隔資料夾名稱，並使用分號 (;) 來分隔多個顯示資料夾。 例如，輸入 `Category\Goal\Scientific;Category\Goal\Metric`。  
  
 **父 KPI**  
 選取現有的 KPI，在其下分類供用戶端應用程式使用的 KPI。  
  
> [!NOTE]  
>  如果此選項設定為現有的 KPI，則會忽略 [顯示資料夾]****。  
  
 **目前時間成員**  
 鍵入會傳回成員的 MDX 運算式，該成員用來識別 KPI 的暫時內容。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
> [!IMPORTANT]  
>  MDX 計算式必須傳回成員的唯一名稱，該成員在時間維度內與 [相關聯的量值群組]**** 中所指定的量值群組相關聯。  
  
 **Weight**  
 展開即可檢視或編輯 KPI 加權因數的 MDX 運算式。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
 **說明**  
 鍵入 KPI 的選擇性描述。  
  
## <a name="see-also"></a>另請參閱  
 [Kpi &#40;Cube 設計師&#41; &#40;Analysis Services-多維度資料&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)  
  
  
