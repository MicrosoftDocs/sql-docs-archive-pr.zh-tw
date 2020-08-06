---
title: 建立新條件或開啟條件對話方塊，一般頁面 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.condition.f1
ms.assetid: 106954bf-e4ba-412b-9c1a-907d06153dcd
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 72e4a77df553ac8e97609e82bd51c8fd93b64b23
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606805"
---
# <a name="create-new-condition-or-open-condition-dialog-box-general-page"></a>建立新條件或開啟條件對話方塊，一般頁面
  使用此對話方塊可建立或變更以原則為基礎的管理條件。 條件是一種布林運算式，可指定以原則為基礎之管理 Managed 目標所允許的一組狀態 (與 Facet 有關)。 可以在 [運算式/欄位]**** 方塊中選取的屬性需視所使用的 Facet 而定。 如需條件如何與 Facet 和原則相關的詳細資訊，請參閱 [使用原則式管理來管理伺服器](administer-servers-by-using-policy-based-management.md)。  
  
## <a name="options"></a>選項。  
 **名稱**  
 為新的條件輸入新的條件名稱。 如果是現有的條件，則會顯示名稱。  
  
 **Facet**  
 此條件所使用的 Facet。  
  
 **AndOr**  
 當您加入多個運算式時，指出應該使用 **And** 還是 **Or**聯結運算式。 只有當有一個運算式時，才保留空白。  
  
 **欄位**  
 每一個 Facet 都會公開一或多個可以設定的屬性。 在此欄位方塊中，請從可用的屬性清單中選取屬性，以便為這個條件建立運算式。  
  
 **運算子**  
 為這個運算式選取比較運算子。 運算子如下：=、!=、>、>=、<、<=、[NOT]LIKE、[NOT]IN。 並非所有運算子都適用於某些屬性。  
  
 **ReplTest1**  
 這個運算式的值設定。 允許的值取決於此 Facet 而定。 值可以是 TRUE/FALSE、字串或數字。 字串值必須括在單引號中，例如 **'AdventureWorks'**。 並非所有運算子都適用於某些屬性。  
  
## <a name="group-clauses"></a>群組子句  
 子句可加以群組，使其當成單一單位來運作，並與查詢的其餘部分區隔開來，這種方式與在數學方程式或邏輯陳述式的運算式周圍放置括號類似。 當您建立複雜的查詢時，群組子句將會很實用。  
  
 **群組子句**  
  
-   按下 SHIFT 或 CTRL 鍵，然後按一下兩個或多個子句來選取範圍。 以滑鼠右鍵按一下選取的區域，然後按一下 [群組子句]****。  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來管理伺服器](administer-servers-by-using-policy-based-management.md)  
  
  
