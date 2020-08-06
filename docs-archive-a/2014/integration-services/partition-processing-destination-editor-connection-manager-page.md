---
title: 資料分割處理目的地編輯器 (連線管理員頁面) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partprocessingtransformation.connection.f1
helpviewer_keywords:
- Partition Processing Destination Editor
ms.assetid: 7add6f82-eed1-47fc-a5d7-7b91f3f24d34
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5a0f79dfcc9c0d98d871a49618f4dabfb8a3bbac
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595163"
---
# <a name="partition-processing-destination-editor-connection-manager-page"></a>資料分割處理目的地編輯器 (連接管理員頁面)
  使用 [資料分割處理目的地編輯器]**** 對話方塊的 [連線管理員]**** 頁面，以指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連線。  
  
 若要深入了解資料分割處理目的地，請參閱＜ [Partition Processing Destination](data-flow/partition-processing-destination.md)＞。  
  
> [!NOTE]  
>  此處描述的工作不適用於 Analysis Services 表格式模型。  您無法針對表格式模型，將輸入資料行對應至資料分割資料行。 您可以改用 Analysis Services 執行 DDL 工作 ( [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md) ) 來處理資料分割。  
  
## <a name="options"></a>選項。  
 **[ODBC 目的地編輯器]**  
 從清單中選取現有的連線管理員，或按一下 [新增]  來建立新的連線。  
  
 **新增**  
 使用 [加入 Analysis Services 連接管理員]**** 對話方塊來建立新的連接。  
  
 **可用的資料分割清單**  
 選取要處理的資料分割。  
  
 **處理方法**  
 選取處理方法。 此選項的預設值是 **[完整]**。  
  
|值|描述|  
|-----------|-----------------|  
|加入 (累加)|執行資料分割的累加處理。|  
|完整|執行資料分割的完整處理。|  
|僅限資料|執行資料分割的更新處理。|  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [分割區處理目的地編輯器 &#40;對應頁面&#41;](../../2014/integration-services/partition-processing-destination-editor-mappings-page.md)   
 [資料分割處理目的地編輯器 &#40;進階頁面&#41;](../../2014/integration-services/partition-processing-destination-editor-advanced-page.md)  
  
  
