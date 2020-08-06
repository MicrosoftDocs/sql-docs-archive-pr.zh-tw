---
title: 傳送作業工作編輯器 (作業頁面) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferjobstask.jobs.f1
helpviewer_keywords:
- Transfer Jobs Task Editor
ms.assetid: e72b1dc7-8cda-4ee6-abb5-d438370f04df
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d2d506da6997965e40d66521f7dccb8218e165fb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607455"
---
# <a name="transfer-jobs-task-editor-jobs-page"></a>傳送作業工作編輯器 (作業頁面)
  使用 [傳送作業工作編輯器] 對話方塊的 [作業] 頁面，即可指定屬性用來將一或多個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 作業，從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的一個執行個體複製到另一個。 如需有關傳送作業工作的詳細資訊，請參閱＜ [Transfer Jobs Task](control-flow/transfer-jobs-task.md)＞。  
  
> [!NOTE]  
>  若要存取來源伺服器上的作業，使用者就必須至少是伺服器上之 **SQLAgentUserRole** 固定資料庫角色的成員。 若要在目的地伺服器上順利建立作業，使用者就必須是 **sysadmin** 固定伺服器角色的成員，或是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 固定資料庫角色的成員。 如需 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 固定資料庫角色及其權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
## <a name="options"></a>選項。  
 **SourceConnection**  
 在清單中選取一個 SMO 連線管理員，或按一下 **\<New connection...>** ，以建立新的來源伺服器連線。  
  
 **DestinationConnection**  
 在清單中選取一個 SMO 連線管理員，或按一下 **\<New connection...>** ，以建立新的目的地伺服器連線。  
  
 **TransferAllJobs**  
 選取工作是否應將所有作業或只有指定的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 作業，從來源複製到目的地伺服器。  
  
 此屬性具有下表所列的選項：  
  
|值|描述|  
|-----------|-----------------|  
|**True**|複製所有作業。|  
|**False**|只複製指定的作業。|  
  
 **JobsList**  
 按一下瀏覽按鈕 **(...)** 來選取要複製的作業。 必須至少選取一個作業。  
  
> [!NOTE]  
>  選取要複製的作業之前，請指定 **SourceConnection** 。  
  
 當 **TransferAllJobs** 設定為 **True** 時，無法使用 **JobsList**選項。  
  
 **IfObjectExists**  
 選取工作應如何處理已經存在於目的地伺服器上，且具有相同名稱的作業。  
  
 此屬性具有下表所列的選項：  
  
|值|描述|  
|-----------|-----------------|  
|**FailTask**|如果具有相同名稱的作業己經存在於目的地伺服器上，工作就會失敗。|  
|**Overwrite**|工作會覆寫目的地伺服器上具有相同名稱的作業。|  
|**Skip**|工作會略過存在於目的地伺服器上具有相同名稱的作業。|  
  
 **EnableJobsAtDestination**  
 選取是否應啟用已複製到目的地伺服器的作業。  
  
 此屬性具有下表所列的選項：  
  
|值|描述|  
|-----------|-----------------|  
|**True**|啟用目的地伺服器上的作業。|  
|**False**|停用目的地伺服器上的作業。|  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 工作](control-flow/integration-services-tasks.md)   
 [[傳送作業工作編輯器] &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [運算式頁面](expressions/expressions-page.md)   
 [SMO 連線管理員](connection-manager/smo-connection-manager.md)  
  
  
