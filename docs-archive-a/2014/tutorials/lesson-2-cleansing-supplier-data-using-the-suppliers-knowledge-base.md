---
title: 第2課：使用供應商知識庫清理供應商資料 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 215c14de-fc3f-46de-a022-bf69b9ea2a96
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ebc0231cd0f28fcad23656cf22abd8d68eca7dc4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584908"
---
# <a name="lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base"></a>第 2 課：使用供應商知識庫清理供應商資料
  在這一課，您會使用您在第一課建立的**供應商**知識庫來清理 Excel 檔案中的供應商資料。 DQS 中的資料清理包含**電腦輔助**的程式，可分析資料符合知識庫中知識的方式，以及可讓您從電腦輔助的程式中檢查和修改結果的**互動式進程**。 資料清理功能會識別資料來源中不正確的資料，然後針對不正確的資料進行更正或建議更正。 它也會使用定義域值、同義字的前置值、定義域規則、以詞彙為主的關聯及參考資料來標準化及豐富客戶資料。 您可以用互動方式核准或拒絕電腦輔助程序所提議的變更。 如需詳細資訊，請參閱[資料清理](https://msdn.microsoft.com/library/gg524800.aspx)。  
  
 電腦輔助程序會使用以下的臨界值，您可以在 DQS 用戶端主頁面上使用 [組態] 選項設定此值。  
  
-   **建議的最低分數：** DQS 用來建議取代值的最低分數或信賴等級。  
  
-   **自動校正的最低分數：** DQS 用來自動校正值的最低分數或信賴等級。  
  
 如需如何設定這些設定的詳細資訊，請參閱[設定清理和](https://msdn.microsoft.com/library/hh510415.aspx)比對的臨界值。  
  
 在這一課，您會使用供應商知識庫來執行下列工作，以清理輸入資料。  
  
1.  建立清理用的資料品質專案、選取供應商知識庫做為用來分析及清理 Excel 檔案中來源資料的知識庫，並選取清理活動。  
  
2.  將您想要清理的 Excel 資料行對應到知識庫中適當的 DQS 定義域/複合定義域。  
  
3.  執行電腦輔助的清理活動。 電腦輔助程序會在 Data Quality Client 中顯示資料品質資訊，讓您可用來以互動方式清理資料。  
  
4.  檢視及管理清理活動的結果。 您可以檢閱電腦輔助程序所發現正確的值、不正確但是已更正的值、不正確且有建議值的值或是無效的值。 您可以用互動方式核准或拒絕變更，使用 [更正為] 欄位更正或覆寫電腦輔助程序的建議。  
  
5.  將清理程序的結果匯出到 Excel 檔案。  
  
6.  將清理專案中的值匯入定義域，以新的規則、值、更正等功能來增強知識庫中的知識。  
  
## <a name="next-step"></a>後續步驟  
 [工作 1：建立資料品質專案](../../2014/tutorials/task-1-creating-a-data-quality-project.md)  
  
  
