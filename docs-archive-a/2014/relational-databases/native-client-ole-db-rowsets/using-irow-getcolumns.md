---
title: 使用 IRow::GetColumns | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
author: rothja
ms.author: jroth
ms.openlocfilehash: f323dda790946565bc0dbd63c9e1f9d17ac7494b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593369"
---
# <a name="using-irowgetcolumns"></a>使用 IRow::GetColumns
  **IRow** 實作可允許以順向循序方式存取資料行。 每次當您存取資料列中的數個資料行時，可以使用 **IRow::GetColumns** 的單一呼叫或是呼叫 **IRow::GetColumns** 多次來存取資料列中的所有資料行。  
  
 **IRow::GetColumns** 的多次呼叫不應該重疊。 例如，如果初次呼叫 **IRow::GetColumns** 會擷取資料行 1、2 和 3，則第二次呼叫 **IRow::GetColumns** 就應該擷取資料行 4、5 和 6。 如果之後的 **IRow::GetColumns** 呼叫重疊，則狀態旗標 (DBCOLUMNACCESS 中的 dwstatus 欄位) 會設定為 DBSTATUS_E_UNAVAILABLE。  
  
## <a name="see-also"></a>另請參閱  
 [使用 IRow 來提取單一資料列](fetching-a-single-row-with-irow.md)  
  
  
