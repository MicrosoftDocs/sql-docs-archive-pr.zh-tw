---
title: SQL Server 目的地自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b736aa6d-c154-44a0-be08-f25733fca1d9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a4ad136319e4ec6bd42c9da8dd8e99ab00cddadc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599111"
---
# <a name="sql-server-destination-custom-properties"></a>SQL Server 目的地自訂屬性
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地同時具有自訂屬性，以及所有資料流程元件通用的屬性。  
  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|AlwaysUseDefaultCodePage|Boolean|強制使用 DefaultCodePage 屬性值。 此屬性的預設值為 `False`。|  
|BulkInsertCheckConstraints|Boolean|一個值，指定大量插入是否會檢查條件約束。 此屬性的預設值為 `True`。|  
|BulkInsertFireTriggers|Boolean|一個值，指定大量插入是否會引發資料表上的觸發程序。 此屬性的預設值為 `False`。|  
|BulkInsertFirstRow|整數|一個值，指定要插入的第一個資料列。 此屬性的預設值是 **-1**，表示未指派任何值|  
|BulkInsertKeepIdentity|Boolean|一個值，指定值是否可插入識別欄位中。 此屬性的預設值為 `False`。|  
|BulkInsertKeepNulls|Boolean|一個值，指定大量插入是否會保留 Null 值。 此屬性的預設值為 `False`。|  
|BulkInsertLastRow|整數|一個值，指定要插入的最後一個資料列。 此屬性的預設值是 **-1**，表示未指派任何值。|  
|BulkInsertMaxErrors|整數|一個值，指定停止大量插入之前可以發生的錯誤數目。 此屬性的預設值是 **-1**，表示未指派任何值。|  
|BulkInsertOrder|String|排序資料行的名稱。 每個資料行都可依遞增或遞減順序來排序。 如果使用了多個排序資料行，這些資料行名稱會以逗號隔開。|  
|BulkInsertTableName|String|要將資料複製到其中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫資料表或檢視表。|  
|BulkInsertTablock|Boolean|一個值，指定在進行大量插入期間是否會鎖定資料表。 此屬性的預設值為 `True`。|  
|DefaultCodePage|整數|無法從資料來源中取得字碼頁資訊時要使用的字碼頁。|  
|MaxInsertCommitSize|整數|一個值，指定要在批次中插入的資料列數目上限。 當此值為零時，就會在單一批次中插入所有資料列。|  
|逾時|整數|一個值，指定如果沒有資料可供插入， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地在終止之前等候的秒數。 值為 0 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地將不會逾時。這個屬性的預設值為 30。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地的輸入和輸入資料行沒有自訂屬性。  
  
 如需詳細資訊，請參閱 [SQL Server 目的地](sql-server-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](../common-properties.md)  
  
  
