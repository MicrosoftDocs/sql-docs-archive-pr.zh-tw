---
title: 從 CLR 資料庫物件進行資料存取 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], data access
- routines [CLR integration]
- data access [CLR integration]
- ADO.NET [CLR integration]
- internal data access [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], data access
- managed code [SQL Server], database objects
- .NET Data Access Provider for SQL Server [CLR integration]
- managed code [SQL Server], data access
- SqlClient provider
- in-process data access providers [CLR integration]
ms.assetid: 9a0f4dee-71c1-42e9-a85e-52382807010f
author: rothja
ms.author: jroth
ms.openlocfilehash: d229d490a9f3a7bc6f613259ee0535218de47975
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599515"
---
# <a name="data-access-from-clr-database-objects"></a>從 CLR 資料庫物件進行資料存取
  Common language runtime (CLR) 常式可以輕鬆地存取儲存在其執行之實例 [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)] 中的資料，以及儲存在遠端實例中的資料。 常式可以存取的特定資料取決於藉以執行程式碼的使用者內容。 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 來自 managed 用戶端和仲介層應用程式之資料的 .NET Framework Data Provider，從 CLR 資料庫物件中存取資料。 因為這個緣故，您可以將 ADO.NET 和 `SqlClient` 的知識運用在用戶端和中間層應用程式。  
  
> [!NOTE]  
>  根據預設，執行資料存取不允許使用使用者定義型別方法與使用者定義函數。 您必須將 `DataAccess` 或 `SqlMethodAttribute` 的 `SqlFunctionAttribute` 屬性設定為 `DataAccessKind.Read` 才能使用者定義型別 (UDT) 方法或使用者定義函數進行唯讀的資料存取。 資料修改作業無法從 UDT 或使用者定義函數進行，如果嘗試進行，則會在執行階段擲回例外狀況。  
  
 本節僅討論從 CLR 資料庫物件中存取資料時，功能與行為上的特定差異。 如需有關 ADO.NET 功能的詳細資訊，請參閱隨附在 .NET Framework SDK 中的 ADO.NET 文件集。  
  
 下表列出本節的主題。  
  
 [內容連接](context-connection.md)  
 描述 SQL Server 的內容連接。  
  
 [連接的模擬和認證](impersonation-and-credentials-for-connections.md)  
 描述模擬連接以及連接認證。  
  
 [ADO.NET 的 SQL Server 同處理序特定擴充](../../clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
 討論同處理序的特定 `SqlPipe`、`SqlContext`、`SqlTriggerContext` 與 `SqlDataRecord` 物件。  
  
 [CLR 整合和交易](../../native-client-ole-db-transactions/transactions.md)  
 描述 System.Transactions 命名空間中提供的新交易架構如何整合 ADO.NET 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 整合。  
  
 [從 CLR 資料庫物件進行 XML 序列化](../../../database-engine/dev-guide/xml-serialization-from-clr-database-objects.md)  
 說明如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中啟用 CLR 資料庫物件的 XML 序列化案例。  
  
  
