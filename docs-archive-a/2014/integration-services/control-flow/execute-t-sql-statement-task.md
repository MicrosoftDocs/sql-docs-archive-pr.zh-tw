---
title: 執行 T-SQL 陳述式工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executetsqlstatementtask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- Execute T-SQL Statement task [Integration Services]
ms.assetid: 7e9086ca-d27e-46c0-bfad-d61333ebd55e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7ebc73ad843ac7fcf1dfbe7699ecd8ea53edcdad
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688106"
---
# <a name="execute-t-sql-statement-task"></a>執行 T-SQL 陳述式工作
  「執行 T-SQL 陳述式」工作會執行 Transact-SQL 陳述式。 如需詳細資訊，請參閱 [Transact-SQL 參考 &#40;資料庫引擎&#41;](/sql/t-sql/language-reference) 和 [Integration Services &#40;SSIS&#41; 查詢](../integration-services-ssis-queries.md)。  
  
 此工作與執行 SQL 工作類似。 不過，「執行 T-SQL 陳述式」工作僅支援 Transact-SQL 版的 SQL 語言，而且您無法在使用其他 SQL 語言方言的伺服器上使用此工作執行陳述式。 如果您需要執行參數化查詢、將查詢結果儲存至變數，或使用屬性運算式，則應使用執行 SQL 工作而非「執行 T-SQL 陳述式」工作。 如需相關資訊，請參閱 [Execute SQL Task](execute-sql-task.md)。  
  
## <a name="configuration-of-the-execute-t-sql-task"></a>設定執行 T-SQL 工作  
 您可以透過 [ [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師] 設定屬性。 這項工作位於「 **設計師」中** [工具箱] **的** [維護計畫工作] [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 區段。  
  
 如需有關可在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列主題：  
  
-   [執行 T-SQL 陳述式工作 &#40;維護計畫&#41;](../../relational-databases/maintenance-plans/execute-t-sql-statement-task-maintenance-plan.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](integration-services-tasks.md)   
 [控制流程](control-flow.md)   
 [Integration Services 套件中的 MERGE](merge-in-integration-services-packages.md)  
  
  
