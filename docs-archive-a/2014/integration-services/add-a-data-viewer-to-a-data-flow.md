---
title: 將資料檢視器加入至資料流程 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data viewers [Integration Services]
- data flow [Integration Services], data viewers
- adding data viewers
ms.assetid: 5e573274-a170-4132-bfc8-a8ff3a8411e4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7abd76417552ec50da736afe024a5ae36ee6a2ae
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585538"
---
# <a name="add-a-data-viewer-to-a-data-flow"></a>將資料檢視器加入資料流程
  本主題描述如何在資料流程中加入和設定資料檢視器。 資料檢視器可以顯示在兩個資料流程元件之間移動的資料。 例如，在資料流程中的轉換修改從資料來源擷取的資料之前，資料檢視器可以先顯示該資料。  
  
 將一個資料流程元件的輸出與另一元件的輸入連接，路徑可連接資料流程中的元件。  
  
 在可以將資料檢視器加入封裝之前，該封裝必須包括「資料流程」工作和至少兩個連接的資料流程元件。  
  
### <a name="to-add-a-data-viewer-to-a-data-flow"></a>若要將資料檢視器加入資料流程  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  如果 [控制流程]  索引標籤尚未處於使用中，請按一下該索引標籤。  
  
4.  按一下要將資料檢視器附加至其資料流程的 [資料流程] 工作，然後按一下 [資料流程]  索引標籤。  
  
5.  以滑鼠右鍵按一下兩個資料流程元件之間的路徑，然後按一下 [編輯]  。  
  
6.  在 [一般]  頁面上，您可以檢視和編輯路徑屬性。 例如，您可以從 [PathAnnotation]  下拉式清單選取出現在路徑旁的註解。  
  
7.  在 [中繼資料]  頁面上，您可以檢視資料行中繼資料，並且將中繼資料複製到 [剪貼簿]。  
  
8.  在 [資料檢視器]  頁面上，按一下 [啟用資料檢視器]  。  
  
9. 在 [要顯示的資料行] 區域中，選取要在資料檢視器中顯示的資料行。 根據預設，所有可用的資料行都會選取，並且在 [顯示的資料行]  清單中列出。 將不想使用的資料行移至 [未使用的資料行]  清單，方法是選取它們然後按一下向左箭號。  
  
    > [!NOTE]  
    >  在此方格中，代表 DT_DATE、DT_DBTIME2、DT_FILETIME、DT_DBTIMESTAMP、DT_DBTIMESTAMP2 和 DT_DBTIMESTAMPOFFSET 資料類型的值會以 ISO 8601 格式化字串的形式出現，而且空格分隔符號會取代 `T` 分隔符號。 代表 DT_DATE 和 DT_FILETIME 資料類型的值包括小數秒的七位數。 由於 DT_FILETIME 資料類型只會儲存小數秒的三位數，所以此方格會將其餘四位數顯示為零。 代表 DT_DBTIMESTAMP 資料類型的值包括小數秒的三位數。 如果是代表 DT_DBTIME2、DT_DBTIMESTAMP2 和 DT_DBTIMESTAMPOFFSET 資料類型的值，則小數秒的位數會對應到針對資料行資料類型指定的小數位數。 如需 ISO 8601 格式的詳細資訊，請參閱 [日期和時間格式](../../2014/integration-services/date-and-time-formats.md)。 如需有關資料類型的詳細資訊，請參閱＜ [Integration Services Data Types](data-flow/integration-services-data-types.md)＞。  
  
10. 按一下 [確定]  。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 轉換](data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 路徑](data-flow/integration-services-paths.md)   
 [資料流程](data-flow/data-flow.md)   
 [偵錯資料流程](troubleshooting/debugging-data-flow.md)  
  
  
