---
title: 修改的功能 (自主資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- contained database, modifications to DBs
ms.assetid: a2942509-39a2-4903-b504-ae80a300a9de
author: stevestein
ms.author: sstein
ms.openlocfilehash: bc52821deeb879022881f838c61823b23c0c10c8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709518"
---
# <a name="modified-features-contained-database"></a>修改的功能 (自主資料庫)
  下列功能已經修改成部分自主資料庫所支援的功能。 由於功能通常會進行修改，因此它們不會跨越資料庫界限。  
  
 如需相關資訊，請參閱 [自主資料庫](contained-databases.md)。  
  
## <a name="alter-database"></a>ALTER DATABASE  
  
### <a name="application-level"></a>應用程式層級  
 從自主資料庫內部使用 ALTER DATABASE 陳述式時，其語法與用於非自主資料庫的語法有所不同。 這項差異包括延伸超過資料庫至執行個體之陳述式元素的限制。 如需詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)。  
  
### <a name="instance-level"></a>執行個體層級  
 在自主資料庫外部使用時，ALTER DATABASE 的語法與用於非自主資料庫的語法有所不同。 這些變更可防止跨越資料庫界限。 如需詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)。  
  
## <a name="create-database"></a>CREATE DATABASE  
 自主資料庫的 CREATE DATABASE 語法與非自主資料庫的語法有所不同。 如需新語法需求和允許事項的相關資訊，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)。  
  
## <a name="temporary-tables"></a>暫存資料表  
 雖然自主資料庫允許使用本機暫存資料表，不過其行為與非自主資料庫的資料表行為有所不同。 在非自主資料庫中，暫存資料表資料是在 **tempdb**的定序中定序。 在自主資料庫中，暫存資料表資料是在自主資料庫的定序中定序。  
  
 與暫存資料表相關聯的所有中繼資料 (例如資料表和資料行名稱、索引等等) 都將位於目錄定序中。  
  
 具名條件約束無法用於暫存資料表中。  
  
 暫存資料表無法參考使用者定義型別、XML 結構描述集合或使用者定義函數。  
  
## <a name="collation"></a>定序  
 在非自主資料庫模型中，有三種不同的定序類型：資料庫定序、執行個體定序和 tempdb 定序。 自主資料庫只會使用兩種定序：資料庫定序和新的目錄定序。 如需自主資料庫定序的詳細資訊，請參閱 [自主資料庫定序](contained-database-collations.md) 。  
  
## <a name="user-options"></a>User Options  
 啟用自主資料庫時， [執行個體的](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md) user options 選項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]必須設定為 0。  
  
## <a name="see-also"></a>另請參閱  
 [自主資料庫定序](contained-database-collations.md)   
 [自主資料庫](contained-databases.md)  
  
  
