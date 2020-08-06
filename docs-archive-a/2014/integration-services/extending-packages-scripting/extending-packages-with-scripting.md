---
title: 使用指令碼擴充封裝 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- SQL Server Integration Services, scripting
- SSIS, scripting
- scripts [Integration Services], about scripting
ms.assetid: 67fe18ef-f3aa-41d4-9b9d-5defd4618c4b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3bc3aac2483a29a686f8a2c4dfbf0688c5810546
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704313"
---
# <a name="extending-packages-with-scripting"></a>使用指令碼擴充封裝
  如果您發現 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的內建元件不符合需求，可以透過撰寫自己的延伸模組，擴充 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的功能。 您有兩個完全不同的選項可擴充封裝：其一是在指令碼工作與指令碼元件所提供的強大包裝函數中撰寫程式碼；其二則是可以從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型提供的基底類別衍生，從頭建立自訂 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 延伸模組。

 本節探索兩者中較簡單的選項：以指令碼擴充套件。

 指令碼工作和指令碼元件可讓您利用非常少量的編碼，同時擴充 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的控制流程和資料流程。 這兩個物件都使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 開發環境與 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 程式設計語言，且可從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 類別庫提供的所有功能以及自訂組件獲益。 通常在開發自訂工作或自訂資料流程元件時，需要撰寫所有的基礎結構程式碼。指令碼工作和指令碼元件可讓開發人員不需要撰寫全部的基礎結構程式碼，即可建立自訂功能。

## <a name="in-this-section"></a>本節內容
 [比較腳本工作和腳本元件](../extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)討論腳本工作與腳本元件之間的相似性和差異。

 [比較腳本解決方案和自訂物件](comparing-scripting-solutions-and-custom-objects.md)討論在腳本方案和開發自訂物件之間選擇時要使用的準則。

 [參考腳本解決方案中的其他元件](referencing-other-assemblies-in-scripting-solutions.md)討論在腳本專案中參考和使用外部元件和命名空間所需的步驟。

 [使用腳本工作擴充封裝](../extending-packages-scripting/task/extending-the-package-with-the-script-task.md)討論如何使用腳本工作來建立自訂工作。 通常會在每個封裝執行時呼叫工作，或是在封裝開啟每個資料來源時呼叫一次。

 [使用腳本元件擴充資料流程](data-flow-script-component/extending-the-data-flow-with-the-script-component.md)討論如何使用腳本元件建立自訂的資料流程來源、轉換和目的地。 資料流程元件通常會為處理的每個資料列呼叫一次。

## <a name="reference"></a>參考
 [Integration Services 錯誤和訊息參考](../integration-services-error-and-message-reference.md)列出預先定義的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 錯誤碼及其符號名稱和描述。

## <a name="related-sections"></a>相關章節
 [使用自訂物件擴充封裝](../extending-packages-custom-objects/extending-packages-with-custom-objects.md)討論如何建立程式自訂工作、資料流程元件以及其他封裝物件，以便在多個封裝中使用。

 [以程式設計方式建立套件](../building-packages-programmatically/building-packages-programmatically.md)描述如何以程式設計方式建立、設定、執行、載入、儲存和管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。

![Integration Services 圖示 (小型) ](../media/dts-16.gif "Integration Services 圖示 (小)")會**保持最**新狀態 Integration Services  <br /> 若要取得 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 的最新下載、文件、範例和影片以及社群中的選定方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。

## <a name="see-also"></a>另請參閱
 [SQL Server Integration Services](../sql-server-integration-services.md)


