---
title: 元件屬性對話方塊 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.assemblyproperties.f1
ms.assetid: da1174d6-d82b-4337-ac19-7368dbd95a84
author: minewiskan
ms.author: owend
ms.openlocfilehash: b9fdd506da42c5088b173db0981b5df94f91e5f2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593184"
---
# <a name="assembly-properties-dialog-box-analysis-services---multidimensional-data"></a>組件屬性對話方塊 (Analysis Services - 多維度資料)
  使用 **中的** [組件屬性] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 對話方塊，即可設定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫中之組件參考的屬性。 以滑鼠右鍵按一下物件總管**** 中的組件，然後選取 [屬性]****，即可顯示 [組件屬性]**** 對話方塊。  
  
## <a name="options"></a>選項  
  
|詞彙|定義|  
|----------|----------------|  
|**名稱**|鍵入即可變更組件參考的名稱。<br /><br /> 注意：變更此值並不會改變此組件參考所參考的組件名稱，但會變更 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體或資料庫在參考此組件參考時所使用的名稱。|  
|**識別碼**|顯示組件參考所參考的組件識別碼。|  
|**說明**|鍵入即可變更組件參考的描述。|  
|**建立時間戳記**|顯示建立組件參考的日期和時間。|  
|**上次結構描述更新**|顯示上次更新組件參考之中繼資料的日期和時間。|  
|**型別**|顯示組件參考的類型。 會顯示下列各值：<br /><br /> **.Net 元件**：元件參考是指 [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework 元件。<br /><br /> **COM DLL**：元件參考指的是 com 程式庫。|  
|**Source**|顯示組件參考的來源。 這個屬性通常包含組件參考所參考之組件的完整路徑和檔案名稱。|  
|**權限集合**|選取用來決定是否可以存取組件參考的權限集合。 如需有關此屬性之可用值的詳細資訊，請參閱 <xref:Microsoft.AnalysisServices.ClrAssembly.PermissionSet%2A>。|  
|**模擬資訊**|選取在存取組件參考時要使用的模擬資訊。 如需此屬性之可用值的詳細資訊，請參閱 [ImpersonationInfo 元素 &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl)|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 的設計工具和對話方塊 &#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [多維度模型組件管理](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
