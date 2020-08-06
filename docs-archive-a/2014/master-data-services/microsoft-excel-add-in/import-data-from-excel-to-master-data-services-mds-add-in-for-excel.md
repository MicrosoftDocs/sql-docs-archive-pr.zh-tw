---
title: 將 Excel 中的資料發佈到 MDS (適用于 Excel 的 MDS 增益集) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 89fce454-a816-4b33-a26a-d1b9741d269b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 597a954760816d8938628974998fe8f6daad1af5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599036"
---
# <a name="publish-data-from-excel-to-mds-mds-add-in-for-excel"></a>將資料從 Excel 發行至 MDS (適用於 Excel 的 MDS 增益集)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，若您已結束使用 Excel 且想要儲存變更，以讓其他使用者能夠存取，請將資料發行至 MDS 儲存機制。  
  
> [!NOTE]
>  -   當您發行變更時，系統會刪除 MDS 管理之資料格的註解。  
> -   MDS 管理的資料格中不支援公式。 MDS 管理之資料格中的公式會處理為文字值。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 [ **Explorer** ] 功能區域的許可權。  
  
-   使用中工作表必須包含 MDS 管理的資料，而且您必須已經對 MDS 管理的資料進行變更或加入作業。  
  
-   如果您要加入成員，而且系統會自動產生實體的代碼，您就不需要指定 **Code** 值。 如需詳細資訊，請參閱[自動建立程式碼 &#40;Master Data Services&#41;](../automatic-code-creation-master-data-services.md)。  
  
### <a name="to-publish-data-to-the-mds-repository"></a>若要將資料發行至 MDS 儲存機制  
  
1.  按一下 [發行和驗證]**** 群組中的 [發行]****。  
  
2.  選擇性。 如果顯示 [發行並註解]**** 對話方塊，請選擇要針對所有更新共用相同的註解，還是個別註解每個變更。  
  
3.  選擇性。 選取 [不要再顯示這個對話方塊]**** 核取方塊。 未來，您隨時都可以透過選擇 [設定]**** 並選取 [發行時顯示發行和註解對話方塊]**** 核取方塊，顯示此對話方塊。  
  
4.  按一下 [發佈]。  
  
> [!NOTE]  
>  如果您要將新的成員 (資料列) 加入至工作表，但是無法順利將它們發行至 MDS 儲存機制，表示您可能沒有工作表中所有屬性的 [更新]**** 權限。 在 [檢閱]**** 索引標籤上，按一下 [變更]**** 群組中的 [取消保護工作表]****，再次嘗試發行。  
  
## <a name="next-steps"></a>後續步驟  
 [套用商務規則 &#40;適用於 Excel 的 MDS 增益集&#41;](apply-business-rules-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>另請參閱  
 [發行資料 &#40;適用于 Excel 的 MDS 增益集&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)   
 [驗證資料 &#40;適用於 Excel 的 MDS 增益集&#41;](validating-data-mds-add-in-for-excel.md)  
  
  
