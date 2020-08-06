---
title: 建立和管理 (SSAS 表格式) 的階層 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8dd30cd0-a831-4d25-b577-648d7f3c7fa6
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0bab3e09aadb4e0c857b9c1da3111e03e90f777e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594214"
---
# <a name="create-and-manage-hierarchies-ssas-tabular"></a>建立及管理階層 (SSAS 表格式)
  您可以在 [圖表檢視] 中，透過模型設計師建立及管理階層。 若要在 [圖表檢視] 中檢視模型設計師，請按一下 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的 [模型]**** 功能表，然後指向 [模型檢視]****，再按一下 [圖表檢視]****。  
  
 本主題也包括下列工作：  
  
-   [建立階層](#bkmk_create)  
  
-   [編輯階層](#bkmk_edit)  
  
-   [刪除階層](#bkmk_delete)  
  
##  <a name="create-a-hierarchy"></a><a name="bkmk_create"></a> 建立階層  
 您可以使用資料行和資料表內容功能表建立階層。 當您建立階層時會顯示新的父層級，而所選的資料行則做為子層級。  
  
#### <a name="to-create-a-hierarchy-from-the-context-menu"></a>從內容功能表建立階層  
  
1.  在模型設計師 ([圖表檢視]) 的資料表視窗中，以滑鼠右鍵按一下資料行，然後按一下 [建立階層]****。  
  
     若要選取多個資料行，請按一下每個資料行，然後按一下滑鼠右鍵開啟內容功能表，再按一下 [建立階層]****。  
  
     資料表視窗底部會建立父階層層級，並將所選的資料行複製到階層下做為子層級。  
  
2.  輸入階層的名稱。  
  
 您可以將其他資料行拖曳至階層的父層級，這會複製資料行。 將子層級置於階層中要顯示的位置。  
  
> [!NOTE]  
>  如果您複選量值及一個或多個資料行，或者選取多個資料表的資料行，即會停用內容功能表中的 [建立階層] 命令。  
  
##  <a name="edit-a-hierarchy"></a><a name="bkmk_edit"></a>編輯階層  
 您可以重新命名階層、重新命名子層級、變更子層級順序、加入其他資料行做為子層級、從階層移除子層級、顯示子層級的來源名稱 (資料行名稱)，以及隱藏子層級 (如果它與階層父層級同名)。  
  
#### <a name="to-change-the-name-of-a-hierarchy-or-child-level"></a>若要變更階層或子層級的名稱  
  
1.  以滑鼠右鍵按一下階層父層級或子層級，然後按一下 [重新命名]****。  
  
2.  輸入新的名稱或編輯現有的名稱。  
  
#### <a name="to-change-the-order-of-a-child-level-in-a-hierarchy"></a>變更階層中子層級的順序  
  
-   按一下子層級並將其拖曳至階層中的新位置。  
  
-   或按兩下階層的子層級，然後按一下 [上移]，將層級在清單中上移，或按一下 [下移]，將層級在清單中下移。  
  
-   或按一下子層級予以選取，然後按 Alt + 向上鍵將層級在清單中上移，或按 Alt + 向下鍵將層級在清單中下移。  
  
#### <a name="to-add-another-child-level-to-a-hierarchy"></a>將另一個子層級加入至階層  
  
-   按一下並將資料行拖曳至父層級或階層的特定位置。 資料行會複製為階層的子層級。  
  
-   或以滑鼠右鍵按一下資料行，然後指向 [加入至階層]****，再按一下階層。  
  
> [!NOTE]  
>  您可以加入隱藏的資料行 (報表中不顯示的資料行) 做為階層中的子層級。 子層級不是隱藏的。  
  
#### <a name="to-remove-a-child-level-from-a-hierarchy"></a>若要從階層中移除子層級  
  
-   以滑鼠右鍵按一下子層級，然後按一下 [從階層移除]****。  
  
-   或按一下子層級，然後按 **Delete**鍵。  
  
> [!NOTE]  
>  如果重新命名階層子層級，則不會再與其複製來源資料行共用相同名稱。 使用 [顯示來源名稱]**** 命令查看其複製來源資料行。  
  
#### <a name="to-show-a-source-name"></a>顯示來源名稱  
  
-   以滑鼠右鍵按一下階層子層級，然後按一下 [顯示來源名稱]****。 即會顯示其複製來源資料行的名稱。  
  
##  <a name="delete-a-hierarchy"></a><a name="bkmk_delete"></a>刪除階層  
  
#### <a name="to-delete-a-hierarchy-and-remove-its-child-levels"></a>刪除階層及移除其子層級  
  
-   以滑鼠右鍵按一下父階層層級，然後按一下 [刪除階層]。  
  
-   或按一下父階層層級，然後按 Delete。 這也會移除所有子層級。  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型設計師 &#40;SSAS 表格式&#41;](../tabular-model-designer-ssas-tabular.md)   
 [SSAS 表格式&#41;的階層 &#40;](hierarchies-ssas-tabular.md)   
 [量值 &#40;SSAS 表格式&#41;](measures-ssas-tabular.md)  
  
  
