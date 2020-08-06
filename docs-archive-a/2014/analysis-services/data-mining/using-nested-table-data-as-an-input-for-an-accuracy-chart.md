---
title: 使用嵌套資料表資料當做精確度圖表的輸入 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Mining Accuracy Chart [Analysis Services], nested tables
- Mining Accuracy Chart [Analysis Services], input tables
- nested tables
- adding nested tables
ms.assetid: 162e0686-ada3-4dd3-9151-9589926e6613
author: minewiskan
ms.author: owend
ms.openlocfilehash: 97d5bbd75d09b1a9e4276c4723ad6986dbabf9e4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584822"
---
# <a name="using-nested-table-data-as-an-input-for-an-accuracy-chart"></a>使用巢狀資料表當做精確度圖表的輸入
  當您使用外部資料測試採礦模型的精確度時，如果採礦模型包含巢狀資料表，則外部資料必須也包含案例資料表和相關聯的巢狀資料表。  
  
 本主題描述如何處理用於模型測試的巢狀資料表、如何對應模式和外部資料中的巢狀與案例資料表，以及如何將篩選套用至巢狀資料表。  
  
 在處理巢狀資料表時，請牢記以下要訣：  
  
-   如果選取了 **[使用採礦模型測試案例]** 或 **[使用採礦結構測試案例]** 選項，就不需要指定案例資料表或巢狀資料表。 使用這些選項時，測試資料的定義會儲存在採礦結構中，而且當您建立精確度圖表時會自動選取測試資料。  
  
-   如果資料來源中的案例與巢狀資料表之間已經有關聯性存在，則採礦結構中的資料行會自動對應到輸入資料表中的同名資料行。  
  
-   在指定案例資料表之前，無法選取巢狀資料表。 此外，除非採礦模型也使用案例資料表和巢狀資料表結構，否則您無法指定巢狀資料表當做輸入。  
  
### <a name="use-a-nested-table-as-input-to-an-accuracy-chart"></a>使用巢狀資料表當做精確度圖表的輸入  
  
1.  按兩下採礦結構，在資料採礦設計師中將它開啟。  
  
2.  選取 **[採礦精確度圖表]** 索引標籤，然後選取 **[輸入選擇]** 索引標籤。  
  
3.  在 **[選取要用於精確度圖表的資料集]** 中選取 **[指定不同的資料集]** 選項。  
  
4.  按一下 [流覽] 按鈕** ( ...] ) ** ，從目前伺服器上的資料來源視圖清單中選擇外部資料集。  
  
5.  按一下 [選取案例資料表] ****。 在 **[選取資料表]** 對話方塊中，從資料來源檢視中選取包含案例資料的資料表，然後按一下 **[確定]**。  
  
6.  按一下 **[選取巢狀資料表]**。 在 **[選取資料表]** 對話方塊中，選取包含巢狀資料的資料表，然後按一下 **[確定]**。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     如果您需要修改巢狀資料表與案例資料表之間的關聯性，請按一下 **[修改聯結]** ，開啟 **[建立關聯性]** 對話方塊。  
  
## <a name="see-also"></a>另請參閱  
 [選擇和對應模型測試資料](choose-and-map-model-testing-data.md)   
 [將篩選套用至模型測試資料](apply-filters-to-model-testing-data.md)  
  
  
