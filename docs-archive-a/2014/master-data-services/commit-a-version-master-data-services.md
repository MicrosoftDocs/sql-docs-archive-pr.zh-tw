---
title: 認可版本 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- committing versions [Master Data Services]
- versions [Master Data Services], committing
ms.assetid: 6b967a39-b333-4b84-9e5f-4fb07e156826
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: cec3244d4ddaa78d9168e3ede503fa16756633a0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699976"
---
# <a name="commit-a-version-master-data-services"></a>認可版本 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可認可模型版本，以防止模型成員及其屬性的變更。 已認可的版本無法解除鎖定。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[版本管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
-   版本的狀態必須是 [已鎖定]****。 如需詳細資訊，請參閱 [鎖定版本 &#40;Master Data Services&#41;](../../2014/master-data-services/lock-a-version-master-data-services.md)(管理員 (Master Data Services))。  
  
-   所有成員必須都已驗證成功。  
  
### <a name="to-commit-a-version"></a>若要認可版本  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[版本管理]**。  
  
2.  在 [管理版本]**** 頁面上，按一下功能表列上的 [驗證版本]****。  
  
3.  在 [驗證版本]**** 頁面上，選取要認可的模型和版本。  
  
4.  按一下 [認可]****。  
  
5.  在確認對話方塊中按一下 **[確定]**。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [建立版本旗標 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-version-flag-master-data-services.md)  
  
-   [將旗標指派給版本 &#40;Master Data Services&#41;](../../2014/master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
-   [複製版本 &#40;Master Data Services&#41;](../../2014/master-data-services/copy-a-version-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [版本 &#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)  
  
  
