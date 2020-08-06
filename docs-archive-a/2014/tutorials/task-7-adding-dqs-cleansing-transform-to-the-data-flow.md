---
title: 工作7：將 DQS 清理轉換加入至資料流程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0b749c71-dfb6-493a-804f-600290d46eef
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 887bc361a51b61e9137404e054bd52e2b630ca5d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592379"
---
# <a name="task-7-adding-dqs-cleansing-transform-to-the-data-flow"></a>工作 7：將 DQS 清理轉換新增至資料流程
  在這項工作中，您將使用 DQS 將 DQS 清理轉換加入至資料流程來清理輸入供應商資料。 如需有關轉換的詳細資訊，請參閱**[DQS 清理轉換](https://msdn.microsoft.com/library/ee677619.aspx)**。  
  
1.  以滑鼠右鍵**按一下 [資料流程**] 索引標籤中的 [ **DQS 清理**]，然後按一下 [**重新命名**] 輸入**清理供應商資料**，然後按**enter**。  
  
2.  選取 [**從 Excel 檔案讀取供應商資料**];拖曳藍色連接器以**清理供應商資料**。 現在已連接這些元件。  
  
     ![讀取供應商資料-> 清理供應商資料](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-01.jpg "讀取供應商資料-> 清理供應商資料")  
  
3.  按兩下 [**清理供應商資料**]。  
  
4.  在 [ **DQS 清理轉換編輯器**] 中，按一下 [**資料品質連接管理員] 下拉式清單**旁邊的 [**新增**]。  
  
5.  在 [ **DQS 清理連接管理員**] 對話方塊中，輸入** (local) **或**period** (. ) 以連接到本機伺服器。 本課程假設您已經在本機伺服器上安裝 DQS。  
  
6.  按一下 [**測試連接**] 來測試 DQS 伺服器的連接。  
  
7.  按一下 **[確定]** ，關閉對話方塊。  
  
8.  針對 [**資料品質知識庫**] 選取 [**供應商**]。  
  
     ![DQS 清理轉換編輯器 - 供應商知識庫](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-02.jpg "DQS 清理轉換編輯器 - 供應商知識庫")  
  
9. 切換至頂端的 [**對應**] 索引標籤。  
  
10. 從**可用的輸入**資料行中，選取 [**供應商名稱**]、[ **ContactEmailAddress**]、[**位址線** **]、[****城市**]、[**國家/地區**] 和 [**郵遞區號**]，方法是選取  
  
     ![DQS 清理轉換編輯器 - 對應](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-03.jpg "DQS 清理轉換編輯器 - 對應")  
  
11. 在底部窗格中，使用 [**定義域**] 資料行中的下拉式清單來對應這些資料行：  
  
    |資料行|網域|  
    |------------|------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|連絡人電子郵件|  
    |[地址行]|[地址行]|  
    |城市|城市|  
    |州|州|  
    |國家/地區|國家/地區|  
    |Zip Code|Zip|  
  
12. 按一下 **[確定]** 以關閉 [ **DQS 清理轉換編輯器**] 對話方塊。  
  
## <a name="next-step"></a>後續步驟  
 [工作 8：新增條件式分割轉換來分割清理輸出](../../2014/tutorials/task-8-adding-conditional-split-transform-to-split-cleansing-output.md)  
  
  
