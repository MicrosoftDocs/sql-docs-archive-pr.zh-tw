---
title: '[報表資料] 窗格 (報表產生器) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10435"
helpviewer_keywords:
- Report Data pane
ms.assetid: 1492aa39-aeb1-4509-ab97-b9edd0901b7e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c87ee4411f5c1ec4c07e0fc9f0357f6fb33e3c9f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585089"
---
# <a name="report-data-pane-report-builder"></a>報表資料窗格 (報表產生器)
  [報表資料]**** 窗格可用於檢視報表中目前定義的參數、資料來源、資料集、欄位集合和影像。 [圖表資料] 會以階層檢視來顯示表示報表中資料的項目。 最上層節點代表內建欄位、參數、影像和資料來源參考。 請展開每個節點以檢視資料項目。 例如，當您展開資料來源節點時，為該資料來源所定義的資料集就會顯示。 在展開資料集時，其欄位集合就會顯示。 您可以將項目拖曳至報表設計介面或 [群組] 窗格，以便連結資料與報表頁面上的選取報表項目。 如需詳細資訊，請參閱[報表設計檢視 &#40;報表產生器&#41;](report-builder/report-design-view-report-builder.md)。

## <a name="options"></a>選項
 **內建欄位**表示報表中常用的欄位，例如報表名稱或頁碼。 如需詳細資訊，請參閱[運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md)。

 **參數**代表報表參數的集合，每一個都可以是單一值或多重值。 如需詳細資訊，請參閱 MSDN 上的 [報表參數 &#40;報表產生器和報表設計師&#41;](report-design/report-parameters-report-builder-and-report-designer.md)類型之報表資料來源為基礎的資料集。

 **影像**表示報表中所使用的影像集。 如需詳細資訊，請參閱[影像 &#40;報表產生器及 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)。

 **資料來源**表示內嵌資料來源或共用資料來源的參考。 資料來源代表報表資料的來源。 資料來源就是使用它之資料集集合的父節點。 如需詳細資訊，請參閱[將資料加入報表 &#40;報表產生器和 SSRS&#41;](report-data/report-datasets-ssrs.md)和[報表產生器中的資料連線、資料來源及連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)。

 **資料集**表示藉由執行一個命令從資料來源抓取的資料，例如，從資料庫中抓取 [!INCLUDE[tsql](../includes/tsql-md.md)] 資料的查詢 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 資料集是由查詢所指定之欄位集合的父節點，也包括導出欄位。 報表產生器支援查詢設計工具，可協助您指定查詢。 如需詳細資訊，請參閱[將資料加入報表 &#40;報表產生器和 SSRS&#41;](report-data/report-datasets-ssrs.md)。

## <a name="see-also"></a>另請參閱
 [資料集欄位集合 &#40;報表產生器和 ssrs 報表產生器&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md) [[對話方塊]、[窗格] 和 [嚮導] 的](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)[[群組] 窗格](report-design/grouping-pane-report-builder.md)&#40;報表產生器&#41;[尋找、查看和管理報表 &#40;報表產生器和 SSRS &#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)


