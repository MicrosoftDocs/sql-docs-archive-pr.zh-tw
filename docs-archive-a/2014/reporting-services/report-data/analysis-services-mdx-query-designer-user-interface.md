---
title: Analysis Services MDX 查詢設計工具使用者介面 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10012"
- sql12.rtp.rptdesigner.dataview.asquerydesigner.f1
helpviewer_keywords:
- MDX [Reporting Services], creating datasets
- query designers [Reporting Services]
ms.assetid: d9c7c0b3-fce4-4a65-b679-408273e6a925
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 163a48497b073ddee9aad64b998594b12e8cad23
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688618"
---
# <a name="analysis-services-mdx-query-designer-user-interface"></a>Analysis Services MDX 查詢設計工具使用者介面
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 提供了圖形化查詢設計工具，可用來建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源的多維度運算式 (MDX) 查詢和資料採礦運算式 (DMX) 查詢。 此主題即描述 MDX 查詢設計工具。 如需 DMX 查詢設計工具的詳細資訊，請參閱 [Analysis Services Connection Type for DMX &#40;SSRS&#41;](analysis-services-connection-type-for-dmx-ssrs.md)。

 MDX 圖形化查詢設計工具有兩種模式：設計模式和查詢模式。 每一種模式都會提供 [中繼資料] 窗格，您可以在這個窗格中，從選取的 Cube 中拖曳成員，以建立 MDX 查詢，在處理報表時擷取資料。

> [!IMPORTANT]
>  當使用者建立與執行查詢時，可以存取資料來源。 您應該授與資料來源的最小權限，例如唯讀權限。

## <a name="graphical-mdx-query-designer-in-design-mode"></a>設計模式中的圖形化 MDX 查詢設計工具
 當您為報表資料集編輯 MDX 查詢時，圖形化 MDX 查詢設計工具會在 [設計] 模式下開啟。

 下圖會標示出設計模式的窗格。

 ![Analysis Services MDX 查詢設計工具，設計檢視](../../analysis-services/media/rsqd-dsawas-mdx-designmode.gif "Analysis Services MDX 查詢設計工具，設計檢視")

 下表列出此模式下的窗格：

|窗格|函式|
|----------|--------------|
|[Select Cube (選取 Cube)] 按鈕 (**...**)|顯示目前選取的 Cube。|
|[中繼資料] 窗格|顯示在選取的 Cube 上定義之量值、關鍵效能指標 (KPI) 和維度的階層式清單。|
|[導出成員] 窗格|顯示目前已定義，可在查詢中使用的導出成員。|
|[篩選] 窗格|用來選擇維度和相關階層，以便篩選來源端的資料和限制傳回給報表的資料。|
|[資料] 窗格|在您從 [中繼資料] 窗格和 [導出成員] 窗格中拖曳項目時，顯示結果集的資料行標題。 如果已選取 **[自動執行]** 按鈕，便會自動更新結果集。 .|

 您可以將 [中繼資料] 窗格中的維度、量值和 KPI 以及 [導出成員] 窗格中的導出成員，拖曳至 [資料] 窗格中。 在 [篩選] 窗格中，則可以選取維度和相關階層，以及設定篩選運算式來限制查詢可使用的資料。 如果已選取工具列上的 [自動執行]**** (![自動執行查詢](../../analysis-services/media/rsqdicon-autoexecute.gif "自動執行查詢")) 切換按鈕，則每次您將中繼資料物件放到 [資料] 窗格中時，查詢設計工具便會執行查詢。 您可以使用工具列上的 [執行]**** (![執行查詢](../../analysis-services/media/rsqdicon-run.gif "執行查詢")) 按鈕，以手動方式執行查詢。

 當您在此模式下建立 MDX 查詢時，查詢中會自動包含下列其他屬性：

 **成員屬性** ：MEMBER_CAPTION、MEMBER_UNIQUE_NAME

 **資料格屬性** ：VALUE、BACK_COLOR、FORE_COLOR、FORMATTED_VALUE、FORMAT_STRING、FONT_NAME、FONT_SIZE、FONT_FLAGS

 若要指定您自己的其他屬性，您必須在 [查詢] 模式下手動編輯 MDX 查詢。

### <a name="graphical-mdx-query-designer-toolbar-in-design-mode"></a>設計模式中的圖形化 MDX 查詢設計工具工具列
 查詢設計工具工具列會提供按鈕，協助您使用圖形化介面設計 MDX 查詢。 下表列出這些按鈕及其功能。

|按鈕|描述|
|------------|-----------------|
|**當成文字編輯**|這種資料來源類型不啟用|
|**匯入**|從檔案系統上的報表定義 (.rdl) 檔案匯入現有的查詢。 如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。|
|![變更為 MDX 查詢檢視](../../analysis-services/media/rsqdicon-commandtypemdx.gif "變更為 MDX 查詢檢視")|切換到命令類型 MDX。|
|![變更為 DMX 查詢語言檢視](../media/rsqdicon-commandtypedmx.gif "變更為 DMX 查詢語言檢視")|切換到命令類型 DMX。|
|![重新整理結果資料](../../analysis-services/media/rsqdicon-refresh.gif "重新整理結果資料")|重新整理資料來源中的中繼資料。|
|![新增導出成員](../../analysis-services/media/rsqdicon-addcalculatedmember.gif "加入導出成員")|顯示 **[導出成員產生器]** 對話方塊。|
|![切換以顯示空資料格](../../analysis-services/media/rsqdicon-showemptycells.gif "切換以顯示空資料格")|在顯示或隱藏 [資料] 窗格中的空白資料格之間切換 (這相當於使用 MDX 中的 NON EMPTY 子句)。|
|![自動執行查詢](../../analysis-services/media/rsqdicon-autoexecute.gif "自動執行查詢")|每次進行變更時，自動執行查詢並顯示結果。 結果會顯示在 [資料] 窗格中。|
|![顯示彙總按鈕](../../analysis-services/media/rsqdicon-showaggregations.gif "顯示彙總按鈕")|將彙總顯示在 [資料] 窗格中。|
|![刪除](../../analysis-services/media/rsqdicon-delete.gif "刪除")|從查詢中刪除 [資料] 窗格中選取的資料行。|
|![[查詢參數] 對話方塊圖示](../../analysis-services/media/iconqueryparameter.gif "[查詢參數] 對話方塊圖示")|顯示 **[查詢參數]** 對話方塊。 當您指定查詢參數的值時，將會自動建立同名的報表參數。 查詢參數的值會設定為參考此報表參數的運算式。|
|![準備查詢按鈕](../../analysis-services/media/rsqdicon-preparequery.gif "準備查詢按鈕")|準備查詢。|
|![執行查詢](../../analysis-services/media/rsqdicon-run.gif "執行查詢")|執行查詢並將結果顯示在 [資料] 窗格中。|
|![取消查詢](../../analysis-services/media/rsqdicon-cancel.gif "取消查詢")|取消查詢。|
|![切換到設計模式](../../analysis-services/media/rsqdicon-designmode.gif "切換到設計模式")|在「設計」模式與「查詢」模式之間切換。|

## <a name="graphical-mdx-query-designer-in-query-mode"></a>查詢模式中的圖形化 MDX 查詢設計工具
 若要將圖形化查詢設計工具變更為 **[查詢]** 模式，請按一下工具列上的 **[設計模式]** 按鈕。

 下圖會標示出「查詢」模式中的窗格。

 ![Analysis Services MDX 查詢設計工具，查詢檢視](../../analysis-services/media/rsqd-dsawas-mdx-querymode.gif "Analysis Services MDX 查詢設計工具，查詢檢視")

 下表列出此模式下的窗格：

|窗格|函式|
|----------|--------------|
|[Select Cube (選取 Cube)] 按鈕 (**...**)|顯示目前選取的 Cube。|
|[中繼資料/函數/範本] 窗格|顯示在選取的 Cube 上定義之量值、KPI 和維度的階層式清單。|
|[查詢] 窗格|顯示查詢文字。|
|結果窗格|顯示執行查詢的結果。|

 [中繼資料] 窗格會顯示 **[中繼資料]**、 **[函數]** 和 **[範本]** 的索引標籤。 從 **[中繼資料]** 索引標籤中，可以將維度、階層、KPI 和量值拖曳至 [MDX 查詢] 窗格中。 從 **[函數]** 索引標籤中，可以將函數拖曳至 [MDX 查詢] 窗格中。 從 **[範本]** 索引標籤中，可以將 MDX 範本加入至 [MDX 查詢] 窗格中。 當您執行查詢時，[結果] 窗格會顯示 MDX 查詢的結果。

 您可以擴充在 [設計] 模式下產生的預設 MDX 查詢，以包含其他成員屬性和資料格屬性。 當您執行查詢時，這些值不會出現在結果集中。 但是，這些值會傳回 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ，而且您可以在報表中使用這些值。 如需詳細資訊，請參閱＜Analysis Services 資料庫的擴充欄位屬性 (SSRS)＞。

### <a name="graphical-query-designer-toolbar-in-query-mode"></a>查詢模式中的圖形化查詢設計工具工具列
 查詢設計工具工具列會提供按鈕，協助您使用圖形化介面設計 MDX 查詢。

 「設計」模式與「查詢」模式的工具列按鈕完全相同，唯一不同的是在「查詢」模式中未啟用下列按鈕：

-   **當成文字編輯**

-   **新增導出成員** (![新增導出成員](../../analysis-services/media/rsqdicon-addcalculatedmember.gif "加入導出成員"))

-   **顯示空資料格** (![切換以顯示空資料格](../../analysis-services/media/rsqdicon-showemptycells.gif "切換以顯示空資料格"))

-   **自動執行** (![自動執行查詢](../../analysis-services/media/rsqdicon-autoexecute.gif "自動執行查詢"))

-   **顯示彙總** (![顯示彙總按鈕](../../analysis-services/media/rsqdicon-showaggregations.gif "顯示彙總按鈕"))

## <a name="see-also"></a>另請參閱
 [在 Analysis Services &#40;報表產生器和 ssrs 的 MDX 查詢設計工具中定義參數，&#41;](define-parameters-in-the-mdx-query-designer-for-analysis-services.md) [建立共用資料集或內嵌資料集 &#40;報表產生器和 ssrs](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)&#41;Analysis Services[適用于 DMX &#40;ssrs&#41;](analysis-services-connection-type-for-dmx-ssrs.md) [RSREPORTDESIGNER.CONFIG 設定檔](../report-server/rsreportdesigner-configuration-file.md)Analysis Services 連線類型 &#40;[ssrs](analysis-services-connection-type-for-mdx-ssrs.md)&#41;


