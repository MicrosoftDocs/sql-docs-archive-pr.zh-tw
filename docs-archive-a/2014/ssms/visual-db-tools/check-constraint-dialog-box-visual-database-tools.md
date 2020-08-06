---
title: 檢查條件約束對話方塊 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.checkconstraint
ms.assetid: ad0bbf7f-b0de-406a-bd0a-cb779816b101
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7244984b869a1c68e597984a1cd03e16e53d0306
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584238"
---
# <a name="check-constraint-dialog-box-visual-database-tools"></a>檢查條件約束對話方塊 (Visual Database Tools)
  當您在資料表設計工具的資料表定義方格上按一下滑鼠右鍵，再按 [檢查條件約束]  時，這個對話方塊便會出現。 此對話方塊包含一組附加至資料庫資料表的非唯一條件約束的屬性。 套用至唯一條件約束的屬性會出現在 [索引/索引鍵]  對話方塊中。  
  
> [!NOTE]  
>  如果資料表是要發佈以進行複寫，則必須使用 Transact-SQL 陳述式 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) 或 SQL Server 管理物件 (SMO) 變更結構描述。 使用 [資料表設計工具] 或 [資料庫圖表設計工具] 變更結構描述時，會嘗試卸除並重新建立資料表。 您無法卸除已發行的物件，因此結構描述變更將會失敗。  
  
## <a name="options"></a>選項。  
 **選取的檢查條件約束**  
 列出可用的檢查條件約束。 若要檢視條件約束的屬性，請在清單中選取該條件約束。  
  
 **加入**  
 為選取的資料庫資料表建立新的條件約束，並提供該條件約束的預設名稱和其他值。 在輸入條件約束的運算式之後，條件約束才會有效。  
  
 **刪除**  
 從資料表中刪除選取的條件約束。 若要刪除加入的檢查條件約束，請使用此按鈕移除該條件約束。  
  
 **一般類別目錄**  
 展開以顯示 [運算式]  屬性欄位。  
  
 **運算式**  
 顯示已選取之檢查條件約束的運算式。 對於新的條件約束，退出此方塊之前必須先輸入運算式。 您也可以編輯現有的檢查條件約束。 如需詳細資訊，請參閱 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)。  
  
 **識別類別目錄**  
 展開以顯示 [名稱]  與 [描述]  屬性。  
  
 **名稱**  
 顯示已選取之檢查條件約束的名稱。 若要變更這個條件約束的名稱，請直接在屬性欄位中輸入文字。  
  
 **說明**  
 描述此檢查條件約束。 您可以在屬性欄位中鍵入來編輯描述，或按一下屬性欄位右側的省略符號按鈕 ( **...** )，並編輯 [描述屬性]  對話方塊中的描述。  
  
 **資料表設計工具類別目錄**  
 展開以顯示 [檢查建立或重新啟用時的現有資料]  、[於 INSERT 及 UPDATE 時強制套用]  與 [強制複寫]  的屬性。  
  
 **檢查建立或重新啟用時的現有資料**  
 指定是否依照條件約束驗證所有先前已存在的資料 (在建立條件約束前已存在於資料表中的資料)。  
  
 **於 INSERTs 及 UPDATEs 時強制套用**  
 指定是否在將資料插入資料表中或更新資料表時，強制使用條件約束。  
  
 **強制複寫**  
 指示當複寫代理程式在此資料表上執行插入或更新時，是否要強制使用條件約束。  
  
## <a name="see-also"></a>另請參閱  
 [Unique 條件約束和 Check 條件約束](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [[索引和索引鍵] 對話方塊 &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
