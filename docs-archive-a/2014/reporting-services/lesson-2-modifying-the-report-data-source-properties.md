---
title: 第 2 課：修改報表資料來源屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 05e56a58ce28ee1e1e450d3af012cbd1ffe668ca
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592527"
---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>Lesson 2: Modifying the Report Data Source Properties
  在這一課，您將使用報表管理員來選取傳遞給收件者的報表。 您將定義的資料驅動訂閱將散發 **建立基本資料表報表 &amp;#40;SSRS 教學課程&amp;#41;** 教學課程中建立的 [建立基本資料表報表 &#40;SSRS 教學課程&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)報表。 在下面的步驟中，您將修改報表用來取得資料的資料來源連接資訊。 只有使用 **預存認證** 來存取報表資料來源的報表可以透過資料驅動訂閱散發。 自動報表處理需要預存認證。

 您也會將資料集和報表修改成使用參數來依據 `[Order]` 篩選報表，讓訂閱能夠針對特定訂單和轉譯格式輸出不同的報表執行個體。

 **本主題內容：**

-   [若要修改資料來源屬性](#bkmk_modify_datasource)

-   [若要修改 AdventureWorksDataset](#bkmk_modify_dataset)

-   [若要加入報表參數並重新發行報表](#bkmk_add_reportparameter)

-   [若要重新部署報表](#bkmk_redeploy)

##  <a name="to-modify-the-data-source-properties"></a><a name="bkmk_modify_datasource"></a>若要修改資料來源屬性

1.  以系統管理員許可權啟動[報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md) ，例如，以滑鼠右鍵按一下 Internet Explorer 的圖示，然後按一下 [以**系統管理員身分執行**]。

2.  瀏覽到包含 **Sales Orders** 報表的資料夾，然後在報表的內容功能表中，按一下 **[管理]**。

     ![開啟報表內容功能表並選取管理](../../2014/tutorials/media/ssrs-tutorial-datadriven-manage-report.gif "開啟報表內容功能表並選取管理")

3.  按一下 [資料來源]**** 索引標籤。

4.  針對 **[連接類型]**，選取 **[Microsoft SQL Server]**。

5.  自訂資料來源連接字串將如下所示，而且它會假設範例資料庫位於本機資料庫伺服器上：

    ```
    Data source=localhost; initial catalog=AdventureWorks2012
    ```

6.  按一下 **[安全地儲存在報表伺服器中的認證]**。

7.  輸入您的使用者名稱 (使用 *domain\user*格式) 和密碼。 如果您沒有存取 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫的權限，請指定有這項權限的登入。

8.  按一下 **[連接到資料來源時做為 windows 認證**]，然後按一下 **[確定]**。 如果您並未使用網域帳戶 (例如，您是使用[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]登入)，請勿點選這個核取方塊。

9. 按一下 [測試連接]****，確認您能夠連線到資料來源。

10. 按一下 [套用]。

11. 檢視報表以確認報表是以您指定的認證來執行。 若要查看報表，請按一下 [**視圖**] 索引標籤。請注意，一旦報表開啟之後，您必須選取員工名稱，然後按一下 [**查看報表**] 按鈕來查看報表。

##  <a name="to-modify-the-adventureworksdataset"></a><a name="bkmk_modify_dataset"></a>修改 AdventureWorksDataset

1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中開啟 Sales Orders 報表。

2.  以滑鼠右鍵按一下 `AdventureWorksDataset` 資料集，然後按一下 [資料集屬性]  。

3.  在 `WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)` 陳述式前面加入 `Group By` 陳述式。 完整的查詢語法如下：

    ```
    SELECT soh.OrderDate AS Date, soh.SalesOrderNumber AS [Order], pps.Name AS Subcat, pp.Name AS Product, SUM(sd.OrderQty) AS Qty, SUM(sd.LineTotal)  AS LineTotal
    FROM Sales.SalesPerson AS sp INNER JOIN
      Sales.SalesOrderHeader AS soh ON sp.BusinessEntityID = soh.SalesPersonID INNER JOIN
       Sales.SalesOrderDetail AS sd ON sd.SalesOrderID = soh.SalesOrderID INNER JOIN
       Production.Product AS pp ON sd.ProductID = pp.ProductID
    INNER JOIN
       Production.ProductSubcategory AS pps ON pp.ProductSubcategoryID = pps.ProductSubcategoryID 
    INNER JOIN
        Production.ProductCategory AS ppc ON ppc.ProductCategoryID = pps.ProductCategoryID

    WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)

    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name, soh.SalesPersonID
    HAVING (ppc.Name = 'Clothing')
    ```

4.  按一下 [檔案] &gt; [新增] &gt; [專案]

##  <a name="to-add-a-report-parameter-and-republish-the-report"></a><a name="bkmk_add_reportparameter"></a>若要加入報表參數並重新發行報表

1.  在 [**報表資料**] 窗格中，按一下 [**新增**]，然後按一下 [**參數 ...** ]

2.  在 **[名稱]** 中，輸入 `OrderNumber`。

3.  在 **[提示]** 中，輸入 `OrderNumber`。

4.  選取 [允許空白值 ("")]****。

5.  選取 [允許 Null 值]****。

6.  按一下 [確定]  。 參數將會加入至 [**報表資料] 窗格**，而且看起來會像下圖：

     ![新的參數已加入至報表資料窗格](../../2014/tutorials/media/ssrs-tutorial-datadriven-parameter.gif "新的參數已加入至報表資料窗格")

7.  按一下 [**預覽**] 索引標籤以執行報表。請注意位於報表頂端的參數輸入方塊。 您可以：

    -   按一下 [檢視報表] 查看完整報表，而不使用參數。

    -   取消選取 Null 選項並輸入訂單號碼 (例如 so71949)，即可單獨檢視報表中的單一訂單。

         ![具有可見參數區域的報表檢視器](../../2014/tutorials/media/ssrs-tutorial-datadriven-reportviewer-parameter.gif "具有可見參數區域的報表檢視器")

8.  請重新部署報表，讓下一課的訂閱組態能夠運用您在這一課所做的變更。 如需用於資料表教學課程的專案屬性詳細資訊，請參閱[第 6 課：新增群組和總計 &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md) 的＜將報表發行至報表伺服器 (選擇性)＞一節。

##  <a name="to-re-deploy-the-report"></a><a name="bkmk_redeploy"></a>重新部署報表

1.  請重新部署報表，讓下一課的訂閱組態能夠運用您在這一課所做的變更。 如需用於資料表教學課程的專案屬性詳細資訊，請參閱[第 6 課：新增群組和總計 &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md) 的＜將報表發行至報表伺服器 (選擇性)＞一節。

2.  在工具列上，按一下 **[建置]** ，然後按一下 **[部署教學課程]**。

## <a name="next-steps"></a>後續步驟
 您已順利設定報表來利用預存認證取得資料。 之後，您可以使用報表管理員中的 [資料驅動訂閱] 頁面來指定訂閱。 請參閱 [第 3 課：定義資料驅動訂閱](../reporting-services/lesson-3-defining-a-data-driven-subscription.md)。

## <a name="see-also"></a>另請參閱
 [管理報表資料來源](report-data/manage-report-data-sources.md)[指定報表資料來源的認證和連接資訊](report-data/specify-credential-and-connection-information-for-report-data-sources.md)[建立資料驅動訂閱 &#40;Ssrs 教學課程&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md) [建立基本資料表報表 &#40;ssrs 教學課程&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)


