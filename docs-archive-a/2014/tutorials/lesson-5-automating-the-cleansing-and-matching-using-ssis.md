---
title: 第5課：使用 SSIS 自動化清理和比對 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f068d4db-2d56-41b1-bed2-0cffa3ca411d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 90f967b2446e11a27f5a87803bb71d6e1ec53557
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87702194"
---
# <a name="lesson-5-automating-the-cleansing-and-matching-using-ssis"></a>第 5 課：使用 SSIS 將清理和比對自動化
  在第1課中，您已建立供應商知識庫，並用它來清理第2課中的資料，並使用**DQS 用戶端**工具來比對第3課的資料。 在真實世界的案例中，您可能必須從 DQS 不支援的來源提取資料，或者您想要自動化清理和比對程式，而不需要使用**DQS 用戶端**工具。 SQL Server Integration Services (SSIS) 具有元件，可讓您用來整合各種不同來源的資料，以及使用**[Dqs 清理轉換](https://msdn.microsoft.com/library/ee677619.aspx)** 元件來叫用 dqs 所公開的清理功能。 目前，DQS 不會公開要使用之 SSIS 的比對功能，但您可以使用**[模糊群組轉換](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)** 來識別資料中的重複項。  
  
 您可以使用以**實體為基礎的暫存功能**，將資料上傳至 MDS。 當您在 MDS 中建立實體時，將會自動建立對應的暫存資料表和預存程序。 例如，當您建立供應商實體時，會自動建立**supplier_Leaf stg.<** 資料表和**udp_Supplier_Leaf stg.<** 預存程式。 您會使用暫存資料表和程序來建立、更新及刪除實體成員。 在這一課，您會建立 Supplier 實體的新實體成員。 為了將資料載入 MDS 伺服器，SSIS 封裝會先將資料載入暫存資料表 stg.supplier_Leaf，然後觸發相關的預存程序 stg.udp_Supplier_Leaf。 如需詳細資訊，請參閱匯[入資料](../master-data-services/overview-importing-data-from-tables-master-data-services.md)。  
  
 在這一課，您會執行下列工作：  
  
1.  在 MDS 中移除供應商資料 (如果您已經完成之前的四個課程)。 您在這一課建立的 SSIS 封裝會將資料自動上傳至 MDS。 您在稍早已使用 DQS 用戶端，手動將已清理和比對的供應商資料上傳至 MDS 伺服器。  
  
2.  請在 Supplier 實體中建立訂閱檢視，向其他應用程式公開此實體中的資料。 此動作會建立一個 SQL 檢視表，您將使用 SQL Server Management Studio 加以驗證。 您不會在這一版的教學課程中使用這個檢視表。  
  
3.  使用**SQL Server Data Tools**建立及執行 SSIS 專案。 專案會使用**資料清理**轉換，將清理要求提交至 DQS 伺服器。 DQS 尚未公開相符的功能，因此您將使用**模糊群組**轉換來識別重複專案。  
  
4.  確認已使用主資料管理員在 MDS 中建立資料。  
  
5.  檢閱 SSIS 封裝所建立之 DQS 清理專案的結果，並選擇性地執行互動式清理，進一步建立知識庫。  
  
## <a name="next-step"></a>後續步驟  
 [工作 1 &#40;必要條件&#41;：在 MDS 中移除供應商資料](../../2014/tutorials/task-1-prerequisite-removing-supplier-data-in-mds.md)  
  
  
