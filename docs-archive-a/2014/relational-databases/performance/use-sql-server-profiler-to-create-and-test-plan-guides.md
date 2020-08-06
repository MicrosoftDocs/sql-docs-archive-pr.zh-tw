---
title: 使用 SQL Server Profiler 建立及測試計畫指南 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- checking plan guides
- plan guides [SQL Server], testing
- plan guides [SQL Server], SQL Server Profiler
- matching queries to plan guides [SQL Server]
- testing plan guides
- SQL Server Profiler, plan guides
- plan guides [SQL Server], creating
- capturing query text [SQL Server]
- verifying plan guides
- Profiler [SQL Server Profiler], plan guides
- query-to-plan guide matching [SQL Server]
ms.assetid: 7018dbf0-1a1a-411a-88af-327bedf9cfbd
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 543905343d74c9fbabe5f671d9021657ea5f76b5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87701077"
---
# <a name="use-sql-server-profiler-to-create-and-test-plan-guides"></a>使用 SQL Server Profiler 建立及測試計畫指南
  當您建立計畫指南時，可使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來擷取精確的查詢文字，以供使用於 **sp_create_plan_guide** 預存程序的 <陳述式文字> 引數。 這有助於確保計畫指南符合編譯時期的查詢。 在建立計畫指南之後， [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 也可用來測試計畫指南實際上是否符合查詢。 一般而言，您應該使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來測試計畫指南，以確認查詢符合您的計畫指南。  
  
## <a name="capturing-query-text-by-using-sql-server-profiler"></a>使用 SQL Server Profiler 擷取查詢文字  
 如果您執行查詢並使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來擷取與提交至 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]完全相同的文字，您可以建立 SQL 或 TEMPLATE 類型的計畫指南來完全符合查詢文字。 這可確保計畫指南是由查詢最佳化工具使用。  
  
 請看應用程式以獨立批次提交的下列查詢：  
  
```  
SELECT COUNT(*) AS c  
FROM Sales.SalesOrderHeader AS h  
INNER JOIN Sales.SalesOrderDetail AS d  
  ON h.SalesOrderID = d.SalesOrderID  
WHERE h.OrderDate BETWEEN '20000101' and '20050101';  
```  
  
 假設您要此查詢使用合併聯結作業執行，但 SHOWPLAN 指出該查詢不是使用合併聯結。 您不能在應用程式中直接變更查詢，而是要建立計畫指南來指定在編譯時期將 MERGE JOIN 查詢提示附加至查詢。  
  
 若要擷取和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所接收的一模一樣的查詢文字，請遵循這些步驟：  
  
1.  啟動 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 追蹤，確定已選取 [SQL:BatchStarting] 事件類型。  
  
2.  讓應用程式執行查詢。  
  
3.  暫停 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 追蹤。  
  
4.  按一下對應到此查詢的 [SQL:BatchStarting] 事件。  
  
5.  以滑鼠右鍵按一下，並選取 [擷取事件資料]。  
  
    > [!IMPORTANT]  
    >  請勿嘗試從 Profiler 追蹤視窗的下方窗格選取要複製的批次文字。 這可能造成建立的計畫指南與原始批次不符。  
  
6.  將事件資料儲存至檔案。 這是批次文字。  
  
7.  在 [記事本] 中開啟批次文字檔，將文字複製到「複製與貼上緩衝區」。  
  
8.  建立計畫指南，並將所複製的文字貼到 **@stmt**引數所指定的引號內 ( **@stmt** )。 您必須在引數中的單引號前面加上另一個單引號，以將 **@stmt** 其轉義。 當您插入這些單引號的時候，請小心不要加入或移除任何其他字元。 例如，您必須將 **'** 20000101 **'** 日期常值分隔為 **''** 20000101 **''** 。  
  
 以下是計畫指南：  
  
```  
EXEC sp_create_plan_guide   
    @name = N'MyGuide1',  
    @stmt = N'<paste the text copied from the batch text file here>',  
    @type = N'SQL',  
    @module_or_batch = NULL,  
    @params = NULL,  
    @hints = N'OPTION (MERGE JOIN)';  
```  
  
## <a name="testing-plan-guides-by-using-sql-server-profiler"></a>使用 SQL Server Profiler 測試計畫指南  
 若要確認計畫指南符合查詢，請遵循這些步驟：  
  
1.  啟動 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 追蹤，確定已選取 [執行程序表 XML] 事件類型 (位於 [效能] 節點之下)。  
  
2.  讓應用程式執行查詢。  
  
3.  暫停 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 追蹤。  
  
4.  為受影響的查詢尋找 [執行程序表 XML] 事件。  
  
    > [!NOTE]  
    >  不可使用 [Showplan XML for Query Compile] 事件。 [PlanGuideDB] 不存在該事件中。  
  
5.  如果計畫指南的類型為 OBJECT 或 SQL，請確認 [執行程序表 XML] 事件包含您預期符合查詢之計畫指南的 **PlanGuideDB** 和 **PlanGuideName** 屬性。 若為 TEMPLATE 計畫指南，則請確認 [執行程序表 XML] 事件包含預期計畫指南的 **TemplatePlanGuideDB** 和 **TemplatePlanGuideName** 屬性。 這可確認計畫指南有用。 這些屬性包含在計畫的 **\<StmtSimple>** 元素下。  
  
## <a name="see-also"></a>另請參閱  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)  
  
  
