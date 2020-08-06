---
title: 執行緒視窗
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Threads Window [Transact-SQL]
ms.assetid: e153f619-0049-4162-9076-c24a454f3278
author: rothja
ms.author: jroth
ms.openlocfilehash: 6f3460c892c182996a753c2a16076418a6b2008f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87697873"
---
# <a name="threads-window"></a>執行緒視窗
  [執行緒] 視窗會顯示有關所偵錯之 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器工作階段使用的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行緒資訊。 您必須在偵錯模式中，才能顯示執行緒資訊。  
  
## <a name="task-list"></a>工作清單  
 **若要存取執行緒視窗**  
  
-   在 [偵錯]  功能表中，按一下 [視窗]  ，再按一下 [執行緒]  。  
  
## <a name="columns"></a>資料行  
 **識別碼**  
 這是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具指派給執行緒的唯一識別碼。 您可以從 sys.dm_os_threads 動態管理檢視選取資料列，以尋找有關執行緒的詳細資訊。  
  
 如果您不是在輕量型共用模式下執行，請選取一個資料列，其中的 os_thread_id 值符合 [識別碼]  資料行中的值。 如果您在輕量型共用模式下執行，請選取一個資料列，其中的 fiber_context_address 值符合 [識別碼]  資料行中的值。  
  
 **名稱**  
 使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ComputerName/InstanceName [SPID] **格式顯示有關**工作階段的資訊。  
  
 **ComputerName**  
 正在執行查詢編輯器工作階段連接之 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的電腦名稱。  
  
 **InstanceName**  
 查詢編輯器工作階段連接之 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的名稱。  
  
 **[SPID]**  
 可唯一識別此工作階段的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作階段處理序識別碼。 您可以取得有關此工作階段的資訊，其方式是在 sys.sysprocesses 檢視表中選取與 spid 資料行有相同值的資料列。  
  
 **位置**  
 顯示所偵錯之查詢編輯器工作階段內使用的指令碼檔案名稱。  
  
 **優先順序**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具不支援這個功能。  
  
 **暫止**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具不支援這個功能。  
  
## <a name="see-also"></a>另請參閱  
 [Transact-SQL 偵錯工具](transact-sql-debugger.md)   
 [Transact-SQL 偵錯工具資訊](transact-sql-debugger-information.md)   
 [sys.dm_os_threads &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql)   
 [sys.sysprocesses &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql)  
