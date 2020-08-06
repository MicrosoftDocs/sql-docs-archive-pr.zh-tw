---
title: WMI 事件監看員工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmieventwatchertask.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Event Watcher task [Integration Services]
ms.assetid: b5bb52e9-a77e-41e1-93f9-d4c3bc6b2c9a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: be20624e5ccdf665e6274f647c342498e9c0f0a9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708514"
---
# <a name="wmi-event-watcher-task"></a>WMI 事件監看員工作
  「WMI 事件監看員」工作使用 Management Instrumentation 查詢語言 (WQL) 事件查詢來監看 Windows Management Instrumentation (WMI) 事件，以指定感興趣的事件。 您可將「WMI 事件監看員」工作用於下列用途：  
  
-   等待檔案已加入資料夾的通知，然後起始檔案的處理。  
  
-   當伺服器的可用記憶體降至低於指定的百分比時，執行刪除檔案的封裝。  
  
-   監看應用程式的安裝，然後執行使用此應用程式的封裝。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含讀取 WMI 資訊的工作。  
  
 如需有關這項工作的詳細資訊，請按下列主題：  
  
-   [WMI 資料讀取器工作](wmi-data-reader-task.md)  
  
## <a name="wql-queries"></a>WQL 查詢  
 WQL 是 SQL 用語，其包含的延伸模組可支援 WMI 事件通知和其他 WMI 特定功能。 如需有關 WQL 的詳細資訊，請參閱 [MSDN Library](https://go.microsoft.com/fwlink/?linkid=62553)中的 Windows Management Instrumentation 文件集。  
  
> [!NOTE]  
>  不同 Windows 版本的 WMI 類別也有所不同。  
  
 以下查詢監看 CPU 使用超過 40% 時發出的通知。  
  
```  
SELECT * from __InstanceModificationEvent WITHIN 2 WHERE TargetInstance ISA 'Win32_Processor' and TargetInstance.LoadPercentage > 40  
```  
  
 以下查詢監看檔案加入資料夾後發出的通知。  
  
```  
SELECT * FROM __InstanceCreationEvent WITHIN 10 WHERE TargetInstance ISA "CIM_DirectoryContainsFile" and TargetInstance.GroupComponent= "Win32_Directory.Name=\"c:\\\\WMIFileWatcher\""   
```  
  
## <a name="custom-logging-messages-available-on-the-wmi-event-watcher-task"></a>WMI 事件監看員工作上可用的自訂記錄訊息  
 下表列出「WMI 事件監看員」工作的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)和[自訂訊息以進行記錄](../custom-messages-for-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`WMIEventWatcherEventOccurred`|指出發生了工作正在進行監視的事件。|  
|`WMIEventWatcherTimedout`|指出工作已經逾時。|  
|`WMIEventWatcherWatchingForWMIEvents`|指出工作已經開始執行 WQL 查詢。 項目包含查詢。|  
  
## <a name="configuration-of-the-wmi-event-watcher-task"></a>WMI 事件監看員工作的組態  
 您可以利用下列方式設定「WMI 資料讀取器」工作：  
  
-   指定要使用的 WMI 連接管理員。  
  
-   指定 WQL 查詢的來源。 來源可以在工作的外部，可以是一個變數或檔案，或者查詢可儲存於工作屬性內。  
  
-   指定發生 WMI 事件時工作採取的行動。 您可以記錄事件通知和事件後的狀態，或者引發自訂 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 事件，以提供與 WMI 事件、通知及事件後狀態相關聯的資訊。  
  
-   定義工作回應事件的方式。 工作可以根據事件設定為成功或失敗，也可以讓工作只再次監看事件。  
  
-   指定 WMI 查詢逾時後工作採取的行動。您可以記錄逾時及逾時後的狀態，或者引發一個自訂 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 事件，用來指示 WMI 事件逾時，並記錄逾時和逾時狀態。  
  
-   定義工作回應逾時的方式。工作可設定為成功或失敗，也可以讓工作只再次監看事件。  
  
-   指定工作監看事件的次數。  
  
-   指定逾時。  
  
 如果來源是一個檔案，則「WMI 事件監看員」工作會使用「檔案」連接管理員以連接到檔案。 如需相關資訊，請參閱 [Flat File Connection Manager](../connection-manager/file-connection-manager.md)。  
  
 「WMI 事件監看員」工作使用 WMI 連接管理員連接到可從中讀取 WMI 資訊的伺服器。 如需相關資訊，請參閱 [WMI Connection Manager](../connection-manager/wmi-connection-manager.md)。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [WMI 事件監看員工作編輯器 &#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [WMI 事件監看員工作編輯器 &#40;WMI 選項頁面&#41;](../wmi-event-watcher-task-editor-wmi-options-page.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-wmi-event-watcher-task"></a>WMI 事件監看員工作的程式設計組態  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiEventWatcherTask.WmiEventWatcherTask>  
  
  
