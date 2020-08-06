---
title: 修改預設資料表名稱 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ddd97483-a76d-43c1-8b40-fc7cc57fb0c2
author: minewiskan
ms.author: owend
ms.openlocfilehash: 254f797be95f60211983400b019415431d4cf39c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584796"
---
# <a name="modifying-default-table-names"></a>修改預設資料表名稱
  您可以針對資料來源檢視中的物件，變更 **FriendlyName** 屬性的值，使其更明顯且更容易使用。  
  
 在下列工作中，您會在資料來源檢視中變更每個資料表的易記名稱，方法是從這些資料表中移除 "**Dim**" 和 "**Fact**" 前置詞。 這樣可以讓 Cube 和維度物件 (將在下一課定義) 更明顯且更容易使用。  
  
> [!NOTE]  
>  您也可以在資料來源檢視中變更資料行的易記名稱、定義導出資料行和聯結資料表或檢視，使其更容易使用。  
  
### <a name="to-modify-the-default-name-of-a-table"></a>若要修改資料表的預設名稱  
  
1.  在 [資料來源檢視設計師]**** 的 [資料表]**** 窗格中，以滑鼠右鍵按一下 **FactInternetSales** 資料表，然後按一下 [屬性]****。  
  
2.  如果未顯示 [Microsoft Visual Studio] 視窗右側的 [屬性] 視窗，請按一下 [屬性] 視窗標題列上的 [自動隱藏]**** 按鈕，讓該視窗保持可見狀態。  
  
     當 [屬性] 視窗保持開啟時，要在資料來源檢視中變更每一個資料表的屬性會更加容易。 如果您未使用 [自動隱藏]**** 按鈕使視窗固定開啟，則在 [圖表]**** 窗格中按一下不同的物件時即會關閉視窗。  
  
3.  將**FactInternetSales**物件的**FriendlyName**屬性變更為 *`InternetSales`* 。  
  
     當您按一下而離開 **FriendlyName** 屬性的資料格時，即套用變更。 在下一課，您將定義以此事實資料表為基礎的量值群組。 事實資料表的名稱是 InternetSales 而不是 FactInternetSales，因為您在這一課已做了變更。  
  
4.  按一下 [資料表]**** 窗格中的 [DimProduct]****。 在 [屬性視窗中，將 [ **FriendlyName** ] 屬性變更為 *`Product`* 。  
  
5.  以相同方式變更資料來源檢視中其餘每個資料表的 **FriendlyName** 屬性，以便移除 "**Dim**" 前置詞。  
  
6.  完成時，按一下 [自動隱藏]**** 按鈕，再次隱藏 [屬性] 視窗。  
  
7.  在 [檔案]**** 功能表上或 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 的工具列上，按一下 [全部儲存]****，即可儲存您到目前為止在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程專案中所做的變更。 如果您想要的話，可以在此停止教學課程，之後再繼續。  
  
## <a name="next-lesson"></a>下一課  
 [第2課：定義和部署 Cube](lesson-2-defining-and-deploying-a-cube.md)  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源視圖](multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [變更資料來源檢視的屬性 &#40;Analysis Services&#41;](multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md)  
  
  
