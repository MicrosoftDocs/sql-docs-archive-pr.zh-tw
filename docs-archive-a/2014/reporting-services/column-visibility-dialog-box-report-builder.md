---
title: 資料行可見度對話方塊 (報表產生器) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10127"
ms.assetid: 0c030cab-6087-45a5-99f0-c7bd693f20a1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4c775734a4dbba2120a2af86e35a3872f5fff718
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688625"
---
# <a name="column-visibility-dialog-box-report-builder"></a>資料行可見性對話方塊 (報表產生器)
  使用 **[資料行可見性]** 對話方塊在報表第一次執行時顯示或隱藏選取的資料行，或使用其他報表項目來切換資料行的可見性。  
  
## <a name="options"></a>選項  
 **一開始執行報表時**  
 選擇一個選項以指出報表項目最初顯示在報表中的方式。  
  
 **顯示**  
 選擇此選項，即可顯示資料行。  
  
 **隱藏**  
 選擇此選項，即可隱藏資料行。  
  
 **依據運算式顯示或隱藏**  
 選擇此選項即可使用運算式改變初始可見性。  
  
 輸入會評估為 `Boolean` 值的運算式，`True` 會隱藏項目，`False` 會顯示項目。 按一下運算式 (*fx*) ] 按鈕，即可編輯運算式。  
  
 **此報表項目可以切換顯示**  
 選擇這個選項可顯示一個切換影像，讓使用者在 HTML 報表檢視器中顯示或隱藏這個資料行。  
  
 輸入或選取您想要顯示切換影像之報表中的文字方塊名稱，例如 Textbox1。 您所選的文字方塊必須位於這個報表項目的目前範圍或涵蓋範圍中。 例如，若要切換與子群組相關之資料列的可見性，請選取與父群組有關之資料列中的文字方塊。 若要切換圖表的可見性，請選取與圖表位於相同涵蓋範圍的文字方塊，例如，報表主體或矩形。  
  
## <a name="see-also"></a>另請參閱  
 [運算式範例 &#40;報表產生器及 SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [將展開或折迭動作新增至 &#40;報表產生器和 SSRS 的專案&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [&#40;報表產生器和 SSRS&#41;的影像](report-design/images-report-builder-and-ssrs.md)   
 [對話方塊、窗格和嚮導的報表產生器說明](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [影像屬性對話方塊、一般 &#40;報表產生器及 SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
