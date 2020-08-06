---
title: FileTable 結構描述 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], table schema
ms.assetid: e1cb3880-cfda-40ac-91fc-d08998287f44
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fa6a6d3d033633a136f51437c415a2998c075859
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707610"
---
# <a name="filetable-schema"></a>FileTable 結構描述
  描述 FileTable 預先定義且固定的結構描述。  
  
|檔案屬性名稱|type|大小|預設|描述|檔案系統可存取性|  
|-------------------------|----------|----------|-------------|-----------------|-------------------------------|  
|**path_locator**|`hierarchyid`|變動|識別此項目位置的 `hierarchyid`。|此節點在階層式 FileNamespace 中的位置。<br /><br /> 資料表的主索引鍵。|可透過設定 Windows 路徑值加以建立及修改。|  
|**stream_id**|**[uniqueidentifier] rowguidcol**||`NEWID()` 函數所傳回的值。|FILESTREAM 資料的唯一識別碼。|不適用。|  
|**file_stream**|`varbinary(max)`<br /><br /> `filestream`|變動|NULL|包含 FILESTREAM 資料。|不適用。|  
|**file_type**|`nvarchar(255)`|變動|NULL。<br /><br /> 檔案系統中的建立或重新命名作業，將會根據名稱填入副檔名值。|代表檔案的類型。<br /><br /> 當您建立全文檢索索引時，此資料行可用以做為 `TYPE COLUMN`。<br /><br /> **file_type** 是保存的計算資料行。|自動計算， 無法設定。|  
|**名稱**|`nvarchar(255)`|變動|GUID 值。|檔案或目錄名稱。|可使用 Windows API 加以建立或修改。|  
|**parent_path_locator**|`hierarchyid`|變動|識別內含此項目之目錄的 `hierarchyid`。|上層目錄的 `hierarchyid`。<br /><br /> **parent_path_locator** 是保存的計算資料行。|自動計算， 無法設定。|  
|**cached_file_size**|`bigint`|||FILESTREAM 資料的大小 (以位元組為單位)。<br /><br /> **cached_file_size** 是保存的計算資料行。|雖然快取的檔案大小會自動保持最新狀態，不過在少見的情況下，它可能會呈現未同步狀態。 若要計算確切的大小，請使用 `DATALENGTH()` 函數。|  
|**creation_time**|`datetime2(4)`<br /><br /> `not null`|8 個位元組|目前時間。|建立檔案的日期與時間。|自動計算， 也可以使用 Windows API 加以設定。|  
|**last_write_time**|`datetime2(4)`<br /><br /> `not null`|8 個位元組|目前時間。|上次更新檔案的日期與時間。|自動計算， 也可以使用 Windows API 加以設定。|  
|**last_access_time**|`datetime2(4)`<br /><br /> `not null`|8 個位元組|目前時間。|上次存取檔案的日期與時間。|自動計算， 也可以使用 Windows API 加以設定。|  
|**is_directory**|`bit`<br /><br /> `not null`|1 個位元組|FALSE|指出資料列是否代表目錄。 此值會自動計算，而且無法設定。|自動計算， 無法設定。|  
|**is_offline**|`bit`<br /><br /> `not null`|1 個位元組|FALSE|離線檔案屬性。|自動計算， 也可以使用 Windows API 加以設定。|  
|**is_hidden**|`bit`<br /><br /> `not null`|1 個位元組|FALSE|隱藏檔案屬性。|自動計算， 也可以使用 Windows API 加以設定。|  
|**is_readonly**|`bit`<br /><br /> `not null`|1 個位元組|FALSE|唯讀檔案屬性。|自動計算， 也可以使用 Windows API 加以設定。|  
|**is_archive**|`bit`<br /><br /> `not null`|1 個位元組|FALSE|封存屬性。|自動計算， 也可以使用 Windows API 加以設定。|  
|**is_system**|`bit`<br /><br /> `not null`|1 個位元組|FALSE|系統檔案屬性。|自動計算， 也可以使用 Windows API 加以設定。|  
|**is_temporary**|`bit`<br /><br /> `not null`|1 個位元組|FALSE|暫存檔案屬性。|自動計算， 也可以使用 Windows API 加以設定。|  
  
## <a name="see-also"></a>另請參閱  
 [建立、改變及卸除 FileTable](create-alter-and-drop-filetables.md)  
  
  
