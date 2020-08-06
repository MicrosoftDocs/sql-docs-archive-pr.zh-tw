---
title: 報表參數概念 (報表產生器和 SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: b0aa2159-4e49-4713-8824-5ef9a9edbc62
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4b740362daea83b50a62f0b4453ce818ab21ace7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688573"
---
# <a name="report-parameters-concept-report-builder-and-ssrs"></a>報表參數概念 (報表產生器及 SSRS)
  您可以將參數加入至報表，以便連結相關報表、控制報表外觀、篩選報表資料，或是將報表的範圍縮小至特定使用者或位置。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 報表參數是透過下列方式建立：  
  
-   當您定義包含查詢變數的資料集查詢時自動建立。 系統會針對每個查詢變數建立具有相同名稱的對應資料集查詢參數和報表參數。 查詢參數可能是查詢變數的參考，或預存程序之輸入參數的參考。  
  
-   當您加入包含查詢參數之共用資料集的參考時自動建立。  
  
-   當您在 [報表資料] 窗格中建立報表參數時手動建立。 報表是您可以在報表的運算式中包含的其中一個內建集合。 運算式是用來定義整個報表定義中的值，因此，您可以使用參數來控制報表外觀，或將值傳遞到也使用參數的相關子報表或報表中。  
  
 如需詳細資訊，請參閱 MSDN 上的 [報表參數 &#40;報表產生器和報表設計師&#41;](report-parameters-report-builder-and-report-designer.md)類型之報表資料來源為基礎的資料集。  
  
 在將資料傳回報表之前和之後，通常會使用參數來篩選報表資料。 如需詳細資訊，請參閱 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)(將互動式排序加入資料表或矩陣 (報表產生器及 SSRS))。  
  
 當您設計報表時，報表參數會儲存在報表定義中。 當您發行報表時，報表參數會儲存，並且與報表定義分開管理。 將報表儲存到報表伺服器之後，您可以執行下列操作：  
  
-   直接在報表伺服器上，從報表定義個別變更報表參數值。  
  
-   建立多個連結報表，其中每個連結報表都是一個報表定義的連結，這些報表定義中包含一組個別的參數值，您可以在報表伺服器上分別管理這些參數值。  
  
 如果您打算建立報表快照集、記錄或已發行報表的訂閱，則必須了解報表參數如何影響報表的設計需求。  
  
## <a name="see-also"></a>另請參閱  
 [報表撰寫概念 &#40;報表產生器和 SSRS&#41;](report-authoring-concepts-report-builder-and-ssrs.md)   
 [報表內嵌資料集和共用資料集 &#40;報表產生器和 SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [教學課程：將參數加入至報表 &#40;報表產生器&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)  
  
  
