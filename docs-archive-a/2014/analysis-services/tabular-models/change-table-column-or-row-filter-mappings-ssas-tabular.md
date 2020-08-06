---
title: " (SSAS 表格式) 變更資料表、資料行或資料列篩選對應 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2124c526-5772-4f84-a019-9dd3e906e8dd
author: minewiskan
ms.author: owend
ms.openlocfilehash: d8a597fb51804ea12caace63f3308b07bffc5899
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594707"
---
# <a name="change-table-column-or-row-filter-mappings-ssas-tabular"></a>變更資料表、資料行或資料列篩選對應 (SSAS 表格式)
  本主題描述如何在 **中使用** [編輯資料表屬性] [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]對話方塊來變更資料表、資料行或資料列篩選對應。  
  
 視您一開始是透過從清單中選取資料表或使用 SQL 查詢匯入資料而定， **[編輯資料表屬性]** 對話方塊的選項都不同。 若您一開始是從清單中選取來匯入資料， **[編輯資料表屬性]** 對話方塊就會顯示資料表預覽模式。 這種模式僅會顯示來源資料表的前五十個資料列。 若您一開始是使用 SQL 陳述式匯入資料， **[編輯資料表屬性]** 對話方塊就只會顯示 SQL 陳述式。 若是使用 SQL 查詢陳述式，您可以設計篩選或以手動方式編輯 SQL 陳述式，只擷取資料列的子集。  
  
 如果您將來源變更為具有與目前資料表不同之資料行的資料表，就會顯示資料行不同的警告訊息。 然後，您必須選取要放入目前資料表中的資料行，並按一下 **[儲存]**。 您可以選取資料表左邊的核取方塊，以取代整個資料表。  
  
> [!NOTE]  
>  如果您的資料表有多個資料分割，您無法使用 [編輯資料表屬性] 對話方塊變更資料列篩選對應。 若要針對具有多個資料分割的資料表變更資料列篩選對應，請使用資料分割管理員。 如需詳細資訊，請參閱 [資料分割 &#40;SSAS 表格式&#41;](partitions-ssas-tabular.md)。  
  
#### <a name="to-change-table-column-or-row-filter-mappings"></a>變更資料表、資料行或資料列篩選對應  
  
1.  在模型設計師中，按一下資料表，然後按一下 **[資料表]** 功能表，再按一下 **[資料表屬性]**。  
  
2.  在 **[編輯資料表屬性]** 對話方塊中，找出包含您所要篩選之準則的資料行，再按一下資料行標題右邊的向下箭號。  
  
3.  在 [**自動篩選**] 功能表中，執行下列其中一項：  
  
    -   在資料行值清單中，選取或清除做為篩選依據的一個或多個值，然後按一下 [確定]。  
  
         如果值的數量非常大，在清單中可能不會顯示個別的項目。 但是您會看到「要顯示的項目太多」這個訊息。  
  
    -   按一下 [數字篩選]**** 或 [文字篩選]**** (視資料行的類型而定)，然後按一下其中一個比較運算子命令 (例如 [等於])，或按一下 [自訂篩選]。 在 **[自訂篩選]** 對話方塊中，建立篩選，然後按一下 **[確定]**。  
  
         如果發生錯誤而需要從頭開始，請按一下 **[清除資料列篩選]**。  
  
## <a name="see-also"></a>另請參閱  
 [編輯資料表屬性對話方塊 &#40;SSAS&#41;](../edit-table-properties-dialog-box-ssas.md)  
  
  
