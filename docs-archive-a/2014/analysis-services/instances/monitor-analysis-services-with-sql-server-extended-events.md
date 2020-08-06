---
title: 使用 SQL Server 擴充事件 (XEvents) 來監視 Analysis Services |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b57cc2fe-52dc-4fa9-8554-5a866e25c6d7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9d12d9bc8d6a56702e1b44f8404b25681a1033f0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598038"
---
# <a name="use-sql-server-extended-events-xevents-to-monitor-analysis-services"></a>使用 SQL Server 擴充事件 (XEvents) 監視 Analysis Services
  Analysis Services 透過使用[擴充事件](../../relational-databases/extended-events/extended-events.md)來提供追蹤功能。  
  
 「擴充事件」是一種可針對伺服器系統高度擴充和設定的事件基礎結構。 「擴充事件」是一種使用極少量效能資源的一種輕量型效能監視系統。  
  
 所有 Analysis Services 事件都可以透過 XEvents 來捕捉，並以[擴充事件](../../relational-databases/extended-events/extended-events.md)中所定義的特定取用者為目標。  
  
## <a name="initiating-extended-events-in-analysis-services"></a>起始 Analysis Services 中的擴充事件  
 您可以使用類似的 XMLA 建立物件指令碼命令來啟用擴充事件追蹤，如下所示：  
  
```  
<Execute ...>  
   <Command>  
      <Batch ...>  
         <Create ...>  
            <ObjectDefinition>  
               <Trace>  
                  <ID>trace_id</ID>  
                  <Name>trace_name</Name>  
                  <ddl300_300:XEvent>  
                     <event_session ...>  
                        <event package="AS" name="AS_event">  
                           <action package="PACKAGE0" .../>  
                        </event>  
                        <target package="PACKAGE0" name="asynchronous_file_target">  
                           <parameter name="filename" value="data_filename.xel"/>  
                           <parameter name="metadatafile" value="metadata_filename.xem"/>  
                        </target>  
                     </event_session>  
                  </ddl300_300:XEvent>  
               </Trace>  
            </ObjectDefinition>  
         </Create>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 其中，下列元素會由使用者根據追蹤需要而定義：  
  
 *trace_id*  
 定義此追蹤的唯一識別碼。  
  
 *trace_name*  
 提供給此追蹤的名稱；通常是人們可讀取的追蹤定義。 使用 *trace_id* 值作為名稱是常見的做法。  
  
 *AS_event*  
 要公開的 Analysis Services 事件。 如需事件的名稱，請參閱 [Analysis Services 追蹤事件](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events) 。  
  
 *data_filename*  
 包含事件資料之檔案的名稱。 此名稱的後置字元為時間戳記，以防重複傳送追蹤時，資料遭到覆寫。  
  
 *metadata_filename*  
 包含事件中繼資料之檔案的名稱。 此名稱的後置字元為時間戳記，以防重複傳送追蹤時，資料遭到覆寫。  
  
## <a name="stopping-extended-events-in-analysis-services"></a>停止 Analysis Services 中的擴充事件  
 若要停止擴充事件追蹤物件，您需要使用類似的 XMLA 刪除物件指令碼命令來刪除該物件，如下所示：  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Batch ...>  
         <Delete ...>  
            <Object>  
               <TraceID>trace_id</TraceID>  
            </Object>  
         </Delete>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 其中，下列元素會由使用者根據追蹤需要而定義：  
  
 *trace_id*  
 定義要刪除之追蹤的唯一識別碼。  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)  
  
  
