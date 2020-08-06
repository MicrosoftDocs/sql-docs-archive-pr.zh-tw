---
title: 從採礦結構移除資料行 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], columns
- removing columns
- deleting columns
- columns [data mining], mining structure columns
ms.assetid: 41073ffe-9351-416b-9f0c-62634bc213f9
author: minewiskan
ms.author: owend
ms.openlocfilehash: 44ad1de08d57d00fd9798e1ceeddb85d146d7111
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584838"
---
# <a name="remove-columns-from-a-mining-structure"></a>從採礦結構中移除資料行
  在建立採礦結構之後，您可以使用資料採礦設計師，從採礦結構中移除資料行。 移除採礦結構資料行的原因可能包含下列：  
  
-   採礦結構包含某個資料行的多個複本並且您想要在模型中避免使用重複資料。  
  
-   資料應受到保護，但已啟用鑽研。  
  
-   資料未在模型化中使用並且不應處理。  
  
 從採礦結構中刪除資料行並不會在資料來源檢視或外部資料中變更該資料行，只刪除中繼資料。 但在您變更採礦結構中使用的資料行時，必須重新處理採礦結構和以它為基礎的所有模型。  
  
### <a name="to-remove-a-column-from-the-mining-structure"></a>若要從採礦結構中移除資料行  
  
1.  選取資料採礦設計師中的 **[採礦結構]** 索引標籤。  
  
2.  展開採礦結構的樹狀，以顯示所有資料行。  
  
3.  以滑鼠右鍵按一下您想要刪除的資料行，然後選取 [刪除]****。  
  
4.  在 **[刪除物件]** 對話方塊中，按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構工作和使用說明](mining-structure-tasks-and-how-tos.md)  
  
  
