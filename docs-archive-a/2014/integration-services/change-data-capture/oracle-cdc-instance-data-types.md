---
title: Oracle CDC 執行個體資料類型 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: eec13d8d-c15a-4542-bfc4-da66b1a6bfe0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 71d4ce02db89c1bfd11fe9a3a3535fc92fbc49fc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687103"
---
# <a name="oracle-cdc-instance-data-types"></a>Oracle CDC 執行個體資料類型
  Oracle CDC 執行個體支援大多數的 Oracle 資料類型。 以下章節描述支援的資料類型和不支援的資料類型。  
  
## <a name="supported-data-types"></a>支援的資料類型  
 下表描述可以擷取的 Oracle 資料類型，以及變更資料表中這些類型與 SQL Server 資料類型的預設對應。 為來源 Oracle 資料表加入擷取執行個體時，您可以覆寫這些對應的一部分。  
  
|Oracle 資料庫資料類型|SQL Server 資料類型|  
|-------------------------------|--------------------------|  
|BINARY_FLOAT|real|  
|BINARY_DOUBLE|FLOAT|  
|CHAR|NVARCHAR|  
|日期|DATETIME|  
|FLOAT|FLOAT|  
|INT|NUMERIC (38)|  
|INTERVAL|DATETIME|  
|NCHAR|NVARCHAR|  
|NUMBER|FLOAT|  
|NAVARCHAR2|NVARCHAR|  
|RAW|VARBINARY|  
|real|FLOAT|  
|timestamp|DATETIME2|  
|TIMESTAMP WITH TIME ZONE|VARCHAR (37)|  
|TIMESTAMP WITH LOCAL TIME ZONE|VARCHAR (37)|  
|VARCHAR2|VARCHAR|  
|XMLTYPE|NVARCHAR (MAX)|  
  
## <a name="non-supported-data-types"></a>不支援的資料類型  
 如果來源 Oracle 資料表中的資料行具有以下 Oracle 資料類型，則無法擷取這些資料表。 如果擷取的資料行具有這些資料類型，則會顯示為 null；但是，其值的變更會在擷取之資料表的變更遮罩中指示。  
  
-   LONG  
  
-   XMLTYPE  
  
-   BLOB  
  
-   CLOB  
  
 如果來源 Oracle 資料表中的資料行具有以下 Oracle 資料類型，則無法擷取這些資料表。  
  
-   BFILE  
  
-   ROWID  
  
-   REF  
  
-   UROWID  
  
-   巢狀資料表  
  
 如果資料表中有以下資料類型存在，這些資料類型會讓 LogMinder 無法針對資料表的任何資料行取得任何資料：  
  
-   使用者定義資料類型  
  
-   VARRAY  
  
## <a name="see-also"></a>另請參閱  
 [Attunity Oracle 異動資料擷取設計工具](change-data-capture-designer-for-oracle-by-attunity.md)   
 [Oracle CDC 執行個體](the-oracle-cdc-instance.md)  
  
  
