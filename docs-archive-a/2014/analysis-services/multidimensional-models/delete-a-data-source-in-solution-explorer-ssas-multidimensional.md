---
title: 在方案總管 (SSAS 多維度) 中刪除資料來源 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.deleteobjects.f1
helpviewer_keywords:
- data sources [Analysis Services], deleting
- deleting data sources
- removing data sources
ms.assetid: b45441ef-f909-4736-98b9-cc80d0acac99
author: minewiskan
ms.author: owend
ms.openlocfilehash: d6101c8704579894590994d88e0286197148b694
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606456"
---
# <a name="delete-a-data-source-in-solution-explorer-ssas-multidimensional"></a>在方案總管中刪除資料來源 (SSAS 多維度)
  您可以刪除資料來源物件，以便從 Analysis Services 多維度模型專案中將它永久移除。  
  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，資料來源會提供建構資料來源檢視的基礎，而接著會使用資料來源檢視，於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或資料庫中定義維度、Cube 和採礦結構。 因此，刪除資料來源會使 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中的其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件無效。 刪除物件之前，一定要檢閱所提供的相依物件清單。  
  
> [!IMPORTANT]  
>  您無法從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以線上模式開啟的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 資料庫中，刪除其他物件所相依的資料來源。 在刪除資料來源之前，您必須先刪除相依於該資料來源之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中的所有物件。 如需線上模式的詳細資訊，請參閱 [在連線模式下連接至 Analysis Services 資料庫](connect-in-online-mode-to-an-analysis-services-database.md)。  
  
### <a name="to-delete-a-data-source"></a>若要刪除資料來源  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟您想要從中刪除資料來源的專案，或是連接到您想要從中刪除資料來源的資料庫。  
  
2.  在**方案總管**中，展開 [資料來源]**** 資料夾。  
  
3.  以滑鼠右鍵按一下該資料來源，然後按一下 [刪除]****。 [刪除物件]**** 對話方塊隨即出現，其中顯示刪除資料來源之後將失效的物件。 按一下 [確定]**** 刪除資料來源之前，請先仔細檢閱這份清單。  
  
4.  儲存專案。  
  
     從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案刪除資料來源之後，您必須儲存修改過的專案，否則下次開啟此專案時會收到錯誤，因為當此專案嘗試載入已刪除的資料來源時，該資料來源的基礎 XML 檔案將會遺失。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源](data-sources-in-multidimensional-models.md)   
 [&#40;SSAS 多維度&#41;支援的資料來源](supported-data-sources-ssas-multidimensional.md)  
  
  
