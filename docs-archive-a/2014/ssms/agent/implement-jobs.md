---
title: 實作作業 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent]
- SQL Server Agent jobs
- SQL Server Agent jobs, about jobs
- jobs [SQL Server Agent], about jobs
ms.assetid: 69e06724-25c7-4fb3-8a5b-3d4596f21756
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1925b3113db8d7c57ac4344958c0247763cfd1b1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584951"
---
# <a name="implement-jobs"></a>實作作業
  您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業，使例行性管理工作自動化，並重複執行它們，使管理更有效率。  
  
 作業是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 循序執行的一系列指定作業。 作業可執行各式各樣的活動，包括執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼、命令列應用程式、Microsoft ActiveX Script、Integration Services 封裝、Analysis Services 命令和查詢，或複寫工作。 作業可執行重複性工作或可排程的工作，而且可產生警示，將作業狀態自動通知使用者，藉此大幅簡化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的管理。  
  
 您可以手動執行作業，或將作業設定為根據排程或為了回應警示而執行。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**說明**|**主題**|  
|包含有關建立作業及指派擁有權的資訊。|[建立作業](create-jobs.md)|  
|包含有關將作業組織成類別目錄的資訊。|[組織作業](organize-jobs.md)|  
|包含關於您可以建立的不同種類作業步驟及如何管理它們的資訊。|[管理作業步驟](manage-job-steps.md)|  
|包含關於如何定義作業何時開始執行及作業執行頻率等資訊。|[建立及附加排程至作業](create-and-attach-schedules-to-jobs.md)|  
|包含關於手動執行作業 (沒有排程) 的資訊。|[執行作業](run-jobs.md)|  
|包含關於如何設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 回應作業的資訊。 例如，您可以設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 在作業完成時通知管理者。|[指定作業回應](specify-job-responses.md)|  
|包含關於如何檢視現有的作業、其執行的記錄及如何修改它們等資訊。|[檢視或修改作業](view-or-modify-jobs.md)|  
|包含如何刪除作業的相關資訊。|[刪除作業](delete-jobs.md)|  
  
## <a name="see-also"></a>另請參閱  
 [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)  
  
  
