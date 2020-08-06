---
title: 檢視及閱讀容錯移轉叢集執行個體診斷記錄檔 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 68074bd5-be9d-4487-a320-5b51ef8e2b2d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 774dc4ec4a02c72420d004909cb7e6ee1b31f3a7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595559"
---
# <a name="view-and-read-failover-cluster-instance-diagnostics-log"></a>檢視及閱讀容錯移轉叢集執行個體診斷記錄檔
  SQL Server 資源 DLL 的所有重大錯誤和警告事件都會寫入 Windows 事件記錄檔。 SQL Server 的特定診斷資訊執行記錄檔是由 [sp_server_diagnostics &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) 系統預存程序所擷取，並且會寫入 SQL Server 容錯移轉叢集診斷 (也稱為 *SQLDIAG* 記錄) 記錄檔。  
  
-   **開始之前**  [建議](#Recommendations)、 [安全性](#Security)  
  
-   **使用下列項目，檢視診斷記錄：**  [SQL Server Management Studio](#SSMSProcedure)、[Transact-SQL](#TsqlProcedure)  
  
-   **使用下列項目，設定診斷記錄設定：** [Transact-SQL](#TsqlConfigure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
 根據預設，SQLDIAG 會儲存在 SQL Server 實例目錄的本機 LOG 資料夾底下，例如 ' C\Program Files\Microsoft SQL Server\MSSQL12. \<InstanceName>AlwaysOn 容錯移轉叢集實例之擁有節點的 \MSSQL\LOG ' (FCI) 。 每個 SQLDIAG 記錄檔的大小會固定為 100 MB。 電腦上會儲存十個此類型的記錄檔，再將它們回收以用於新的記錄檔。  
  
 記錄檔會使用擴充的事件檔案格式。 **sys.fn_xe_file_target_read_file** 系統函數可用來讀取擴充事件所建立的檔案。 系統會以 XML 格式針對每個資料列傳回一個事件。 查詢系統檢視，即可將 XML 資料剖析為結果集。 如需詳細資訊，請參閱 [sys.fn_xe_file_target_read_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要有 VIEW SERVER STATE 權限才能執行 **fn_xe_file_target_read_file**。  
  
 以管理員的身分開啟 SQL Server Management Studio  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要檢視診斷記錄檔：**  
  
1.  從 **[檔案]** 功能表中，依序選取 **[開啟]** 和 **[檔案]**，然後選擇想要檢視的診斷記錄檔。  
  
2.  事件在右窗格中會顯示為資料列，而且依預設只會顯示 **[name]** 和 **[timestamp]** 這兩個資料行。  
  
     這也會啟動 **[ExtendedEvents]** 功能表。  
  
3.  若要查看其他資料行，請前往 **[ExtendedEvents]** 功能表，並選取 **[選擇資料行]**。  
  
     隨即開啟對話方塊，內含可讓您選取資料行進行顯示的可用資料行。  
  
4.  您可以使用 **[ExtendedEvents]** 功能表並選取 **[篩選]** 選項，來篩選和排序事件資料。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要檢視診斷記錄檔：**  
  
 若要檢視 SQLDIAG 記錄檔中的所有記錄項目，請使用下列查詢：  
  
```  
SELECT  
xml_data.value('(event/@name)[1]','varchar(max)') AS 'Name'  
,xml_data.value('(event/@package)[1]','varchar(max)') AS 'Package'  
,xml_data.value('(event/@timestamp)[1]','datetime') AS 'Time'  
,xml_data.value('(event/data[@name=''state'']/value)[1]','int') AS 'State'  
,xml_data.value('(event/data[@name=''state_desc'']/text)[1]','varchar(max)') AS 'State Description'  
,xml_data.value('(event/data[@name=''failure_condition_level'']/value)[1]','int') AS 'Failure Conditions'  
,xml_data.value('(event/data[@name=''node_name'']/value)[1]','varchar(max)') AS 'Node_Name'  
,xml_data.value('(event/data[@name=''instancename'']/value)[1]','varchar(max)') AS 'Instance Name'  
,xml_data.value('(event/data[@name=''creation time'']/value)[1]','datetime') AS 'Creation Time'  
,xml_data.value('(event/data[@name=''component'']/value)[1]','varchar(max)') AS 'Component'  
,xml_data.value('(event/data[@name=''data'']/value)[1]','varchar(max)') AS 'Data'  
,xml_data.value('(event/data[@name=''info'']/value)[1]','varchar(max)') AS 'Info'  
FROM  
 ( SELECT object_name AS 'event'  
  ,CONVERT(xml,event_data) AS 'xml_data'  
  FROM sys.fn_xe_file_target_read_file('C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log\SQLNODE1_MSSQLSERVER_SQLDIAG_0_129936003752530000.xel',NULL,NULL,NULL)   
)   
AS XEventData  
ORDER BY Time;  
  
```  
  
> [!NOTE]  
>  您可以篩選特定元件或使用 WHERE 子句之狀態的結果。  
  
##  <a name="using-transact-sql"></a><a name="TsqlConfigure"></a> 使用 Transact-SQL  
 **設定診斷記錄屬性**  
  
> [!NOTE]  
>  如需這個程序的範例，請參閱本節稍後的 [範例 &#40;Transact-SQL&#41;](#TsqlExample)。  
  
 使用資料定義語言 (DDL) 語句， `ALTER SERVER CONFIGURATION` 您可以啟動或停止[Sp_server_diagnostics &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)程式所捕捉的記錄診斷資料，並設定 SQLDIAG 記錄檔設定參數，例如記錄檔換用計數、記錄檔大小和檔案位置。 如需語法的詳細資料，請參閱 [Setting diagnostic log options](/sql/t-sql/statements/alter-server-configuration-transact-sql#Diagnostic)。  
  
###  <a name="examples-transact-sql"></a><a name="ConfigTsqlExample"></a> 範例 (Transact-SQL)  
  
####  <a name="setting-diagnostic-log-options"></a><a name="TsqlExample"></a> Setting diagnostic log options  
 本節的範例示範如何設定診斷記錄檔選項的值。  
  
##### <a name="a-starting-diagnostic-logging"></a>A. 啟動診斷記錄  
 下列範例會啟動診斷資料記錄。  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG ON;  
```  
  
##### <a name="b-stopping-diagnostic-logging"></a>B. 停止診斷記錄  
 下列範例會停止診斷資料記錄。  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG OFF;  
```  
  
##### <a name="c-specifying-the-location-of-the-diagnostic-logs"></a>C. 指定診斷記錄的位置  
 下列範例會將診斷記錄檔的位置設定為指定的檔案路徑。  
  
```  
ALTER SERVER CONFIGURATION  
SET DIAGNOSTICS LOG PATH = 'C:\logs';  
```  
  
##### <a name="d-specifying-the-maximum-size-of-each-diagnostic-log"></a>D. 指定每個診斷記錄的大小上限  
 下列範例會將每個診斷記錄檔的大小上限設為 10 MB。  
  
```  
ALTER SERVER CONFIGURATION   
SET DIAGNOSTICS LOG MAX_SIZE = 10 MB;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Failover Policy for Failover Cluster Instances](failover-policy-for-failover-cluster-instances.md)  
  
  
