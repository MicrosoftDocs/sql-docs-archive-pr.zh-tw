---
title: " (SSAS 表格式) 的 Kpi |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a0524602-5239-45a7-8c44-2477302a3637
author: minewiskan
ms.author: owend
ms.openlocfilehash: 54cc7341f2d0f002496c1936f2c4f0808cd5e243
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687214"
---
# <a name="kpis-ssas-tabular"></a>KPI (SSAS 表格式)
  表格式模型中的「關鍵效能指標」(KPI)** 可用來針對由量值或絕對值定義的「目標」** 值，量測由「基底」** 量值定義之值的績效。 本主題為表格式模型作者提供對於表格式模型中 KPI 的基本了解。  
  
 本主題的章節：  
  
-   [優點](#bkmk_benefits)  
  
-   [範例](#bkmk_example)  
  
-   [建立和編輯 Kpi](#bkmk_create)  
  
-   [相關工作](#bkmk_related_tasks)  
  
##  <a name="benefits"></a><a name="bkmk_benefits"></a> 優點  
 在商務用語中，關鍵效能指標 (KPI) 是量測商務目標的可量化度量。 KPI 通常會在一段時間內進行評估。 例如，組織的銷售部門可以使用 KPI，針對預計的毛利來測量每月的毛利。 會計部門可以針對營收測量每月支出，以評估成本，而人力資源部門可以測量每季員工營業額。 每一個都是 KPI 的範例。 商務專業人員經常會使用在商務計分卡中分組的 KPI，以取得商務成就之快速與精確的記錄摘要，或識別趨勢。  
  
 表格式模型中的 KPI 包括：  
  
 **基底值**  
 基底值是由解析為值的量值來定義。 例如，此值可以是實際銷售的彙總，也可以是指定期間內的導出量值，例如收益。  
  
 **目標值**  
 目標值是由解析為值的量值或由絕對值來定義。 例如，目標值可能是組織業務經理想要提升銷售或利潤所用的量。  
  
 **狀態臨界值**  
 狀態臨界值是由介於高低臨界值之間的範圍來定義，或由固定值來定義。 狀態臨界值會顯示圖形，幫助使用者輕鬆地判斷基底值相較於目標值的狀態。  
  
##  <a name="example"></a><a name="bkmk_example"></a> 範例  
 任職於 Adventure Works 的銷售經理想要建立樞紐分析表，用來快速顯示銷售員工是否達成給定期間 (年份) 的銷售配額。 對於每個銷售員工，她要樞紐分析表顯示實際銷售金額 (美元)、銷售配額量 (美元)，以及顯示每個銷售員工狀態是低於、等於或高於其銷售配額的簡單圖形。 她希望能依年份配量這些資料。  
  
 為了達到此目的，銷售經理會登錄其組織 BI 解決方案開發人員的協助，以將銷售 KPI 加入至 AdventureWorks 表格式模型。 然後銷售經理使用 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 連接至 Adventure Works 表格式模型做為資料來源，並建立具有欄位 (量值和 KPI) 和交叉分析篩選器的樞紐分析表，以分析銷售主力是否達成其配額。  
  
 在模型中，FactResellerSales 資料表的 SalesAmount 資料行上建立了量值，提供每個銷售員工的實際銷售金額 (美元)。 此量值會定義 KPI 的基底值。  
  
 Sales 量值是以下列公式建立的：  
  
```  
Sales:=Sum(FactResellerSales[SalesAmount])  
```  
  
 FactSalesQuota 資料表的 SalesAmountQuota 資料行為每個員工定義了銷售量配額。 此資料行的值會做為 KPI 的目標量值 (值)。  
  
 SalesAmountQuota 量值是以下列公式建立的：  
  
```  
Target SalesAmountQuota:=Sum(FactSalesQuota[SalesAmountQuota])  
```  
  
> [!NOTE]  
>  FactSalesQuota 資料表的 EmployeeKey 資料行和 DimEmployees 資料表的 EmployeeKey 之間有關聯性。 此關聯性為必要項，因此 DimEmployee 資料表中的每個銷售員工才能顯示在 FactSalesQuota 資料表中。  
  
 現在已建立量值做為 KPI 的基底值和目標值，Sales 量值就會延伸至新的銷售 KPI。 在銷售 KPI 中，目標 SalesAmountQuota 量值是定義為目標值。 狀態臨界值是定義為範圍百分比，其目標為 100%，表示 Sales 量值所定義的實際銷售符合目標 SalesAmoutnQuota 量值所定義的配額量。 高低百分比定義於狀態列，而且選取圖形類型。  
  
 銷售經理現在可以建立樞紐分析表，將 KPI 的基底值、目標值和狀態新增至 [值] 欄位。 Employees 資料行會加入至 RowLabel 欄位，而 CalendarYear 資料行則會加入為交叉分析篩選器。  
  
 銷售經理現在可以依年份來配量每個銷售員工的實際銷售金額、銷售配額量和狀態。 她可以分析數年來銷售趨勢，決定是否需要調整銷售員工的銷售配額。  
  
##  <a name="create-and-edit-kpis"></a><a name="bkmk_create"></a>建立和編輯 Kpi  
 若要建立 KPI，請使用模型設計師中的 [關鍵效能指標] 對話方塊。 由於 KPI 必須與量值關聯，因此您可以透過擴充判斷為基底值的量值，然後建立判斷為目標值的量值或輸入絕對值，來建立 KPI。 定義基底量值 (基底值) 和目標值之後，即可定義基底值與目標值之間的狀態臨界值參數。 此狀態會以圖形格式顯示 (使用可選取的圖示、橫條、圖形或色彩)。 然後可將基底和目標值以及狀態，以可根據其他資料欄位分割的值形式加入報表或樞紐分析表。  
  
 若要檢視 [關鍵效能指標] 對話方塊，請在資料表的量值方格中，以滑鼠右鍵按一下做為基底值的量值，然後按一下 **[建立 KPI]**。 將量值擴充至 KPI 做為基底值之後，量值方格中的量值名稱旁會出現圖示，指出量值與 KPI 相關聯。  
  
##  <a name="related-tasks"></a><a name="bkmk_related_tasks"></a> 相關工作  
  
|主題|描述|  
|-----------|-----------------|  
|[建立及管理 KPI &#40;SSAS 表格式&#41;](kpis-ssas-tabular.md)|描述如何使用基底量值、目標量值及狀態臨界值建立 KPI。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SSAS 表格式&#41;的量值](measures-ssas-tabular.md)   
 [檢視方塊 &#40;SSAS 表格式&#41;](perspectives-ssas-tabular.md)  
  
  
