---
title: 教學課程： 將參數加入至報表 （報表產生器） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: eab34ec4-b3ad-4a76-95cc-07b2f75ee6d7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dff41066a2d505ab53b17a10fb3da9b6cb17130f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704785"
---
# <a name="tutorial-add-a-parameter-to-your-report-report-builder"></a>教學課程：將參數加入至報表 (報表產生器)
  將參數加入至報表可讓使用者從資料來源或報表中篩選報表資料。 系統會針對您包含在資料集查詢中的每個查詢參數，自動建立報表參數。 參數資料類型會決定該類型會如何在報表檢視器工具列上顯示。  
  
 ![rs_tut_Parameter](../../2014/tutorials/media/rs-tut-parameter.gif "rs_tut_Parameter")  
  
##  <a name="what-you-will-learn"></a><a name="BackToTop"></a>您將瞭解的內容  
 在本教學課程中，您將學習如何執行下列作業：  
  
1.  [從資料表或矩陣精靈建立矩陣報表和資料集](#Setup)  
  
2.  [從資料表或矩陣精靈組織資料、選擇配置和樣式](#CompleteWizard)  
  
3.  [加入查詢參數來建立報表參數](#Query)  
  
4.  [變更報表參數的預設資料類型和其他屬性](#ChangeDefaultProperties)  
  
    1.  [加入資料集來提供可用值與顯示名稱](#AddDataset)  
  
    2.  [指定可以用於建立多個值之下拉式清單的值](#AvailableValues)  
  
    3.  [指定預設值讓報表能夠自動執行](#DefaultValues)  
  
    4.  [從具有名稱/值組的資料集中查閱值](#NameValue)  
  
5.  [在報表中顯示選取的參數值](#Expression)  
  
6.  [在篩選中使用報表參數](#Filter)  
  
7.  [將報表參數變更為可以接受多個值](#Multivalued)  
  
8.  [加入條件式可見性的布林參數](#Boolean)  
  
9. [加入報表標題](#Title)  
  
10. [儲存報表](#Save)  
  
> [!NOTE]  
>  在本教學課程中，精靈的步驟會合併為一個程序。 如需如何瀏覽至報表伺服器、選擇資料來源以及建立資料集的逐步指示，請參閱本系列的第一個教學課程：[教學課程：建立基本資料表報表 &#40;報表產生器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
 完成本教學課程的估計時間：25 分鐘。  
  
## <a name="requirements"></a>需求  
 如需需求的資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="1-create-a-matrix-report-and-dataset-from-the-table-or-matrix-wizard"></a><a name="Setup"></a>1. 從資料表或矩陣 Wizard 建立矩陣報表和資料集  
 建立矩陣報表、資料來源與資料集。  
  
> [!NOTE]  
>  在本教學課程中，查詢會包含資料值，因此不需要外部資料來源。 這樣會使查詢相當冗長。 在商業環境中，查詢不會包含資料。 這僅供教學之用。  
  
#### <a name="to-create-a-new-matrix-report"></a>若要建立新的矩陣報表  
  
1.  按一下 [ **開始**]、依序指向 [ **程式集**] 和 [ [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]**報表產生器**]，然後按一下 [ **報表產生器**]。  
  
     [**消費者入門**] 對話方塊隨即出現。  
  
    > [!NOTE]  
    >   如果 **[使用者入門]** 對話方塊沒有出現，請在 **[報表產生器]** 按鈕中按一下 **[新增]**。  
  
2.  在左窗格中，確認已選取 **[報表]** 。  
  
3.  在右窗格中，按一下 **[資料表或矩陣精靈]**。  
  
4.  按一下 [建立]。  
  
5.  在 **[選擇資料集]** 頁面上，按一下 **[建立資料集]**。  
  
6.  按 [下一步] 。  
  
7.  在 **[選擇與資料來源的連接]** 頁面上，選取類型為 **[SQL Server]** 的資料來源。 請從清單中選取資料來源，或者瀏覽到報表伺服器再進行選取。  
  
8.  按 [下一步] 。  
  
9. 在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]**。  
  
10. 將下列查詢貼入查詢窗格中：  
  
    ```  
    ;WITH CTE (StoreID, Subcategory, Quantity)   
    AS (  
    SELECT 200 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 2002 AS Quantity  
    UNION SELECT  200 AS StoreID, 'Camcorders' AS Subcategory, 1954 AS Quantity  
    UNION SELECT  200 AS StoreID, 'Accessories' AS Subcategory, 1895 AS Quantity  
    UNION SELECT  199 AS StoreID, 'Digital Cameras' AS Subcategory, 1849 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 1579 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Camcorders' AS Subcategory, 1561 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Digital Cameras' AS Subcategory, 1553 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Accessories' AS Subcategory, 1534 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Accessories' AS Subcategory, 1755 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Camcorders' AS Subcategory, 1631 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 1772 AS Quantity)  
    SELECT StoreID, Subcategory, Quantity  
    FROM CTE  
    ```  
  
     此查詢會將數個 [!INCLUDE[tsql](../includes/tsql-md.md)] SELECT 陳述式的結果結合在一個通用資料表運算式內，來指定以 Contoso 範例資料庫中簡化之資料為基礎的值。 Contoso 銷售資料表示客戶商品的全球銷售資料。 本教學課程會使用相機的銷售資料。 其中的子類別有數位相機、數位單眼反光式 (SLR) 相機、攝錄影機與相關配件。  
  
     查詢所指定的資料行名稱包含商店識別碼、銷售項目類別，以及三個商店之銷售訂單中所訂購的數量。 在這個查詢中，商店名稱並不屬於結果集的內容。 稍後在本教學課程中，您會利用個別資料集查詢對應於商店識別碼的商店名稱。  
  
     此查詢並不包含查詢參數。 您稍後將在本教學課程中加入參數。  
  
11. 在 [查詢設計工具] 工具列上，按一下 [**執行**] (**！**) 。 結果集會顯示 11 個資料列，這些資料列會顯示四間商店中每個子類別所銷售的項目數量，並包含下列資料行：StoreID、Subcategory、Quantity。  
  
12. 按 [下一步] 。  
  
##  <a name="2-organize-data-choose-layout-and-style-from-the-table-or-matrix-wizard"></a><a name="CompleteWizard"></a>2. 從資料表或矩陣 Wizard 組織資料、選擇配置和樣式  
 使用精靈提供起始設計來顯示資料。 精靈中的預覽窗格可協助您在完成資料表或矩陣設計之前，先視覺化群組資料的結果。  
  
#### <a name="to-organize-data-into-groups"></a>若要將資料組織為群組  
  
1.  在 [排列欄位]**** 頁面上，將 [Subcategory] 拖曳至 [資料列群組]****。  
  
2.  將 [StoreID] 拖曳至 [資料行群組]****。  
  
3.  將 [Quantity] 拖曳至 [值]****。  
  
     現在，您已經按照子類別的分組，以資料列組織銷售量的值。 每一間商店都會有一個資料行。  
  
4.  按 [下一步] 。  
  
5.  在 **[選擇配置]** 頁面的 **[選項]** 下方，確定已經選取 **[顯示小計和總計]** 。  
  
     當您執行報表時，最後一個資料行將會顯示所有商店之每個子類別的總數量，而最後一個資料列則會顯示每家商店之所有子類別的總數量。  
  
6.  按 [下一步] 。  
  
7.  在 [**選擇樣式**] 頁面的 [樣式] 窗格中，選取樣式。  
  
8.  按一下 [完成] 。  
  
     矩陣會加入至設計介面。 此矩陣會顯示 3 個資料行和 3 個資料列。 第一個資料列的資料格內容為 Subcategory、StoreID 和 Total。 第二個資料列的資料格內容包含多個運算式，分別表示子類別、每家商店所售出的項目數量以及所有商店之每個子類別的數量總計。 最後一個資料列的資料格顯示每家商店的銷售總額。  
  
9. 按一下矩陣內部，將滑鼠停留在第一個資料行的邊緣，抓取控點並且擴展資料行寬度。  
  
10. 按一下 **[執行]** 預覽報表。  
  
 報表就會在報表伺服器上執行，並且顯示標題以及進行報表處理的時間。  
  
 在這個案例中，資料行標題顯示的商店識別碼而非商店名稱。 稍後，您會加入運算式，在包含商店識別碼/商店名稱組的資料集中，查詢商店名稱。  
  
##  <a name="3-add-a-query-parameter-to-create-a-report-parameter"></a><a name="Query"></a>3. 加入查詢參數來建立報表參數  
 當您將查詢參數加入至查詢時，報表產生器會自動建立一個單一值報表參數，其中包含名稱、提示與資料類型的預設屬性。  
  
#### <a name="to-add-a-query-parameter"></a>若要加入查詢參數  
  
1.  切換至 [設計] 檢視。  
  
2.  在 [報表資料] 窗格中，展開 [資料集]**** 資料夾，並以滑鼠右鍵按一下 **DataSet1**，然後按一下 [查詢]****。  
  
3.  新增下列 [!INCLUDE[tsql](../includes/tsql-md.md)] `WHERE` 子句做為查詢中的最後一行：  
  
    ```  
    WHERE StoreID = (@StoreID)  
    ```  
  
     `WHERE`子句會將抓取的資料限制為查詢參數所指定的存放區識別碼 *@StoreID* 。  
  
4.  在 [查詢設計工具] 工具列上，按一下 [**執行**] (**！**) 。 **定義查詢參數**] 對話方塊隨即開啟，並且提示您輸入查詢參數的值*@StoreID*。  
  
5.  在 **[參數值]** 中，輸入 **200**。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     結果集會針對商店識別碼 **200**顯示 Accessories、Camcorders 與 Digital SLR Cameras 售出的數量。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  在 [報表資料] 窗格中，展開 **[參數]** 資料夾。  
  
 請注意，現在有一個名為的報表參數 *@StoreID* 。 根據預設，參數的資料類型為 **[文字]**。 由於商店識別碼是一個整數，所以在下一個步驟中，您會將資料類型變更為 Integer。  
  
##  <a name="4-change-default-data-type-and-other-properties-for-a-report-parameter"></a><a name="ChangeDefaultProperties"></a>4. 變更報表參數的預設資料類型和其他屬性  
 建立報表參數之後，您可以調整屬性的預設值。  
  
#### <a name="to-change-the-default-data-type-for-a-report-parameter"></a>若要變更報表參數的預設資料類型  
  
1.  在 [報表資料] 窗格的 [**參數**] 節點下，以滑鼠右鍵按一下 *@StoreID* ，然後按一下 [**參數屬性**]。  
  
2.  在 [提示] 中輸入 **商店識別碼？** 。當您執行報表時，此文字會出現在報表檢視器工具列上。  
  
3.  在 **[資料類型]** 的下拉式清單中，選取 **[整數]**。  
  
4.  接受對話方塊中其餘的預設值。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  預覽報表。 報表檢視器會顯示的提示 *@StoreID* 。  
  
7.  在報表檢視器工具列上，就在 Store ID 旁，輸入 **200**，然後按一下 **[檢視報表]**。  
  
##  <a name="4a-add-a-dataset-to-provide-available-values-and-display-names"></a><a name="AddDataset"></a>4a. 加入資料集來提供可用值與顯示名稱  
 為了確保使用者只會輸入有效的參數值，您可以建立列出多個值的下拉式清單，供使用者選擇。 這些值可以取自資料集或是根據您另外指定的清單。 可用的值必須透過資料集提供，且該資料集具有不含參數參考的查詢。  
  
#### <a name="to-create-a-dataset-for-valid-values-for-a-parameter"></a>建立資料集以提供有效的參數值  
  
1.  切換至 [設計] 檢視。  
  
2.  在 [報表資料] 窗格中，以滑鼠右鍵按一下 [資料集]**** 資料夾，然後按一下 [加入資料集]****。  
  
3.  在 **[名稱]** 中輸入 **Stores**。  
  
4.  選取 **[在報表中使用內嵌資料集]** 選項。  
  
5.  在 **[資料來源]** 中，從下拉式清單選擇您於第一個步驟中建立的資料集。  
  
6.  在 **[查詢類型]** 中，確認已選取 **[文字]** 。  
  
7.  在 **[查詢]** 中，貼上下列文字：  
  
    ```  
    SELECT 200 AS StoreID, 'Contoso Catalog Store' as StoreName  
    UNION SELECT 199 AS StoreID, 'Contoso North America Online Store' as StoreName  
    UNION SELECT 307 AS StoreID, 'Contoso Asia Online Store' as StoreName  
    UNION SELECT 306 AS StoreID, 'Contoso Europe Online Store' as StoreName  
    ```  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     [報表資料] 窗格會在 **Stores** 資料集節點下顯示 StoreID 和 StoreName 欄位。  
  
##  <a name="4b-specify-available-values-to-create-a-drop-down-list-of-values"></a><a name="AvailableValues"></a>4b. 指定可以用於建立多個值之下拉式清單的值  
 建立資料集來提供可用的值之後，您必須變更報表屬性，以指定要用於填入 ReportViewer 工具列中有效下拉式清單值的資料集與欄位。  
  
#### <a name="to-provide-available-values-for-a-parameter-from-a-dataset"></a>若要從資料集提供可用的參數值  
  
1.  在 [報表資料] 窗格中，以滑鼠右鍵按一下參數 *@StoreID* ，然後按一下 [**參數屬性**]。  
  
2.  按一下 **[可用的值]**，然後按一下 **[從查詢取得值]**。  
  
3.  在 [資料集]**** 的下拉式清單中，按一下 [Stores]****。  
  
4.  在 [值欄位]**** 的下拉式清單中，按一下 [StoreID]。  
  
5.  從 [標籤欄位]**** 的下拉式清單中，按一下 StoreName。 標籤欄位會指定值的顯示名稱。  
  
6.  按一下 [一般]****。  
  
7.  在 [提示] 中輸入 **商店名稱？**。  
  
     使用現在會從商店名稱的清單中選取，而非從商店識別碼的清單中選取。 請注意，參數資料類型仍為 **[整數]** ，因為參數是根據商店識別項而不是商店名稱。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 預覽報表。  
  
     在報表檢視器工具列中，參數文字方塊現在是顯示的下拉式清單 **\<Select a Value>** 。  
  
10. 從下拉式清單中選取 Contoso Catalog Store，然後按一下 **[檢視報表]**。  
  
 報表會針對商店識別碼 **200**顯示 Accessories、Camcorders 與 Digital SLR Cameras 售出的數量。  
  
##  <a name="4c-specify-default-values-so-the-report-runs-automatically"></a><a name="DefaultValues"></a>4c. 指定預設值讓報表能夠自動執行  
 您可以指定每一個參數的預設值，讓報表能夠自動執行。  
  
#### <a name="to-specify-a-default-value-from-a-dataset"></a>若要從資料集指定預設值  
  
1.  切換至 [設計] 檢視。  
  
2.  在 [報表資料] 窗格中，以滑鼠右鍵按一下 [] *@StoreID* ，然後按一下 [**參數屬性**]。  
  
3.  按一下 **[預設值]**，然後按一下 **[從查詢取得值]**。  
  
4.  在 [資料集]**** 的下拉式清單中，按一下 [Stores]****。  
  
5.  在 [值欄位]**** 的下拉式清單中，按一下 [StoreID]。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  預覽報表。  
  
 若是 *@StoreID* ，報表檢視器會顯示值 "Contoso 北美洲 Online Store"。 這是來自資料集 **Stores**中結果集的第一個值。 報表會針對商店識別碼 **199**顯示  Digital Cameras 售出的數量。  
  
#### <a name="to-specify-a-custom-default-value"></a>若要指定自訂預設值  
  
1.  切換至 [設計] 檢視。  
  
2.  在 [報表資料] 窗格中，以滑鼠右鍵按一下 [] *@StoreID* ，然後按一下 [**參數屬性**]。  
  
3.  按一下 **[預設值]**，再按一下 **[指定值]**，然後按一下 **[加入]**。 新的值資料列隨即加入。  
  
4.  在 [ **值**] 中，輸入 **200**。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  預覽報表。  
  
 對於 *@StoreID* ，報表檢視器會顯示值 "Contoso Catalog Store"。 這是商店識別碼 **200**的顯示名稱。 報表會針對商店識別碼 **200**顯示 Accessories、Camcorders 與 Digital SLR Cameras 售出的數量。  
  
##  <a name="4d-look-up-a-value-from-a-dataset-that-has-namevalue-pairs"></a><a name="NameValue"></a>4d. 從具有名稱/值組的資料集中查閱值  
 資料集可能同時包含識別碼與對應的名稱欄位。 如果您只有識別碼，那麼可以查詢包含名稱/值組之資料集 (您先前建立) 中的對應名稱。  
  
#### <a name="to-look-up-a-value-from-a-dataset"></a>若要從資料集查詢值  
  
1.  切換至 [設計] 檢視。  
  
2.  在設計介面的矩陣中，即第一個資料列欄標題中，以滑鼠右鍵按一下 `[StoreID]`，然後按一下 [運算式]****。  
  
3.  在運算式窗格中，刪除所有文字，但是保留開頭的 `equals` (=)。  
  
4.  在 **[類別目錄]** 中，展開 **[一般函數]**，再按一下 **[其他]**。 [項目] 窗格顯示函數集。  
  
5.  在 [項目] 中，按兩下 **[查詢]**。 運算式窗格會顯示 `=Lookup(`。 [範例] 窗格會示 Lookup 語法的範例。  
  
6.  輸入下列運算式： `=Lookup(Fields!StoreID.Value,Fields!StoreID.Value,Fields!StoreName.Value,"Stores")`  
  
     Lookup 函數會接受 StoreID 值並在 "Stores" 資料集中尋找該值，然後再傳回 StoreName 值。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     [存放區] 資料行標題包含複雜運算式的顯示文字： **<\<Expr>>** 。  
  
8.  預覽報表。  
  
 每一頁頂端的文字方塊會顯示商店名稱，而非商店識別碼。  
  
##  <a name="5-display-the-selected-parameter-value-in-the-report"></a><a name="Expression"></a>5. 在報表中顯示選取的參數值  
 如果使用者對報表有任何疑問，這有助於明白先前選擇了哪些參數值。 您可以在報表中保留使用者為每一個參數所選取的值。 其中一個方法是在頁尾的文字方塊中顯示參數。  
  
#### <a name="to-display-the-selected-parameter-value-and-label-on-a-page-footer"></a>若要在頁尾中顯示選取的參數值與標籤  
  
1.  切換至 [設計] 檢視。  
  
2.  以滑鼠右鍵按一下頁尾，指向 **[插入]**，然後按一下 **[文字方塊]**。 將文字方塊拖曳到具有時間戳記的文字方塊中。 抓取文字方塊的側邊控點，然後拉長寬度。  
  
3.  從 [報表資料] 窗格中，將參數拖曳 *@StoreID* 至文字方塊。 此文字方塊便會顯示 `[@StoreID]`。  
  
4.  若要顯示參數標籤，按一下文字方塊，直到插入游標出現在現有運算式之後，輸入一個空格，然後將參數的其他複本從 [報表資料] 窗格拖曳至文字方塊。 此文字方塊便會顯示 `[@StoreID] [@StoreID]`。  
  
5.  以滑鼠右鍵按一下第一個運算式，然後按一下 **[運算式]**。 **[運算式]** 對話方塊隨即開啟。 將文字 `Value` 取代為 `Label`。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     文字便會顯示 `[@StoreID.Label] [@StoreID]`。  
  
7.  預覽報表。  
  
##  <a name="6-use-the-report-parameter-in-a-filter"></a><a name="Filter"></a>6. 在篩選中使用報表參數  
 篩選有助於控制在自外部資料來源擷取報表後，要在其中使用哪些資料。 若要協助使用者可以控制他們想要看的資料，您可以在矩陣的篩選中加入報表參數。  
  
#### <a name="to-specify-a-parameter-in-a-matrix-filter"></a>若要在矩陣篩選中指定參數  
  
1.  切換至 [設計] 檢視。  
  
2.  以滑鼠右鍵按一下矩陣上的資料行標頭控制代碼，然後按一下 **[Tablix 屬性]**。  
  
3.  按一下 **[篩選]**，然後按一下 **[加入]**。 新的篩選資料列隨即顯示。  
  
4.  在 [運算式]**** 的下拉式清單中，選取 StoreID 資料集欄位。 資料類型會顯示 **[整數]**。 當運算式值為資料集欄位時，會自動設定資料類型。  
  
5.  在 [**運算子**] 中，確認 `equals` 已選取 [ (=) ]。  
  
6.  在 **[值]** 中，輸入 `[@StoreID]`。 `[@StoreID]` 為表示 `=Parameters!StoreID.Value`的簡單運算式語法。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  預覽報表。  
  
     矩陣只會顯示 "Contoso Catalog Store" 的資料。  
  
9. 在報表檢視器工具列上，為 **[Store name?]** 選取 **[Contoso Asia Online Store]**，然後按一下 **[檢視報表]**。  
  
 矩陣會顯示對應於您所選商店的資料。  
  
##  <a name="7-change-the-report-parameter-to-accept-multiple-values"></a><a name="Multivalued"></a>7. 變更報表參數以接受多個值  
 若要將參數由單一值變更為多重值，您必須變更查詢以及所有包含參數參考的所有運算式，包含篩選條件。 多重值參數為值的陣列。 在資料集查詢中，查詢語法必須經過測試，確認值組中包含一個值。 在報表運算式中，運算式語法必須存取值的陣列，而不是單一值。  
  
#### <a name="to-change-a-parameter-from-single-to-multivalued"></a>將參數由單一值變更為多重值  
  
1.  切換至 [設計] 檢視。  
  
2.  在 [報表資料] 窗格中，以滑鼠右鍵按一下 [] *@StoreID* ，然後按一下 [**參數屬性**]。  
  
3.  選取 **[允許多個值]**。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  在 [報表資料] 窗格中，展開 [資料集]**** 資料夾，並以滑鼠右鍵按一下 **DataSet1**，然後按一下 [查詢]****。  
  
6.  在 `equals` `IN` [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢中最後一行的子句中，將 (=) 變更為 `WHERE` ：  
  
    ```  
    WHERE StoreID IN (@StoreID)  
    ```  
  
     `IN` 運算子會測試一個值，確認已包含一組值。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  以滑鼠右鍵按一下矩陣上的資料行標頭控制代碼，然後按一下 **[Tablix 屬性]**。  
  
9. 按一下 **[篩選]** 。  
  
10. 在 **[運算子]** 中，選取 **[In]**。  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. 在顯示頁尾中參數的文字方塊中，刪除所有文字。  
  
13. 以滑鼠右鍵按一下文字方塊，然後按一下 **[運算式]**。 輸入下列運算式： `=Join(Parameters!StoreID.Label, ", ")`  
  
     這個運算式會串聯使用者選取的所有商店名稱。  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
15. 在您剛剛建立之運算式前面的文字方塊上按一下，然後輸入下列：選取的參數值：  
  
16. 預覽報表。  
  
17. 按一下 [Store Name?] 旁的下拉式清單  
  
     每一個有效值會顯示在核取方塊旁。  
  
18. 按一下 **[全選]**，然後按一下 **[檢視報表]**。  
  
     報表會示所有商店中所有子類別的出售數量。  
  
19. 從下拉式清單中，按一下 [全選]**** 清除清單，並按一下 [Contoso Catalog Store] 與 [Contoso Asia Online Store]，然後按一下 [檢視報表]****。  
  
##  <a name="8-add-a-boolean-parameter-for-conditional-visibility"></a><a name="Boolean"></a>8. 加入條件式可見度的布林值參數  
  
#### <a name="to-add-a-boolean-parameter"></a>加入布林參數  
  
1.  在設計介面的 [報表資料] 窗格中，以滑鼠右鍵按一下 [參數]****，然後按一下 [加入參數]****。  
  
2.  在 **[名稱]** 中，輸入 ShowSelections  
  
3.  在 **[提示]** 中，輸入 Show selections?  
  
4.  在 **[資料類型]** 的下拉式清單中，按一下 **[布林值]**。  
  
5.  按一下 **[預設值]**。  
  
6.  按一下 **[指定值]**，然後按一下 **[加入]**。  
  
7.  在 **[值]** 中，輸入 **False**。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-set-visibility-based-on-a-boolean-parameter"></a>根據布林參數設定可見性  
  
1.  在設計介面上，以滑鼠右鍵按一下頁尾中顯示參數值的文字方塊，然後按一下 [文字方塊屬性]****。  
  
2.  按一下 **[可見性]** 。  
  
3.  選取 **[依據運算式顯示或隱藏]** 選項，然後按一下 **Fx**運算式按鈕。  
  
4.  輸入下列運算式： `=Not Parameters!ShowSelections.Value`  
  
     文字方塊 Visibility 選項會由 Hidden 屬性所控制。 套用 `Not` 運算子，如此一來，當選取該參數時，Hidden 屬性會為 False，而且會顯示文字方塊。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  預覽報表。  
  
     顯示參數選項的文字方塊不會出現。  
  
8.  在報表檢視器工具列中，按一下 [**顯示選擇**] 旁的 `True` 。  
  
9. 預覽報表。  
  
 頁尾中的文字方塊會顯示您所選取的所有商店。  
  
##  <a name="9-add-a-report-title"></a><a name="Title"></a>9. 加入報表標題  
  
#### <a name="to-add-a-report-title"></a>若要加入報表標題  
  
1.  在設計介面上，按一下 **[按一下以加入標題]**。  
  
2.  輸入「參數化產品銷售」，然後按一下文字方塊外部。  
  
##  <a name="10-save-the-report"></a><a name="Save"></a>10. 儲存報表  
  
#### <a name="to-save-the-report-on-a-report-server"></a>若要將報表儲存在報表伺服器上  
  
1.  在 **[報表產生器]** 按鈕中，按一下 **[另存新檔]**。  
  
2.  按一下 **[最近使用的網站和伺服器]**。  
  
3.  選取或輸入您有權儲存報表之報表伺服器的名稱。  
  
     **[連接到報表伺服器]** 訊息隨即顯示。 連接完成時，您就會看見報表伺服器管理員指定為預設報表位置之報表資料夾的內容。  
  
4.  在 **[名稱]** 中，將預設名稱取代為「參數化產品銷售」。  
  
5.  按一下 [檔案] 。  
  
 報表就會儲存至報表伺服器。 您所連接的報表伺服器會顯示在視窗底部的狀態列中。  
  
## <a name="next-steps"></a>後續步驟  
 以上總結如何將參數加入至報表的逐步解說。 若要深入了解參數，請參閱[報表參數 &#40;報表產生器和報表設計師&#41;](report-design/report-parameters-report-builder-and-report-designer.md)。  
  
## <a name="see-also"></a>另請參閱  
 [教學課程 &#40;報表產生器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的報表產生器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
