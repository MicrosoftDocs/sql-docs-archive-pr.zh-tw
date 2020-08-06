---
title: 層級和成員 (瀏覽器索引標籤、維度設計師)  (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.browsertab.levelsandmembers.f1
ms.assetid: 3f61e384-5b4e-4480-a7ed-b408de2fdea7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 21680f00b82b5410e2c7a67122fdcfeb78c999dc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87710945"
---
# <a name="level-and-members-browser-tab-dimension-designer-analysis-services---multidimensional-data"></a>層級和成員 (瀏覽器索引標籤，維度設計師) (Analysis Services - 多維度資料)
  使用此頁面來瀏覽目前選取之階段和語言的成員。 若要選取要瀏覽的階層或語言，請使用 **[工具列]** 窗格上的 **[階層]** 和 **[語言]** 選項。 如需 [工具列] 窗格的詳細資訊，請參閱[工具列 &#40;瀏覽器索引標籤、維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](toolbar-browser-tab-dimension-designer-analysis-services-multidimensional-data.md)。  
  
## <a name="writeback-mode"></a>回寫模式  
 如果啟用回寫模式，此窗格的功能就會變更。 選取的維度必須是可寫入的 (換言之，維度的 `WriteEnabled` 屬性必須設定為 True)，而且必須將維度部署至 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體才能啟用回寫模式。  
  
 若要啟用回寫模式，您可以從 [工具列]**** 窗格中選取 [回寫]****，或以滑鼠右鍵按一下 [層級和成員]**** 窗格，然後從內容功能表中選取 [回寫]****。  
  
 如果已啟用回寫模式，您可以在 **[層級和成員]** 窗格中執行下列的其他動作：  
  
|若要這樣做，|執行|  
|-----------|-------------|  
|在選取的階層內建立同層級成員和子成員。|以滑鼠右鍵按一下選取的成員，然後從內容功能表中選取 [建立同層級]**** 來建立同層級成員，或選取 [建立子系]**** 來建立子成員。|  
|將選取的成員在階層間向上或向下移動。|將選取的成員拖曳至適當的父成員或子成員處，或在 **[工具列]** 窗格上按一下 **[增加縮排]** 或 **[減少縮排]** ，將選取的成員在階層的各層級間向上或向下移動。|  
|重新命名選取的成員。|以滑鼠右鍵按一下選取的成員，然後選取 [重新命名]****，或按一下已經選取的成員。|  
|編輯成員屬性值|針對選取的成員按兩下已選取成員屬性中的值，以編輯該值。|  
  
## <a name="options"></a>選項  
 **目前層級**  
 顯示目前在 [樹狀]**** 中選取之成員所屬的層級。  
  
 **路徑**  
 顯示目前選取之階層和語言的成員。  
  
 如果是從 [工具列] 窗格的 **[成員屬性]** 選項中選取成員屬性，則每個成員屬性都會顯示為一個資料行。  
  
 如果啟用回寫模式，與維度中之索引鍵屬性相關聯的每一個索引鍵資料行都會顯示一個資料行。  
  
## <a name="context-menu"></a>操作功能表  
 以滑鼠右鍵按一下所選取成員之 [層級和成員]**** 窗格的任何部份，即可顯示提供下列選項的內容功能表：  
  
 **建立同層級**  
 建立與選取之成員同層級的新成員。  
  
> [!NOTE]  
>  唯有選取了 (所有) 層級以外層級的成員時，才會啟用此選項。  
  
> [!NOTE]  
>  只有啟用回寫模式時才會顯示此選項。  
  
 **建立子系**  
 在選取之成員的下一個較低層級上建立新成員，作為選取之成員的子成員。  
  
> [!NOTE]  
>  唯有選取了最低層級以外層級的成員時，才會啟用此選項。  
  
> [!NOTE]  
>  只有啟用回寫模式時才會顯示此選項。  
  
 **剪下**  
 將選取的成員複製至剪貼簿，並將它們從階層中移除。  
  
> [!NOTE]  
>  唯有選取所有成員以外的成員時，才會啟用此選項。  
  
> [!NOTE]  
>  只有啟用回寫模式時才會顯示此選項。  
  
 **貼上**  
 將之前使用 [剪下]**** 移除的成員，貼在選取之成員的後面。  
  
> [!NOTE]  
>  只有啟用回寫模式時才會顯示此選項。  
  
 **刪除**  
 從階層中移除選取的成員。  
  
> [!NOTE]  
>  唯有選取所有成員以外的成員時，才會啟用此選項。  
  
> [!NOTE]  
>  只有啟用回寫模式時才會顯示此選項。  
  
 **重新命名**  
 選取即可編輯選取之成員的名稱。  
  
> [!NOTE]  
>  唯有選取所有成員以外的成員時，才會啟用此選項。  
  
> [!NOTE]  
>  只有啟用回寫模式時才會顯示此選項。  
  
 **篩選成員**  
 顯示 [篩選成員]**** 對話方塊，以針對選取的階層篩選顯示在 [層級和成員]**** 中的成員。 如需 [篩選成員]**** 對話方塊的詳細資訊，請參閱[篩選成員對話方塊 &#40;Analysis Services - 多維度資料&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **全部展開**  
 展開 [樹狀]**** 中的所有成員。  
  
> [!NOTE]  
>  唯有選取了最低層級以外層級的成員時，才會啟用此選項。  
  
 **全部摺疊**  
 摺疊 [樹狀]**** 中的所有成員。  
  
 **展開成員**  
 展開 [樹狀]**** 中選取的成員。  
  
 **摺疊成員**  
 摺疊 [樹狀]**** 中選取的成員。  
  
 **回寫**  
 選取即可啟用回寫模式。  
  
## <a name="see-also"></a>另請參閱  
 [[工具列 &#40;瀏覽器] 索引標籤、[維度設計師]&#41; &#40;Analysis Services-多維度資料&#41;](toolbar-browser-tab-dimension-designer-analysis-services-multidimensional-data.md)   
 [瀏覽器 &#40;維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](browser-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
