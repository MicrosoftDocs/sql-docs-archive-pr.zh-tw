---
title: ISSAbort (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 7195311fefe3f0f1b7b4d6d789aa8d8487bc3bfe
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709846"
---
# <a name="issabort-ole-db"></a>ISSAbort (OLE DB)
  **ISSAbort**介面（在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者中公開）提供了[ISSAbort：： Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)方法，可用於取消目前的資料列集，加上使用命令批次處理的任何命令，這是一開始產生資料列集，而且尚未完成執行。  
  
 **ISSAbort**是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端提供者特定的介面，可在**ICommand：： Execute**或**IOpenRowset：： OpenRowset**所傳回的**IMultipleResults**物件上使用**QueryInterface** 。  
  
## <a name="in-this-section"></a>本節內容  
  
|方法|描述|  
|------------|-----------------|  
|[ISSAbort：： Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|取消目前的資料列集加上與目前命令相關聯之任何批次處理的命令。|  
  
## <a name="see-also"></a>另請參閱  
 [介面 &#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  
