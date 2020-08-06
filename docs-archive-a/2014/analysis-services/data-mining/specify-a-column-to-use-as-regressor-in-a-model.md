---
title: 在模型中指定當做回歸輸入變數使用的資料行 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d8e0cb8e-302a-4166-9ed0-e2d9e2919b0a
author: minewiskan
ms.author: owend
ms.openlocfilehash: 86899d3793985b5e3c07618360d7b6a540935a54
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584830"
---
# <a name="specify-a-column-to-use-as-regressor-in-a-model"></a>在模型中指定當做迴歸輸入變數使用的資料行
  線性迴歸模型會把可預測屬性的值表示為公式的結果，此公式結合輸入的方式會使資料盡可能地貼近預估迴歸線。 這種演算法只接受數值當做輸入，而且會自動偵測提供最佳解的輸入。  
  
 不過，您可以藉由將 FORCE_REGRESSOR 參數加入模型並且指定所使用的迴歸輸入變數，指定將資料行包含為迴歸輸入變數。 當屬性具有某種意義 (即使其效果過小而無法由模型偵測出來)，或者您想要確保屬性包含在公式中時，就可以這麼做。  
  
 下列程序描述如何使用 [類神經網路教學課程](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)所使用的相同範例資料來建立簡單的線性迴歸模型。 此模型不一定很強固，但可以示範如何使用資料採礦設計師自訂線性迴歸模型。  
  
### <a name="how-to-create-a-simple-linear-regression-model"></a>如何建立簡單的線性迴歸模型  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的**方案總管**中，展開 [採礦結構]****。  
  
2.  在設計師中按兩下 Call Center.dmm 將其開啟。  
  
3.  從 [採礦模型]**** 功能表選取 [新增採礦模型]****。  
  
4.  針對演算法選取 [Microsoft 線性迴歸]****。 輸入「撥接中心迴歸」**** 當作名稱。  
  
5.  按照下列指示，在 [採礦模型]**** 索引標籤中變更資料行的使用方式。 未列於下列清單的所有資料行都應該設定為 [忽略]**** (若尚未設定)。  
  
     FactCallCenterID**Key**  
  
     ServiceGrade**PredictOnly**  
  
     Total Operators**Input**  
  
     AverageTimePerIssue**Input**  
  
6.  從 [採礦模型]**** 功能表選取 [Set Model Parameters (設定模型參數)]****。  
  
7.  針對 FORCE_REGRESSOR 參數，在 [值]**** 資料行中輸入資料行名稱 (將名稱放入方括弧並以逗號分隔)，如下所示：  
  
    ```  
    [Average Time Per Issue],[Total Operators]  
    ```  
  
    > [!NOTE]  
    >  演算法將會自動偵測可做為最佳迴歸輸入變數的資料行。 當您想要確定最終公式中是否包含了某資料行時，只需強制使用迴歸輸入變數即可。  
  
8.  從 [採礦模型]**** 功能表選取 [處理模型]****。  
  
     在檢視器中，模型會以包含迴歸公式的單一節點來表示。 您可以在 [採礦圖例]**** 中檢視公式，或者也可以藉由使用查詢來擷取公式的係數。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 線性回歸演算法](microsoft-linear-regression-algorithm.md)   
 [資料採礦查詢](data-mining-queries.md)   
 [Microsoft 線性回歸演算法技術參考](microsoft-linear-regression-algorithm-technical-reference.md)   
 [線性迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
