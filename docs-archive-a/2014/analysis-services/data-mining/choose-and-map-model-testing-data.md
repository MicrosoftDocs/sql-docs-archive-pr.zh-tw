---
title: 選擇和對應模型測試資料 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- columns [data mining], mining accuracy charts
- Mining Accuracy Chart [Analysis Services], column mappings
- input column mapping [Analysis Services]
- mapping input columns [Analysis Services]
ms.assetid: be0d9f20-40c3-4dac-81da-281cfe724126
author: minewiskan
ms.author: owend
ms.openlocfilehash: 84f1d01c40070069d610bb028ab003223c5afbcd
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594847"
---
# <a name="choose-and-map-model-testing-data"></a>選擇和對應模型測試資料
  若要在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中建立精確度圖表，您必須選擇將用來測試模型的資料，並將資料對應至模型。  
  
 根據預設，只要您在建立採礦結構時建立了鑑效組資料集， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會使用採礦模型測試資料。 建立鑑效組測試集是測試根據相同採礦結構之模型的最簡單方式，因為資料行名稱和資料類型永遠符合模型，並且您可以合理地確定資料分佈是相似的。 此外，設計工具將自動建立輸入和模型資料行之間的關聯性。  
  
 您也可以指定外部資料來源。 對於外部資料，有一些其他需求：  
  
-   外部資料集必須在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的執行個體中定義為資料來源檢視。  
  
-   外部資料集至少必須包含一個資料行，而且該資料行可以對應至採礦模型中的可預測資料行。 您可以選擇忽略某些資料行。  
  
-   您無法加入新的資料行或是對應不同資料來源檢視中的資料行。 您所選的資料來源檢視必須包含預測查詢所需的所有資料行。  
  
-   如果外部資料行名稱與模型中的資料行名稱完全符合，則設計工具會自動對應這些資料行。 如果對應錯誤，您可以變更這些對應、刪除對應，或是為現有的資料行建立新的對應。  
  
-   如果您使用外部資料來源，可以套用篩選，將測試資料限制為相關的案例子集。  
  
-   即使在使用鑑效組測試集時，您也應該意識到篩選器可能在與採礦結構關聯的測試資料和採礦模型測試案例之間造成差異。  
  
 本主題描述如何選擇和對應測試資料：  
  
 [選取輸入資料表來測試採礦模型的精確度](#bkmk_SelectInputs)  
  
 [將模型資料行對應到測試資料的資料行](#bkmk_MapColumns)  
  
 [變更測試資料中的資料行對應至模型的方式](#bkmk_ChangeMappings)  
  
##  <a name="to-select-input-tables-to-test-the-accuracy-of-a-mining-model"></a><a name="bkmk_SelectInputs"></a> 若要選取輸入資料表來測試採礦模型的精確度  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的資料採礦設計師中，按兩下包含您想要建立圖表之模型的採礦結構。  
  
2.  選取 **[採礦精確度圖表]** 索引標籤。  
  
3.  在 [採礦精確度圖表]**** 檢視的 [輸入選擇]**** 索引標籤中，選取下列其中一個選項：  
  
     **使用採礦模型測試案例**  
  
     **使用採礦結構測試案例**  
  
     **指定不同的資料集**  
  
4.  如果您選取了 [指定不同的資料集]****，請選擇性地按一下 [開啟篩選編輯器]****，以便建立輸入資料集的篩選條件。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  按一下 [增益圖]**** 索引標籤或 [分類矩陣]**** 索引標籤，以便使用指定的測試資料來自動建立圖表。  
  
##  <a name="to-map-model-columns-to-the-columns-in-the-testing-data"></a><a name="bkmk_MapColumns"></a> 若要將模型資料行對應到測試資料的資料行  
  
1.  在資料採礦設計師中，按兩下包含您想要建立圖表之模型的採礦結構，以開啟結構與模型。  
  
2.  選取 **[採礦精確度圖表]** 索引標籤，然後選取 **[輸入選擇]** 索引標籤。  
  
3.  在 [輸入選擇]**** 索引標籤的 [選取要用於精確度圖表的資料集]**** 下，選取 [指定不同的資料集]****。  
  
4.  按一下 [流覽] 按鈕** ( ...] ) **開啟對話方塊，並建立外部資料集的定義。  
  
5.  在 [選取採礦結構]**** 對話方塊中，選取包含您要使用之模型的採礦結構，然後按一下 [確定]****。  
  
6.  在 [採礦精確度圖表]**** 索引標籤的 [選取輸入資料表]**** 資料表上，按一下 [選取案例資料表]****，即可開啟 [選取資料表]**** 對話方塊。  
  
7.  在 **[選取資料表]** 對話方塊中，從 **[資料來源]** 清單裡選取一個資料來源。 選擇含有資料的資料表，而這項資料就是您想要在預測查詢中判斷模型精確度時使用的資料。  
  
8.  在 [資料表/檢視表名稱]**** 方塊中，選取包含您要用來測試模型之資料的資料表。  
  
9. 必要時，請編輯對應。 採礦結構中的資料行會自動對應至輸入資料表中名稱相同的資料行。 若要手動建立對應，請按一下 [選取輸入資料表]**** 資料表中的資料行，然後將它拖曳到 [採礦結構]**** 資料表中的對應資料行上。 若要刪除對應，請按一下將 [採礦結構]**** 資料表中的資料行連結到 [選取輸入資料表]**** 資料表中之對應資料行的線條，然後按下 DELETE 鍵。  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-modify-the-way-input-data-is-mapped-to-the-model"></a><a name="bkmk_ChangeMappings"></a>若要修改輸入資料對應至模型的方式  
  
1.  在資料採礦設計師中，按兩下包含您想要繪製之模型的結構。  
  
2.  選取 **[採礦精確度圖表]** 索引標籤。  
  
3.  按一下 [輸入選擇]**** 索引標籤。  
  
4.  在 [**選取要用於精確度圖表的資料集**] 中，選取 [**指定不同的資料集**] 選項。  
  
5.  按一下 [流覽] 按鈕** ( ...] ) **開啟對話方塊，並建立外部資料源的定義。  
  
6.  在 [指定資料行對應]**** 對話方塊中，按一下 [選取案例資料表]****。  
  
7.  在 [選取資料表] 對話方塊中，從清單中選取資料來源檢視，然後選取包含案例資料的資料表。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  如果您需要的資料表無法使用，請關閉此對話方塊，然後建立包含此資料表的新資料來源檢視。 如需如何建立資料來源檢視的資訊，請參閱[定義資料來源檢視 &#40;Analysis Services&#41;](../multidimensional-models/defining-a-data-source-view-analysis-services.md)。  
  
9. 如果採礦模型包含巢狀資料表，請按一下 [選取巢狀資料表]****，然後從資料來源檢視的資料表清單中選取巢狀資料表。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. 選取您要修改之對應的連接線，然後選取 [修改連接]****。  
  
     **[修改對應]** 對話方塊會開啟。 在此對話方塊的資料表中，[採礦結構資料行]**** 會列出所選取採礦結構包含的每一個資料行，而 [資料表資料行]**** 則會列出輸入資料表中，對應到採礦結構之資料行的資料行。  
  
11. 在 [資料表資料行]**** 之下，選取對應到在 [採礦結構資料行]**** 之下，您要修改關聯性之資料列的資料列。 從清單中選取新的資料行，或選取清單中的空白項目來刪除資料行。  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     新的資料行對應會顯示在 [指定資料行對應]**** 對話方塊中。 您可以選取資料行之間的線，然後按 DELETE 鍵來移除對應。 您可以在 [採礦結構]**** 資料表中選取資料行，並將它拖曳到 [選取輸入資料表]**** 資料表中的對應資料行，以建立新的連接。  
  
## <a name="see-also"></a>另請參閱  
 [測試及驗證工作與操作方法 &#40;資料採礦&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
  
