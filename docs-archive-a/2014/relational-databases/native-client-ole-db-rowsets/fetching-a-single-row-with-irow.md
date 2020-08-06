---
title: 使用 IRow 來擷取單一資料列 | Microsoft Docs
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
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 07c803ca-299a-42c5-ba02-360b9631d15f
author: rothja
ms.author: jroth
ms.openlocfilehash: b5573fe1fef39f29329e373323f5f8aaf15f2c58
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598831"
---
# <a name="fetching-a-single-row-with-irow"></a>使用 IRow 來提取單一資料列
  Native Client OLE DB 提供者中的**IRow**介面實 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已簡化，以提高效能。 **IRow** 允許直接存取單一資料列物件的資料行。 如果您事先知道命令執行的結果只會產生單一資料列，**IRow** 就會擷取該資料列的資料行。 如果結果集包含多個資料列，**IRow** 就只會公開第一個資料列。  
  
 **IRow** 實作不允許資料列的任何導覽。 此資料列中的每個資料行只會存取一次，但有一項例外狀況：您可以存取一次資料行來尋找資料行大小，然後再次存取，以便提取資料。  
  
> [!NOTE]  
>  **IRow::Open** 僅支援開啟 DBGUID_STREAM 和 DBGUID_NULL 類型的物件。  
  
 若要使用 **ICommand::Execute** 方法來取得資料列物件，您必須傳遞 IID_IRow。 **IMultipleResults** 介面必須用來處理多個結果集。 **IMultipleResults** 支援 **IRow** 和 **IRowset**。 **IRowset** 可用於大量作業。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [使用 IRow::GetColumns](using-irow-getcolumns.md)  
  
-   [使用 IRow 擷取 BLOB 資料](../../database-engine/dev-guide/fetching-blob-data-using-irow.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](rowsets.md)  
  
  
