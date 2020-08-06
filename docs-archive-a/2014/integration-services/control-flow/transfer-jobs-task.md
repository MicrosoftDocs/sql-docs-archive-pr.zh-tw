---
title: 傳送作業工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferjobstask.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d692934d5f7c8c1449b123ee8b9caf1d8bb34744
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584664"
---
# <a name="transfer-jobs-task"></a>傳送作業工作
  「傳送作業」工作會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體之間，傳送一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent 作業。  
  
 「傳送作業」工作可以設定為傳送所有作業，或只傳送指定的作業。 您還可以指出是否在目的地啟用已傳送的作業。  
  
 要傳送的作業可能已存在於目的地上。 可以設定「傳送作業」工作以下列方式處理現有的作業：  
  
-   覆寫現有的作業。  
  
-   存在重複的作業時讓工作失敗。  
  
-   略過重複的作業。  
  
 在執行階段，「傳送作業」工作會使用一或兩個 SMO 連接管理員，連接到來源和目的地伺服器。 SMO 連接管理員會在「傳送作業」工作以外另行設定，然後在「傳送作業」工作中參考。 存取伺服器時，SMO 連接管理員會指定要使用的伺服器和驗證模式。 如需詳細資訊，請參閱 [SMO Connection Manager](../connection-manager/smo-connection-manager.md)。  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>在 SQL Server 的執行個體之間傳送作業  
 「傳送作業」工作支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來源和目的地。 將哪一個用作來源或目的地是沒有限制的。  
  
## <a name="events"></a>事件  
 「傳送作業」工作會引發報告已傳送作業數目的資訊事件，並在覆寫作業時引發警告事件。 該工作並不報告作業傳送的累加進度，它只報告 0% 和 100% 完成。  
  
## <a name="execution-value"></a>執行值  
 工作之 `ExecutionValue` 屬性中定義的執行值會傳回已傳送的作業數目。 透過將使用者自訂變數指派給「傳送作業」工作的 `ExecValueVariable` 屬性，可將與作業傳送相關的資訊用於封裝中的其他物件。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)和[在封裝中使用變數](../use-variables-in-packages.md)。  
  
## <a name="log-entries"></a>記錄項目  
 「傳送作業」工作包含下列自訂記錄項目：  
  
-   TransferJobsTaskStarTransferringObjects   此記錄項目報告傳送已開始。 記錄項目會包含開始時間。  
  
-   TransferJobsTaskFinishedTransferringObjects   此記錄項目報告傳送已完成。 記錄項目會包含結束時間。  
  
 此外，`OnInformation` 事件的記錄項目會報告已傳送的作業數目，並會為在目的地上覆寫的每個作業，寫入 `OnWarning` 事件的記錄項目。  
  
## <a name="security-and-permissions"></a>安全性和權限  
 若要傳送作業，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的來源和目的地執行個體上，使用者都必須是系統管理員 (sysadmin) 固定伺服器角色的成員，或者是 msdb 資料庫上固定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent 固定資料庫角色的其中一個成員。  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>設定傳送作業工作  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [傳送作業工作編輯器 &#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [傳送作業工作編輯器 &#40;作業頁面&#41;](../transfer-jobs-task-editor-jobs-page.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>相關工作  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](integration-services-tasks.md)   
 [控制流程](control-flow.md)  
  
  
