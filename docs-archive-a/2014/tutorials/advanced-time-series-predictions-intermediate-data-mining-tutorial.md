---
title: " (元資料採礦教學課程的先進時間序列預測) |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b614ebdb-07ca-44af-a0ff-893364bd4b71
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 70ebf856ba0782cbf44969aba30602818015582a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704501"
---
# <a name="advanced-time-series-predictions-intermediate-data-mining-tutorial"></a>進階時間序列預測 (中繼資料採礦教學課程)
  您已經從預測模型的瀏覽得知，雖然大部分地區的銷售都遵循類似的模式，但是某些地區和某些模型 (如太平洋地區的 M200 模型) 則呈現了非常不同的趨勢。 這不令您吃驚，因為您知道地區之間的差異是很常見的，而且可能是因為許多因素所造成，其中包括促銷活動、不正確的報表或地理政治事件。  
  
 但是您的使用者要求全球適用的模型。 因此，為了讓個別因素對預測的影響降至最低，您決定建立一個根據全球銷售彙總量值的模型。 然後您可以使用這個模型，針對各地區做預測。  
  
 在這項工作中，您將建立執行進階預測工作所需的所有資料來源。 您將建立兩個做為預測查詢輸入的資料來源檢視和一個用於建立新模型的資料來源檢視。  
  
 **步驟**  
  
1.  [準備擴充銷售資料 (用於預測)](#bkmk_newExtendData)  
  
2.  [準備彙總資料 (用於建立模型)](#bkmk_newReplaceData)  
  
3.  [準備數列資料 (用於交叉預測)](#bkmk_CrossData2)  
  
4.  [使用 EXTEND 做預測](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
5.  [建立交叉預測模型](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
6.  [使用 REPLACE 做預測](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
7.  [檢閱新預測](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
##  <a name="creating-the-new-extended-sales-data"></a><a name="bkmk_newExtendData"></a>建立新的擴充銷售資料  
 您需要取得最新的銷售數字，以更新銷售資料。 特別值得注意的是來自太平洋地區的最新資料，這裡剛發起區域性銷售促銷，讓新店面及其商品吸引眾人目光。  
  
 在此案例中，我們假設已從 Excel 活頁簿匯入資料，其中只包含三個月的新資料供幾個區域使用。 您將使用 Transact-sql 腳本來建立資料的資料表，然後定義要用於預測的資料來源 view。  
  
#### <a name="create-the-table-with-new-sales-data"></a>使用新銷售資料建立資料表  
  
1.  在 Transact-SQL 查詢視窗中，執行下列陳述式，將銷售資料加入至 AdventureWorksDW 資料庫 (或其他任何資料庫)。  
  
    ```  
    USE [database name];  
    GO  
    IF OBJECT_ID ([dbo].[NewSalesData]) IS NOT NULL   
        DROP TABLE [dbo].[NewSalesData];  
    GO  
    CREATE TABLE [dbo].[NewSalesData]([Series] [nvarchar](255) NULL,  
    [NewDate] [datetime] NULL,  
    [NewQty] [float] NULL,  
    [NewAmount] [money] NULL) ON [PRIMARY]  
  
    GO  
    ```  
  
2.  使用下列指令碼插入新值。  
  
    ```  
    INSERT INTO [NewSalesData]  
    (Series,NewDate,NewQty,NewAmount)  
    VALUES('T1000 Pacific', '7/25/08', 55, '$130,170.22'),  
    ('T1000 Pacific', '8/25/08', 50, '$114,435.36 '),  
    ('T1000 Pacific', '9/25/08', 50, '$117,296.24 '),  
    ('T1000 Europe', '7/25/08', 37, '$88,210.00 '),  
    ('T1000 Europe', '8/25/08', 41, '$97,746.00 '),  
    ('T1000 Europe', '9/25/08', 37, '$88,210.00 '),  
    ('T1000 North America', '7/25/08', 69, '$164,500.00 '),  
    ('T1000 North America', '8/25/08', 66, '$157,348.00 '),  
    ('T1000 North America', '9/25/08', 58, '$138,276.00 '),  
    ('M200 Pacific', '7/25/08', 65, '$149,824.35'),  
    ('M200 Pacific', '8/25/08', 54,  '$124,619.46'),  
    ('M200 Pacific', '9/25/08', 61, '$141,143.39'),  
    ('M200 Europe', '7/25/08', 75, '$173,026.00'),  
    ('M200 Europe', '8/25/08', 76, '$175,212.00'),  
    ('M200 Europe', '9/25/08', 84, '$193,731.00'),  
    ('M200 North America', '7/25/08', 94, '$216,916.00'),  
    ('M200 North America', '8/25/08', 94, '$216,891.00'),  
    ('M200 North America', '9/25/08', 91,'$209,943.00');  
    ```  
  
    > [!WARNING]  
    >  引號用於貨幣值，以避免通用分隔符號和貨幣符號發生問題。 您也可以使用下列格式傳入貨幣值：`130170.22`  
    >   
    >  請注意，範例資料庫中使用的日期已在此版本中變更。 如果您使用的是舊版的 AdventureWorks，可能需要針對插入的日期進行相應的調整。  
  
###  <a name="create-a-data-source-view-using-the-new-sales-data"></a><a name="bkmk_newReplaceData"></a>使用新的銷售資料來建立資料來源視圖  
  
1.  在**方案總管**中，以滑鼠右鍵按一下 [**資料來源視圖**]，然後選取 [**新增資料來源視圖**]。  
  
2.  在資料來源檢視精靈中，進行下列選擇：  
  
     **資料來源**：[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]  
  
     **選取資料表和視圖**：選取您剛才建立的資料表 NewSalesData。  
  
3.  按一下 [完成] 。  
  
4.  在 [資料來源] 視圖設計介面中，以滑鼠右鍵按一下 [NewSalesData]，然後選取 [**流覽資料**] 以驗證資料。  
  
> [!WARNING]  
>  此資料僅供預測，資料不完整沒有關係。  
  
##  <a name="creating-the-data-for-the-cross-prediction-model"></a><a name="bkmk_CrossData2"></a>建立交叉預測模型的資料  
 原始預測模型中所用的資料已經依 vTimeSeries 檢視稍微分組，數款自行車已摺疊為較少的類別目錄數目，各國結果已合併為地區。 若要建立可用於全球預測的模型，您將直接在資料來源檢視設計工具中建立一些其他簡單彙總。 新的資料來源檢視只包含所有地區所有產品的銷售總和與平均值。  
  
 在建立用於模型的資料來源之後，您必須建立一個用於預測的新資料來源檢視。 例如，如果您要使用新的全球模型來預測歐洲銷售，必須只饋送歐洲地區的資料。 因此，您將設定可篩選原始資料的新資料來源檢視，並針對各組預測查詢來變更篩選條件。  
  
#### <a name="to-create-the-model-data-using-a-custom-data-source-view"></a>若要使用自訂資料來源檢視建立模型資料  
  
1.  在**方案總管**中，以滑鼠右鍵按一下 [**資料來源視圖**]，然後選取 [**新增資料來源視圖**]。  
  
2.  在精靈的歡迎頁面中，按 **[下一步]**。  
  
3.  在 **[選取資料來源]** 頁面上，選取 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]，然後按 **[下一步]**。  
  
4.  在頁面中，**選取 [資料表和視圖]**，不要加入任何資料表，只要按 **[下一步]** 即可。  
  
5.  在 [**完成嚮導]** 頁面上，輸入名稱 `AllRegions` ，然後按一下 **[完成**]。  
  
6.  接下來，以滑鼠右鍵按一下空白的資料來源視圖設計介面，然後選取 [新增] [**指名的查詢**]。  
  
7.  在 [**建立指名的查詢**] 對話方塊中，針對 [**名稱**] 輸入 `AllRegions` ，並針對 [**描述**] 輸入**所有模型和地區的銷售總和和平均值**。  
  
8.  在 SQL 文字窗格中，輸入下列陳述式，然後按一下 [確定]：  
  
    ```  
    SELECT ReportingDate,   
    SUM([Quantity]) as SumQty, AVG([Quantity]) as AvgQty,  
    SUM([Amount]) AS SumAmt, AVG([Amount]) AS AvgAmt,  
    'All Regions' as [Region]  
    FROM dbo.vTimeSeries   
    GROUP BY ReportingDate  
    ```  
  
9. 以滑鼠右鍵按一下 `AllRegions` 資料表，然後選取 [**流覽資料**]。  
  
###  <a name="to-create-the-series-data-for-cross-prediction"></a><a name="bkmk_CrossData"></a>若要建立交叉預測的數列資料  
  
1.  在**方案總管**中，以滑鼠右鍵按一下 [**資料來源視圖**]，然後選取 [**新增資料來源視圖**]。  
  
2.  在資料來源檢視精靈中，進行下列選擇：  
  
     **資料來源**：[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]  
  
     **選取資料表和檢視表**：不選取任何資料表  
  
     **名稱**：`T1000 Pacific Region`  
  
3.  按一下 [完成] 。  
  
4.  以滑鼠右鍵按一下**T1000 太平洋 Region. dsv**的空白設計介面，然後選取 [**新增**] [指名的查詢]。  
  
     **[建立具名查詢]** 對話方塊隨即出現。 重新輸入名稱，然後加入以下的描述：  
  
     **名稱**：`T1000 Pacific Region`  
  
     **描述**： ** `vTimeSeries` 依區域和模型篩選**  
  
5.  在文字窗格中，輸入下列查詢，然後按一下 [確定]：  
  
    ```  
    SELECT ReportingDate, ModelRegion, Quantity, Amount  
    FROM dbo.vTimeSeries  
    WHERE (ModelRegion = N'T1000 Pacific')  
    ```  
  
    > [!NOTE]  
    >  因為您需要為各數列分別建立預測，您可能會想要複製查詢文字，並將它儲存到文字檔中，以便重複將它用於其他資料數列。  
  
6.  在 [資料來源] 視圖設計介面中，以滑鼠右鍵按一下 [T1000]，然後選取 [**流覽資料**]，確認資料已正確篩選。  
  
     在建立交叉預測查詢時，您將會使用此資料做為模型的輸入。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [使用更新的資料 &#40;中繼資料採礦教學課程的時間序列預測&#41;](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 時間序列演算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Microsoft 時間序列演算法技術參考](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [多維度模型中的資料來源檢視](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)  
  
  
