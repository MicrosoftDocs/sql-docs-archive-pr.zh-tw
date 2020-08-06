---
title: 建立、刪除或修改角色 (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- deleting roles
- removing roles
- roles [Reporting Services], definitions
- modifying roles
- roles [Reporting Services], deleting
- roles [Reporting Services], modifying
ms.assetid: 3d1d56e6-a283-44a7-8417-36cb4d2c74d1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 543bddda88e41af39d3200df4728716d46b3ae8b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704849"
---
# <a name="create-delete-or-modify-a-role-management-studio"></a>建立、刪除或修改角色 (Management Studio)
  Reporting Services 會提供定義報表伺服器之存取層級的預先定義角色。 需要存取報表伺服器的每個使用者或群組會透過描述可執行之工作的角色來達成此目的。 這些角色完全是針對報表伺服器所定義。 您無法針對報表伺服器的特定部分變更角色定義，或指定要根據情況以不同的方式使用某個角色。  
  
 若要建立、修改或刪除角色，請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 您只能刪除未使用的角色。  
  
 若要將使用者和群組指派至您所建立的角色，請使用報表管理員。 如需詳細資訊，請參閱[將報表伺服器的存取權授與使用者 &#40;報表管理員&#41;](grant-user-access-to-a-report-server.md)。  
  
> [!NOTE]  
>  如果報表伺服器是針對 SharePoint 整合模式所設定，而且您已連接至與報表伺服器整合的 SharePoint 網站，就可以檢視並修改權限等級，以便控制報表伺服器內容和作業的存取權。  
  
### <a name="to-create-a-role-definition"></a>若要建立角色定義  
  
1.  在 [物件總管] 中，展開報表伺服器節點。  
  
2.  展開安全性資料夾。  
  
3.  如果您要建立項目層級角色定義，請以滑鼠右鍵按一下 [角色]****，然後指向 [新增角色]****。  
  
     如果您要建立系統層級角色定義，請以滑鼠右鍵按一下 [系統角色]****，然後指向 [新增系統角色]****。  
  
4.  為角色輸入唯一的名稱。 名稱至少必須包含一個字元。 它也可以包括空格和特定符號，但不得包括下列字元：; ? ： \@ & = +，$/* \< > |"或/。  
  
5.  選擇性地輸入描述。 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，此描述僅會出現在本頁面上。 透過報表管理員檢視此項目的使用者，可以在該工具中看到此描述。  
  
6.  選取這個角色的成員可以執行的工作。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-or-modify-a-role-definition"></a>若要刪除或修改角色定義  
  
1.  在 [物件總管] 中，展開報表伺服器節點。  
  
2.  展開安全性資料夾。  
  
3.  若要刪除或修改項目層級的角色定義，請展開 [角色] 資料夾。 執行下列其中一項：  
  
    1.  若要刪除角色定義，請以滑鼠右鍵按一下項目，然後按一下 [刪除]****。 就會顯示 **[刪除物件]** 對話方塊。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    2.  若要修改角色定義，請以滑鼠右鍵按一下項目，然後按一下 [屬性]****。 就會顯示 **[使用者角色屬性]** 對話方塊的 [一般] 頁面。  
  
         選取這個角色的成員可以執行的工作，然後按一下 **[確定]**。  
  
4.  若要刪除或修改系統層級角色定義，請展開 [系統角色]  資料夾。 執行下列其中一項：  
  
    1.  若要刪除系統角色定義，請以滑鼠右鍵按一下項目，然後按一下 [刪除]****。 就會顯示 **[刪除物件]** 對話方塊。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    2.  若要修改系統角色定義，請以滑鼠右鍵按一下項目，然後按一下 [屬性]****。 就會顯示 **[系統角色屬性]** 對話方塊的 [一般] 頁面。  
  
         選取這個角色的成員可以執行的工作，然後按一下 **[確定]** 來套用變更。  
  
## <a name="see-also"></a>另請參閱  
 [連接到 Management Studio 中的報表伺服器](../tools/connect-to-a-report-server-in-management-studio.md)   
  (create-and-manage-role-assignments.md)    
 [SQL Server Management Studio 中的 Reporting Services &#40;SSRS&#41;](../tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
  
