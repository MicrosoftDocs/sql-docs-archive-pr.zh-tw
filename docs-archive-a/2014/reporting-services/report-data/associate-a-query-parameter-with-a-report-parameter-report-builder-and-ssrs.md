---
title: 建立查詢參數與報表參數的關聯 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- queries [Reporting Services], parameters
- parameters [Reporting Services], queries
ms.assetid: 6d297e1a-ff71-472a-addc-349e863092b5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f65aa36e8910378d68963c8c9990518b661025ab
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688617"
---
# <a name="associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs"></a>將查詢參數與報表參數產生關聯 (報表產生器及 SSRS)
  當您定義包含查詢變數的資料集查詢時，就會剖析查詢命令。 系統會針對每個查詢變數建立對應的資料集參數和報表參數。 資料集參數會指向報表參數。 如此可讓使用者輸入一個值來直接傳遞給查詢。 每次您編輯查詢命令時，系統都會進行相同的程序。  
  
 如果您重新命名繫結至查詢參數的報表參數，您需要使用本主題的查詢，手動將查詢參數連結到重新命名過的報表參數。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-associate-a-query-parameter-with-a-report-parameter"></a>將查詢參數與報表參數相關聯  
  
1.  在 [報表資料] 窗格中，以滑鼠右鍵按一下資料集，然後按一下 [資料集屬性]****，再按一下 [參數]****。  
  
    > [!NOTE]  
    >  如果看不到 [報表資料] 窗格，請按一下 [檢視]**** 功能表上的 [報表資料]****。  
  
2.  在 [參數名稱]**** 資料行中，尋找查詢參數的名稱。 參數名稱會依據查詢自動填入。 每當您變更查詢時，系統都會檢查查詢，看看是否有新的查詢參數。 當查詢變更時，您手動建立的查詢參數並不會變更。  
  
    -   在 [參數名稱]**** 中，尋找存在於查詢中的查詢參數名稱。 您也可以手動加入新的查詢參數，並輸入名稱。  
  
    -   在 [參數值]**** 中，鍵入或選取會評估為要傳遞到查詢參數之值的運算式。 這通常是報表參數的名稱。  
  
        > [!NOTE]  
        >  並非只有報表參數才能做為查詢參數的值。 您可以使用任何會評估為值的運算式，以做為參數值。  
  
3.  重複步驟 2 可以加入其他查詢參數。  
  
## <a name="see-also"></a>另請參閱  
 [報表內嵌資料集和共用資料集 &#40;報表產生器和 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [報表參數概念 &#40;報表產生器和 SSRS&#41;](../report-design/report-parameters-concepts-report-builder-and-ssrs.md)  
  
  
