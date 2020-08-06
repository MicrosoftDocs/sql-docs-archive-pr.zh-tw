---
title: FileTable DDL、函式、預存程序和檢視 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], database objects
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3fca483581a47720cf0d923506f4439e3e614520
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707613"
---
# <a name="filetable-ddl-functions-stored-procedures-and-views"></a>FileTable DDL、函數、預存程序及檢視
  列出已加入或變更以支援 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中 FileTable 功能的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 陳述式和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫物件。  
  
 下表中的 [狀態] 資料行會指出項目為 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中的新項目，或是存在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，但已在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中變更，可支援語意搜尋。  
  
 如需支援 FILESTREAM 的陳述式和資料庫物件清單，請參閱＜ [FILESTREAM DDL, Functions, Stored Procedures, and Views](../views/views.md)＞。  
  
##  <a name="transact-sql-data-definition-language-ddl-statements"></a><a name="ddl"></a> Transact-SQL 資料定義語言 (DDL) 陳述式  
  
|Object|狀態|相關資訊|  
|------------|------------|----------------------|  
|[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)<br /><br /> [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)|已變更|[啟用 FileTable 的必要條件](enable-the-prerequisites-for-filetable.md)<br /><br /> [管理 FileTable](manage-filetables.md)|  
|[ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)|已變更|[建立、改變及卸除 FileTable](create-alter-and-drop-filetables.md)<br /><br /> [管理 FileTable](manage-filetables.md)|  
|[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)|已變更|[啟用 FileTable 的必要條件](enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)|已變更|[建立、改變及卸除 FileTable](create-alter-and-drop-filetables.md)|  
|[RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)<br /><br /> [RESTORE 引數 &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)|已變更||  
  
##  <a name="functions"></a><a name="func"></a> 函數  
  
|Object|狀態|相關資訊|  
|------------|------------|----------------------|  
|[FileTableRootPath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filetablerootpath-transact-sql)|**已加入**|[使用 FileTable 中的目錄與路徑](work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql)|**已加入**|[使用 FileTable 中的目錄與路徑](work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql)|**已加入**|[使用 FileTable 中的目錄與路徑](work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="stored-procedures"></a><a name="sproc"></a> 預存程序  
  
|Object|狀態|相關資訊|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles)|**已加入**|[管理 FileTable](manage-filetables.md)|  
  
##  <a name="catalog-views"></a><a name="cv"></a> 目錄檢視  
  
|Object|狀態|相關資訊|  
|------------|------------|----------------------|  
|[sys.database_filestream_options &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql)|**已加入**|[啟用 FileTable 的必要條件](enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql)|**已加入**|[建立、改變及卸除 FileTable](create-alter-and-drop-filetables.md)<br /><br /> [管理 FileTable](manage-filetables.md)|  
|[sys.filetables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetables-transact-sql)|**已加入**|[管理 FileTable](manage-filetables.md)|  
|[sys.tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|已變更|[管理 FileTable](manage-filetables.md)|  
  
##  <a name="dynamic-management-views"></a><a name="dmv"></a> 動態管理檢視  
  
|Object|狀態|相關資訊|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql)|**已加入**|[管理 FileTable](manage-filetables.md)|  
  
## <a name="see-also"></a>另請參閱  
 [管理 FileTable](manage-filetables.md)  
  
  
