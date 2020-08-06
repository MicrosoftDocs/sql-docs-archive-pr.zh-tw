---
title: 將旗標指派給版本 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- version flags [Master Data Services], assigning flags
- versions [Master Data Services], assigning flags
ms.assetid: 6629ec7e-32e7-4a1e-8b31-eb43c5923766
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 2de0d0d8d8ea96814e13b9123fe4fcd4782d6bef
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606394"
---
# <a name="assign-a-flag-to-a-version-master-data-services"></a>將旗標指派給版本 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，將旗標指派給版本，指出使用者或訂閱系統應該使用的版本。  
  
> [!NOTE]  
>  版本旗標一次只能指派給一個版本。 如果指派的旗標已指派給另一個版本，該旗標會移至選取的版本。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[版本管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
-   您必須已建立要指派的版本旗標。 如需詳細資訊，請參閱 [建立版本旗標 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-version-flag-master-data-services.md)(管理員 (Master Data Services))。  
  
### <a name="to-assign-a-flag-to-a-version"></a>若要將旗標指派給版本  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[版本管理]**。  
  
2.  在 [管理版本]**** 頁面上，於您要指派旗標之版本的資料列，按兩下 [旗標]**** 資料行中的資料格。  
  
3.  從清單中選取您要指派的旗標。  
  
    > [!NOTE]  
    >  如果您要的旗標無法使用，此旗標可能只適用於 [已認可]**** 版本。 若要確認，請移至 [管理版本旗標]**** 頁面並檢視旗標的 [僅限認可的版本]**** 欄位。  
  
4.  按下 ENTER 鍵儲存變更。  
  
## <a name="see-also"></a>另請參閱  
 [建立 &#40;Master Data Services 的版本旗標&#41;](../../2014/master-data-services/create-a-version-flag-master-data-services.md)   
 [版本 &#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)  
  
  
