---
title: 刪除使用者或群組 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting groups [Master Data Services]
- groups [Master Data Services], deleting
- users [Master Data Services], deleting
- deleting users [Master Data Services]
ms.assetid: 0bbf9d2c-b826-48bb-8aa9-9905db6e717f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: be302bc974994d0f4f17a8e61244065c76fa93ca
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599547"
---
# <a name="delete-users-or-groups-master-data-services"></a>刪除使用者或群組 (Master Data Services)
  當您不再希望使用者或群組存取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]時，可以刪除他們。  
  
 在刪除使用者和群組時，請注意下列行為：  
  
-   如果刪除有 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]存取權之群組成員的使用者，該使用者仍然可以存取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ，直到從 Active Directory 或本機群組移除使用者為止。  
  
-   如果刪除群組，群組中已存取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 的所有使用者都會顯示在 **[使用者]** 清單，直到刪除使用者為止。  
  
-   對安全性的變更不會傳播至 MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 20 分鐘。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[使用者及群組的權限]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
### <a name="to-delete-users-or-groups"></a>若要刪除使用者或群組  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[使用者及群組的權限]**。  
  
2.  若要刪除使用者，請停留在 **[使用者]** 頁面。 若要刪除群組，請按一下功能表列上的 [管理群組]****。  
  
3.  在方格中，選取要刪除之使用者或群組的資料列。  
  
4.  按一下 **[刪除選取的使用者]** 或 **[刪除選取的群組]**。  
  
5.  在確認對話方塊中按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [安全性 &#40;Master Data Services&#41;](../../2014/master-data-services/security-master-data-services.md)  
  
  
