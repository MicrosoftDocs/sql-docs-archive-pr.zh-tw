---
title: " (查詢執行的選項-SQL Server-ANSI 頁面) |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionAnsi
ms.assetid: 0f4c6887-0562-417e-806c-b5cffb1e7c5c
author: rothja
ms.author: jroth
ms.openlocfilehash: 198505c5d14b9fda510d4635dbaa3d3d49483ddf
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599649"
---
# <a name="options-query-execution-sql-server-ansi-page"></a> (查詢執行的選項-SQL Server-ANSI 頁面) 
  這些 ANSI (ISO) 標準 SET 選項共同定義了使用者查詢的查詢處理環境是執行觸發，還是預存程序。 不過，這些 SET 選項並沒有包含符合 ISO 標準所需的所有選項。 使用此頁面來指定 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 將使用 ISO 標準中指定的全部或部分設定來執行查詢。 這些選項的變更僅適用於新的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢。 若要變更目前查詢的選項，請按一下 [**查詢**] 功能表上的 [**查詢選項**]，或在查詢視窗中按一下滑鼠右鍵， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 然後選取 [**查詢選項**]。 在 **[查詢選項]** 對話方塊中，於 **[執行]** 之下，按一下 **[ANSI]**。  
  
## <a name="ui-element-list"></a>UI 元素清單  
 **SET ANSI_DEFAULTS**  
 選取此核取方塊，即可選取所有預設的 ISO 設定。 並非所有 ISO 選項皆預設為選取。  
  
 **SET QUOTED_IDENTIFIER**  
 如果選取此核取方塊， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 就會依循 ISO 有關引號分隔識別碼和常值字串的規則。 以引號分隔的識別碼可能是 Transact-SQL 的保留關鍵字，或是包含通常識別碼的 Transact-SQL 語法規則不允許的字元。 依預設，這個核取方塊為已選取。  
  
 **SET ANSI_NULL_DFLT_ON**  
 當此值已設定，在 CREATE TABLE 或 ALTER TABLE 陳述式期間未明確定義為 NOT NULL 的所有使用者自訂的資料類型或資料行，都會預設為允許 Null 值。 依預設，這個核取方塊為已選取。  
  
 **SET IMPLICIT_TRANSACTIONS**  
 如果選取此核取方塊，SET IMPLICIT_TRANSACTIONS 會將連接設定為隱含交易模式。 如果清除此核取方塊，則會將連接設定為自動認可交易模式。 若要檢閱選取後會啟動隱含交易的陳述式，請參閱 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-implicit-transactions-transact-sql)。 依預設，不會勾選此核取方塊。  
  
 **SET CURSOR_CLOSE_ON_COMMIT**  
 如果選取此核取方塊，交易認可後開啟的資料指標就會自動關閉 (符合 ISO)。 這個值若設定為 OFF，資料指標跨交易界限時會維持開啟，只有在關閉連接或明確地關閉時才會關閉資料指標。 依預設，不會勾選此核取方塊。  
  
 **SET ANSI_PADDING**  
 控制資料行針對數值名稱長度短於資料行所定義大小的儲存方式，以及資料行針對 **char**、 **varchar**、 **binary**以及 **varbinary** 資料尾端具有空白之數值的儲存方式。 這項設定只會影響新資料行的定義。 建立好資料行之後， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會根據建立資料行之時的設定來儲存值。 這項設定後來的變更並不會影響現有的資料行。 依預設，這個核取方塊為已選取。  
  
 **SET ANSI_WARNINGS**  
 指定數個錯誤狀況的 ISO 標準行為：  
  
-   如果選取此核取方塊，而 Null 值出現在彙總函式 (例如，SUM、AVG、MAX、MIN、STDEV、STDEVP、VAR、VARP 或 COUNT) 中，就會產生警告訊息。 設定為 OFF 時，則不會發出警告。  
  
-   如果清除此核取方塊，除以零及算術溢位錯誤會造成陳述式回復，並產生錯誤訊息。 設定為 OFF 時，除以零及算術溢位錯誤會造成傳回 Null 值。 如果在 **character**、**Unicode** 或 **binary** 資料行中嘗試 INSERT 或 UPDATE 作業，且新值長度超過資料行的大小上限時，除以零或算術溢位錯誤會造成傳回 Null 值。 如果 SET ANSI_WARNINGS 為 ON，INSERT 或 UPDATE 作業就會依 ISO 標準的指定加以取消。 字元資料行尾端的空格會被忽略，二進位資料行尾端的 Null 也會被忽略。 當它是 OFF 時，便會將資料截斷成為資料行大小，陳述式會繼續作業。  
  
 依預設，這個核取方塊為已選取。  
  
 **SET ANSI_NULLS**  
 -   指定搭配 null 值一起使用時，等於 (=) 和不等於 (<>) 比較運算子的 ISO 相容行為。 如果選取 SET ANSI_NULLS，所有針對 Null 值的比較，都會評估為 UNKNOWN，也就是符合 ISO 的行為。 如果未選取 SET ANSI_NULLS，所有資料針對 Null 值的比較，都會評估為 TRUE。 依預設，這個核取方塊為已選取。  
  
 **重設為預設值**  
 將此頁面上的所有值重設為原始預設值。  
  
  
