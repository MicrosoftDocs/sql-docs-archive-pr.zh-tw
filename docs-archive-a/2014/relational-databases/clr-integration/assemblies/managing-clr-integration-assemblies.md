---
title: 管理 CLR 整合元件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- database objects [CLR integration], assemblies
- common language runtime [SQL Server], assemblies
- assemblies [CLR integration], managing
ms.assetid: bdbbf325-14f6-460e-a35a-d3861d3c961e
author: rothja
ms.author: jroth
ms.openlocfilehash: 191ccd73ca42ef4c26291e6de88f5f2b0cf565ef
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704157"
---
# <a name="managing-clr-integration-assemblies"></a>管理 CLR 整合組件
  Managed 程式碼會經過編譯，然後以稱為組件的單位進行部署。 組件會封裝為 DLL 或可執行檔 (.exe)。 可執行檔可以自行執行，而 DLL 則必須裝載在現有的應用程式中。 Managed DLL 元件可以載入並由裝載 [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 CREATE ASSEMBLY 語句的資料庫，然後才可以在進程中載入並使用它。 這些組件也可以使用 ALTER ASSEMBLY 陳述式，從比較新的版本升級，或者使用 DROP ASSEMBLY 陳述式，從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 移除。  
  
 組件資訊會儲存在安裝該組件所在資料庫的 `sys.assembly_files` 資料表中。 `sys.assembly_files` 資料表包含下列資料行。  
  
|資料行|描述|  
|------------|-----------------|  
|assembly_id|為組件定義的識別項。 此號碼會指派給與同一組件相關的所有物件。|  
|NAME|物件的名稱。|  
|file_id|識別每個物件的數字，其中會將 1 的值指派給與給定 `assembly_id` 相關聯的第一個物件。 如果有多個物件與相同的 `assembly_id` 相關聯，則每個後續的 `file_id` 值都會以 1 遞增。|  
|內容|組件或檔案的十六進位表示法。|  
  
## <a name="in-this-section"></a>本節內容  
 [建立組件](creating-an-assembly.md)  
 討論如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中建立 SAFE、EXTERNAL_ACCESS 與 UNSAFE CLR 組件。  
  
 [變更組件](altering-an-assembly.md)  
 描述如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中更新 CLR 組件。  
  
 [卸除組件](dropping-an-assembly.md)  
 討論如何從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 卸除 CLR 組件。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合安全性](../security/clr-integration-security.md)   
 [CLR 整合程式碼存取安全性](../security/clr-integration-code-access-security.md)  
  
  
