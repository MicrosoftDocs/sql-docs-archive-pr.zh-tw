---
title: 變更指標圖示和指標集合 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 8a056adf-4473-473d-9b0c-314675af7bfd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 398d21319ab6da22f2b10c3607baf8f110d6e65b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706206"
---
# <a name="change-indicator-icons-and-indicator-sets-report-builder-and-ssrs"></a>變更指標圖示和指標集合 (報表產生器及 SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會提供預先設定的指標集合，這個指標集合在已傳遞的報表中可能不一定會有效地描述您的資料，運作也不一定良好。 本主題提供變更指標圖示外觀，以及變更指標集合以加入不同、更多或更少之指標圖示的程序。  
  
 您可以使用運算式來設定選項，如色彩。 如需詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-color-of-an-indicator-icon"></a>若要變更指標圖示的色彩  
  
1.  以滑鼠右鍵按一下您要變更的指標，然後按一下 [指標屬性]  。  
  
2.  按一下左窗格中的 **[值和狀態]** 。  
  
3.  在您要變更的圖示旁邊按一下 [色彩]  資料行中的向下箭號，然後按一下要使用的色彩：[無色彩]  或 [更多色彩]  。  
  
     您可以選擇按一下 **「運算式」** \(*fx*) 按鈕來編輯設定 **[色彩]** 選項值的運算式。  
  
     如果您按一下 [更多色彩]  ，[選取色彩]  對話方塊隨即開啟，讓您從中選擇色彩。 如需其選項的詳細資訊，請參閱[選取色彩對話方塊 &#40;報表產生器及 SSRS&#41;](../select-color-dialog-box-report-builder-and-ssrs.md)。 按一下 [確定]  關閉 [選取色彩]  對話方塊。  
  
4.  按一下 [確定]  。  
  
### <a name="to-change-the-icon"></a>若要變更圖示  
  
1.  以滑鼠右鍵按一下您要變更的指標，然後按一下 [指標屬性]  。  
  
2.  按一下左窗格中的 **[值和狀態]** 。  
  
3.  按一下您要變更之圖示旁邊的向下鍵，然後選取不同的圖示。  
  
     您可以選擇按一下 **「運算式」** \(*fx*) 按鈕來編輯設定 **[圖示]** 選項值的運算式。  
  
4.  按一下 [確定]  。  
  
### <a name="to-use-a-custom-image-as-an-indicator-icon"></a>若要使用自訂影像做為指標圖示  
  
1.  以滑鼠右鍵按一下您要變更的指標，然後按一下 [指標屬性]  。  
  
2.  按一下左窗格中的 **[值和狀態]** 。  
  
3.  在您要變更的圖示旁邊按一下向下箭號，然後選取 [影像]  。  
  
4.  在 [選取影像來源]  清單中，按一下 [外部]  、[內嵌]  或 [資料庫]  。  
  
5.  根據影像的來源，執行下列其中一項：  
  
    -   若要使用儲存在報表外部的影像，按一下 [瀏覽]  ，然後找出影像。 報表將包含影像的參考。  
  
    -   若要使用內嵌在報表中的影像，按一下 [匯入]  ，然後找出影像。 影像會加入至報告定義，並與它一起儲存。  
  
    -   若要使用資料庫中的影像，請在 [使用此欄位]  清單中， 選取清單中的欄位，然後在 [使用此 MIME 類型]  清單中，選取影像的 MIME 類型。  
  
6.  按一下 [確定]  。  
  
### <a name="to-add-an-icon-to-the-indicator-set"></a>若要將圖示加入至指標集合  
  
1.  以滑鼠右鍵按一下您要變更的指標，然後按一下 [指標屬性]  。  
  
2.  按一下左窗格中的 **[值和狀態]** 。  
  
3.  按一下 [新增]  。 指標隨即使用預設圖示與 [無色彩]  選項新增。  
  
     設定指標使用您想要的圖示和色彩。 本主題稍早的程序描述執行這項操作的步驟。  
  
4.  按一下 [確定]  。  
  
### <a name="to-delete-an-icon-to-the-indicator-set"></a>若要從指標集合刪除圖示  
  
1.  以滑鼠右鍵按一下您要變更的指標，然後按一下 [指標屬性]  。  
  
2.  按一下左窗格中的 **[值和狀態]** 。  
  
3.  選取要刪除的圖示，然後按一下 [刪除]  。  
  
4.  按一下 [確定]  。  
  
## <a name="see-also"></a>另請參閱  
 [指標 &#40;報表產生器及 SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  
