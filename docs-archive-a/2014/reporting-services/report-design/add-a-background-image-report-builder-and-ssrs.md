---
title: 新增背景影像 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c777fefb-8695-44a7-b5cd-a18c587583f2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d7bc15e1b063a73c463cdb1e7e99075af2a3dce9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707169"
---
# <a name="add-a-background-image-report-builder-and-ssrs"></a>加入背景影像 (報表產生器及 SSRS)
  您可以將背景影像加入至報表項目 (如矩形、文字方塊、清單、矩陣、資料表和部分圖表) 或是加入至報表區段 (如頁首、頁尾或報表主體)。 您可以針對在 [屬性] 窗格中顯示 **[BackgroundImage]** 之報表設計介面上的任何選定項目來定義背景影像。 如同其他影像，背景影像可以是報表伺服器上影像的 URL、資料集欄位中的影像，或是報表定義中內嵌的影像。 若要使用內嵌在報表中的影像，您必須先將影像加入至報表定義，然後才可以將影像加入至設計介面。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-image-in-the-report-definition"></a>將影像內嵌在報表定義中  
  
1.  在 [報表資料] 窗格中，以滑鼠右鍵按一下 [影像]  節點，然後按一下 [新增影像]  。  
  
    > [!NOTE]  
    >  如果看不到 [報表資料] 窗格，請按一下 [檢視]  索引標籤上的 [報表資料]  。  
  
2.  瀏覽至您要內嵌在報表定義中的影像，然後按一下 **[確定]** 。  
  
### <a name="to-add-a-background-image"></a>加入背景影像  
  
1.  在報表設計檢視中，選取您想要將背景影像加入其中的報表項目。  
  
2.  如果看不到 [屬性] 窗格，請選取 **[檢視]** 索引標籤上的 **[屬性]** 。  
  
3.  在 [屬性] 窗格中，展開 **[BackgroundImage]** ，並執行下列動作：  
  
    -   如果是內嵌的影像：  
  
         將 **[來源]** 設定為 **[內嵌]** 。  
  
         將 **[值]** 設定為內嵌在報表中之影像的名稱。  
  
    -   如果是外部影像：  
  
         將 **[來源]** 設定為 **[外部]** 。  
  
         將 **[值]** 設定為影像的有效路徑。 這可以位於原生模式或 SharePoint 整合模式的報表伺服器上，也可以位於其他任何網站上。 如需詳細資訊，請參閱[新增外部影像 &#40;報表產生器及 SSRS&#41;](add-an-external-image-report-builder-and-ssrs.md)。  
  
    -   如果是包含在報表項目所連接之資料庫欄位中的影像：  
  
         將 **[來源]** 設定為 **[資料庫]** 。  
  
         將 **[值]** 設定為報表資料集中欄位的名稱。 如需詳細資訊，請參閱[新增資料繫結影像 &#40;報表產生器及 SSRS&#41;](add-a-data-bound-image-report-builder-and-ssrs.md)。  
  
         針對 **MIMEType** 或檔案格式，選取適用於影像的 MIME 類型，例如 .bmp。  
  
        > [!NOTE]  
        >  唯有 **[來源]** 屬性設定為 **[資料庫]** 時，MIMEType 才適用。 如果 **[來源]** 屬性設定為 **[外部]** 或 **[內嵌]** ，就會忽略 **[MIMEType]** 的值。  
  
    -   針對 **[BackgroundRepeat]** ，請選取運算式、 **[Default]** 、 **[Repeat]** 、 **[RepeatX]** 、 **[RepeatY]** 或 **[Clip]** 。  
  
         如果是圖表中的背景影像， **[BackgroundRepeat]** 可以設定為 **[Default]** 、 **[Repeat]** 、 **[Fit]** 和 **[Clip]** ，但是不能設定為 **[RepeatX]** 或 **[RepeatY]** 。  
  
## <a name="see-also"></a>另請參閱  
 [影像 &#40;報表產生器及 SSRS&#41;](images-report-builder-and-ssrs.md)   
 [影像屬性對話方塊、一般 &#40;報表產生器及 SSRS&#41;](../image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
