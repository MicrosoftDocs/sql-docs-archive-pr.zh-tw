---
title: " (XMLA) 取消命令 |Microsoft Docs"
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- connections [XML for Analysis]
- associated connections [XML for Analysis]
- XML for Analysis, canceling
- associated sessions [XML for Analysis]
- canceling connections
- canceling commands
- canceling sessions
- SPID
- XMLA, canceling
- server process IDs [XML for Analysis]
- sessions [XML for Analysis]
ms.assetid: b59f8197-c33d-4e65-9022-848ccba540f5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 003c70362c38ae1838b4679abf6485fa031a9143
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687302"
---
# <a name="canceling-commands-xmla"></a>取消命令 (XMLA)
  視發出命令之使用者的系統管理許可權而定，XML for Analysis (XMLA) 中的 [[取消](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)] 命令可以取消會話、會話、連接、伺服器進程或相關聯會話或連接上的命令。  
  
## <a name="canceling-commands"></a>取消命令  
 使用者可以傳送沒有指定屬性的 `Cancel` 命令，取消目前明確的工作階段內容中目前執行的命令。  
  
> [!NOTE]  
>  使用者無法取消在明確的工作階段中執行的命令。  
  
### <a name="canceling-batch-commands"></a>取消批次命令  
 如果使用者取消 `Batch` 命令，則會取消 `Batch` 命令中尚未執行的所有其餘命令。 如果 `Batch` 命令是交易式的，則會回復在執行 `Cancel` 命令之前所執行的任何命令。  
  
## <a name="canceling-sessions"></a>取消工作階段  
 藉由在命令的[SessionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)屬性中指定明確會話的會話識別碼 `Cancel` ，資料庫管理員或伺服器管理員可以取消會話，包括目前執行的命令。 資料庫管理員只能取消他或她擁有管理權限的資料庫之工作階段。  
  
 資料庫管理員可以擷取 DISCOVER_SESSIONS 結構描述資料列集，以擷取指定資料庫的使用中工作階段。 為了抓取 DISCOVER_SESSIONS 架構資料列集，資料庫管理員會使用 XMLA `Discover` 方法，並為方法的[限制](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictions-element-xmla)屬性中的 SESSION_CURRENT_DATABASE 限制資料行指定適當的資料庫識別碼 `Discover` 。  
  
## <a name="canceling-connections"></a>取消連接  
 藉由在命令的[ConnectionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/connectionid-element-xmla)屬性中指定連接識別碼 `Cancel` ，伺服器管理員可以取消與指定連接相關聯的所有會話，包括所有執行中的命令，以及取消連接。  
  
> [!NOTE]  
>  如果實例 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 無法找出並取消與連接相關聯的會話（例如，當資料提取在提供 HTTP 連接時開啟多個會話時），實例就無法取消連接。 如果在 `Cancel` 命令期間遇到這個情況，就會發生錯誤。  
  
 伺服器管理員可以擷取使用 `Discover` 方法的 DISCOVER_CONNECTIONS 結構描述資料列集，來為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體擷取使用中的連接。  
  
## <a name="canceling-server-processes"></a>取消伺服器處理序  
 藉由在命令的[spid](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)屬性中指定伺服器處理序識別碼 (spid) `Cancel` ，伺服器管理員可以取消與指定之 spid 相關聯的命令。  
  
## <a name="canceling-associated-sessions-and-connections"></a>取消關聯的工作階段和連接。  
 您可以將[CancelAssociated](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cancelassociated-element-xmla)屬性設定為 true，以取消與命令中指定之連線、會話或 SPID 相關聯的連接、會話和命令 `Cancel` 。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;XMLA&#41;的探索方法](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)   
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
