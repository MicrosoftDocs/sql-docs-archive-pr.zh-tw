---
title: MSSQLSERVER_2814 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2814 (Database Engine error)
ms.assetid: 22800748-9be9-4511-9428-6b8b40e5bef9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 26b1fae5b683ed72cb93c3f81981bd41e2f4ad4e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596041"
---
# <a name="mssqlserver_2814"></a>MSSQLSERVER_2814
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2814|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PR_POSSIBLE_INFINITE_RECOMPILE|  
|訊息文字|偵測到 SQLHANDLE %hs、PlanHandle %hs、起始位移 %d、結尾位移 %d 可能發生無限重新編譯。 上次重新編譯的原因是 %d。|  
  
## <a name="explanation"></a>說明  
 一個或多個陳述式導致此查詢批次重新編譯至少 50 次。 為了避免進一步重新編譯，您應該更正指定的陳述式。  
  
 下表列出重新編譯的原因。  
  
|原因代碼|描述|  
|-----------------|-----------------|  
|1|結構描述已變更|  
|2|統計資料已變更|  
|3|延遲編譯|  
|4|Set 選項已變更|  
|5|Temp 資料表已變更|  
|6|遠端資料列集已變更|  
|7|For Browse 權限已變更|  
|8|查詢通知環境已變更|  
|9|分割區檢視已變更|  
|10|資料指標選項已變更|  
|11|已要求選項 (重新編譯)|  
  
## <a name="user-action"></a>使用者動作  
  
1.  您可以執行下列查詢來檢視導致重新編譯的陳述式。 請將 *sql_handle*、*starting_offset*、*ending_offset* 和 *plan_handle* 預留位置取代成錯誤訊息中指定的值。 請注意，特定和準備 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的 **database_name** 和 **object_name** 資料行將成為 NULL。  
  
     SELECT DB_NAME(st.dbid) AS database_name  
  
     , OBJECT_NAME(st.objectid) AS object_name  
  
     , st.text  
  
     FROM sys.dm_exec_query_stats AS qs  
  
     CROSS APPLY sys.dm_exec_sql_text (*sql_handle*) AS st  
  
     WHERE qs.statement_start_offset = *starting_offset*  
  
     AND qs.statement_end_offset = *ending_offset*  
  
     AND qs.plan_handle = *plan_handle*;  
  
2.  為了避免重新編譯，請根據原因代碼的說明，修改陳述式、批次或程序。 例如，一個預存程序可能會包含一個或多個 SET 陳述式。 您應該從此程序中移除這些陳述式。 如需重新編譯原因和解決方案的其他範例，請參閱 [Batch Compilation, Recompilation, and Plan Caching Issues in SQL Server 2005](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/administrator/cc966425(v=technet.10))(SQL Server 2005 中的批次編譯、重新編譯及計畫快取問題)。  
  
3.  如果持續發生問題，請連絡 Microsoft 客戶支援服務。  
  
## <a name="see-also"></a>另請參閱  
 [SQL:StmtRecompile 事件類別](../event-classes/sql-stmtrecompile-event-class.md)  
  
  
