---
title: 執行 Transact-SQL 偵錯工具
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, sysadmin requirement
- Transact-SQL debugger, supported versions
- Query Editor [Database Engine], right-click menu
- Transact-SQL debugger, Query Editor shortcut menu
- Transact-SQL debugger, stopping
- Transact-SQL debugger, Debug menu
- Transact-SQL debugger, Debug toolbar
- Transact-SQL debugger, keyboard shortcuts
- Transact-SQL debugger, starting
ms.assetid: 386f6d09-dbec-4dc7-9e8a-cd9a4a50168c
author: rothja
ms.author: jroth
ms.openlocfilehash: 2f9f9b8d45755542006e841e20ddaaa73141bc7e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592595"
---
# <a name="run-the-transact-sql-debugger"></a>執行 Transact-SQL 偵錯工具
  在您開啟 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢編輯器視窗之後，就可以啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 偵錯工具。 然後，您可以在偵錯模式中執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，直到停止偵錯工具為止。 您可以設定選項來自訂偵錯工具的執行方式。  
  
## <a name="starting-and-stopping-the-debugger"></a>啟動和停止偵錯工具  
 啟動 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具的需求如下：  
  
-   如果您的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器連接至另一部電腦上的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，就必須設定偵錯工具進行遠端偵錯。 如需詳細資訊，請參閱[設定 Transact-sql 偵錯工具](configure-firewall-rules-before-running-the-tsql-debugger.md)。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 必須在屬於系統管理員 (sysadmin) 固定伺服器角色成員的 Windows 帳戶底下執行。  
  
-   您必須使用屬於系統管理員 (sysadmin) 固定伺服器角色成員的 Windows 驗證或 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 驗證登入來連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢編輯器視窗。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器視窗必須連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Service Pack 2 (SP2) 或更新版本中的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 執行個體。 當 [查詢編輯器] 視窗連接至處於單一使用者模式下的執行個體時，您就無法執行偵錯工具。  
  
 我們建議您在測試伺服器而非實際伺服器上偵錯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，原因如下：  
  
-   偵錯是具有高度權限的作業。 因此，只有系統管理員 (sysadmin) 固定伺服器角色的成員才能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中偵錯。  
  
-   在您調查許多 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的作業時，偵錯工作階段通常會執行一段很長的時間。 工作階段所取得的鎖定 (例如更新鎖定) 可能會長時間保留，直到工作階段結束，或者交易已認可或回復為止。  
  
 一旦啟動 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具，就會讓 [查詢編輯器] 視窗進入偵錯模式。 當 [查詢編輯器] 視窗進入偵錯模式時，偵錯工具就會在第一行程式碼上暫停。 然後，您就可以逐步執行程式碼、在特定的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式上暫停執行作業，以及使用偵錯工具視窗來檢視目前的執行狀態。 您可以透過按一下 **[查詢]** 工具列上的 **[偵錯]** 按鈕，或按一下 **[偵錯]** 功能表上的 **[開始偵錯]** ，啟動偵錯工具。  
  
 [查詢編輯器] 視窗會保持在偵錯模式中，直到 [查詢編輯器] 視窗中的最後一個陳述式完成或是您停止偵錯模式為止。 您可以使用下列任何一種方法來停止偵錯模式和陳述式執行：  
  
-   在 **[偵錯]** 功能表上，按一下 **[停止偵錯]** 。  
  
-   在 **[偵錯]** 工具列上，按一下 **[停止偵錯]** 按鈕。  
  
-   在 **[查詢]** 功能表上，按一下 **[取消執行查詢]** 。  
  
-   在 **[查詢]** 工具列上，按一下 **[取消執行查詢]** 按鈕。  
  
 您也可以按一下 [!INCLUDE[tsql](../../includes/tsql-md.md)] [偵錯] **功能表上的** [中斷所有連結] **，藉以停止偵錯模式，並且允許其餘** 陳述式完成執行。  
  
## <a name="controlling-the-debugger"></a>控制偵錯工具  
 您可以使用下列功能表命令、工具列和快速鍵來控制 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具的運作方式：  
  
-   **[偵錯]** 功能表和 **[偵錯]** 工具列。 在開啟的 [查詢編輯器] 視窗中放置焦點之前， **[偵錯]** 功能表和 **[偵錯]** 工具列是處於非使用中狀態。 此外，它們會維持使用中狀態，直到目前的專案關閉為止。  
  
-   偵錯工具鍵盤快速鍵。  
  
-   查詢編輯器快速鍵功能表。 當您在 [查詢編輯器] 視窗中，以滑鼠右鍵按一下某一行時，就會顯示快速鍵功能表。 當 [查詢編輯器] 視窗處於偵錯模式時，快速鍵功能表就會顯示套用至選取行或字串的偵錯工具命令。  
  
-   偵錯工具所開啟之視窗 (例如 **[監看式]** 或 **[中斷點]** 視窗) 中的主要項目和內容命令。  
  
 下表將顯示偵錯工具功能表命令、工具列按鈕和鍵盤快速鍵。  
  
|偵錯功能表命令|編輯器快速鍵命令|工具列按鈕|鍵盤快速鍵|動作|  
|------------------------|-----------------------------|--------------------|-----------------------|------------|  
|**視窗/中斷點**|無法使用|**[中斷點]**|CTRL+ALT+B|顯示您可以用來檢視和管理中斷點的 **[中斷點]** 視窗。|  
|**視窗/監看式/監看式 1**|無法使用|**中斷點/監看式/監看式 1**|CTRL+ALT+W、1|顯示 **[監看式 1]** 視窗。|  
|**視窗/監看式/監看式 2**|無法使用|**中斷點/監看式/監看式 2**|CTRL+ALT+W、2|顯示 **[監看式 2]** 視窗。|  
|**視窗/監看式/監看式 3**|無法使用|**中斷點/監看式/監看式 3**|CTRL+ALT+W、3|顯示 **[監看式 3]** 視窗。|  
|**視窗/監看式/監看式 4**|無法使用|**中斷點/監看式/監看式 4**|CTRL+ALT+W、4|顯示 **[監看式 4]** 視窗。|  
|**視窗/區域變數**|無法使用|**中斷點/區域變數**|CTRL+ALT+V、L|顯示 **[區域變數]** 視窗。|  
|**視窗/呼叫堆疊**|無法使用|**中斷點/呼叫堆疊**|CTRL+ALT+C|顯示 **[呼叫堆疊]** 視窗。|  
|**視窗/執行緒**|無法使用|**中斷點/執行緒**|CTRL+ALT+H|顯示 **[執行緒]** 視窗。|  
|**繼續**|無法使用|**繼續**|ALT+F5|執行到下一個中斷點。 在處於偵錯模式的 [查詢編輯器] 視窗中放置焦點之前， **[繼續]** 是處於非使用中狀態。|  
|**[偵錯]**|無法使用|**[偵錯]**|ALT+F5|讓 [查詢編輯器] 視窗進入偵錯模式，並且執行到第一個中斷點。 如果您在處於偵錯模式的 [查詢編輯器] 視窗中放置焦點， **[開始偵錯]** 就會由 **[繼續]** 所取代。|  
|**全部中斷**|無法使用|**全部中斷**|CTRL+ALT+BREAK|[!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具不會使用這項功能。|  
|**停止偵錯**|無法使用|**停止偵錯**|SHIFT+F5|讓 [查詢編輯器] 視窗離開偵錯模式，並且返回一般模式。|  
|**功能表上的**|無法使用|無法使用|無法使用|停止偵錯模式，但在 [查詢編輯器] 視窗中執行其餘陳述式。|  
|**逐步執行**|無法使用|**逐步執行**|F11|執行下一個陳述式，而且如果下一個陳述式會執行預存程序、觸發程序或函數，就會在偵錯模式中開啟新的 [查詢編輯器] 視窗。|  
|**逐程序**|無法使用|**逐程序**|F10|與 **[逐步執行]** 相同，但是不會偵錯任何函數、預存程序或觸發程序。|  
|**跳出**|無法使用|**跳出**|SHIFT+F11|執行觸發程序、函數或預存程序中的其餘程式碼，但是不會針對任何中斷點暫停。 當控制權返回呼叫模組的程式碼時，就會繼續進行一般偵錯模式。|  
|無法使用|**執行至資料指標處**|無法使用|CTRL+F10|執行所有程式碼 (從上一個停止位置到目前的資料指標位置)，但是不會在任何中斷點上停止。|  
|**QuickWatch**|**QuickWatch**|無法使用|CTRL+ALT+Q|顯示 **[快速監看式]** 視窗。|  
|**切換中斷點**|**中斷點/插入中斷點**|無法使用|F9|將中斷點放置在目前或選取的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式上。|  
|無法使用|**中斷點/刪除中斷點**|無法使用|無法使用|從選取行中刪除中斷點。|  
|無法使用|**中斷點/停用中斷點**|無法使用|無法使用|停用選取行的中斷點。 雖然中斷點會保留在程式碼行上，但是在重新啟用之前，它將不會停止執行作業。|  
|無法使用|**中斷點/啟用中斷點**|無法使用|無法使用|啟用選取行的中斷點。|  
|**刪除所有中斷點**|無法使用|無法使用|CTRL+SHIFT+F9|刪除所有中斷點。|  
|**停用所有中斷點**|無法使用|無法使用|無法使用|停用所有中斷點。|  
|無法使用|**加入監看式**|無法使用|無法使用|將選取的運算式加入至 **[監看式]** 視窗。|  
  
## <a name="see-also"></a>另請參閱  
 [Transact-sql 偵錯工具](transact-sql-debugger.md)   
 [逐步執行 Transact-sql 程式碼](step-through-transact-sql-code.md)   
 [Transact-sql 偵錯工具資訊](transact-sql-debugger-information.md)   
 [Database Engine 查詢編輯器 &#40;SQL Server Management Studio&#41;](database-engine-query-editor-sql-server-management-studio.md)  
  
  
