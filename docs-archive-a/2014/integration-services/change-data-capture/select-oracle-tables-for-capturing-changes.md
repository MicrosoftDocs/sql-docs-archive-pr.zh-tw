---
title: 選取 Oracle 資料表來擷取變更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- selOraTabDia
ms.assetid: 2e295dc8-999d-4c4d-96cc-1519674b47a4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e9064789dce83ff7d3917ed026c861743142e048
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704342"
---
# <a name="select-oracle-tables-for-capturing-changes"></a>選取 Oracle 資料表來擷取變更
  使用此對話方塊來選取 CDC 執行個體中所包含的資料表。 選取的資料表會加入至新增執行個體精靈中 **[選取資料表和資料行]** 頁面的清單中。 您可以在此對話方塊中執行下列動作。  
  
 根據預設，此對話方塊的資料表清單中不包含任何資料表。 您可以選取核取方塊資料行頂端的核取方塊，以選取所有資料表或是搜尋特定資料表。  
  
 **若要搜尋特定資料表**  
 依照以下方式輸入搜尋準則，然後按一下 [搜尋]  ：  
  
-   **結構描述**：從清單中選取資料庫結構描述。 清單中只會包含具有該結構描述的資料表。  
  
-   **資料表名稱模式**：輸入任何字元字串。 只會顯示包含所輸入之字元字串的資料表。  
  
> [!NOTE]  
>  您可以在一個或兩個欄位中輸入準則。  
  
-   **顯示前 1000 個相符的資料表**：預設會選取這個核取方塊。 它會將顯示畫面限制為前 1000 個相符的資料表。 如果您清除此核取方塊，符合準則的所有資料表都會顯示。 如果有大量的資料表，則顯示清單可能需要很長的時間。  
  
 **若要選取包含在 CDC 執行個體中的資料表**  
 按一下您想要包含之任何資料表旁邊的核取方塊，然後按一下 [加入]  。 資料表隨即加入至新增執行個體精靈中 **[選取資料表和資料行]** 頁面的清單中。  
  
 按一下 **[關閉]** ，關閉此對話方塊，而不加入任何其他資料表。  
  
> [!NOTE]  
>  如果您選取的資料表包含不支援的資料類型，您會看到錯誤訊息而且不會包含該資料表。  
  
## <a name="see-also"></a>另請參閱  
 [如何建立 SQL Server 變更資料庫執行個體](how-to-create-the-sql-server-change-database-instance.md)   
 [選取 Oracle 資料表和資料行](select-oracle-tables-and-columns.md)  
  
  
