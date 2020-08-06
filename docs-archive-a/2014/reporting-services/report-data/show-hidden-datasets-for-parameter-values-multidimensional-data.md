---
title: 針對多維度資料 (報表產生器和 SSRS) 的參數值顯示隱藏的資料集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: eb01c4ca-4fd6-4629-b595-f0d2565915df
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6f9c005b6e7c8927316c19a3302e32f4407f9885
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87710214"
---
# <a name="show-hidden-datasets-for-parameter-values-for-multidimensional-data-report-builder-and-ssrs"></a>針對多維度資料的參數值顯示隱藏的資料集 (報表產生器及 SSRS)
  您的報表可能包含自動產生的資料集 (也稱為隱藏的資料集)，而這些資料集預設不會顯示在 [報表資料] 窗格中。 這些資料集是以下列方式建立的：  
  
-   在多維度資料庫的某些查詢設計工具中，您可以在查詢窗格的篩選區域中指定要篩選的欄位，然後選取是否要建立篩選的查詢參數。 如果您選取參數選項，系統就會自動建立報表資料集，以便提供報表參數的有效值。  
  
-   如果您匯入了以多維度資料庫為基礎的查詢，可能也會在報表中加入隱藏的資料集。  
  
 您無法從精靈使用隱藏的資料集。  
  
 您可以在 [報表資料] 窗格中變更檢視，以便顯示報表中的所有資料集。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-hidden-datasets"></a>顯示隱藏的資料集  
  
-   在 [報表資料] 窗格中，以滑鼠右鍵按一下 [資料集] 資料夾，然後按一下 [顯示隱藏資料集]  。  
  
## <a name="see-also"></a>另請參閱  
 [查詢設計工具 &#40;報表產生器&#41;](../query-designers-report-builder.md)   
 [Reporting Services 查詢設計工具](../reporting-services-query-designers.md)   
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [將資料加入報表 &#40;報表產生器和 SSRS&#41;](report-datasets-ssrs.md)  
  
  
