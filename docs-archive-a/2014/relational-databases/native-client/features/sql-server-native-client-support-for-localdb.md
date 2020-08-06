---
title: LocalDB 的 SQL Server Native Client 支援 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
author: rothja
ms.author: jroth
ms.openlocfilehash: b08ea46e8db1b665280116a439b95748f69d03ef
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593362"
---
# <a name="sql-server-native-client-support-for-localdb"></a>SQL Server Native Client 對 LocalDB 的支援
  從 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 開始，將會提供稱為 LocalDB 的輕量版 SQL Server。 本主題將討論如何連接到 LocalDB 執行個體中的資料庫。  
  
## <a name="remarks"></a>備註  
 如需有關 LocalDB 的詳細資訊，包括如何安裝 LocalDB 和設定 LocalDB 執行個體，請參閱：  
  
-   [SQL Server Express LocalDB 參考](../../sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2014 Express LocalDB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 總而言之，LocalDB 可讓您：  
  
-   使用 `sqllocaldb.exe i` 來探索預設執行個體的名稱。  
  
-   使用 `AttachDBFilename` 連接字串關鍵字來指定伺服器應該附加的資料庫檔案。 使用時 `AttachDBFilename` ，如果您未以**資料庫**連接字串關鍵字來指定資料庫的名稱，當應用程式關閉時，資料庫將會從 LocalDB 實例中移除。  
  
-   在連接字串中指定 LocalDB 執行個體：  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 必要時，您可以使用 sqllocaldb.exe 來建立 LocalDB 執行個體。 您也可以使用 sqlcmd.exe，在 LocalDB 執行個體中加入和修改資料庫。 例如： `sqlcmd -S (localdb)\v11.0` 。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
