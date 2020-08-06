---
title: 定義局部加總行為 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- semiadditive
- Business Intelligence enhancements [Analysis Services], semiadditive behavior
- measures [Analysis Services], semiadditive
ms.assetid: b25726bc-728b-4601-ad87-9015c39dc615
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9c2028c350046fdcc9f98bcd0f0612d6a91ccabb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596384"
---
# <a name="define-semiadditive-behavior"></a>定義局部加總行為
  在許多商務狀況中，經常見到局部加總量值並未跨所有維度一致地彙總。 每個以不同時間之結餘快照集為基礎的 Cube 都會出現這個問題。 您可以在處理安全性、帳戶結餘、預算、人力資源、保險政策和理賠、以及其他許多商務領域的應用程式中發現這些快照集。  
  
 將局部加總行為加入 Cube，以定義個別量值或帳戶類型屬性成員的彙總方法。 如果 Cube 包含帳戶維度，您可以根據帳戶類型自動設定局部加總行為。  
  
 若要加入局部加總行為，請在 Cube 設計師中開啟 Cube，然後從 [Cube] 功能表中選擇 [加入商業智慧]****。 請在 [商業智慧精靈] 中，選取 [選擇增強功能]**** 頁面上的 [定義局部加總行為]**** 選項。 然後，此精靈會引導您逐步完成識別具有局部加總行為的量值。  
  
 除了 Standard 版中提供的 LastChild 之外，只有商業智慧或 Enterprise 版中提供局部加總行為。  
  
## <a name="define-semiadditive-behavior"></a>定義局部加總行為  
 在精靈的 [定義局部加總行為]**** 頁面上，選取下列其中一個選項來選擇如何定義局部加總：  
  
 **關閉局部加總行為**  
 從先前定義局部加總行為的 Cube 中移除局部加總行為。 如果量值設成下列任何彙總函式類型，此選取項目會將其重設為 `SUM`：  
  
-   依帳戶  
  
-   子系的平均  
  
-   第一個子系  
  
-   最後一個子系  
  
-   最後一個非空白子系  
  
-   第一個非空白子系  
  
-   無  
  
 此選項不會變更具有一般彙總函式的量值： `Sum` 、 `Min` 、 `Max` 、 `Count` 或 `Distinct``Count` 。  
  
 **此 wizard 偵測到「帳戶」帳戶維度，其中包含局部加總成員。伺服器會根據為每個帳戶類型指定的局部加總行為，來匯總此維度的成員。**  
 讓系統將帳戶類型維度所建立維度之量值群組中的所有量值設定為「依帳戶」彙總函式，而且伺服器將會根據每一個帳戶類型所指定之局部加總行為來彙總此維度的成員。  
  
> [!NOTE]  
>  依預設，如果精靈偵測到帳戶類型維度，這個選項為已選取。  
  
 **定義個別量值的局部加總行為**  
 個別選取每個量值的局部加總行為。 預設值為 `SUM` (完整加總)。  
  
> [!NOTE]  
>  依預設，如果精靈沒有偵測到帳戶類型維度，這個選項為已選取。  
  
 針對每個量值，您可以從下表描述之局部加總功能的類型進行選取。  
  
|局部加總函數|描述|  
|---------------------------|-----------------|  
|子系的平均|成員的彙總是其子系的平均。|  
|ByAccount|系統會讀取帳戶類型所指定的局部加總行為。|  
|計數|此彙總為成員的計數。|  
|Distinct Count|此彙總為唯一成員的計數。|  
|第一個子系|成員值判斷為時間維度第一個子系的值。|  
|FirstNonEmpty|成員值判斷為包含資料之時間維度第一個子系的值。|  
|LastChild|成員值判斷為時間維度最後一個子系的值。|  
|LastNonEmpty|成員值判斷為包含資料之時間維度最後一個子系的值。|  
|最大值|套用標準最大彙總函式。|  
|最小值|套用標準最小彙總函式。|  
|無|不套用任何彙總。|  
|加總|套用標準總和函數。|  
  
 當精靈完成時，會覆寫全部現有的局部加總行為。  
  
  
