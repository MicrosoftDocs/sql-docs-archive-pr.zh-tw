---
title: 使用 SSMS (SSAS 表格式) 管理角色 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 652faac0-1cfc-438b-8119-2f4b090a2381
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4ee34d5e75d5d4ce3679d46d29af3215852d2bbe
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687208"
---
# <a name="manage-roles-by-using-ssms-ssas-tabular"></a>使用 SSMS 管理角色 (SSAS 表格式)
  對於部署的表格式模型，可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]建立、編輯和管理角色。  
  
 本主題的工作：  
  
-   [若要建立新角色](#bkmk_new_role)  
  
-   [若要複製角色](#bkmk_copy_role)  
  
-   [若要編輯角色](#bkmk_edit_role)  
  
-   [若要刪除角色](#bkmk_deletet_role)  
  
> [!CAUTION]  
>  透過在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中使用 [角色管理員] 定義的角色重新部署表格式模型專案，將會覆寫已部署表格式模型中定義的角色。  
  
> [!CAUTION]  
>  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中開啟模型專案時使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 管理表格式模型工作空間資料庫可能會造成 Model.bim 檔案損毀。 當您針對表格式模型工作空間資料庫建立及管理角色時，請在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中使用 [角色管理員]。  
  
###  <a name="to-create-a-new-role"></a><a name="bkmk_new_role"></a>若要建立新的角色  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，展開您要建立新角色的表格式模型資料庫，然後以滑鼠右鍵按一下 [角色]****，再按一下 [新增角色]****。  
  
2.  在 [建立角色]**** 對話方塊的 [選取頁面] 視窗中，按一下 [一般]****。  
  
3.  在 [一般設定] 視窗中，於 [名稱]**** 欄位內輸入角色的名稱。  
  
     依預設，每個新角色的預設角色名稱是以累加的方式進行編號。 建議您輸入清楚識別成員類型的名稱，例如「財務經理」或「人力資源專員」。  
  
4.  在 [為這個角色設定資料庫權限]**** 中，選取下列其中一個權限選項：  
  
    |權限|描述|  
    |----------------|-----------------|  
    |**完整控制權 (管理員)**|成員可以對模型結構描述進行修改，也可以檢視所有資料。|  
    |**處理資料庫**|成員可以執行「處理」和「全部處理」作業。 無法修改模型結構描述，也無法檢視資料。|  
    |**讀取**|成員可以檢視資料 (根據資料列篩選)，但無法對模型結構描述進行任何變更。|  
  
5.  在 [建立角色]**** 對話方塊的 [選取頁面] 視窗中，按一下 [成員資格]****。  
  
6.  在成員資格設定視窗中，按一下 [加入]****，然後在 [選取使用者或群組]**** 對話方塊中，加入您要當做成員加入的 Windows 使用者或群組。  
  
7.  如果您建立的角色具有「讀取」權限，您可以使用 DAX 公式加入任何資料表的資料列篩選。 若要加入資料列篩選，請在 [**角色屬性- \<rolename> ** ] 對話方塊的 [**選取頁面**] 中，按一下 [資料**列篩選**]。  
  
8.  在 [資料列篩選] 視窗中，選取資料表，然後按一下 [ **Dax 篩選**] 欄位，然後在 [ **dax 篩選 \<tablename> 條件-** ] 欄位中輸入 DAX 公式。  
  
    > [!NOTE]  
    >  [DAX 篩選準則] \<tablename> 欄位不包含 [自動完成查詢編輯器] 或 [插入函數] 功能。 若要在撰寫 DAX 公式時使用自動完成功能，您必須在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中使用 DAX 公式編輯器。  
  
9. 按一下 [確定]****，儲存角色。  
  
###  <a name="to-copy-a-role"></a><a name="bkmk_copy_role"></a> 若要複製角色  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，展開包含您要複製之角色的表格式模型資料庫，然後展開 [角色]****，再以滑鼠右鍵按一下此角色，然後按一下 [複製]****。  
  
###  <a name="to-edit-a-role"></a><a name="bkmk_edit_role"></a>編輯角色  
  
-   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，展開包含您要編輯之角色的表格式模型資料庫，然後展開 [角色]****，再以滑鼠右鍵按一下此角色，然後按一下 [屬性]****。  
  
     在 [**角色屬性** \<rolename> ] 對話方塊中，您可以變更許可權、加入或移除成員，以及加入/編輯資料列篩選。  
  
###  <a name="to-delete-a-role"></a><a name="bkmk_deletet_role"></a>若要刪除角色  
  
-   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，展開包含您要刪除之角色的表格式模型資料庫，然後展開 [角色]****，再以滑鼠右鍵按一下此角色，然後按一下 [刪除]****。  
  
## <a name="see-also"></a>另請參閱  
 [角色 &#40;SSAS 表格式&#41;](roles-ssas-tabular.md)  
  
  
