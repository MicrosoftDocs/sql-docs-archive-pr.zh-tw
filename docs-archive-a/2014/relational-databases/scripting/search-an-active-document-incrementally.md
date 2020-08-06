---
title: 以累加方式搜尋作用中的文件
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- searches [SQL Server Management Studio], incremental
- Query Editor [SQL Server Management Studio], incremental search
- incremental searches [SQL Server Management Studio]
ms.assetid: 490bb36c-dd43-4219-9e2a-ff27046b9395
author: rothja
ms.author: jroth
ms.openlocfilehash: aefc2f0b7abff5992a8f4f7817e564ef1b72009d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592596"
---
# <a name="search-an-active-document-incrementally"></a>以累加方式搜尋作用中的文件
  您可以輸入文字，以累加方式來搜尋單一文件或視窗。 搜尋作業會反白顯示第一組符合文件或視窗中之累加搜尋期間所輸入之字元的字元。 累加搜尋會自動搜尋文件或視窗內的所有文字，不過，隱藏的文字除外。  
  
 對於 **[大小寫須相符]** 選項，累加搜尋會使用上一次搜尋的準則。 例如，如果您利用 [檔案中尋找]  對話方塊搜尋了多個檔案，且選取 [大小寫須相符]  ，您下次累加搜尋時，搜尋會區分大小寫。  
  
### <a name="to-search-incrementally"></a>累加搜尋  
  
1.  開啟您要搜尋的檔案或視窗。  
  
2.  在 **[編輯]** 功能表上，指向 **[進階]** ，再按一下 **[累加搜尋]** 。  
  
     此時游標圖示會改成含箭頭 (表示搜尋方向) 的雙筒望遠鏡，狀態列會顯示「累加搜尋」。  
  
3.  開始輸入文字字串。  
  
     狀態列會顯示您輸入的文字，編輯器會反白顯示符合這個文字的第一個出現項目。 當您繼續輸入時，編輯器會移到下一個相符項目，並反白顯示這個項目。 如果找不到相符項目，狀態列會顯示如下：  
  
    ```  
    Incremental Search: <text> (not found)  
    ```  
  
 累加搜尋是從文件的目前位置開始執行，由上至下，由左至右。 您可以利用鍵盤快速鍵來執行累加搜尋。  
  
> [!NOTE]  
>  如需完整的鍵盤快速鍵清單，請參閱 [SQL Server Management Studio 鍵盤快速鍵](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)。  
  
## <a name="see-also"></a>另請參閱  
 [搜尋和取代](search-and-replace.md)   
 [以互動方式搜尋文件](search-documents-interactively.md)   
 [使用結果清單搜尋文件](search-documents-using-results-lists.md)   
 [使用萬用字元搜尋文字](search-text-with-wildcards.md)   
 [使用規則運算式搜尋文字](search-text-with-regular-expressions.md)  
  
  
