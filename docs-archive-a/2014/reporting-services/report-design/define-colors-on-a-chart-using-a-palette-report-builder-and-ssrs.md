---
title: 使用調色盤定義圖表的色彩 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d95efc22-5a32-43d4-9bd2-12753e7fd395
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7db137ed87b0c84e43577dcf2936a6287abd8e36
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595744"
---
# <a name="define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs"></a>使用調色盤定義圖表的色彩 (報表產生器及 SSRS)
  您可以選取預先定義的調色盤，或定義自訂調色盤來變更圖表的色彩調色盤。 自訂調色盤是報表專屬的。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-colors-on-the-chart-using-a-built-in-color-palette"></a>若要使用內建的色彩調色盤變更圖表的色彩  
  
1.  開啟 [屬性] 窗格。  
  
2.  在設計介面上，按一下圖表。 圖表物件的屬性會顯示在 [屬性] 窗格中。  
  
     物件名稱 (預設為**Chart1** ) 就會出現在 [屬性] 窗格頂端的下拉式清單中。  
  
3.  在 [圖表]  區段中，從下拉式清單為 Palette 屬性選取新的調色盤。  
  
    > [!NOTE]  
    >  您無法在預先定義的調色盤中變更色彩或順序。  
  
### <a name="to-define-your-own-colors-on-the-chart-using-a-custom-color-palette"></a>若要使用自訂色彩調色盤，在圖表上定義自己的色彩  
  
1.  開啟 [屬性] 窗格。  
  
2.  在設計介面上，按一下圖表。 圖表物件的屬性會顯示在 [屬性] 窗格中。  
  
3.  在 [**圖表**] 區段中，針對 `Palette` 屬性選取 [**自訂**]。  
  
4.  在 CustomPaletteColors 屬性中，按一下 [編輯集合] \( **...** ) 按鈕。 **[ReportColorExpression 集合編輯器]** 便會開啟。  
  
5.  按一下 **[加入]** 來加入色彩。 從下拉式清單中選取一個色彩，或選取 [運算式]，然後為特定色彩指定一個十六進位值，例如，ff6600 代表「橙色」。  
  
     如需有關十六進位值的詳細資訊，請參閱 MSDN 上的 [色彩表](https://go.microsoft.com/fwlink/?linkid=9258) 。  
  
6.  按一下 **[加入]** ，將其他色彩加入到調色盤中。  
  
7.  在您完成後，按一下 **[確定]** 。  
  
 如果您要使用自訂調色盤，可以藉由變更色彩的順序來變更圖表中不同序列的色彩。  
  
## <a name="see-also"></a>另請參閱  
 [設定圖表上數列色彩的格式 &#40;報表產生器及 SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [跨多個形狀圖指定一致的色彩 &#40;報表產生器及 SSRS&#41;](shape-charts-report-builder-and-ssrs.md)  
  
  
