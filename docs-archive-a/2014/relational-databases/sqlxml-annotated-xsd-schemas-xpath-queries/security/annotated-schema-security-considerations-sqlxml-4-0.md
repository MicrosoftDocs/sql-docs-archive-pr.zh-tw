---
title: " (SQLXML 4.0) 的批註式架構安全性考慮 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping schema [SQLXML], security
- annotated XDR schemas, security
- XDR schemas [SQLXML], security
- annotations [SQLXML]
- annotated XSD schemas, security
- SQLXML, annotated XSD schemas
- SQLXML, annotated XDR schemas
- security [SQLXML], annotated schemas
- XSD schemas [SQLXML], security
ms.assetid: 7d7e44dc-b6d3-4e0f-95c7-8f99930c94f2
author: rothja
ms.author: jroth
ms.openlocfilehash: 098f554410a846ed0223d17117b51025dfcf7897
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585218"
---
# <a name="annotated-schema-security-considerations-sqlxml-40"></a>註解式結構描述安全性考量 (SQLXML 4.0)
  下面是使用註解式結構描述的安全性指導方針：  
  
-   請避免在對應結構描述中使用預設的對應。 預設對應會在產生的 XML 文件中公開資料庫資訊 (資料表和資料行名稱)，因為根據預設，元素名稱會對應到資料表名稱，而屬性名稱則對應到資料行名稱。 因此，看到 XML 文件的任何使用者都可以存取資料庫中的資料表和資料行資訊，因此暴露潛在的安全性風險。 為避免此風險，請在結構描述中指定任意的元素和屬性名稱，並使用註解將其明確地對應到資料表和資料行。 如需在建立 XSD 架構時使用預設對應的詳細資訊，請參閱[XSD 專案和屬性對資料表和資料行的預設對應 &#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)。  
  
-   使用註解指定的明確對應會公開資料庫資訊 (例如資料表名稱和資料行名稱)。 因此，您可能不會想要公開地提供這些結構描述。  
  
-   某些查詢 (例如，根據對應結構描述利用遞迴指定的查詢 (透過將 `max-depth` 註解設定為較高的值指定)) 執行時間可能更久。 您可以選擇性地指定超時限制，方法是設定 [命令逾時] 屬性 (以秒為單位的) 。 例如：  
  
    ```  
    cn.Open "Provider=SQLOLEDB;Server=localhost;Database=tempdb;Integrated Security=SSPI;Command Properties='Command Time Out=50';"  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [SQLXML 4.0 中的註解式 XSD 結構描述](../../sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
  
  
