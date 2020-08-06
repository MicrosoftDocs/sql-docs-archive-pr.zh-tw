---
title: 移動資料庫檔案 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- files [SQL Server], moving
- data files [SQL Server], moving
- file moving [SQL Server]
- moving full-text catalogs
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- scheduled disk maintenance [SQL Server]
- moving files
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5491f3c4dfd47cac4047d0409c78001be80d6f13
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705154"
---
# <a name="move-database-files"></a>移動資料庫檔案
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，您可以在 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) 陳述式的 FILENAME 子句中指定新的檔案位置，以移動系統和使用者資料庫。 可以使用此方式來移動資料、記錄以及全文檢索目錄檔案。 在下列狀況下這個方法將非常有用：  
  
-   失敗復原。 例如，資料庫因硬體失敗而導致在質疑模式下或被關閉。  
  
-   計畫的重新放置。  
  
-   排程的磁碟維護重新放置。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[移動使用者資料庫](move-user-databases.md)|描述將使用者資料庫檔案和全文檢索目錄檔案移到新位置的程序。|  
|[移動系統資料庫](system-databases.md)|描述將系統資料庫檔案移到新位置的程序。|  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [資料庫卸離與附加 &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)  
  
  
