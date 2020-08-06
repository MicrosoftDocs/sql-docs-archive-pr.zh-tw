---
title: 在資料表中插入及更新資料 (教學課程) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- inserting and updating data
ms.assetid: 514dc87a-b829-43b5-8fc8-1a400a260284
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0646019f166e1c2cc126a4cc7d2ed8f27a7bd2f3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597479"
---
# <a name="inserting-and-updating-data-in-a-table-tutorial"></a>在資料表中插入及更新資料 (教學課程)
  既然您現在建立好 **Products** 資料表，就可以準備使用 INSERT 陳述式，將資料插入資料表。 在插入資料後，您將使用 UPDATE 陳述式來變更資料列的內容。 您將使用 UPDATE 陳述式的 WHERE 子句，限制對單一資料列進行更新。 接下來所述的四個陳述式將輸入下面資料。  
  
|ProductID|ProductName|價格|ProductDescription|  
|---------------|-----------------|-----------|------------------------|  
|1|Clamp|12.48|Workbench clamp|  
|50|Screwdriver|3.17|Flat head|  
|75|Tire Bar||Tool for changing tires.|  
|3000|3mm Bracket|.52||  
  
 基本語法包括：INSERT、資料表、資料行清單、VALUES 以及要插入的值清單。 程式行前面的兩個連字號表示該程式行是註解，而編譯器會忽略這行文字。 在本案例中，註解說明所允許的語法變化。  
  
### <a name="to-insert-data-into-a-table"></a>將資料插入資料表  
  
1.  執行下列陳述式，將資料列插入上一項工作中建立的 `Products` 資料表。 以下是基本語法。  
  
    ```  
    -- Standard syntax  
    INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
        VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
    GO  
  
    ```  
  
2.  下列陳述式示範如何可以在透過切換欄位清單 (括號內) 和值清單內 `ProductID` 和 `ProductName` 的位置所提供的參數中變更順序。  
  
    ```  
    -- Changing the order of the columns  
    INSERT dbo.Products (ProductName, ProductID, Price, ProductDescription)  
        VALUES ('Screwdriver', 50, 3.17, 'Flat head')  
    GO  
  
    ```  
  
3.  下列陳述式示範只要依照正確的順序列出值，就可以省略資料行的名稱。 這是常見的語法，但不建議您使用，因為其他使用者可能會很難了解您的程式碼。 `NULL` 已針對 `Price` 資料行指定，這是因為此產品的價格不明。  
  
    ```  
    -- Skipping the column list, but keeping the values in order  
    INSERT dbo.Products  
        VALUES (75, 'Tire Bar', NULL, 'Tool for changing tires.')  
    GO  
  
    ```  
  
4.  只要是在預設的結構描述中存取及變更資料表，就可以省略結構描述名稱。 因為 `ProductDescription` 資料行可以接受 Null 值及無值，所以在陳述式中便可以完全省略 `ProductDescription` 資料行名稱和值。  
  
    ```  
    -- Dropping the optional dbo and dropping the ProductDescription column  
    INSERT Products (ProductID, ProductName, Price)  
        VALUES (3000, '3mm Bracket', .52)  
    GO  
    ```  
  
### <a name="to-update-the-products-table"></a>更新 Products 資料表  
  
1.  輸入並執行下列 `UPDATE` 陳述式，將第二個產品的 `ProductName` 從 `Screwdriver`變更為 `Flat Head Screwdriver`。  
  
    ```  
    UPDATE dbo.Products  
        SET ProductName = 'Flat Head Screwdriver'  
        WHERE ProductID = 50  
    GO  
    ```  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [讀取資料表的資料 &#40;教學課程&#41;](lesson-1-4-reading-the-data-in-a-table.md)  
  
## <a name="see-also"></a>另請參閱  
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)  
  
  
