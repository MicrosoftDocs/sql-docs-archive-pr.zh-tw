---
title: 工作1：定義比對原則 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6f89a720-fce5-4f60-bef3-a159bbc9f25c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bb2556874174939c46d91c6d89e797393d590914
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585709"
---
# <a name="task-1-defining-a-matching-policy"></a>工作 1：定義比對原則
  在這項工作中，您會建立包含一個規則的比對原則。 此規則會有一個必要條件：**供應商識別碼**，這表示供應商識別碼必須符合，才能使用規則中的其他網域。 此規則會使用其他兩個網域： [**具有相似性**的**供應商名稱**] 值設為 [ **70%** ] **，並將**[**相似性**] 值設為**30%**。  
  
1.  在**DQS 用戶端**的主頁面中，按一下 [**供應商**知識庫] 旁的**向右箭**號，然後選取 [比對**原則**]。  
  
     ![主頁面上的 [比對原則] 功能表](../../2014/tutorials/media/et-definingamatchingpolicy-01.jpg "主頁面上的 [比對原則] 功能表")  
  
2.  在 [**對應**] 頁面上，針對 [**資料來源**] 選取 [ **Excel**檔案]。  
  
3.  按一下 **[流覽]**，確認 [篩選] 設定為 [ **Excel 活頁簿**]，然後選取您在執行清理活動之後所匯出的**清理供應商 List.xls**檔案。  
  
    > [!NOTE]  
    >  在此活動結束時，您將無法匯出結果，因為此活動主要著重於定義比對原則。 您將會針對比對活動建立資料品質專案，並在下一課使用這個比對原則來執行專案，以便從供應商清單中移除重複項。  
  
4.  將**供應商的資料行對應至****供應商識別碼**網域、**供應商名稱**資料行至**供應商名稱**網域、 **ContactEmailAddress**資料行到**連絡人電子郵件**網域。 您只需要將來源資料行對應至定義比對原則所要使用的定義域。 在此情況下，您會提供 Supplier ID、Supplier Name 和 Contact Email 等定義域給比對原則活動使用。  
  
     ![比對原則定義程序的 [對應] 頁面](../../2014/tutorials/media/et-definingamatchingpolicy-02.jpg "比對原則定義程序的 [對應] 頁面")  
  
5.  按 **[下一步]** 移至 [比對**原則**] 頁面，您將在其中定義比對原則，其中包含一個規則。  
  
6.  按一下工具列上的 [建立比對**規則**] 按鈕，以在原則中建立規則。  
  
     ![[建立比對規則] 工具列按鈕](../../2014/tutorials/media/et-definingamatchingpolicy-03.jpg "[建立比對規則] 工具列按鈕")  
  
7.  在右側的 [**規則詳細資料**] 窗格中，針對 [**規則名稱**] 輸入 [**移除重複的供應商**]。  
  
8.  在右窗格的工具列中，按一下 [**加入新的定義域元素**]。  
  
     ![規則詳細資料 - [加入新的定義域項目] 按鈕](../../2014/tutorials/media/et-definingamatchingpolicy-04.jpg "規則詳細資料 - [加入新的定義域項目] 按鈕")  
  
9. 選取**網域**的 [**供應商識別碼**]，然後選取 [必要條件 **] 核取方塊**。 請注意，**相似性**會自動設定為 [**精確**]。 藉由將**供應商識別碼**設定為**必要條件，您**可以指定兩筆記錄中此欄位的值必須傳回100% 相符，否則這些記錄不會被視為相符，而且會忽略規則中的其他子句。  
  
     ![移除重複供應商規則定義](../../2014/tutorials/media/et-definingamatchingpolicy-05.jpg "移除重複供應商規則定義")  
  
10. 再次按一下工具列上的 [**加入新的定義域元素**]。  
  
11. 選取 [**供應商名稱**] [網域]，選取 [**類似** **]，並針對 [****權數**] 輸入**70** 。  您在此指定供應商名稱不需要完全相同但可以類似，以便讓記錄視為相符。 權數表示此欄位的分數占整體符合分數的比重。  
  
12. 重複先前的兩個步驟，為**權數**新增具有**30**的**連絡人電子郵件**網域。  
  
13. 請注意，[**最小符合分數**] 設定為 [ **80%**]，這是您在**DQS 管理**的 [設定 **] 頁面的**[**一般**] 索引標籤中看到的值。 您在這裡只能增加這個分數，使其高於此臨界值。  
  
14. 請注意，已選取 [重**迭**的叢集] 選項。 有了這個選項，記錄就會出現在多個叢集中。 如果您將設定變更為 [非重疊的叢集]，具有共同記錄的叢集就會結合到單一叢集中。  
  
15. 此頁面上的 [**開始**] 按鈕可讓您分別測試原則中的每個規則，而下一個頁面中的 [開始] 按鈕可讓您測試整個原則 (原則) 中的所有規則。  
  
16. 按 **[下一步]** 切換至 [比對**結果**] 頁面。  
  
## <a name="next-step"></a>後續步驟  
 [工作 2：測試和發行比對原則](../../2014/tutorials/task-2-testing-and-publishing-the-matching-policy.md)  
  
  