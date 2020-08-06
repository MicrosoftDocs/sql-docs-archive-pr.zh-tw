---
title: 第2課：加入資料 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 13c3a8cc-b1db-4aba-ad9b-038b7971be8d
author: minewiskan
ms.author: owend
ms.openlocfilehash: c844ea6558949407ca9b8206601ff7fe802ec399
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593666"
---
# <a name="lesson-2-add-data"></a>第 2 課：加入資料
  在這一課，您將會使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的 [資料表匯入精靈] 連接 AdventureWorksDW SQL Database、選取資料、預覽及篩選資料，然後將資料匯入您的模型工作空間。  
  
 使用 [資料表匯入精靈] 可讓您從各種關聯式來源匯入資料：Access、SQL、Oracle、Sybase、Informix、DB2、Teradata 以及其他來源。 從每一個關聯式來源匯入資料的步驟非常類似以下所述內容。 此外，您也可以使用預存程序選取資料。  
  
 若要深入了解匯入資料和可做為匯入來源的各種不同類型資料來源，請參閱[資料來源 &#40;SSAS 表格式&#41;](data-sources-ssas-tabular.md)。  
  
 這堂課的預估完成時間：**20 分鐘**  
  
## <a name="prerequisites"></a>Prerequisites  
 本主題是表格式模型教學課程的一部分，請依序完成。 在執行這堂課中的工作之前，您必須已完成上一堂課：[第1課：建立新的表格式模型專案](lesson-1-create-a-new-tabular-model-project.md)。  
  
## <a name="create-a-connection"></a>建立連接  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2012-database"></a>若要建立與 AdventureWorksDW2012 資料庫的連接  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，按一下 [模型]**** 功能表，然後按一下 [從資料來源匯入]****。  
  
     這樣會啟動 [資料表匯入精靈]，引導您設定與資料來源的連接。 如果 [從資料來源匯入]**** 呈現灰色，請按兩下**方案總管**中的 **Model.bim**，在設計師中開啟模型。  
  
2.  在 [資料表匯入精靈]**** 的 [關聯式資料庫]**** 底下，按一下 [Microsoft SQL Server]****，然後按一下 [下一步]****。  
  
3.  在 [**連接到 Microsoft SQL Server 資料庫]** 頁面的 [**易記連接名稱**] 中，輸入 `Adventure Works DB from SQL` 。  
  
4.  在 [伺服器名稱]**** 中，輸入您安裝 AdventureWorksDW 資料庫的伺服器名稱。  
  
5.  在 [資料庫名稱]**** 欄位中，按一下向下箭頭並選取 **AdventureWorksDW**，然後按一下 [下一步]****。  
  
6.  在 [模擬資訊]**** 頁面中，您必須指定 Analysis Services 在匯入和處理資料時，用來連接資料來源的認證。 確認已選取 [特定的 Windows 使用者名稱和密碼]****，然後在 [使用者名稱]**** 和 [密碼]**** 中輸入您的 Windows 登入認證，再按一下 [下一步]****。  
  
    > [!NOTE]  
    >  使用 Windows 使用者帳戶和密碼是連線至資料來源最安全的方法。 如需詳細資訊，請參閱[模擬 &#40;SSAS 表格式&#41;](tabular-models/impersonation-ssas-tabular.md)。  
  
7.  在 [選擇如何匯入資料]**** 頁面中，確認已選取 [從資料表和檢視表清單來選取要匯入的資料]****。 若要從資料表和檢視表的清單中選取，請按一下 [下一步]**** 顯示來源資料庫內所有來源資料表的清單。  
  
8.  在 [選取資料表和檢視表]**** 頁面中，選取下列資料表的核取方塊：**DimCustomer**、**DimDate**、**DimGeography**、**DimProduct**、**DimProductCategory**、**DimProductSubcategory** 和 **FactInternetSales**。  
  
9. 模型中的資料表最好使用較容易理解的名稱。 按一下 [易記名稱]**** 資料行中 **DimCustomer** 的資料格。 從 DimCustomer 中移除 "Dim"，以重新命名資料表。  
  
10. 重新命名其他資料表：  
  
    |來源名稱|易記名稱|  
    |-----------------|-------------------|  
    |DimDate|Date|  
    |DimGeography|[地理位置]|  
    |DimProduct|產品|  
    |DimProductCategory|產品類別|  
    |DimProductSubcategory|產品子類別目錄|  
    |FactInternetSales|Internet Sales|  
  
     **請不要**按一下 [完成]****。  
  
 現在，您已經連接到資料庫、選取了要匯入的資料表，並且已使用易記的資料表名稱，即可前往下一節[在匯入之前篩選資料表資料](#FilterData)。  
  
##  <a name="filter-the-table-data"></a><a name="FilterData"></a>篩選資料表資料  
 您要從資料庫匯入的 DimCustomer 資料表包含來自原始 SQL Server Adventure Works 資料庫的資料子集。 您將會從 DimCustomer 資料表中篩選出一些不必要的資料行。 如果可能的話，您會想要篩選掉不會使用的資料，以便節省模型使用的記憶體中空間。  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>若要在匯入之前篩選資料表資料  
  
1.  選取 **Customer** 資料表的資料列，然後按一下 [預覽和篩選]****。 [預覽選取的資料表]**** 視窗隨即開啟，其中會顯示 DimCustomer 來源資料表內的所有資料行。  
  
2.  清除下列資料行上方的核取方塊：  
  
    |客戶|  
    |--------------|  
    |**SpanishEducation**|  
    |**FrenchEducation**|  
    |**SpanishOccupation**|  
    |**FrenchOccupation**|  
  
     因為這些資料行的值與網際網路銷售分析無關，所以不需要匯入這些資料行。 消除不必要的資料行列將使您的模型變小。  
  
3.  確認已檢查過所有其他資料行，然後按一下 [確定]****。  
  
     請注意，[套用的**篩選**] 字樣現在會顯示在 [ **Customer** ] 資料列的 [**篩選詳細資料] 資料**行;如果您按一下該連結，您會看到剛才套用之篩選的文字描述。  
  
4.  藉由清除每個資料表中下列資料行的核取方塊，篩選其餘資料表：  
  
    |Date|  
    |----------|  
    |**DateKey**|  
    |**SpanishDayNameOfWeek**|  
    |**FrenchDayNameOfWeek**|  
    |**SpanishMonthName**|  
    |**FrenchMonthName**|  
  
    |[地理位置]|  
    |---------------|  
    |**SpanishCountryRegionName**|  
    |**FrenchCountryRegionName**|  
    |**IpAddressLocator**|  
  
    |產品|  
    |-------------|  
    |**SpanishProductName**|  
    |**FrenchProductName**|  
    |**FrenchDescription**|  
    |**ChineseDescription**|  
    |**ArabicDescription**|  
    |**HebrewDescription**|  
    |**ThaiDescription**|  
    |**GermanDescription**|  
    |**JapaneseDescription**|  
    |**TurkishDescription**|  
  
    |產品類別|  
    |----------------------|  
    |**SpanishProductCategoryName**|  
    |**FrenchProductCategoryName**|  
  
    |產品子類別目錄|  
    |-------------------------|  
    |**SpanishProductSubcategoryName**|  
    |**FrenchProductSubcategoryName**|  
  
    |Internet Sales|  
    |--------------------|  
    |**OrderDateKey**|  
    |**DueDateKey**|  
    |**ShipDateKey**|  
  
 現在您已預覽並篩選掉不必要的資料，那麼就可以開始匯入資料。 請前往下一節 **匯入選取的資料表和資料行資料**。  
  
##  <a name="import-the-selected-tables-and-column-data"></a><a name="Import"></a>匯入選取的資料表和資料行資料  
 現在您可以匯入選取的資料。 此精靈會匯入資料表資料，包含資料表之間的任何關聯性。 新的資料表和資料行會在模型中使用您指定的易記名稱建立，而且不會匯入您篩選掉的資料。  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>匯入選取的資料表和資料行資料  
  
1.  檢閱您的選擇。 如果確認無誤，請按一下 [完成]****。  
  
     當匯入資料時，精靈會顯示已經提取的資料列數。 所有資料都匯入之後，就會顯示一則訊息，指出此作業已順利完成。  
  
    > [!TIP]  
    >  若要查看在匯入的資料表之間自動建立的關聯性，請在 [資料準備]**** 資料列上按一下 [詳細資料]****。  
  
2.  按一下 **關閉**。  
  
     精靈隨即關閉，而且您可以看見模型設計師。 每一個資料表都已經加入成為模型設計師中的新索引標籤。  
  
## <a name="save-the-model-project"></a>儲存模型專案  
 請您務必經常儲存模型專案。  
  
#### <a name="to-save-the-model-project"></a>儲存模型專案  
  
-   在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的 [檔案]**** 功能表上，按一下 [全部儲存]****。  
  
## <a name="next-step"></a>後續步驟  
 若要繼續進行本教學課程，請前往下一課： [第 3 課：重新命名資料行](rename-columns.md)。  
  
  
