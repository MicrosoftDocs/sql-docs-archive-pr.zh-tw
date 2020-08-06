---
title: 合併的許可權 (Master Data Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], consolidated member attribute permissions
- consolidated members [Master Data Services], attribute permissions
- permissions [Master Data Services], consolidated members
- members [Master Data Services], consolidated member permissions
ms.assetid: 084055a3-5fd3-43f3-b620-ac6afab42a3d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c4c93e74acc84d6e742139263bedc011c4028efb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607441"
---
# <a name="consolidated-permissions-master-data-services"></a>合併的權限 (Master Data Services)
  合併的權限適用於某個實體所有合併成員的屬性值。  
  
 合併的權限只適用於啟用明確階層和集合的實體。  
  
 **注意：**  
  
-   分葉權限只適用於使用者介面的總管**** 功能區域。  
  
-   系統不會強制使用指派給 **Name** 和 **Code** 屬性的權限。  
  
|權限|描述|  
|----------------|-----------------|  
|**唯讀**|顯示合併成員，但使用者無法加入、移除或變更這些成員。|  
|**更新**|顯示合併成員，而且使用者可以加入、移除及變更這些成員。|  
|**Deny**|不顯示實體的合併成員。|  
  
## <a name="attribute-permissions"></a>屬性權限  
 屬性權限適用於特定實體的屬性值。 只有屬性權限的使用者無法加入或移除成員。  
  
|權限|描述|  
|----------------|-----------------|  
|**唯讀**|顯示屬性，但使用者無法變更屬性值。|  
|**更新**|顯示屬性，而且使用者可以變更屬性值。|  
|**Deny**|不顯示屬性。<br /><br /> 注意：您無法明確拒絕存取 Name 和 Code 屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [指派模型物件使用權限 &#40;Master Data Services&#41;](assign-model-object-permissions-master-data-services.md)   
 [分葉許可權 &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [模型物件使用權限 &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [成員 &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)  
  
  
