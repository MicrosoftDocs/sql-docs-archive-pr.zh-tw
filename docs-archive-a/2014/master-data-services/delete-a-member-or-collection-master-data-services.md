---
title: 刪除成員或集合 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services], deleting
- leaf members [Master Data Services], deleting
- deleting members [Master Data Services]
- members [Master Data Services], deleting
- consolidated members [Master Data Services], deleting
ms.assetid: 519130a7-4226-4d71-9124-d2ee0ce7e5bd
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9b248750c0e755c3fc9e32d45068c754e64957b7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687016"
---
# <a name="delete-a-member-or-collection-master-data-services"></a>刪除成員或集合 (Master Data Services)
  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，刪除您不再需要的成員或集合。 如果您要大量刪除成員，請改用暫存處理序。 如需詳細資訊，請參閱[使用暫存進程停用或刪除成員 &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)。  
  
> [!NOTE]  
>  如果某個成員是當做另一個成員的網域屬性值使用，您就無法刪除該成員。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 [ **Explorer** ] 功能區域的許可權。  
  
-   針對成員，您至少必須擁有要從中刪除成員的分葉模型物件的 [**更新**] 許可權。  
  
-   針對集合，您必須至少擁有分頁集合物件 **更新** 權限，才能將其刪除。  
  
### <a name="to-delete-a-member-or-collection"></a>若要刪除成員或集合  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，選取 **[模型]** 清單中的模型。  
  
2.  從 **[版本]** 清單中選取版本。  
  
3.  按一下 **[總管]**。  
  
4.  若要刪除：  
  
    -   分葉成員，請從功能表列指向 [實體]****，然後按一下包含該成員的實體名稱。  
  
    -   合併成員，請從功能表列指向 [階層]****，然後按一下包含該成員的階層名稱。 然後按一下階層中包含此成員的節點。  
  
    -   集合，請從功能表列指向 [集合]****，然後按一下包含該集合的實體名稱。  
  
5.  在方格中，按一下要刪除之成員或集合的資料列。  
  
6.  按一下 [刪除成員]****、[刪除]**** 或 [刪除集合]****。  
  
7.  在確認對話方塊中按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Master Data Services 重新啟用成員或集合&#41;](../../2014/master-data-services/reactivate-a-member-or-collection-master-data-services.md)   
 [成員 &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [集合 &#40;Master Data Services&#41;](../../2014/master-data-services/collections-master-data-services.md)  
  
  
