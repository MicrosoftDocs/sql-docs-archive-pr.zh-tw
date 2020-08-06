---
title: 在執行時間修改 OData 來源查詢 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b3dbc4d27f2d11537a9d66980ef6ca59b80811b2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708505"
---
# <a name="modify-odata-source-query-at-runtime"></a>在執行階段修改 OData 來源查詢
  您可以在執行階段修改 OData 來源查詢，修改的方式是將「運算式」  加入資料流程工作的 [OData Source].[Query] 屬性。  
  
 請注意，資料行必須維持與設計階段所使用的內容相同，否則您在執行封裝時將會收到錯誤。 在使用 $select 查詢選項時，請務必指定相同的資料行 (以相同順序)。 使用 $select 選項有一個更安全的替代方法，也就是直接從來源元件 UI 取消選取您不想要的資料行。  
  
 有幾個不同的方式可以在執行階段動態設定查詢值。 底下是一些較為常見的方法。  
  
## <a name="exposing-the-query-as-a-parameter"></a>將查詢公開為參數  
 下列程序的步驟會將 OData 來源元件所使用的查詢公開為封裝的參數。  
  
1.  以滑鼠右鍵按一下 [資料流程工作]  ，然後選取 [參數化...]  選項。  
  
2.  在 [參數化] 對話方塊中，針對 [屬性] 選取 [\<Name of the OData Source Component>].[Query]。  
  
3.  選擇是要 [建立新的參數]  還是 [使用現有的參數]  。  
  
4.  如果您選取 [建立新的參數]****，請執行下列動作：  
  
    1.  輸入參數的 [名稱]  和 [描述]  。  
  
    2.  指定參數的預設 [值]  。  
  
    3.  為參數指定 [範圍]  ([封裝]  或 [專案]  )。  
  
    4.  指定參數是否為 [必要]  
  
5.  按一下 **[確定]** ，關閉對話方塊。  
  
## <a name="using-an-expression"></a>使用運算式  
 當您想要在執行階段以動態方式建構查詢字串時，此方法相當實用。 在此範例中，MaxRows 變數將會透過其他方式 (指令碼、參數等等) 設定。  
  
1.  選取包含您的 [OData 來源]**** 的 [資料流程工作]****。  
  
2.  在 [屬性]  視窗中，反白顯示 [運算式]  屬性。  
  
3.  按一下 [...] (省略號) ] 按鈕，以顯示 [**屬性運算式編輯器**]。  
  
4.  選取 **[OData Source].[Query]** 屬性。  
  
5.  按一下 [**運算式**] (省略號) ] 按鈕。  
  
6.  輸入 [運算式]  。  
  
7.  按一下 [確定]  。  
  
> [!WARNING]  
>  請注意，當您使用這種方法時，您必須確定設定的值具有正確的 URL 編碼。 當從使用者輸入接受值時 (例如，從參數設定個別查詢選項值)，您必須確定這些值已經過驗證，以免可能發生 SQL 資料隱碼類型的攻擊。  
  
  
