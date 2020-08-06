---
title: 格式化量測計上的指標 (報表產生器及 SSRS)| Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2fdf670a-5237-48fe-813d-97657c5c77d2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c74cb4d4c61c18d25069dab062bf09804f5935b4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686813"
---
# <a name="formatting-pointers-on-a-gauge-report-builder-and-ssrs"></a>格式化量測計上的指標 (報表產生器及 SSRS)
  量測計指標會指出量測計目前的值。 根據預設，加入欄位時，包含在欄位中的值會彙總為量測計上之指標顯示的一個值。 您可以將多個指標加入到量測計中以便在相同的標尺上指出多個值，或者針對您已經加入的每個標尺加入多個標尺和一個指標。 將欄位加入到量測計之後，您必須在對應的標尺上設定最大值與最小值，以便將內容提供給指標值。 您也可以選擇在顯示標尺重要區域的範圍上，設定最小值與最大值。  
  
 您可以用滑鼠右鍵按一下指標，然後選取 [星形指標屬性]  或 [線性指標屬性]  ，以便在指標上設定外觀屬性。 每個量測計指標都包含一組相同的屬性。 每個量測計類型也都有唯一的對應外觀屬性：  
  
-   在星形量測計上，您可以指定指針指標和指針端點。  
  
-   在線性量測計上，您可以指定溫度計指標，這是橫條指標的變化。 溫度計指標可讓您指定球部的形狀。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="how-the-pointer-is-connected-to-data"></a><a name="HowPointer"></a> 如何將指標連接到資料  
 根據預設，加入量測計時，它包含沒有關聯欄位的一個指標。 這就是所謂的空指標。 在欄位加入到資料窗格之前，它將會顯示零。 當您將欄位加入至資料窗格時，該指標會連接到該欄位。 如果您從資料窗格刪除某個欄位，也會一併刪除與該欄位相關聯的指標。  
  
 新增資料之後，當您以滑鼠右鍵按一下指標時，將會出現 [清除指標]  和 [刪除指標]  選項。 **[清除指標值]** 選項將會移除附加到量測計的欄位，但是指標仍然會出現在量測計上。 **[刪除指標]** 選項將會從量測計刪除欄位，並從檢視刪除指標。 如果您將欄位重新加入到量測計中，預設指標將會重新出現。 當您將指標的**Hidden**屬性設定為時 `True` ，不會在設計介面上隱藏指標，但是它會在執行時間隱藏。  
  
  
##  <a name="displaying-multiple-pointers-on-the-gauge"></a><a name="DisplayingMultiple"></a> 在量測計上顯示多個指標  
 您可以將多個指標加入到量測計中，以便在相同的標尺上指出多個值。 這對於同時顯示最低值和最高值可能相當實用。 若要在量測計上針對相同的標尺指定一個以上的指標，以滑鼠右鍵按一下量測計內部的任何位置，然後在快速鍵功能表上按一下 [新增指標]  。 或者，您可以用滑鼠右鍵按一下量測計的任何位置，然後按一下 [新增標尺]  ，即可新增標尺。 接著，您可以加入新的指標，該指標就會與最後一個標尺自動產生關聯。  
  
 當指標重疊時，指標的繪圖順序取決於指標加入到量測計中的順序。 您無法透過變更資料窗格中的欄位順序來重新排列指標的繪製順序。 若要變更多個指標的繪製順序，請開啟 [屬性] 窗格，然後按一下 [指標 (...)]  。然後變更 [指標] 集合中的指標順序。  
  
  
##  <a name="setting-gradients-on-a-needle-cap"></a><a name="SettingGradients"></a> 在指針端點上設定漸層  
 您可以指定僅能在星形量測計之指標上方或下方繪製的指針端點。 所有指針端點樣式都可以使用無法修改的內建漸層繪製。 但 `RoundedDark` 樣式除外，您可以在其中指定漸層色彩與漸層樣式。  
  
  
##  <a name="setting-a-snapping-interval"></a><a name="SettingSnappingInterval"></a> 設定貼齊間隔  
 貼齊間隔會定義捨入值的倍數。 根據預設，量測計將指向您在資料窗格中指定之欄位的確切值。 不過，您可以向上或向下捨入確切值，以便讓指標貼齊預設的間隔。 例如，如果量測計的值為 34.2，而且您將貼齊間隔指定為 5，則量測計指標將會指向 35。 如果量測計的值為 31.2，而且您將貼齊間隔指定為 5，則量測計指標將會指向 30。 如需詳細資訊，請參閱設定量測計的[貼齊間隔 &#40;報表產生器和 SSRS&#41;](../set-a-snapping-interval-on-a-gauge-report-builder-and-ssrs.md)。  
  
  
##  <a name="specifying-an-image-as-a-pointer-on-a-radial-gauge"></a><a name="SpecifyingImage"></a> 將影像指定為星形量測計的指標  
 除了指標樣式的內建清單之外，您也可以將影像指定為指標。 這在使用影像取代現有的指針指標樣式時是最有效果的。 影像會附加在指標上，但是所有指標功能都適用。 當影像用於指標時，色彩與漸層選項則不適用。  
  
 如果指標影像為不規則的形狀，您應該將色彩定義為透明的，以便隱藏不應該出現在量測計上的影像區域。 當您定義透明色彩時，量測計會調換現有指標頂端的影像並修剪影像，這樣就可以只顯示指標的形狀。 量測計會重新調整影像以符合您指標的大小。 當您指定指標的影像時，加入到量測計頂端的任何後續指標都會繪製在影像的下方。 因此，如果量測計上有多個指標，最好不要為指標指定影像。 如需詳細資訊，請參閱[將影像指定為量測計上的指標 &#40;報表產生器和 SSRS&#41;](../specify-an-image-as-a-pointer-on-a-gauge-report-builder-and-ssrs.md)。  
  
  
## <a name="see-also"></a>另請參閱  
 [格式化量測計上的標尺 &#40;報表產生器及 SSRS&#41;](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [格式化量測計上的範圍 &#40;報表產生器及 SSRS&#41;](formatting-ranges-on-a-gauge-report-builder-and-ssrs.md)   
 [量測計 &#40;報表產生器及 SSRS&#41;](gauges-report-builder-and-ssrs.md)  
  
  
