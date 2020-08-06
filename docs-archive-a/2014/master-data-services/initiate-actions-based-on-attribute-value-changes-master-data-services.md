---
title: 根據屬性值變更來起始動作 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], tracking attribute changes
- change tracking groups [Master Data Services], initiating actions
ms.assetid: 5e4402ce-31db-4774-a2a1-552335f87693
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 50931b9f9c4bd5d08596d485ba695143b9c6594e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687954"
---
# <a name="initiate-actions-based-on-attribute-value-changes-master-data-services"></a>根據屬性值變更來起始動作 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，建立商務規則，以根據屬性值變更來起始動作， 例如，當特定的屬性值變更時，您可能想要變更值、傳送通知，或啟動外部工作流程。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
-   您的屬性必須位於變更追蹤群組。 如需詳細資訊，請參閱 [將屬性加入至變更追蹤群組 &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md) 。  
  
### <a name="to-create-a-business-rule-to-initiate-actions-based-on-attribute-value-changes"></a>若要建立商務規則，以根據屬性值變更來起始動作  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列，指向 **[管理]** ，然後按一下 **[商務規則]**。  
  
3.  在 [商務規則維護]**** 頁面上，選取 [模型]**** 清單中的模型。  
  
4.  從 [實體]**** 清單中選取實體。  
  
5.  從 [成員類型]**** 清單中，選取要套用商務規則的成員類型。  
  
6.  從 [屬性]**** 清單中，選取屬性或保留預設值 [全部]****。  
  
7.  按一下 [加入商務規則]****。  
  
8.  按一下 [編輯選取的商務規則]****。  
  
9. 在 [元件]**** 窗格中，展開 [條件]**** 節點。  
  
10. 將 [數值比較]**** 節點底下的 [已變更]**** 拖曳至 [IF]**** 窗格的 [條件]**** 標籤。  
  
11. 在 [**屬性**] 窗格中，按一下屬性，並將它拖曳至 [**編輯條件**] 窗格的 [**選取屬性**] 標籤。 此屬性對規則沒有作用，因此請選取任何可用屬性。  
  
12. 在 [編輯條件]**** 窗格的 [變更追蹤群組]**** 方塊中，輸入已指派為必要條件的變更追蹤群組編號。  
  
13. 在 [編輯條件]**** 窗格中，按一下 [儲存項目]****。  
  
14. 在 [元件]**** 窗格中，展開 [動作]**** 節點。  
  
15. 按一下動作並將它拖曳至 [THEN]**** 窗格的 [動作]**** 標籤。  
  
16. 在 [屬性]**** 窗格中，按一下屬性並將它拖曳至 [編輯動作]**** 窗格的 [選取屬性]**** 標籤。  
  
17. 在 [編輯動作]**** 窗格中，完成任何必要欄位。  
  
18. 在 [編輯動作]**** 窗格中，按一下 [儲存項目]****。  
  
19. 按一下 [上一步]****。  
  
20. (選擇性) 在 [商務規則維護]**** 頁面上，針對包含商務規則的資料列，按兩下 [名稱]****、[描述]**** 或 [通知]**** 資料行中的資料格，以更新值。  
  
    > [!NOTE]  
    >  只針對包含驗證動作的規則才傳送通知。  
  
21. 按一下 [發行商務規則]****。  
  
22. 在確認對話方塊中按一下 **[確定]**。 規則狀態會變更為 [作用中]****。  
  
## <a name="next-steps"></a>後續步驟  
  
-   遵循下列其中一個程序，將商務規則套用至資料：  
  
    -   [根據商務規則驗證特定成員 &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [根據商務規則驗證版本 &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [將屬性新增至變更追蹤群組 &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)   
 [商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
