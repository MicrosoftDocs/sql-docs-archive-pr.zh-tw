---
title: 自動產生 Code 以外的屬性值 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b82f6f81-6e9c-4918-9ea9-4ab5f5d11b15
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 8db6c89bdce2a11a5a54ed3a763a7bc41bd7f1be
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599050"
---
# <a name="automatically-generate-attribute-values-other-than-code-master-data-services"></a>自動產生 Code 以外的屬性值 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中，當您希望每次套用商務規則時，自動將整數指派為值，請自動為實體的屬性自動產生值。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
-   數值屬性必須存在。 如需詳細資訊，請參閱[建立數值屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-numeric-attribute-master-data-services.md)。  
  
### <a name="to-automatically-generate-an-attribute-value"></a>若要自動產生屬性值  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列，指向 **[管理]** ，然後按一下 **[商務規則]**。  
  
3.  在 [商務規則維護]**** 頁面上，選取 [模型]**** 清單中的模型。  
  
4.  從 [實體]**** 清單中選取實體。  
  
5.  從 [成員類型]**** 清單中，選取要套用商務規則的成員類型。  
  
6.  從 [屬性]**** 清單中，保留預設值 [全部]****。  
  
7.  按一下 [加入商務規則]****。  
  
8.  按一下 [編輯選取的商務規則]****。  
  
9. 在 [元件]**** 窗格中，展開 [動作]**** 節點。  
  
10. 在 [預設] 節點中，按一下 [預設為產生的值]****，然後將其拖曳至 [THEN]**** 窗格的 [動作]**** 標籤。  
  
11. 在 [屬性]**** 窗格中，按一下擁有您要產生之值的屬性，並將其拖曳至 [編輯動作]**** 窗格的 [選取屬性]**** 標籤。  
  
12. 在 [開始]**** 和 [遞增量]**** 方塊中輸入值。 如果成員已存在，則將根據最大的現有值設定值。 例如，如果最大的現有值為 299，而且您將 [遞增量]**** 設定為 **1**，則下一個成員的值將設為 300。  
  
13. 在 [編輯動作]**** 窗格中，按一下 [儲存項目]****。  
  
14. 按一下 [上一步]****。  
  
15. (選擇性) 在 [商務規則維護]**** 頁面上，針對包含商務規則的資料列，按兩下 [名稱]****、[描述]**** 或 [通知]**** 資料行中的資料格，以更新值。  
  
16. 按一下 [發行商務規則]****。  
  
17. 在確認對話方塊中按一下 **[確定]**。 規則狀態會變更為 [作用中]****。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [根據商務規則驗證特定成員 &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
-   [根據商務規則驗證版本 &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [自動建立程式碼 &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md)   
 [商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [驗證 &#40;Master Data Services&#41;](../../2014/master-data-services/validation-master-data-services.md)  
  
  
