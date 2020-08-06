---
title: 建立自訂資料流程元件 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- design-time component interface [Integration Services]
- custom data flow components [Integration Services], about data flow components
- custom data flow components [Integration Services]
- data flow components [Integration Services]
- data flow components [Integration Services], developing
ms.assetid: 9d96bcf5-eba8-44bd-b113-ed51ad0d0521
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 110d07ff88707ad1a01f299b6f532df99ce58404
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597231"
---
# <a name="creating-a-custom-data-flow-component"></a>建立自訂資料流程元件
  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中，資料流程工作會公開物件模型，讓開發人員透過使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 與受控碼來建立自訂資料流程元件 (來源、轉換和目的地)。  
  
 資料流程工作是由兩個元件所組成：<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 介面以及定義元件之間資料移動的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 物件之集合。  
  
> [!NOTE]  
>  建立自訂提供者時，您需要使用中繼資料資料行值更新 ProviderDescriptors.xml 檔。  
  
## <a name="design-time-and-run-time"></a>設計階段與執行階段  
 據說在執行之前，資料流程工作會設計狀態階段進行累加變更。 變更可包括元件的加入或移除、連接元件的路徑物件之加入或移除，以及對於元件中繼資料的變更。 當中繼資料變更發生時，元件可以監視變更並對其做出反應。 例如，元件可以不允許某些變更，或是做其他變更以回應變更。 在設計階段，設計工具會透過設計階段 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 介面與元件互動。  
  
 在執行時，資料流程工作會檢查元件的順序、準備執行計劃以及管理執行工作計劃的工作者執行緒集區。 雖然每個工作者執行緒都會執行資料流程工作內部的某些工作，但是工作者執行緒的主要工作是透過執行階段 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100> 介面來呼叫元件的方法。  
  
## <a name="creating-a-component"></a>建立元件  
 若要建立資料流程元件，您可以從 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 基底類別衍生類別、套用 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 類別，然後覆寫基底類別的適當方法。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 與 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100> 介面，並為您公開其方法以便在元件中覆寫。  
  
 視您的元件使用的物件而定，專案將需要參考下列組件的某些或是全部：  
  
|功能|要參考的組件|要匯入的命名空間|  
|-------------|---------------------------|-------------------------|  
|設計師中|Microsoft.SqlServer.PipelineHost|<xref:Microsoft.SqlServer.Dts.Pipeline>|  
|資料流程包裝函數|Microsoft.SqlServer.DTSPipelineWrap|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>|  
|執行階段|Microsoft.SQLServer.ManagedDTS|<xref:Microsoft.SqlServer.Dts.Runtime>|  
|執行階段包裝函數|Microsoft.SqlServer.DTSRuntimeWrap|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper>|  
  
 下列程式碼範例顯示從基底類別衍生的簡單元件，並套用 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>。 您需要加入 DTSPipelineWrap 組件的參考。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "SampleComponent", ComponentType = ComponentType.Transform )]  
    public class BasicComponent: PipelineComponent  
    {  
        // TODO: Override the base class methods.  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
<DtsPipelineComponent(DisplayName:="SampleComponent", ComponentType:=ComponentType.Transform)> _  
Public Class BasicComponent  
  
    Inherits PipelineComponent  
  
    ' TODO: Override the base class methods.  
  
End Class  
```  
  
![Integration Services 圖示 (小型) ](../../media/dts-16.gif "Integration Services 圖示 (小)")會**保持最**新狀態 Integration Services  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [開發資料流程元件的使用者介面](developing-a-user-interface-for-a-data-flow-component.md)  
  
  
