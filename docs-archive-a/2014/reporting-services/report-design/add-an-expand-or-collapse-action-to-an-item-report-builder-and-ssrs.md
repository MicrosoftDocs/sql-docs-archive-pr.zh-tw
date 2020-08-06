---
title: 將展開或摺疊動作新增項目中 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 49f07ad6-242b-4861-8fc1-91ca78c36d6c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 331c6a14a4a898ffcdf86f274c00e7ad3c801ec7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687465"
---
# <a name="add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs"></a>將展開或摺疊動作加入項目中 (報表產生器及 SSRS)
  您可以讓使用者以互動方式展開或摺疊報表項目，或者針對資料表或矩陣，展開或摺疊與群組關聯的資料列和資料行。 若要讓使用者展開或摺疊項目，您可以設定該項目的可見性屬性。 設定可見性適用於 HTML 報表檢視器，有時稱為 *「向下鑽研」* (Drilldown) 動作。  
  
 在報表設計檢視中，請指定要顯示展開和摺疊切換圖示之文字方塊的名稱。 在轉譯過的報表中，文字方塊除了其內容之外，還會顯示一個加號 (+) 或一個減號 (-)。 當使用者按一下切換時，報表顯示會重新整理，根據報表項目的目前可見性設定，顯示或隱藏報表項目。  
  
 展開和摺疊動作通常用於一開始只顯示摘要資料，以及讓使用者按一下加號來顯示詳細資料。 例如，您一開始可以隱藏顯示圖表值的資料表，或針對包含巢狀資料列或資料行群組的資料表隱藏子群組，如同在向下鑽研報表一樣。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-expand-and-collapse-action-to-a-group"></a>若要將展開和摺疊動作加入至群組中  
  
1.  在報表設計檢視中，按一下資料表或矩陣即可選取它。 [群組] 窗格會顯示資料列和資料行群組。  
  
     ![群組窗格](../media/groupingpane.png "群組窗格")  
  
     如果未顯示 [群組] 窗格，請按一下[檢視] **** 功能表，然後按一下 [群組] ****。  
  
2.  以滑鼠右鍵按一下 [群組] 窗格標題列的任意位置，然後按一下 [進階]****。 [群組] 窗格模式會切換以便在設計介面上，顯示資料列和資料行的基礎顯示結構。  
  
     ![含 [進階模式] 功能表的 [群組] 窗格](../media/groupingpane-advancedmode.png "含 [進階模式] 功能表的 [群組] 窗格")  
  
3.  在適當的群組窗格中，按一下您要隱藏相關聯資料列或資料行之資料列群組或資料行群組的名稱。 群組選定之後，[屬性] 窗格會顯示 **[Tablix 成員]** 屬性。  
  
    > [!NOTE]  
    >   如果看不到 [屬性] 窗格，請按一下功能區上的 [檢視] **** ，然後按一下 [屬性] ****。  
  
4.  在中 `Hidden` ，選擇下列其中一個選項，以在您第一次執行報表時設定此報表專案的可見度：  
  
    -   選取 `False` 即可顯示報表專案。  
  
    -   選取 `True` 即可隱藏報表專案。  
  
    -   選取 **\<Expression>** 即可開啟 [**運算式**] 對話方塊，以建立在執行時間評估的運算式來決定可見度。  
  
5.  在 **ToggleItem**中，從下拉式方塊選取要加入切換影像之目標文字方塊的名稱。  
  
     在下圖中，色彩資料列群組已設定為可讓使用者展開和摺疊相關聯的資料列。  
  
     ![設定要展開的資料列群組](../media/expandcollapse-confighiddentoggleitemwithnumbers.png "設定要展開的資料列群組")  
  
    > [!NOTE]  
    >  具有切換影像的文字方塊不能是您要隱藏相關聯資料列或資料行的資料列或資料行群組。 它必須在隱藏項目的相同群組中，或在上階群組中。 例如，若要切換與子群組相關之資料列的可見性，請選取與父群組有關之資料列中的文字方塊。  
  
6.  若要測試切換，請執行報表，然後按一下包含切換影像的文字方塊。 報表顯示會重新整理，以顯示包含已切換之可見性的資料列群組和資料行群組。  
  
     ![執行含可展開資料列群組的報表](../media/expandcollapse-runreport-rowgroup.png "執行含可展開資料列群組的報表")  
  
### <a name="to-add-expand-and-collapse-action-to-a-report-item"></a>若要將展開和摺疊動作加入至報表項目中  
  
1.  在報表設計檢視中，以滑鼠右鍵按一下要顯示或隱藏的報表專案，然後按一下 [ *\<report item>* **屬性**]。 報表專案的 [ *\<report item>* **屬性**] 對話方塊隨即開啟。  
  
2.  按一下 **[可見性]** 。  
  
3.  在 **[一開始執行報表時]** 中，選擇下列其中一個選項來設定第一次執行報表時，此報表項目的可見性：  
  
    -   選取 **[顯示]** 來顯示報表項目。  
  
    -   選取 **[隱藏]** 來隱藏報表項目。  
  
    -   選取 **[依據運算式顯示或隱藏]** ，使用在執行階段評估的運算式來決定可見性。 按一下 [ (**fx**) 開啟 [**運算式**] 對話方塊，以建立運算式。  
  
        > [!NOTE]  
        >  當您指定可見性的運算式時，會設定報表項目的 Hidden 屬性。 運算式會評估為 `Boolean` 值 `True` 來隱藏項目，以及 `False` 來顯示項目。  
  
4.  在 [此報表項目可以切換顯示]**** 中，從下拉式方塊鍵入或選取報表中要顯示切換影像的文字方塊名稱；例如 Textbox1。  
  
     在下圖中，資料表已設定為讓使用者可展開及摺疊該資料表。 [Products 資料表] 文字方塊可以切換資料表的顯示。  
  
     ![設定要展開的報表資料表](../media/expandcollapse-reporttable.png "設定要展開的報表資料表")  
  
    > [!NOTE]  
    >  您選擇的文字方塊必須位於此報表項目的目前或包含範圍 (最高至報表主體 (包含))。 例如，若要切換圖表的可見性，請選取與圖表位於相同涵蓋範圍的文字方塊，例如，報表主體或矩形。 此文字方塊必須位於相同或更高的容器階層中。  
  
5.  若要測試切換，請執行報表，然後按一下包含切換影像的文字方塊。 報表顯示會重新整理，以顯示包含已切換之可見性的報表項目。  
  
     ![執行含有已展開資料表的報表](../media/expandcollapse-runreport-reporttable.png "執行含有已展開資料表的報表")  
  
## <a name="see-also"></a>另請參閱  
 [&#40;報表產生器和 SSRS 的深入分析動作&#41;](drilldown-action-report-builder-and-ssrs.md)   
 [隱藏項目 &#40;報表產生器及 SSRS&#41;](../report-builder/hide-an-item-report-builder-and-ssrs.md)  
  
  
