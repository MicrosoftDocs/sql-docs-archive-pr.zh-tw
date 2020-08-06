---
title: 報表參數 (報表產生器和報表設計師) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.subreportproperties.parameters.f1
- sql12.rtp.rptdesigner.reportparameters.general.f1
- "10091"
- "10073"
- "10070"
- sql12.rtp.rptdesigner.reportparameters.advanced.f1
ms.assetid: 58b96555-d876-4f61-bff8-db5764b9f5f9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 15d8898a18e143c7954766b5a0bf9e7bb6d068eb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595685"
---
# <a name="report-parameters-report-builder-and-report-designer"></a>報表參數 (報表產生器和報表設計師)
  本主題說明 SSRS 報表參數的一般用法、您可以設定的屬性，以及有關參數的詳細資訊。 報表參數可讓您控制報表資料、將相關的報表連接在一起，以及變更報表呈現方式。  
  
[!INCLUDE[applies](../../includes/applies-md.md)]SharePoint 模式和原生模式
  
 如需如何將參數加入報表中的相關示範，請參閱 [教學課程：將參數加入至報表中 (SSRS)](https://technet.microsoft.com/library/aa337432\(v=SQL.105\).aspx)  

  
##  <a name="common-uses-for-parameters"></a><a name="bkmk_Common_Uses_for_Parameters"></a> 參數的一般使用方式  
 以下提供部分最常使用參數的方式。  
  
 **控制報表資料**  
  
-   透過撰寫包含變數的資料集查詢，在資料來源篩選報表資料。  
  
-   篩選共用資料集中的資料。 將共用資料集加入至報表時，無法變更查詢。 在報表中，您可以加入資料集篩選，其中包含您所建立報表參數的參考。  
  
-   可讓使用者指定值，以自訂報表中的資料。 例如，提供兩個參數，做為銷售資料的開始日期和結束日期。  
  
 **連接相關報表**  
  
-   使用參數，將主報表與鑽研報表、子報表和連結報表產生關聯。 當您設計一組報表時，可以將每份報表設計為可回答某些問題。 每份報表對於相關資訊都會提供不同的檢視或不同的詳細程度。 若要提供一組相關聯的報表，請針對目標報表上的相關資料建立參數。  
  
     如需詳細資訊，請參閱[鑽研報表 &#40;報表產生器及 SSRS&#41;](drillthrough-reports-report-builder-and-ssrs.md)、[子報表 &#40;報表產生器及 SSRS&#41;](subreports-report-builder-and-ssrs.md) 和[建立連結報表](../reports/create-a-linked-report.md)。  
  
-   為多位使用者自訂參數集。 根據報表伺服器上的銷售報表建立兩個連結的報表。 其中一個連結的報表使用銷售人員的預先定義參數值，另一個連結的報表則使用銷售經理的預先定義參數值。 這兩個報表會使用相同的報表定義。  
  
 **變更報表呈現方式**  
  
-   透過 URL 要求傳送命令到報表伺服器，以自訂報表的轉譯。 如需詳細資訊，請參閱 [URL 存取 &#40;SSRS&#41;](../url-access-ssrs.md) 和[在 URL 內傳遞報表參數](../pass-a-report-parameter-within-a-url.md)。  
  
-   可讓使用者指定值，協助自訂報表的外觀。 例如，提供 Boolean 參數，指出要展開或摺疊資料表中的所有巢狀資料列群組。  
  
-   在運算式中包含參數，讓使用者自訂報表資料和外觀。  
  
     如需詳細資訊，請參閱[參數集合參考 &#40;報表產生器及 SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)。  
  
##  <a name="parameter-pane"></a><a name="UserInterface"></a>參數窗格  
 當您檢視報表時，報表檢視器工具列會顯示每一個參數，讓使用者能夠以互動的方式指定值。 下圖顯示具有參數、、和之報表的參數區域 @StartDate @EndDate @Subcategory @ShowAllRows 。  
  
 ![rs_ParameterStory](../media/rs-parameterstory.gif "rs_ParameterStory")  
  
1.  **參數窗格** ：報表檢視器工具列會顯示每個參數的提示和預設值。 工具列上的參數配置會自動格式化。 其順序是由參數出現在 [報表資料] 窗格內的順序所決定。  
  
2.  ** @StartDate 和 @EndDate 參數**參數 @StartDate 是資料類型 `DateTime` 。 [開始日期] 提示會在文字方塊旁邊顯示。 若要修改日期，請在文字方塊中輸入新日期，或是使用行事曆控制項。  
  
     參數 @EndDate 會出現在旁 @StartDate 。  
  
3.  ** @Subcategory 參數**參數 @Subcategory 是資料類型 `Text` 。 由於 @Subcategory 具有可用的值清單，因此有效的值會出現在下拉式清單中。 您必須從此清單選擇值。 因為 @Subcategory 是多值的，所以會出現 [**全選**] 選項，讓您可以清除所有，並選取清單中的所有值。  
  
4.  ** @ShowAllRows 參數**參數 @ShowAllRows 是資料類型 `Boolean` 。 使用選項按鈕可指定 `True` 或 `False`。  
  
5.  **顯示或隱藏參數區域控點** ：在報表檢視器工具列上，按一下此箭頭可顯示或隱藏參數窗格。  
  
6.  **參數按鈕** ：在 [報表產生器] 預覽中的 [功能區] 上，按一下 **[參數]** 按鈕即可顯示或隱藏參數窗格。  
  
7.  **檢視報表按鈕** ：在報表檢視器工具列上按一下 **[檢視報表]** ，即可在輸入參數之後執行報表。 如果所有參數都有預設值，則報表會在第一次檢視時自動執行。  
  
##  <a name="creating-parameters"></a><a name="bkmk_Create_Parameters"></a> 建立參數  
 您可以利用下列方式建立報表參數：  
  
-   新增包含變數的資料集查詢，或者包含輸入參數的資料集預存程序。 每個變數或輸入參數都會建立資料集參數，每個資料集參數都會建立報表參數。  
  
     下列報表產生器影像顯示具有變數的資料集查詢 (1)，以及對應的資料集參數 (2) 和報表參數 (3)。  
  
     ![資料集屬性對話方塊和報表窗格](../media/datasetquery-parameters.png "資料集屬性對話方塊和報表窗格")  
  
    > **注意！** 並非所有的資料來源都支援參數。  
  
     資料集可以是內嵌或共用。 當您將共用資料集加入至報表時，不可覆寫報表中標記為內部的資料集參數。 您可以覆寫未標記為內部的資料集參數。  
  
     如需詳細資訊，請參閱本主題中的＜ [資料集查詢](#bkmk_Dataset_Parameters) ＞。  
  
-   從 [報表資料] 窗格手動建立參數。  
  
     您可以設定報表參數，讓使用者能夠以互動的方式輸入值，協助自訂報表的內容或外觀。 您也可以設定報表參數，讓使用者無法變更預先設定的值。  
  

  > **注意！** 由於參數是在伺服器上獨立管理，所以使用新的參數設定來重新發行主報表時，將不會覆寫此報表的現有參數設定。  
  
-   加入報表組件，其中包含參數的參考或包含變數之共用資料集的參考。  
  
     報表組件會儲存在報表伺服器上，而且可供其他人在報表中使用。 本身為參數的報表組件無法從報表伺服器管理。 您可以在 [報表組件庫] 中搜尋參數，並且在加入這些參數之後，於報表中進行設定。 如需詳細資訊，請參閱 [報表組件 &#40;報表產生器及 SSRS&#41;](../report-parts-report-builder-and-ssrs.md)。  
     
   > **注意！** 您可以針對與參數具有相依資料集的資料區域，將參數當做個別的報表組件發行。 雖然參數會列為報表組件，不過您無法直接將報表組件參數加入至報表。 請改為加入報表組件，然後系統就會根據報表組件所包含或參考的資料集查詢，自動產生任何必要的報表參數。 如需報表組件的詳細資訊，請參閱[報表組件 &#40;報表產生器及 SSRS&#41;](../report-parts-report-builder-and-ssrs.md) 和[報表設計師中的報表組件 &#40;SSRS&#41;](report-parts-in-report-designer-ssrs.md)。  
  
### <a name="parameter-values"></a>參數值  
 下列是在報表中選取參數值的選項。  
  
-   從下拉式清單選取單一參數值。  
  
-   從下拉式清單選取多個參數值。  
  
-   從下拉式清單選取一個參數的值，它會決定其他參數下拉式清單中可用的值。 這些是串聯參數。 串聯參數可讓您後續從數千個值篩選出能夠管理的參數值數目。  
  
     如需詳細資訊，請參閱 [將串聯參數加入至報表 &#40;報表產生器及 SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)中建立的行動報表。  
  
-   不需要先選取參數值就能執行報表，因為已經為參數建立預設值。  
  
##  <a name="report-parameter-properties"></a><a name="bkmk_Report_Parameters"></a>報表參數屬性  
 您可以使用 [報表屬性] 對話方塊來變更報表參數屬性。 下表摘要說明您可以針對每個參數設定的屬性：  
  
|屬性|描述|  
|--------------|-----------------|  
|名稱|輸入區分大小寫的參數名稱。 此名稱必須以字母開頭，可以包含字母、數字和底線 (_)。 名稱不能有空格。 若為自動產生的參數，此名稱會符合資料集查詢中的參數。 根據預設，手動建立的參數與 ReportParameter1 類似。|  
|Prompt|在報表檢視器工具列上顯示於參數旁邊的文字。|  
|資料類型|當定義參數的可用值時，使用者會從下拉式清單中選擇值，即使資料類型是也一樣 `DateTime` 。 報表參數的資料類型必須是下列其中一種：<br /><br /> `Boolean`. 使用者會從選項按鈕中選取 True 或 False。<br /><br /> `DateTime`. 使用者會從日曆控制項中選取日期。<br /><br /> **整數**。 使用者會在文字方塊中輸入值。<br /><br /> **Float**。 使用者會在文字方塊中輸入值。<br /><br /> `Text`. 使用者會在文字方塊中輸入值。<br /><br /> 如需有關報表資料類型的詳細資訊，請參閱＜ [RDL Data Types](../reports/report-definition-language-ssrs.md#bkmk_RDL_Data_Types)＞。|  
|允許空白值|如果參數值可為空字串或空白，則選取此選項。<br /><br /> 如果您為參數指定有效值，而且希望空白值是其中一個有效值，則必須將它納入做為您指定的其中一個有效值。 選取此選項並不會自動將空白納入做為可用的值。|  
|允許 null 值|如果參數值可為 null，則選取此選項。<br /><br /> 如果您為參數指定有效值，而且希望 null 是其中一個有效值，則必須將 null 納入做為您指定的其中一個有效值。 選取此選項並不會自動將 null 納入做為可用的值。|  
|允許多個值|提供可用的值，建立可供使用者選擇的下拉式清單。 這是確保資料集查詢中只會提交有效值的好方法。<br /><br /> 如果參數值可以是顯示在下拉式清單中的多個值，則選取此選項。 不允許 Null 值。 選取此選項時，系統會將核取方塊加入到參數下拉式清單內可用值的清單中。 清單的頂端包含 **[全選]** 核取方塊。 使用者可以檢查想要的值。<br /><br /> 如果提供值的資料迅速改變，則使用者看見的清單可能不是最新的。|  
|可見|選取此選項可顯示報表執行時，位於報表頂端的報表參數。 此選項可讓使用者在執行階段選取參數值。|  
|Hidden|選取此選項來隱藏已發行報表中的報表參數。 您仍然可以在報表 URL、訂閱定義或報表伺服器上設定報表參數值。|  
|內部|選取此選項來隱藏報表參數。 已發行報表中的報表參數只能在報表定義中檢視。|  
|可用值|如果您已為參數指定可用的值，則有效值會固定顯示為下拉式清單。 例如，如果您為 `DateTime` 參數提供可用的值，則參數窗格中會出現日期的下拉式清單，而不是行事曆控制項。 為確保報表和子報表之間的值清單一致，您可以在資料來源上設定一個選項，針對與資料來源相關聯的資料集中的所有查詢使用單一交易。<br /><br /> ** \* \* 安全性 \* 注意事項 \* **在任何包含資料類型參數的報表中 `Text` ，請務必使用可用的值清單 (也稱為有效值清單) ，並確定任何執行報表的使用者只具有在報表中查看資料所需的許可權。 如需詳細資訊，請參閱 [安全性 &#40;報表產生器&#41;](../report-builder/security-report-builder.md)中建立的行動報表。|  
|預設值|設定來自查詢或靜態清單的預設值。<br /><br /> 如果每個參數都有預設值，則報表會在第一次檢視時自動執行。|  
|進階|設定報表定義屬性 `UsedInQuery`，其值指出此參數直接或間接影響報表中的資料。<br /><br /> **自動判斷何時重新整理**<br /> 當您想要讓報表處理器判斷此值的設定時，請選擇此選項。 如果報表處理器偵測到一個資料集查詢，且其中包含一個這個參數的直接或間接參照，或者如果報表中有子報表，則此值為 `True`。<br /><br /> **永遠重新整理**<br /> 在資料集查詢或參數運算式中直接或間接使用報表參數時，請選擇此選項。 此選項會將 `UsedInQuery` 設定為 True。<br /><br /> **永不重新整理**<br /> 不在資料集查詢或參數運算式中直接或間接使用報表參數時，請選擇此選項。 此選項會將 `UsedInQuery` 設定為 False。<br /><br /> ** \* \* 注意 \* ： \* **請小心使用 [**永不**重新整理]。 在報表伺服器上，`UsedInQuery` 用於協助控制報表資料與已轉譯之報表的快取選項，以及快照集報表的參數選項。 如果未正確設定 **[永不重新整理]** ，您可能會快取不正確的報表資料或報表，或者使快照集報表的資料不一致。 如需詳細資訊，請參閱[報表定義語言 &#40;SSRS&#41;](../reports/report-definition-language-ssrs.md)。|  
  
##  <a name="dataset-query"></a><a name="bkmk_Dataset_Parameters"></a>資料集查詢  
 若要篩選資料集查詢中的資料，您可以加入限制子句，透過指定結果集中要包含或排除的值限制擷取的資料。  
  
 使用資料來源的查詢設計工具，可協助您建立參數化查詢。  
  
-   如果是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢，不同的資料來源會支援不同的參數語法。 支援的範圍是查詢中依據位置或名稱識別的參數。 如需詳細資訊，請參閱將資料加入報表中的特定外部資料源類型的主題[&#40;報表產生器和 SSRS&#41;](../report-data/report-datasets-ssrs.md)。 在關聯式查詢設計工具中，您必須為篩選選取參數選項，才能建立參數化查詢。 如需詳細資訊，請參閱[關聯式查詢設計工具使用者介面 &#40;報表產生器&#41;](../report-data/relational-query-designer-user-interface-report-builder.md)。  
  
-   針對依據多維資料來源 (例如 Microsoft SQL Server Analysis Services、SAP NetWeaver BI 或 Hyperion Essbase) 的查詢，您可以指定是否根據您在查詢設計工具中指定的篩選建立參數。 如需詳細資訊，請參閱[查詢設計工具 &#40;報表產生器&#41;](../query-designers-report-builder.md) 中對應於資料延伸模組的查詢設計工具主題。  
  
##  <a name="parameter-management-for-a-published-report"></a><a name="bkmk_Manage_Parameters"></a> 在發行的報表上管理參數  
 當您設計報表時，報表參數會儲存在報表定義中。 當您發行報表時，報表參數會儲存，並且與報表定義分開管理。  
  
 在已發行的報表中，可以使用下列項目：  
  
-   **報表參數屬性。** 直接在報表伺服器上，從報表定義個別變更報表參數值。  
  
-   **快取報表。** 若要為報表建立快取計劃，每個參數都必須有預設值。 如需詳細資訊，請參閱 [快取報表 &#40;SSRS&#41;](../report-server/caching-reports-ssrs.md)的版本中預先載入快取的唯一方法。  
  
-   **快取共用資料集。** 若要為共用資料集建立快取計劃，每個參數都必須有預設值。 如需詳細資訊，請參閱 [快取報表 &#40;SSRS&#41;](../report-server/caching-reports-ssrs.md)的版本中預先載入快取的唯一方法。  
  
-   **連結報表。** 您可以使用預設的參數建立連結報表，針對不同的對象來篩選資料。 如需詳細資訊，請參閱 [建立連結報表](../reports/create-a-linked-report.md)。  
  
-   **報表訂閱。** 您可以指定參數值來篩選資料，並透過訂用帳戶傳遞報表。 如需詳細資訊，請參閱[訂閱與傳遞 &#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md)。  
  
-   **URL 存取。** 您可以在報表 URL 中指定參數值。 您也可以使用 URL 存取來執行報表及指定參數值。 如需詳細資訊，請參閱 [URL 存取 &#40;SSRS&#41;](../url-access-ssrs.md)。  
  
 如果您重新發行報表定義，則針對已發行報表所設定的參數屬性通常會保留起來。 如果報表定義和報表同樣重新發行，且參數名稱和資料類型保持相同，則會保留屬性設定。 如果您加入或刪除報表定義中的參數，或變更現有參數的資料類型或名稱，您就可能需要變更已發行報表的參數屬性。  
  
 並非所有的參數都可以在任何情況下修改。 如果報表參數從資料集查詢取得預設值，無法針對已發行的報表修改該值，也無法在報表伺服器上修改該值。 執行階段使用的值會在查詢執行時決定，如果是以運算式為基礎的參數，則會在評估運算式時決定。  
  
 報表執行選項會影響處理參數的方式。 以快照集執行的報表無法使用從查詢所衍生的參數，除非查詢包括參數的預設值。  
  
##  <a name="parameters-for-a-subscription"></a><a name="bkmk_Parameters_Subscription"></a> 訂閱的參數  
 您可以定義視需要或快照集報表的訂閱，並指定在訂閱處理過程中要使用的參數值。  
  
-   **隨需報表。**  您可以為視需要報表的每個參數指定不同於已發行值的參數值。 例如，假設您有一個呼叫服務報表，使用 *Time Period* 參數傳回客戶在目前日期、星期、或月份的服務要求。 如果報表的預設參數值設定為 **today**，您的訂閱可以使用不同的參數值 (例如， **week** 或 **month**)，以產生包含每週或每月數字的報表。  
  
-   **快照集.**  快照集訂閱必須使用為快照集定義的參數值。 您的訂閱無法覆寫快照集所定義的參數值。 例如，假設您訂閱當成報表快照集執行的西區銷售報表，而快照集指定 **Western** 作為區域參數值。 在此情況下，如果您對此報表建立訂閱，則必須在訂閱中使用參數值 **Western** 。 為了提供忽略參數的視覺指示，訂閱頁面上的參數欄位會設定為唯讀欄位。  
  
     報表執行選項會影響處理參數的方式。 當成報表快照集執行的參數化報表，會使用報表快照集所定義的參數值。 參數值是在報表的參數屬性頁面中定義。 以快照集執行的報表無法使用從查詢所衍生的參數，除非查詢包括參數的預設值。  
  
     如果在定義了訂閱之後變更報表快照集內的參數值，報表伺服器就會停用訂閱。 停用訂閱指出已經修改報表。 若要啟動訂閱，請開啟並儲存訂閱。  
  
> [!NOTE]  
>  資料驅動訂閱可以使用從訂閱者資料來源取得的參數值。 如需詳細資訊，請參閱[使用外部資料來源以取得訂閱者資料 &#40;資料驅動訂閱&#41;](../subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)。  
  
 如需詳細資訊，請參閱[訂閱與傳遞 &#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md)。  
  
##  <a name="parameters-and-securing-data"></a><a name="bkmk_Parameters_Security"></a> 參數和資料保護  
 散發包含機密或敏感資訊的參數化報表時，請特別小心。 使用者可以輕鬆地以其他值取代報表參數，造成您不希望發生的資訊洩露。  
  
 使用員工或個人資料之參數的一個安全替代方式，就是根據包含 Users 集合之 **UserID** 欄位的運算式來選取資料。 Users 集合提供一種方法，來取得執行報表之使用者的識別，並使用該識別來擷取使用者特定資料。  
  
> [!IMPORTANT]  
>  在任何含有 `String` 類型之參數的報表中，請務必使用可用的值清單 (也稱為有效值清單)，並確認執行報表的任何使用者只具有檢視報表資料所需的權限。 當您將參數定義為 `String` 類型時，使用者會看到一個可接受任何值的文字方塊。 可用的值清單會限制可輸入的值。 如果報表參數繫結至資料集參數，而且您不要使用可用的值清單，則報表使用者可以在文字方塊中輸入 SQL 語法，如此可能會使您的報表及伺服器暴露在 SQL 資料隱碼攻擊的危險之下。 如果使用者的權限足以執行新的 SQL 陳述式，伺服器可能會出現不良的結果。  
>   
>  如果報表參數未繫結至資料集參數，且參數值有包含在報表中，則報表使用者就可以在參數值中輸入運算式語法或 URL，並將報表轉譯為 Excel 或 HTML。 如果另一個使用者接著檢視報表並按一下轉譯的參數內容，該使用者可能會不小心執行惡意指令碼或連結。  
>   
>  若要減輕不小心執行惡意指令碼的風險，請只從信任的來源開啟轉譯的報表。 如需保護報表安全的詳細資訊，請參閱 [保護報表和資源的安全](../security/secure-reports-and-resources.md)。  
  
##  <a name="how-to-topics"></a><a name="bkmk_How_To_Topics"></a>How To 主題  
 本節列出的程序，為您逐步示範如何使用參數和篩選。  
  
-   [加入、變更或刪除報表參數 &#40;報表產生器及 SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)  
  
-   [為報表參數加入、變更或刪除可用的值 &#40;報表產生器及 SSRS&#41;](add-change-or-delete-available-values-for-a-report-parameter.md)  
  
-   [為報表參數加入、變更或刪除預設值 &#40;報表產生器及 SSRS&#41;](add-change-or-delete-default-values-for-a-report-parameter.md)  
  
-   [變更報表參數的順序 &#40;報表產生器及 SSRS&#41;](change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
-   [將串聯參數加入至報表 &#40;報表產生器及 SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)  
  
-   [將篩選加入資料集中 &#40;報表產生器及 SSRS&#41;](../report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
-   [加入子報表和參數 &#40;報表產生器及 SSRS&#41;](add-a-subreport-and-parameters-report-builder-and-ssrs.md)  
  
-   [參數化預存程式的 SSRS 報表](https://www.c-sharpcorner.com/UploadFile/7d3362/ssrs-report-for-parameterize-stored-procedure/)  
  
## <a name="did-this-article-help-you-were-listening"></a>這篇文章對您有幫助嗎？ 我們正在接聽  
 您要尋找哪些資訊？找到了嗎？ 我們正在聆聽您的意見反應以改善內容。 請將您的意見提交至[sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Report%20Parameters%20page)  
  
##  <a name="related-content"></a><a name="bkmk_Related_Topics"></a> 相關內容  
 [設定 SSRS 報表參數 (測驗)](https://www.trenovision.com/quiz/sql-server-reporting-services-ssrs-quiz/)  
  
 [教學課程：將參數加入至報表 &#40;報表產生器&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)  
  
 [揭開 Reporting Service 中 InvalidReportParameterException 的神秘面紗](https://go.microsoft.com/fwlink/p/?LinkId=393118)  
  
 [報表範例 (報表產生器和 SSRS)](https://go.microsoft.com/fwlink/?LinkId=198283)  
  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)  
  
 [運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)  
  
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
 [安全性 &#40;報表產生器&#41;](../report-builder/security-report-builder.md)  
  
 [互動式排序、文件引導模式及連結 &#40;報表產生器及 SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)  
  
 [鑽研、向下鑽研、子報表和巢狀資料區 &#40;報表產生器及 SSRS&#41;](drillthrough-drilldown-subreports-and-nested-data-regions.md)  
  
  
