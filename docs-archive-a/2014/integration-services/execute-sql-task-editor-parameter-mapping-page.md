---
title: '[執行 SQL 工作編輯器] ([參數對應] 頁面) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.parametermapping.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: 8ebe020a-7921-46b2-8823-398748f379b2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cfbb4468cb69947dfa54fb519b7698286393d578
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594125"
---
# <a name="execute-sql-task-editor-parameter-mapping-page"></a>執行 SQL 工作編輯器 (參數對應頁面)
  使用 [執行 SQL 工作編輯器]  對話方塊的 [參數對應]  頁面，即可將變數對應到 SQL 陳述式中的參數。  
  
 若要了解這項工作，請參閱[執行 SQL 工作](control-flow/execute-sql-task.md)和[執行 SQL 工作中的參數和傳回碼](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)。  
  
## <a name="options"></a>選項。  
 **變數名稱**  
 按一下 [新增] 新增參數對應之後，請從清單中選取系統或使用者定義變數，或按一下 \<**New variable...**> 以使用 [新增變數] 對話方塊新增新的變數。  
  
 **相關主題：** [Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)  
  
 **方向**  
 選取參數的方向。 將每個變數對應到輸入參數、輸出參數或傳回碼。  
  
 **資料類型**  
 選取參數的資料類型。 在工作所使用之連接管理員中選取的提供者，各有其專用的可用資料類型清單。  
  
 **參數名稱**  
 提供參數名稱。  
  
 您必須根據工作所使用的連接管理員類型，來使用數字或參數名稱。 某些連線管理員類型要求參數名稱的第一個字元是 \@ 符號、特定名稱 (如 \@Param1) 或資料行名稱作為參數名稱。  
  
 **相關主題：** [在執行 SQL 工作中設定參數和傳回碼](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)  
  
 **參數大小**  
 提供具有可變長度之參數的大小，例如字串和二進位欄位。  
  
 此設計可確保提供者能為可變長度的參數值配置足夠的空間。  
  
 **加入**  
 按一下即可加入參數對應。  
  
 **移除**  
 在清單中選取參數對應，然後按一下 [移除]  。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [&#40;一般頁面&#41;執行 SQL 工作編輯器](general-page-of-integration-services-designers-options.md)   
 [[執行 SQL 工作編輯器] &#40;[結果集] 頁面&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)   
 [Transact-SQL 參考 &#40;資料庫引擎41;](/sql/t-sql/language-reference)  
  
  
