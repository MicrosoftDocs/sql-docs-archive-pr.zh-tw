---
title: 隱藏或刪除衍生階層中的層級 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- derived hierarchies, hiding levels
- derived hierarchies, deleting levels
ms.assetid: e00582b9-9415-4b66-b4a7-9f590d83875f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 039b05633bcd1fdc69d226e565b3dc5211e9734f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597185"
---
# <a name="hide-or-delete-levels-in-a-derived-hierarchy-master-data-services"></a>隱藏或刪除衍生階層中的層級 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，當您要求群組的層級但是不需要顯示該層級時，請在衍生階層中隱藏該層級。 當您不想要使用層級來群組時，請將它刪除。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
### <a name="to-hide-or-delete-levels-in-a-derived-hierarchy"></a>若要隱藏或刪除衍生階層中的層級  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [**模型視圖**] 頁面上，從功能表列指向 [**管理**]，然後按一下 [**衍生**階層]。  
  
3.  在 [衍生階層維護]**** 頁面上，選取 [模型]**** 清單中的模型。  
  
4.  選取要編輯之衍生階層的資料列。  
  
5.  按一下 [**編輯選取的衍生**階層]。  
  
6.  在 [目前層級]**** 窗格中：  
  
    -   若要隱藏層級，請按一下頂端或底端以外的層級。 從 [可見]**** 清單中，選取 [否]****。 然後按一下 [儲存選取的階層項目]****。  
  
    -   若要刪除最上層，請按一下 [刪除選取的階層項目]****。 在確認對話方塊中按一下 **[確定]**。 您可以只刪除最上層。  
  
## <a name="see-also"></a>另請參閱  
 [在階層中移動成員 &#40;Master Data Services&#41;](../../2014/master-data-services/move-members-within-a-hierarchy-master-data-services.md)   
 [衍生階層 &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)  
  
  
