---
title: 指定叫用計數
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- vs.debug.breakpt.hitcount
helpviewer_keywords:
- Transact-SQL debugger, breakpoint hit count
ms.assetid: 24836939-94ed-4e57-aa85-5d6938d859e4
author: rothja
ms.author: jroth
ms.openlocfilehash: 34c75e990bce1ea5e64c0b45f7acbcaa52fc3c40
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598269"
---
# <a name="specify-a-hit-count"></a>指定叫用計數
  中斷點叫用次數是每次到達中斷點時由 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具遞增的計數器。 如果已到達指定的叫用計數而且滿足任何指定的中斷點條件時，偵錯工具就會執行為中斷點指定的動作。  
  
## <a name="hit-count-considerations"></a>叫用次數考量  
 根據預設，每次叫用中斷點時，執行就會中斷。 您可以選擇下列其中一個選項：  
  
-   永遠中斷 (預設值)。  
  
-   當叫用次數等於指定的值時中斷。  
  
-   當叫用次數倍數於指定的值時中斷。  
  
-   當叫用次數大於或等於指定的值時中斷。  
  
 中斷點叫用次數會在偵錯工作階段的範圍內遞增。 在每個偵錯工作階段啟動時，所有叫用次數都設定為零。  
  
 如果您想要追蹤中斷點的叫用次數，而不讓中斷點中斷執行，請使用非常高的值來指定叫用次數，如此中斷點就絕對不會中斷。  
  
 中斷點的預設動作是在已滿足叫用計數和中斷點條件時中斷執行。 如需指定其他動作的資訊，請參閱 [指定中斷點動作](specify-a-breakpoint-action.md)。  
  
#### <a name="to-specify-a-hit-count"></a>若要指定叫用次數  
  
1.  在編輯器視窗中，以滑鼠右鍵按一下中斷點字符，然後按一下捷徑功能表上的 [叫用次數]  。  
  
     -或-  
  
     在 [中斷點]  視窗中，以滑鼠右鍵按一下中斷點字符，然後按一下捷徑功能表上的 [叫用次數]  。  
  
2.  在 **[中斷點叫用次數]** 對話方塊的 **[當叫用中斷點時]** 方塊中，選取所要的行為。  
  
     如果您選擇 **[永遠中斷]** 以外的任何設定，清單右側就會顯示一個文字方塊。 請在此文字方塊中輸入整數，以便指定所要的叫用次數。  
  
3.  按一下 **[確定]** 實作變更，或按一下 **[取消]** 結束而不套用變更。  
  
#### <a name="to-view-or-reset-the-current-hit-count"></a>若要檢視或重設目前叫用次數  
  
1.  在編輯器視窗中，以滑鼠右鍵按一下中斷點字符，然後按一下捷徑功能表上的 [叫用次數]  。  
  
     -或-  
  
     在 [中斷點]  視窗中，以滑鼠右鍵按一下中斷點字符，然後按一下捷徑功能表上的 [叫用次數]  。  
  
2.  在 **[中斷點叫用次數]** 對話方塊中， **[目前叫用次數:]** 就會顯示在 **[重設]** 按鈕的正上方。  
  
3.  如果您想要將目前叫用次數設定為零，請按一下 **[重設]** 。  
  
4.  按一下 **[確定]** 或 **[取消]** 結束對話方塊。  
  
## <a name="see-also"></a>另請參閱  
 [指定中斷點條件](specify-a-breakpoint-condition.md)  
  
  
