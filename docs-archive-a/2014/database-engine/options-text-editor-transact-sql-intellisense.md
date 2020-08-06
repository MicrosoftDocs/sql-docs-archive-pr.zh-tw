---
title: " (文字編輯器的選項-Transact-sql-IntelliSense) |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.SQL.Advanced
- VS.ToolsOptionsPages.Text_Editor.SQL_Server_Tools.Advanced
dev_langs:
- TSQL
ms.assetid: 1855d916-5bf9-4d94-b0fb-9f9bb05ff950
author: rothja
ms.author: jroth
ms.openlocfilehash: 2d8f9c865516dc5e4c0ddadbdc908a9b4c8ec366
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597994"
---
# <a name="options-text-editor-transact-sql-intellisense"></a> (文字編輯器的選項-Transact-sql-IntelliSense) 
  **[選項]** 對話方塊可讓您變更 [!INCLUDE[ssDE](../includes/ssde-md.md)] 查詢編輯器的 IntelliSense 設定。 在 [工具]**** 功能表上，按一下 [選項]****，依序展開 [文字編輯器]**** 資料夾和 [Transact-SQL]**** 資料夾，然後按一下 [進階]****，即可使用這些設定。  
  
## <a name="transact-sql-intellisense-settings"></a>Transact-SQL IntelliSense 設定  
 為 [!INCLUDE[ssDE](../includes/ssde-md.md)] 查詢編輯器指定 IntelliSense 選項。  
  
### <a name="enable-intellisense"></a>啟用 IntelliSense  
 啟用 IntelliSense 功能。 當此方塊未選取時，就無法使用特定的 IntelliSense 選項。 依預設，這個核取方塊為已選取。  
  
 **底線錯誤**  
 在查詢視窗中識別 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式內的語法和語意錯誤。 所有的錯誤和警告都會以紅色出現。 只有在已經實作 IntelliSense 的 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式中，才會支援警告和錯誤。 依預設，這個核取方塊為已選取。  
  
 **大綱陳述式**  
 在檔案開啟時，啟用大綱功能。 這會建立可摺疊的 [!INCLUDE[tsql](../includes/tsql-md.md)] 程式碼區塊。 依預設，這個核取方塊為已選取。  
  
 **最大指令碼大小**  
 指定停用 IntelliSense 功能時的大小。 如果指令碼超出指定的大小，就會發出警告訊息。 所有的 IntelliSense 功能 (色彩編碼除外) 都會針對該編輯器視窗而停用。 當刪除足夠的文字將指令碼大小縮減為這個限制以下時，IntelliSense 將會重新啟用。 針對大型指令碼啟用 IntelliSense 可能會讓執行速度很慢的電腦降低效能。 允許的大小為 100 KB、500 KB、1 MB、2 MB 和無限制。 預設值是 1 MB。  
  
 **內建函數名稱的大小寫**  
 指定完成清單內所包含的內建 [!INCLUDE[tsql](../includes/tsql-md.md)] 函數名稱是使用大寫字母 (如 DATEADD) 還是小寫字母 (如 dateadd)。 選取最符合您使用之 [!INCLUDE[tsql](../includes/tsql-md.md)] 編碼慣例的選項。  
  
## <a name="see-also"></a>另請參閱  
 [疑難排解 IntelliSense &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/troubleshooting-intellisense.md)  
  
  
