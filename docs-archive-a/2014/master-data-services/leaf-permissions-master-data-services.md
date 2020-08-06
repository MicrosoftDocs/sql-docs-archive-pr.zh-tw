---
title: 分葉權限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], permissions
- members [Master Data Services], leaf member permissions
- permissions [Master Data Services], leaf members
- leaf members [Master Data Services], attribute permissions
- attributes [Master Data Services], leaf member attribute permissions
ms.assetid: bde16e8c-bcd4-4041-8130-55c5450e5f72
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 794e1d138b91e896b8df16765ae8984c6e60aca7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706550"
---
# <a name="leaf-permissions-master-data-services"></a>分葉權限 (Master Data Services)
  分葉權限適用於某個實體所有分葉成員的屬性值。  
  
 如果是沒有啟用明確階層的實體，將權限指派給 [分葉]**** 與指派給實體相同。  
  
 **注意：**  
  
-   分葉權限只適用於使用者介面的總管**** 功能區域。  
  
-   系統不會強制使用指派給 **Name** 和 **Code** 屬性的權限。  
  
|權限|描述|  
|----------------|-----------------|  
|**唯讀**|顯示分葉成員，但使用者無法加入、移除或變更這些成員。<br /><br /> 如果合併成員存在，將會顯示 Name 和 Code，但是使用者無法將其加入、移除或變更。|  
|**更新**|顯示分葉成員，而且使用者可以加入、移除及變更這些成員。<br /><br /> 如果合併成員存在，將會顯示 Name 和 Code，但是使用者無法將其加入、移除或變更。|  
|**Deny**|不顯示實體的分葉成員。|  
  
## <a name="attribute-permissions"></a>屬性權限  
 屬性權限適用於特定實體的屬性值。 只有屬性權限的使用者無法加入或移除成員。  
  
|權限|描述|  
|----------------|-----------------|  
|**唯讀**|顯示屬性，但使用者無法變更屬性值。|  
|**更新**|顯示屬性，而且使用者可以變更屬性值。|  
|**Deny**|不顯示屬性。<br /><br /> 注意：您無法明確拒絕存取 Name 和 Code 屬性。|  
  
### <a name="example"></a>範例  
 如果是 Product 實體，請將 [更新]**** 權限指派給 Subcategory 屬性。 拒絕其他所有屬性的權限。  
  
|名稱|程式碼|Subcategory (更新)|  
|----------|----------|----------------------------|  
|Mountain-100|BK-M101|{5}山區自行車|  
|Mountain-100|BK-M201|{5}山區自行車|  
  
 在總管**** 中，您可以更新 Subcategory 資料行中的任何屬性值。 如果您沒有屬性的權限，就不會顯示該屬性。  
  
> [!NOTE]  
>  在這個範例中，Subcategory 是根據 SubcategoryList 實體的網域屬性。 您可以為 Mountain-100 選取不同的子類別目錄，但是您無法從 SubcategoryList 實體中加入成員或刪除成員。  
  
## <a name="see-also"></a>另請參閱  
 [指派模型物件使用權限 &#40;Master Data Services&#41;](assign-model-object-permissions-master-data-services.md)   
 [合併的許可權 &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-permissions-master-data-services.md)   
 [模型物件使用權限 &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [成員 &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)  
  
  
