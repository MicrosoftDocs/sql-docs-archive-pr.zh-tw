---
title: 取代範本參數 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.templates.replaceparameters.f1
helpviewer_keywords:
- template parameters [Template Explorer]
- templates [Transact-SQL], replacing parameters
- Replace (Query) Template Parameters dialog box
- replacing template parameters
ms.assetid: 1234aa14-3464-4a3e-922a-5cfb8fb23627
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1d87b17a110efe118f7796487448e4d3bae30375
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597517"
---
# <a name="replace-template-parameters"></a>取代範本參數
  範本包含每次使用範本時可由實作特定值替換的參數。 在程式碼編輯器中開啟範本之後，可以使用與您的實作相關的值替換這些參數。  
  
## <a name="before-you-begin"></a>開始之前  
 [指定範本參數的值]  對話方塊是包含三個資料行的方格。 [參數]  和 [類型]  資料行是唯讀的，無法變更。 檢閱 [值]  資料行的內容，並將任意預設值更改為適合您實作的值。  
  
 若要使用此對話方塊，您的指令碼必須以角括弧 (`< >`) 括住參數，格式為 `<`  `,` *資料類型*`,`  `>`。  
  
## <a name="replace-template-parameters"></a>取代範本參數  
 在程式碼編輯器視窗中開啟範本之後：  
  
1.  在 **[查詢]** 功能表上，按一下 **[指定範本參數的值]** 。  
  
2.  在 [指定範本參數的值]  對話方塊中，[值]  資料行包含每一個參數的建議值。 接受該值或以新的值替換。  
  
3.  按一下 [確定]  ，關閉 [取代範本參數]  對話方塊並在查詢編輯器中修改指令碼。  
  
## <a name="see-also"></a>另請參閱  
 [範本瀏覽器](template-explorer.md)   
 [開啟範本](open-a-template.md)  
  
  
