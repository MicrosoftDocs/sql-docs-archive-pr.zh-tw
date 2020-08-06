---
title: 重疊的使用者和群組的權限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- users [Master Data Services], resolving permissions
- permissions [Master Data Services], user and group overlaps
- groups [Master Data Services], resolving permissions
ms.assetid: 31c3cf7d-17d4-4474-b6a7-ffcb9fc45b37
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7044bf6260170cbc598719ec204ddb6f861f6301
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87698359"
---
# <a name="overlapping-user-and-group-permissions-master-data-services"></a>重疊的使用者和群組的權限 (Master Data Services)
  使用者的權限是根據以下條件：  
  
-   來自群組成員資格的權限。  
  
-   明確指派給使用者的權限。  
  
 如果使用者是多個群組的成員，而且這些群組擁有主資料管理員的存取權，將適用以下規則：  
  
-   **[拒絕]** 會覆寫所有其他的權限。  
  
-   **更新**會覆寫**唯讀**。  
  
 這些規則同時適用於[模型]**** 和 [階層成員]**** 索引標籤。 系統會解析每個索引標籤的權限，然後加以結合。 如需詳細資訊，請參閱 [如何決定權限 &#40;Master Data Services&#41;](how-permissions-are-determined-master-data-services.md)。  
  
> [!NOTE]  
>  您可以在使用者介面中，檢視使用者和群組重疊權限的解析。 [模型]**** 和 [階層成員]**** 索引標籤都有下拉式清單，您可以從中選取 [有效]**** 來檢視有效的權限。  
  
## <a name="example-1"></a>範例 1  
 ![mds_conc_user_group_ex_1](../../2014/master-data-services/media/mds-conc-user-group-ex-1.gif "mds_conc_user_group_ex_1")  
  
 使用者屬於群組 1 和群組 2。  
  
 使用者具有 Product 實體的 [**唯讀**] 許可權。  
  
 群組 1 擁有 Product 實體的 **更新** 權限。  
  
 [群組 2] 具有 [Product] 實體的 [**唯讀**] 許可權。  
  
 結果：使用者的有效權限為 Product 實體的 **更新** 權限。  
  
## <a name="example-2"></a>範例 2  
 ![mds_conc_user_group_ex_2](../../2014/master-data-services/media/mds-conc-user-group-ex-2.gif "mds_conc_user_group_ex_2")  
  
 使用者屬於群組 1 和群組 2。  
  
 使用者具有 Product 實體的 [**唯讀**] 許可權。  
  
 群組 1 擁有 Product 實體的 **更新** 權限。  
  
 群組 2 擁有 Product 實體的 **拒絕** 權限。  
  
 結果：使用者的有效權限為 Product 實體的 **拒絕** 權限。  
  
## <a name="example-3"></a>範例 3  
 ![mds_conc_user_group_ex_3](../../2014/master-data-services/media/mds-conc-user-group-ex-3.gif "mds_conc_user_group_ex_3")  
  
 使用者屬於群組 1 和群組 2。  
  
 使用者擁有階層節點內成員群組的 **更新** 權限。  
  
 [群組 1] 具有階層節點中成員群組的 [**唯讀**] 許可權。  
  
 群組2具有階層節點中成員群組的**唯讀**許可權。  
  
 結果：使用者的有效權限為成員的 **更新** 權限。  
  
## <a name="see-also"></a>另請參閱  
 [如何判斷許可權 &#40;Master Data Services&#41;](how-permissions-are-determined-master-data-services.md)   
 [重疊的模型和成員的權限 &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-model-and-member-permissions-master-data-services.md)  
  
  
