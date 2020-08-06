---
title: 建立合併成員 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating consolidated members [Master Data Services]
- members [Master Data Services], creating consolidated members
- consolidated members [Master Data Services], creating
ms.assetid: 431ab2d2-5517-4372-9980-142b05427c08
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c41673f6f3bf1f4de2a831ecd659321b273b6af9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87703041"
---
# <a name="create-a-consolidated-member-master-data-services"></a>Create a Consolidated Member (Master Data Services)
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]當您需要明確階層的父節點時，可以在 中建立合併成員。 合併成員可以有自己的屬性。 它們可用於群組。 如下列範例所示，合併成員可以用於具有帳戶的帳戶群組。

 ![MDS 合併成員](../../2014/master-data-services/media/mds-consolidated-members.png "MDS 合併成員")

## <a name="prerequisites"></a>Prerequisites
 若要執行此程序：

-   您必須擁有存取 [ **Explorer** ] 功能區域的許可權。

-   針對要加入成員之實體的合併模型物件，您必須至少擁有 **[更新]** 權限。

### <a name="to-create-a-consolidated-member"></a>若要建立合併成員

1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，選取 **[模型]** 清單中的模型。

2.  從 **[版本]** 清單中選取版本。

3.  按一下 **[總管]**。

4.  從功能表列指向 **[階層]** ，然後按一下要加入合併成員的階層名稱。

5.  在方格上方，選取 **[合併成員]** 或 **[階層中的所有合併成員]** 選項。

6.  按一下 [新增] 。

7.  填完右邊窗格中的欄位。

8.  選擇性。 在 **[註解]** 方塊中，輸入有關加入此成員之原因的註解。 可存取成員的所有使用者都可以檢視註解。

9. 按一下 [確定]  。

## <a name="next-steps"></a>後續步驟

-   [在階層中移動成員 &#40;Master Data Services&#41;](move-members-within-a-hierarchy-master-data-services.md)

## <a name="see-also"></a>另請參閱
 [建立明確階層 &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md) [建立分葉成員 &#40;Master Data Services](../../2014/master-data-services/create-a-leaf-member-master-data-services.md)&#41;[使用暫存進程成員 Master Data Services &#40;載入或更新 Master Data Services 中](add-update-and-delete-data-master-data-services.md) [Members &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)&#41;&#40;[明確](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)階層 Master Data Services&#41;


