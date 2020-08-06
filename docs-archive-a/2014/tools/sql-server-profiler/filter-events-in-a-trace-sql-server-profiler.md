---
title: 篩選追蹤中的事件 (SQL Server Profiler) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- traces [SQL Server], filters
- traces [SQL Server], events
ms.assetid: 0fd63573-3b35-4f67-9e1e-ed9aabee11a8
author: stevestein
ms.author: sstein
ms.openlocfilehash: fef9dd6956d407011261c54f796a751a0bf94941
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706929"
---
# <a name="filter-events-in-a-trace-sql-server-profiler"></a>篩選追蹤中的事件 (SQL Server Profiler)
  篩選可限制追蹤中收集的事件。 如果沒有設定篩選條件，選定事件類別的所有事件都會傳回到追蹤輸出。 替追蹤設定篩選並非強制的。 不過，篩選可以讓追蹤期間造成的負擔降到最低。  
  
 使用 **[追蹤屬性]** 或 **[追蹤範本屬性]** 對話方塊的 **[事件選取範圍]** 索引標籤，可以將篩選加入到追蹤定義。  
  
### <a name="to-filter-events-in-a-trace"></a>若要篩選追蹤中的事件  
  
1.  在 **[追蹤檔案屬性]** 或 **[追蹤資料表屬性]** 對話方塊中，按一下 **[事件選取範圍]** 索引標籤。  
  
     **[事件選取範圍]** 索引標籤包含方格控制項。 方格控制項是包含每一個可追蹤事件類別的資料表。 資料表針對每個事件類別包含一個資料列。 事件類別可能會依您所連接的伺服器類型與版本而稍有不同。 事件類別在方格的 [事件]**** 資料行中識別，並依事件類別目錄分組。 其餘資料行會列出可針對每個事件類別傳回的資料行。  
  
2.  按一下 [資料行篩選]。   
  
     [編輯篩選]**** 對話方塊隨即顯示。 您可以使用 [編輯篩選]**** 對話方塊包含的比較運算子清單，篩選追蹤中的事件。  
  
3.  若要套用篩選，請按一下比較運算子，再輸入篩選要用的值。  
  
4.  按一下 [確定]  。  
  
 **考量因素：**  
  
-   如果在 [事件選取範圍] 索引標籤的 **StartTime** 與 **EndTime** 資料行上，設定篩選條件，請確定：  
  
    -   輸入的日期符合以下格式： `YYYY/MM/DD HH:mm:sec`。  
  
         -或-  
  
    -   已在 **[一般選項]** 對話方塊中，核取 **[使用地區設定來顯示日期和時間值]** 。 若要檢視 [一般選項]  對話方塊，請在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] [工具]  功能表上，按一下 [選項]  。  
  
         -且-  
  
    -   輸入的日期必須介於 1753 年 1 月 1 日與 9999 年 12 月 31 日。  
  
-   如果從 **osql** 公用程式或 **sqlcmd** 公用程式追蹤事件，對 **%** 資料行篩選時會附加 **%** 。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
