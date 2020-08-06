---
title: Wmi 資料讀取器工作編輯器 (WMI 選項頁面) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmidatareadertask.wmiquery.f1
helpviewer_keywords:
- WMI Data Reader Task Editor
ms.assetid: 4b8d4716-882d-41b0-b77e-e0e2741a2cd5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cfb28e7f8f352f708085bf664757391a05869752
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599553"
---
# <a name="wmi-data-reader-task-editor-wmi-options-page"></a>WMI 資料讀取器工作編輯器 (WMI 選項頁面)
  使用 [WMI 資料讀取器工作編輯器]  對話方塊的 [WMI 選項]  頁面，來指定 Windows Management Instrumentation 查詢語言 (WQL) 查詢的來源和查詢結果的目的地。  
  
 若要了解這個工作，請參閱＜ [WMI Data Reader Task](control-flow/wmi-data-reader-task.md)＞。 如需 WMI 查詢語言 (WQL) 的詳細資訊，請參閱 MSDN Library 中的 Windows Management Instrumentation 主題 [Querying with WQL](https://go.microsoft.com/fwlink/?LinkId=79045)(使用 WQL 查詢)。  
  
## <a name="static-options"></a>靜態選項  
 **WMIConnectionName**  
 在清單中選取 WMI 連線管理員，或按一下 \<**New WMI Connection...**> 來建立新的連線管理員。  
  
 **相關主題：** [WMI 連線管理員](connection-manager/wmi-connection-manager.md)、[WMI 連線管理員編輯器](../../2014/integration-services/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 選取工作執行之 WQL 查詢的來源類型。 這個屬性具有下表中所列的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 WQL 查詢的來源。 選取這個值就會顯示 **[WQLQuerySourceType]** 動態選項。|  
|**檔案連接**|選取包含 WQL 查詢的檔案。 選取這個值就會顯示 **[WQLQuerySourceType]** 動態選項。|  
|**變數**|將來源設定為定義 WQL 查詢的變數。 選取這個值就會顯示 **[WQLQuerySourceType]** 動態選項。|  
  
 **OutputType**  
 指定輸出應為資料表、屬性值或屬性名稱和值。  
  
 **OverwriteDestination**  
 指定是要保留、覆寫還是附加至目的地檔案或變數中的原始資料。  
  
 **DestinationType**  
 選取此工作執行之 WQL 查詢的目的地類型。 這個屬性具有下表中所列的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**檔案連接**|選取檔案以儲存 WQL 查詢的結果。 選取此值會顯示動態選項 **[DestinationType]** 。|  
|**變數**|設定變數以儲存 WQL 查詢的結果。 選取此值會顯示動態選項 **[DestinationType]** 。|  
  
## <a name="wqlquerysourcetype-dynamic-options"></a>WQLQuerySourceType 動態選項  
  
### <a name="wqlquerysourcetype--direct-input"></a>WQLQuerySourceType = 直接輸入  
 **WQLQuerySource**  
 提供查詢，或按一下省略符號 (...)，然後使用 [WQL 查詢]  對話方塊輸入查詢。  
  
### <a name="wqlquerysourcetype--file-connection"></a>WQLQuerySourceType = 檔案連接  
 **WQLQuerySource**  
 在清單中選取檔案連線管理員，或按一下 \<**New connection...**> 來建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="wqlquerysourcetype--variable"></a>WQLQuerySourceType = 變數  
 **WQLQuerySource**  
 在清單中選取變數，或按一下 \<**New variable...**> 來建立新的變數。  
  
 **相關主題：** [Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)  
  
## <a name="destinationtype-dynamic-options"></a>DestinationType 動態選項  
  
### <a name="destinationtype--file-connection"></a>DestinationType = 檔案連接  
 **目的地**  
 在清單中選取檔案連線管理員，或按一下 [\<**New connection...**>] 以建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="destinationtype--variable"></a>DestinationType = 變數  
 **目的地**  
 在清單中選取變數，或按一下 [\<**New variable...**>] 以建立新的變數。  
  
 **相關主題：** [Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [WMI 資料讀取器工作編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [運算式頁面](expressions/expressions-page.md)   
 [WMI 事件監看員工作](control-flow/wmi-event-watcher-task.md)  
  
  
