---
title: 儲存變更指令碼對話方塊 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.generatechangescript
- vdtsql.chm:65544
ms.assetid: fc9d1639-5efa-44fe-a04f-4d4d0def2833
author: stevestein
ms.author: sstein
ms.openlocfilehash: 19a2bb2ce9a219c195421e2efa203fc115e1ae1b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686668"
---
# <a name="save-change-script-dialog-box-visual-database-tools"></a>儲存變更指令碼對話方塊 (Visual Database Tools)
  此對話方塊顯示從上次儲存資料表以來您所做變更的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 這也可以讓您在選擇的位置將指令碼儲存至文字檔。  
  
 您在 [資料表設計師] 中對資料表進行了尚未儲存的變更之後，即可存取這個對話方塊。 在 [資料表設計工具]  功能表中，按一下 [產生變更指令碼]  。  
  
> [!NOTE]  
>  Visual Database Tools 提供的變更指令碼未包含錯誤處理。 這些指令碼會假設資料庫物件在工具開啟之後並未變更，而且因此不會發生變更相關的問題。 在執行變更指令碼之前，應先加入適當的錯誤處理陳述式。  
  
## <a name="options"></a>選項。  
 **於每一次儲存時，自動產生變更指令碼**  
 如果核取，[儲存變更指令碼]  對話方塊會在您將變更儲存至資料表時出現。  
  
 **是**  
 顯示 [儲存]  對話方塊，以便您選擇文字檔的位置。  
  
 **否**  
 取消建立變更指令碼。  
  
  
