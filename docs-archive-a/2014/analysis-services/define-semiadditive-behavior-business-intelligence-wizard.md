---
title: 定義) 的商業智慧 Wizard (局部加總行為 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.semiadditivememberdetection.f1
ms.assetid: e57080ba-ce96-40f8-bca7-6701d1725b3c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5a3c46de038a7e45dcb39805e324260676a03228
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687354"
---
# <a name="define-semiadditive-behavior-business-intelligence-wizard"></a>定義局部加總行為 (商業智慧精靈)
  使用 [定義局部加總行為]**** 頁面，即可啟用或停用量值的局部加總行為。 局部加總行為會決定 Cube 所包含的維度，將如何在時間維度上進行彙總。  
  
> [!NOTE]  
>  除了 Standard 版中提供的 LastChild 之外，只有商業智慧或 Enterprise 版中提供局部加總行為。 此外，由於局部加總行為只會定義在量值上，而不會定義在維度上，如果此行為之前是從維度設計師啟動，或是以滑鼠右鍵按一下 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中方案總管的某維度來啟動，則此頁面將不會出現在商業智慧精靈中。  
  
## <a name="options"></a>選項  
 **關閉局部加總行為**  
 停用 Cube 所包含之所有量值中的局部加總行為。  
  
 **Wizard 已偵測到包含局部加總 \<dimension name> 成員的帳戶維度。伺服器會根據為每個帳戶類型指定的局部加總行為，來匯總此維度的成員。**  
 針對包含局部加總成員的帳戶維度，啟用局部加總行為。 選取此選項會將參考帳戶維度之量值群組中所有量值的彙總函式設定為 `ByAccount`。  
  
 如需帳戶維度的詳細資訊，請參閱 [建立父子式類型維度的財務帳戶](multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)。  
  
 **定義個別成員的局部加總行為**  
 啟用局部加總行為，並為特定量值指定局部加總彙總函式。 彙總函式適用於包含量值之量值群組所參考的所有維度。  
  
 **評估**  
 顯示 Cube 所包含之量值的名稱。  
  
 **局部加總函數**  
 為選取的量值選取彙總函式。 下表列出可用的彙總函式。  
  
|值|描述|  
|-----------|-----------------|  
|**AverageOfChildren**|藉由傳回量值之子系的平均值來進行彙總。|  
|`ByAccount`|藉由與帳戶維度中屬性之指定帳戶類型相關聯的彙總函式來進行彙總。|  
|`Count`|使用 `Count` 函數來進行彙總。|  
|`DistinctCount`|使用 `DistinctCount` 函數來進行彙總。|  
|**FirstChild**|藉由傳回量值在某個時間維度的第一個子成員進行彙總。|  
|**FirstNonEmpty**|藉由傳回量值在某個時間維度的第一個非空白成員進行彙總。|  
|**LastChild**|藉由傳回量值在某個時間維度的最後一個子成員進行彙總。|  
|**LastNonEmpty**|藉由傳回量值在某個時間維度的最後一個非空白成員進行彙總。|  
|`Max`|使用 `Max` 函數來進行彙總。|  
|`Min`|使用 `Min` 函數來進行彙總。|  
|**None**|不執行彙總。|  
|`Sum`|使用 `Sum` 函數來進行彙總。|  
  
> [!NOTE]  
>  唯有在選取 [定義個別成員的局部加總行為]**** 之後，才適用於針對此選項所做的選擇。  
  
## <a name="see-also"></a>另請參閱  
 [商業智慧 Wizard F1 說明](business-intelligence-wizard-f1-help.md)   
 [Cube 設計工具 &#40;Analysis Services-多維度資料&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [維度設計師 &#40;Analysis Services 多維資料&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
