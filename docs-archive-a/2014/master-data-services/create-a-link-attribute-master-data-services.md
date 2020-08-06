---
title: 建立連結屬性 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], creating link attributes
- creating link attributes [Master Data Services]
ms.assetid: e6658e9c-5b08-4b8d-b556-17ec2dd041d2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4770d7904371c10dc6720e8d3d7f28ca797d9b80
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606959"
---
# <a name="create-a-link-attribute-master-data-services"></a>建立連結屬性 (Master Data Services)
  當您想要讓使用者輸入超連結作為屬性值 (例如 `http://www.contoso.com`) 時，可以在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中建立連結屬性。  
  
> [!NOTE]  
>  當使用者輸入連結屬性的值時，字串開頭必須為 **http://** ，否則將會顯示一個錯誤。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
-   建立屬性的實體必須存在。 如需詳細資訊，請參閱[建立實體 &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md)。  
  
### <a name="to-create-a-link-attribute"></a>若要建立連結屬性  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 **[模型檢視]** 頁面上，從功能表列指向 **[管理]** ，然後按一下 **[實體]**。  
  
3.  在 **[實體維護]** 頁面上，選取 **[模型]** 清單中的模型。  
  
4.  針對要建立屬性的實體選取資料列。  
  
5.  按一下 **[編輯選取的實體]**。  
  
6.  在 **[編輯實體]** 頁面上：  
  
    -   如果是分葉成員的屬性，則按一下 **[分葉成員屬性]** 窗格中的 **[加入分葉屬性]**。  
  
    -   如果是合併成員的屬性，則按一下 **[合併成員屬性]** 窗格中的 **[加入合併屬性]**。  
  
    -   如果是集合的屬性，則按一下 **[集合屬性]** 窗格中的 **[加入集合屬性]**。  
  
7.  選取 **[加入屬性]** 頁面上的 **[自由格式]** 選項。  
  
8.  在 **[名稱]** 方塊中，輸入屬性的名稱。 如需不應當做屬性名稱使用的字組清單，請參閱[保留字 &#40;Master Data Services&#41;](../../2014/master-data-services/reserved-words-master-data-services.md)。  
  
9. 在 **[顯示像素寬度]** 方塊中，輸入要在 **[總管]** 方格中顯示的屬性資料行寬度。  
  
10. 從 [資料類型]**** 清單中，選取 [連結]****。  
  
11. 在 [長度]**** 方塊中，輸入允許的最大字元數。  
  
12. (選擇性) 選取 **[啟用變更追蹤]** 以追蹤屬性群組的變更。 如需詳細資訊，請參閱[將屬性加入至變更追蹤群組 &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)。  
  
13. 按一下 **[儲存屬性]**。  
  
14. 按一下 **[實體維護]** 頁面上的 **[儲存實體]**。  
  
## <a name="see-also"></a>另請參閱  
 [Master Data Services &#40;的屬性&#41;](../../2014/master-data-services/attributes-master-data-services.md)   
 [變更屬性名稱 &#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [建立以網域為基礎的屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [建立檔案屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
