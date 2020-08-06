---
title: 以程式設計方式建立封裝 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 7474b1f4-7607-4f28-a6fd-67f7db1dd3f8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8ef8fd0b6b5bdeead718f204a0933771fe58924a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594648"
---
# <a name="building-packages-programmatically"></a>以程式設計方式建立封裝
  如果您需要動態建立封裝，或要在開發環境以外的地方管理和執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，可以使用程式設計方式操作封裝。 在這種方法中，您有連續範圍的選項：

-   在不須修改的情況下載入並執行現有的封裝。

-   載入現有的封裝、重新加以設定 (例如，針對不同的資料來源)，然後執行。

-   建立新封裝、逐物件和逐屬性地加入與設定元件、儲存，然後加以執行。

 您可以透過任何 Managed 程式語言，使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型撰寫用來建立、設定和執行封裝的程式碼。 例如，您可能會想要建立中繼資料驅動的封裝，以根據選取的資料來源及其資料表與資料行，設定其連接或是其資料來源、轉換與目的地。

 本節會描述和示範如何以程式設計方式逐行建立和設定封裝。 在封裝程式設計選項範圍中較不複雜的一端，您無須修改即可直接載入和執行現有的封裝，如[以程式設計方式執行及管理封裝](../run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)中所述。

 並未在此說明的中間選項是以範本形式載入現有的封裝、重新加以設定 (例如，針對不同的資料來源)，然後執行。 您也可以使用本節中的資訊，修改封裝中的現有物件。

> [!NOTE]
>  當您使用現有封裝做為範本，並修改資料流程中的現有資料行時，可能必須移除現有的資料行，並呼叫受影響元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 方法。

## <a name="in-this-section"></a>本節內容
 [以程式設計方式建立封裝](../building-packages-programmatically/creating-a-package-programmatically.md)描述如何以程式設計方式建立封裝。

 [以程式設計方式加入](../building-packages-programmatically/adding-tasks-programmatically.md)工作描述如何將工作加入至封裝。

 [以程式設計方式連接](../building-packages-programmatically/connecting-tasks-programmatically.md)工作描述如何根據上一個工作或容器的執行結果，控制封裝中容器和工作的執行。

 [以程式設計方式新增連接](../building-packages-programmatically/adding-connections-programmatically.md)描述如何將連線管理員加入封裝。

 [以程式設計方式使用變數](../building-packages-programmatically/working-with-variables-programmatically.md)描述如何在封裝執行期間加入和使用變數。

 [以程式設計方式處理事件](../building-packages-programmatically/handling-events-programmatically.md)描述如何處理封裝和工作事件。

 [以程式設計方式啟用記錄](../building-packages-programmatically/enabling-logging-programmatically.md)描述如何啟用封裝或工作的記錄，以及如何將自訂篩選套用至記錄事件。

 [以程式設計方式加入資料流程工作](../building-packages-programmatically/adding-the-data-flow-task-programmatically.md)描述如何加入和設定資料流程工作及其元件。

 [以程式設計方式探索資料流程元件](../building-packages-programmatically/discovering-data-flow-components-programmatically.md)描述如何偵測本機電腦上所安裝的元件。

 [以程式設計方式加入資料流程元件](../building-packages-programmatically/adding-data-flow-components-programmatically.md)描述如何將元件加入至資料流程工作。

 [以程式設計方式連接資料流程元件](../building-packages-programmatically/connecting-data-flow-components-programmatically.md)描述如何連接兩個數據流元件。

 [以程式設計方式選取輸入資料行](../building-packages-programmatically/selecting-input-columns-programmatically.md)描述如何從資料流程中的上游元件提供給元件的輸入資料行。

 [以程式設計方式儲存封裝](../building-packages-programmatically/saving-a-package-programmatically.md)描述如何以程式設計方式儲存封裝。

## <a name="reference"></a>參考
 [Integration Services 錯誤和訊息參考](../integration-services-error-and-message-reference.md)列出預先定義的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 錯誤碼及其符號名稱和描述。

## <a name="related-sections"></a>相關章節
 [使用腳本擴充封裝](../extending-packages-scripting/extending-packages-with-scripting.md)討論如何使用腳本工作來擴充控制流程，以及如何使用腳本元件來擴充資料流程。

 [使用自訂物件擴充封裝](../extending-packages-custom-objects/extending-packages-with-custom-objects.md)討論如何建立程式自訂工作、資料流程元件以及其他封裝物件，以便在多個封裝中使用。

 [以程式設計方式執行和管理封裝](../run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)討論如何列舉、執行和管理封裝及其儲存所在的資料夾。

## <a name="external-resources"></a>外部資源

-   位於 www.codeplex.com/MSFTISProdSamples 的 CodePlex 範例：[Integration Services 產品範例](https://go.microsoft.com/fwlink/?LinkID=131204)

-   blogs.msdn.com 上的部落格文章：[Performance profiling your custom extensions](https://go.microsoft.com/fwlink/?LinkId=238831) (對自訂延伸模組進行效能分析)。

![Integration Services 圖示 (小型) ](../media/dts-16.gif "Integration Services 圖示 (小)")會**保持最**新狀態 Integration Services  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。

## <a name="see-also"></a>另請參閱
 [SQL Server Integration Services](../sql-server-integration-services.md)


