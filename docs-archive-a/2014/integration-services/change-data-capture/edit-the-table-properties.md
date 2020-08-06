---
title: 編輯資料表屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- editTabProps
ms.assetid: 95ea72ba-8e40-4177-a963-0fb4d10c56e3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1ba0809b99474704ec0e93e417a04d776bb26d9a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593520"
---
# <a name="edit-the-table-properties"></a>編輯資料表屬性
  使用此對話方塊，從正在擷取變更的選定資料表中編輯特定資料行。 您也可以編輯 **[安全性角色]** 和 **[擷取執行個體]** 資訊。  
  
### <a name="to-edit-the-columns-to-include-in-the-cdc-instance"></a>若要編輯 CDC 執行個體中所包含的資料行  
  
1.  執行下列其中一項或兩項作業：  
  
    -   選取您要包含的其他任何資料行旁邊的核取方塊。  
  
    -   清除您不想再包含的任何資料行旁邊的核取方塊。  
  
### <a name="to-edit-the-security-role"></a>若要編輯安全性角色  
  
1.  在 **[安全性角色]** 欄位中，輸入新的名稱或是編輯安全性角色的名稱。  
  
### <a name="to-create-a-new-capture-instance"></a>若要建立新的擷取執行個體  
  
1.  在 **[安全性角色]** 區段的 **[名稱]** 欄位中，輸入擷取執行個體的名稱。 根據預設，在此欄位中輸入的名稱會是名稱結尾加上 **_NEW** 的目前擷取執行個體名稱 (例如 **old_instance_NEW**)。  
  
2.  將擷取執行個體儲存為下列其中一項：  
  
    -   **新的擷取執行個體**：此情況下會儲存新的擷取執行個體，而且不會刪除舊的擷取執行個體。  
  
         **注意**：每一個資料表不能有兩個以上的擷取執行個體。 如果已經有兩個擷取執行個體，就無法使用這個選項。  
  
    -   **取代現有的**：此情況下會刪除目前的擷取執行個體，並由您建立的擷取執行個體取代。 如果已經為此資料表定義兩個擷取執行個體，您必須選取其中一個來替換。  
  
 **注意**：您可以從 **[資料表]** 索引標籤的資料表清單中移除擷取執行個體。  
  
 在此對話方塊中輸入資訊完畢後，請按一下 **[確定]** 接受變更。  
  
## <a name="see-also"></a>另請參閱  
 [如何編輯 CDC 執行個體屬性](how-to-edit-the-cdc-instance-properties.md)   
 [針對為了擷取變更所選取的資料表進行變更](make-changes-to-the-tables-selected-for-capturing-changes.md)  
  
  
