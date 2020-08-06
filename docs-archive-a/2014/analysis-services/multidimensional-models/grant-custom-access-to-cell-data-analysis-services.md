---
title: " (Analysis Services) 中授與資料格資料的自訂存取權 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.celldata.f1
helpviewer_keywords:
- user access rights [Analysis Services], cell data
- permissions [Analysis Services], cells
- read contingent permissions
- read permissions
- cells [Analysis Services]
- custom cell data access [Analysis Services]
ms.assetid: 3b13a4ae-f3df-4523-bd30-b3fdf71e95cf
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9ac8113348a749837867a6dacba7fa23fb5e85f2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686518"
---
# <a name="grant-custom-access-to-cell-data-analysis-services"></a>授與資料格資料的自訂存取權 (Analysis Services)
  資料格安全性可用來允許或拒絕存取 Cube 內的量值資料。 下圖顯示在利用其角色僅允許存取特定量值的使用者身分連接時，樞紐分析表中允許和拒絕的量值組合。 在此範例中， **Reseller Sales Amount** 及 **Reseller Total Product Cost** 是唯二能夠透過此角色取得的量值。 所有其他量值都會明確遭到拒絕 (下一節＜允許存取特定量值＞將提供用來取得這個結果的步驟)。  
  
 ![顯示允許與拒絕之資料格的樞紐分析表](../media/ssas-permscellsallowed.png "顯示允許與拒絕之資料格的樞紐分析表")  
  
 資料格權限適用於資料格內部的資料，不適用於它的中繼資料。 請注意資料格如何仍在查詢結果中顯示，但顯示的是 `#N/A` 的值，而非實際的資料格值。 此 `#N/A` 值會出現在資料格中，除非用戶端應用程式轉譯值，或在連接字串中設定安全的資料格值屬性來指定另一個值。  
  
 若要完全隱藏資料格，您必須限制可以看見的成員-維度、維度屬性和維度屬性成員。 如需詳細資訊，請參閱 [授與維度資料的自訂存取權 &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)。  
  
 身為管理員，您可以指定角色成員對 Cube 內的資料格是否擁有讀取、意外讀取或讀取/寫入權限。 在資料格中設定權限是允許的最低安全性層級，因此，在您開始套用這個層級的權限之前，請務必記住下列幾項事實：  
  
-   資料格層級安全性無法延伸已在較高層級中受到限制的權限。 範例：如果角色拒絕對維度資料的存取，資料格層級安全性便無法覆寫拒絕的集合。 另一個範例：假設有一個具有 `Read` cube 許可權的角色，以及一個資料格的**讀取/寫入**許可權，則資料格資料許可權將不會是**讀取/寫入**，它會是 `Read` 。  
  
-   自訂權限通常需要在維度成員與同一角色內的資料格之間協調。 例如，假設您想要針對不同的轉售商組合拒絕對數個與折扣相關之量值的存取。 假設 **Resellers** 是維度， **Discount Amount** 是量值，您就必須在相同角色中，結合量值的權限 (遵循本主題中的指示) 與維度成員的權限。 如需設定維度權限的詳細資訊，請參閱 [授與維度資料的自訂存取權 &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) 。  
  
 資料格層級安全性是透過 MDX 運算式所指定。 由於資料格是 Tuple (也就是，可能橫跨數個維度和量值的交集點)，因此需要使用 MDX 來識別特定資料格。  
  
## <a name="allow-access-to-specific-measures"></a>允許存取特定量值  
 您可以使用資料格安全性，明確選擇要使用哪些量值。 一旦明確識別允許的成員之後，所有其他成員就會變成無法使用。 這可能是透過 MDX 指令碼實作的最簡單案例，如同下列步驟所述。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，選取資料庫，開啟 [角色]**** 資料夾，然後按一下資料庫角色 (或建立新的資料庫角色)。 成員資格應該已經指定，而角色應該擁有 Cube 的 `Read` 存取權。 如需詳細資訊，請參閱 [授與 Cube 或模型權限 &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md) 。  
  
2.  在 **[資料格資料]** 中，檢查 Cube 選取項目以確定您已選擇正確的選項，然後選取 **[啟用讀取權限]**。  
  
     如果您只選取這個核取方塊，而且未提供 MDX 運算式，效果就和拒絕存取 Cube 中的所有資料格一樣。 這是因為當 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 解析 Cube 資料格子集時，預設允許的集合是空集合。  
  
3.  輸入以下 MDX 運算式。  
  
    ```  
    (Measures.CurrentMember IS [Measures].[Reseller Sales Amount]) OR (Measures.CurrentMember IS [Measures].[Reseller Total Product Cost])  
    ```  
  
     這個運算式會明確識別使用者可看見的量值。 透過這個角色連線的使用者將無法使用其他任何量值。 請注意，[CurrentMember &#40;MDX&#41;](/sql/mdx/current-mdx) 會設定內容，且後面會接著允許的量值。 若目前的成員包含 **Reseller Sales Amount** 或 **Reseller Total Product Cost**，則此運算式會顯示值。 否則，便會拒絕存取。 運算式含有多個部分，每個部分都會以括號括起來。 `OR` 運算子可用來指定多個量值。  
  
## <a name="deny-access-to-specific-measures"></a>拒絕存取特定量值  
 下列 MDX 運算式（也在**Create Role**  |  **Cell Data**  |  **允許讀取 cube 內容**中指定）具有相反的效果，因而無法使用某些量值。 在此範例中，**折扣金額**和**折扣百分比**無法使用 `NOT` 和運算子來取得 `AND` 。 透過這個角色連接的使用者將可看見所有其他量值。  
  
```  
(NOT Measures.CurrentMember IS [Measures].[Discount Amount]) AND (NOT Measures.CurrentMember IS [Measures].[Discount Percentage])  
```  
  
 在 Excel 中，可以在下圖中清楚看見資料格安全性：  
  
 ![將資料格顯示為無法使用狀態的 Excel 資料行](../media/ssas-permscellshidemeasure.png "將資料格顯示為無法使用狀態的 Excel 資料行")  
  
## <a name="set-read-permissions-on-calculated-measures"></a>設定導出量值的讀取權限  
 導出量值的權限可以獨立設定它的構成部分。 如果您想要協調導出量值與其相依量值之間的權限，請直接前往下一節有關「意外讀取」的部分。  
  
 若要了解導出量值的讀取權限如何運作，請考量 AdventureWorks 中的 **Reseller Gross Profit** 。 它是衍生自 **Reseller Sales Amount** 和 **Reseller Total Product Cost** 量值。 只要角色擁有 **Reseller Gross Profit** 資料格的讀取權限，就可以檢視這個量值，即使權限在其他量值上明確遭到拒絕也可以檢視。 做為示範，請將下列 MDX 運算式複製到 [**建立角色**  |  **資料格資料**] [  |  **允許讀取 cube 內容**]。  
  
```  
(NOT Measures.CurrentMember IS [Measures].[Reseller Sales Amount])  
AND (NOT Measures.CurrentMember IS [Measures].[Reseller Total Product Cost])  
```  
  
 在 Excel 中，使用目前角色連接到 Cube，然後選擇這三個量值來查看資料格安全性的效果。 請注意，拒絕集合中的量值是無法使用的，但使用者可以看見導出量值。  
  
 ![含有可用與無法使用之資料格的 Excel 資料表](../media/ssas-permscalculatedcells.png "含有可用與無法使用之資料格的 Excel 資料表")  
  
## <a name="set-read-contingent-permissions-on-calculated-measures"></a>設定導出量值的意外讀取權限  
 資料格安全性提供另一種選擇 (意外讀取)，用以設定參與計算之相關資料格的權限。 請再次考量 **Reseller Gross Profit** 範例。 當您輸入上一節所提供的相同 MDX 運算式時，會將此時間放入 [**建立角色**  |  **資料格資料**] 對話方塊的第二個文字區域中 (在下列文字區域中，[允許讀取資料格安全性) 的資料**格內容**]，在 Excel 中觀看時，結果會很明顯。 由於 **Reseller Gross Profit** 會根據 **Reseller Sales Amount** 和 **Reseller Total Product Cost**而定，所以，現在會因為無法存取毛利的構成部分而無法存取毛利。  
  
> [!NOTE]  
>  如果您在同一角色內同時設定資料格的讀取和意外讀取權限會發生什麼事？ 角色將在資料格上提供讀取權限，而非意外讀取權限。  
  
 一如前文所述，在只選取 [啟用意外讀取權限]**** 核取方塊，而未提供任何 MDX 運算式的情況下，會拒絕對 Cube 中所有資料格的存取。 這是因為當 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 解析 Cube 資料格子集時，預設允許的集合是空集合。  
  
## <a name="set-readwrite-permissions-on-a-cell"></a>設定資料格的讀取/寫入權限  
 假設成員對 Cube 本身具有讀取/寫入權限，即可使用資料格的讀取/寫入權限來啟用回寫功能。 在資料格層級授與的權限不得大於在 Cube 層級授與的權限。 如需詳細資訊，請參閱＜ [Set Partition Writeback](set-partition-writeback.md) ＞。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 產生器 &#40;Analysis Services 多維度資料&#41;](../mdx-builder-analysis-services-multidimensional-data.md)   
 [基本 MDX 腳本 &#40;MDX&#41;](mdx/the-basic-mdx-script-mdx.md)   
 [授與處理許可權 &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)   
 [授與維度的許可權 &#40;Analysis Services&#41;](grant-permissions-on-a-dimension-analysis-services.md)   
 [將維度資料的自訂存取權授與 &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)   
 [授與 Cube 或模型權限 &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)  
  
  
