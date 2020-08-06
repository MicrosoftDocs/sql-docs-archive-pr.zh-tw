---
title: " (Master Data Services) 建立訂閱視圖 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- subscription views [Master Data Services], creating
- creating subscription views [Master Data Services]
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e5e2b901e56d75e97a444fd2858ef95872f3b766
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597893"
---
# <a name="create-a-subscription-view-master-data-services"></a>建立訂閱檢視 (Master Data Services)
  當您想要在資料庫中建立資料 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 的視圖以供訂閱系統使用時，請建立訂閱視圖。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[整合管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
### <a name="to-create-a-subscription-view"></a>若要建立訂閱檢視  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，按一下 **[整合管理]**。  
  
2.  按一下功能表列上的 **[建立檢視表]**。  
  
3.  在 [**訂閱視圖**] 頁面上，按一下 [**加入訂閱視圖**]。  
  
4.  在 [**建立訂閱視圖**] 窗格的 [**訂閱視圖名稱**] 方塊中，輸入此視圖的名稱。  
  
5.  從 **[模型]** 清單中選取模型。  
  
6.  選取 [**版本**] 或 [**版本旗**標] 選項，然後從對應的清單中選取。  
  
    > [!TIP]  
    >  根據版本旗標建立訂閱檢視。 當您鎖定版本時，您可以重新指派旗標給開啟的版本，而不用更新訂閱檢視。  
  
7.  選取 [**實體**] 或 [**衍生**階層] 選項，然後從對應的清單中選取。  
  
8.  從 **[格式]** 清單中選取訂閱檢視格式。  
  
9. 如果您從 **[格式]** 清單中選擇 **[明確層級]** 或 **[衍生層級]** ，請輸入階層內要加入檢視中的層級數。  
  
10. 按一下 [檔案] 。  
  
## <a name="see-also"></a>另請參閱  
 [將資料匯出 &#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)   
 [刪除訂閱視圖 &#40;Master Data Services&#41;](delete-a-subscription-view-master-data-services.md)   
 [建立版本旗標 &#40;Master Data Services&#41;](create-a-version-flag-master-data-services.md)  
  
  
