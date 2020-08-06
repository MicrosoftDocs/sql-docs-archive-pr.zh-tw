---
title: 流覽關聯規則模型 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining model, association
- mining models, viewing
- association [data mining]
ms.assetid: faffe208-7a64-4ec6-825f-ecbaa79caff7
author: minewiskan
ms.author: owend
ms.openlocfilehash: de5adbca264fff81b44424d865a2c8201a6fdfc3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593099"
---
# <a name="browsing-an-association-rules-model"></a>瀏覽關聯規則模型
  當您使用 **[流覽]** 開啟關聯模型時，該模型會顯示在互動式檢視器中，類似于中的關聯規則檢視器 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。  此檢視器可讓您快速查看相互關聯的項目，並顯示可用於預測或提出建議的規則。  
  
##  <a name="explore-the-model"></a><a name="BKMK_ViewerTabs"></a>探索模型  
 當您開啟使用關聯規則演算法建立的採礦模型時 [!INCLUDE[msCoName](../includes/msconame-md.md)] ，[**流覽**] 視窗會包含下列視圖，每個都設計成讓您探索模型的不同層面：  
  
-   [項目集](#BKMK_Itemsets)  
  
-   [規則](#BKMK_Rules)  
  
-   [相依性網路](#BKMK_Dependency)  
  
 請記下每個索引標籤上的選項 [**顯示完整名稱**]。 透過選取這個選項，您可以顯示或隱藏項目集的來源資料表，以及縮短或增長規則或項目集的名稱。 當您的案例資料和屬性資料來自不同資料來源時，這個選項特別有用。  
  
 若要試驗關聯模型，您可以使用範例資料活頁簿之 [關聯] 索引標籤上的範例資料，然後使用所有預設值建立關聯模型。 您也可以建立購物籃分析模型，並使用 **[流覽]** 來開啟它。  
  
###  <a name="itemsets"></a><a name="BKMK_Itemsets"></a>專案集  
 [**專案集**] 索引標籤是開始探索關聯模型的絕佳位置。 此索引標籤會顯示常被模型湊在一起的項目清單。  
  
 ![關聯模型中的項目清單](media/dm13-association-itemsets.gif "關聯模型中的項目清單")  
  
 您可以在購物籃模型中找到項目集的最常見範例，在此模型中，項目集表示許多客戶會同時購買的產品配對或組合。 不過，根據您分組及排序項目的方式，項目集可能包含客戶在一段時間內訂購的影片序列，或傾向在特定位置發生的事件。  
  
 專案*集可以包含*最少一個專案到兩個、三個，或多個設定為模型的專案集大小上限。 針對每個專案集，檢視器會顯示專案集的*支援* *、機率和**大小*。 支援和機率是用來排名項目集的主體統計資料，並且是關聯模型所產生的規則。 這些值也可用來計算及描述其重要性。  
  
 **支援**。 支援表示包含此項目的案例數目或輸入資料的資料列數。 例如，如果專案集包含在「購物車」中找到的兩個專案，[**支援**] 資料行中的數位會指出在來源資料中出現該專案組合的次數。  
  
 **大小**。 藉由變更項目集大小，您可以控制項目集清單的長度。 如果您不想要在清單中看到單一產品，請將 [專案集**大小下限**] 選項變更為2個以上。  增加項目集大小下限來限制清單，讓您能夠尋找非常特定的模式， 而且可能會在處理非常龐大的資料集時相當有用。  
  
 您可以變更 [**最小支援**] 和 [**最大資料列**數] 值，以篩選顯示在索引標籤中的專案集數目。 如果您增加 [**最小支援**] 值，此清單會顯示較少的專案集，但專案集會是輸入資料中較常見的一個。 一般是否與重要相同是另一個問題，您可以使用 [**規則**] 索引標籤來探索。  
  
 請注意，變更 [**專案集**] 索引標籤上的 [支援] 值或其他控制項，只會變更顯示的專案，而不會影響基礎模型。 如果您想要產生較少或更多的專案集，或限制其大小，您應該使用 `MINIMUM_SUPPORT` `MAXIMUM_SUPPORT` [**演算法參數**] 對話方塊中提供的參數和。  
  
##### <a name="explore-the-itemsets-list"></a>探索項目集清單  
  
1.  按一下 [**支援**] 資料行，依最高至最低支援排序。 如此可讓您了解客戶最常購買的項目。  
  
2.  若要將焦點放在感興趣的特定專案集，請在 [**篩選**專案集] 方塊中輸入一些文字。  
  
     我們在此輸入 `Gloves` 。 當您套用篩選時，系統會重新整理清單，並只顯示包含手套的項目集。 如此可讓您專注於客戶購買手套及其他一些項目的交易。  
  
     **[篩選項目集]** 選項也會顯示您先前已用過的篩選清單。  
  
3.  變更 [專案集**大小下限**] 的值，以篩選出僅購買手套但沒有其他專案的客戶。  
  
4.  按一下 [**顯示**] 選項的下拉式清單，以控制屬性的顯示方式：  
  
    -   **顯示屬性名稱和值**  
  
    -   **只顯示屬性值**  
  
    -   **只顯示屬性名稱**  
  
     注意名稱有何改變。 在購物籃模型案例中，此模型是建立在多位客戶購買之產品的巢狀資料表上，因此屬性名稱通常是產品名稱，而清單中顯示的產品會標示為 `Existing`，表示客戶確實購買此項目。  
  
     `Existing` 的相反是 `Missing`，在資料採礦中調查時是相當有用的屬性。 例如，假設專案集 A + B 非常熱門，您想要尋找購買專案 A 但不是專案 B 的客戶。您可以使用預測查詢來執行這項操作，並使用其中一個來抓取交易，而不是另一個來進行進一步的分析。 如需有關如何在關聯模型上建立預測查詢的詳細資訊，請參閱 SQL Server 線上叢書中的[關聯模型查詢範例](data-mining/association-model-query-examples.md)  
  
5.  若要強制專案集清單使用新的篩選準則重新顯示，您可以選取或清除 [**顯示完整名稱**] 核取方塊。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="rules"></a><a name="BKMK_Rules"></a>條  
 [**規則**] 索引標籤會合併專案集的相關資訊及其相對值。  
  
 ![關聯模型建立的規則清單](media/dm13-association-rules.gif "關聯模型建立的規則清單")  
  
 機率*代表資料*集中包含目標專案組合的案例分數。 機率類似于*信賴*的統計概念，並可讓您指出規則的結果可能發生的原因。 您可以在此窗格中變更 [**最小**機率] 的值，以篩選顯示的規則。  
  
 您一開始看到的**最小**機率值是建立模型時，演算法所使用的臨界值。 模型完成後，您無法減少此值，但您可以將它增加，只顯示較高的機率專案。  
  
 *重要性*的設計是要測量規則的實用性。 很常見的規則可能非常普遍，而擁有較少的資訊價值。 重要性越高，規則對於預測結果便越有價值。 在 [[購物籃分析] &#40;[適用于 Excel&#41;工具的資料表 AnalysisTools](shopping-basket-analysis-table-analysistools-for-excel.md) ] 中，[重要性] 可以與專案的價格結合，以判斷在銷售方面可能最具價值的組合。  
  
##### <a name="explore-the-rules-list"></a>探索規則清單  
  
1.  嘗試按一下欄位標題-[機率]、[**重要性**] 和 [**規則** **]，以**查看資料變更的方式。  
  
2.  使用 [**篩選規則**] 選項來輸入值，並將焦點放在目標規則上。  
  
     例如，如果您想要查看預測客戶可能隨手套購買的所有規則，請在文字方塊中輸入 "手套"，然後重新整理窗格。  
  
     **[篩選項目集]** 選項也會顯示您先前已用過的篩選清單。  
  
3.  若要強制使用篩選準則重新顯示規則清單，您可以選取或清除 [**顯示完整名稱**] 核取方塊。  
  
4.  使用 [**顯示**] 選項來控制規則名稱的顯示方式。  
  
5.  將 [**最大資料列數**] 選項的值設定為100，然後按一下 [**複製到 Excel**]。  
  
     請注意，變更此值不會對模型中的資料量產生任何影響;它只會控制顯示清單中的資料列數目。 此選項適合搭配超大型模型使用。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="dependency-network"></a><a name="BKMK_Dependency"></a>相依性網路  
 [相依性**網路**] 索引標籤是專案之間相互關聯的視覺化地圖。 圖形中的每個橢圓形 (稱為*節點*) 代表屬性/值組，例如 "背心 = Existing" 或 "Age = 1-30"。  每一行連接橢圓形 (稱為「*邊緣*」) 代表相互關聯的類型。  
  
 ![關聯模型的相依性網路圖表](media/dm13-association-dependencynetwork.gif "關聯模型的相依性網路圖表")  
  
##### <a name="explore-the-dependency-network"></a>探索相依性網路  
  
1.  按一下 [**尋找**] 按鈕，然後使用 [**尋找節點**] 對話方塊來輸入感利率的專案。  
  
     例如，輸入 "手套"，然後將視窗中的圖形最大化，讓您可以輕鬆地查看結果。  
  
     包含項目的節點會醒目提示，而指向節點的箭頭表示連接項目的規則。  
  
     箭頭方向表示規則方向。 例如，如果購買手套的人也可能購買背心，箭號就會從 "手套" 節點開始，並在 "背心" 節點上終止。  
  
     若要取得此規則的其他相關統計資料，您可以按一下 [**規則**] 索引標籤，然後尋找包含「手套-現有」-> 「背心-現有」描述的規則。)   
  
2.  按一下並拖曳檢視器左側的滑桿。  
  
     此滑桿具有篩選規則機率的作用。 降低滑桿只顯示最強的規則。  
  
3.  按一下 [**複製到 excel** ]，將目前視窗的快照集複製到 excel。  
  
     您將無法使用複製到 Excel 的圖形;如果您需要互動式網狀圖形，請使用在[Visio 中觀看資料採礦模型 &#40;資料採礦增益集&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md)。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
## <a name="more-about-association-models"></a>進一步了解關聯模型  
 您可以使用 [**流覽]** 功能來開啟和探索使用 Microsoft 關聯規則演算法建立的任何模型。 這包括使用購物籃分析所建立的模型[&#40;適用于 Excel&#41;工具的資料表 AnalysisTools](shopping-basket-analysis-table-analysistools-for-excel.md) 、**資料表的分析工具**功能區，或中的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。  
  
 如果您使用購物籃分析工具建立關聯規則模型，許多進階選項將會自動為您設定。  
  
 如果您想要設定 [高級參數] 或 [變更最小機率和支援]，請使用 [[關聯] Wizard &#40;適用于 excel&#41;Wizard 的資料採礦用戶端](associate-wizard-data-mining-client-for-excel.md)，或使用 [[將模型加入至 excel 的結構 &#40;資料採礦增益集&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)模型化] 選項來建立您自己的模型。  
  
-   **專案集：** 當您建立模型時，您也可以將值指派給 MINIMUM_PROBABILITY 參數，以控制所產生的專案集數目。 您可以在 [演算法參數] 對話方塊使用這個參數。  
  
-   **規則：**[!INCLUDE[msCoName](../includes/msconame-md.md)]關聯規則演算法會使用機率值來限制所產生的規則數目。 您可以設定 `MINIMUM_PROBABILITY` 或 `MINIMUM _IMPORTANCE` 參數來控制規則數目。  
  
 如需設定 advanced 參數的詳細資訊，請參閱[資料採礦演算法 &#40;SQL Server 資料採礦增益集&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md)。  
  
## <a name="see-also"></a>另請參閱  
 [在 Excel 中流覽模型 &#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
