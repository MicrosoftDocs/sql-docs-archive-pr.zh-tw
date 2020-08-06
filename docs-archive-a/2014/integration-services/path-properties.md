---
title: 路徑屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- paths [Integration Services], properties
ms.assetid: 89b1e347-9579-4f6b-af74-c6519ea08eea
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ca263b866fb6d5d7ceb6352f708f387d79cad4f7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592096"
---
# <a name="path-properties"></a>路徑屬性
  物件模型中的資料流程物件 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 具有元件層級、輸入和輸出，以及輸入資料行和輸出資料行的通用屬性和自訂屬性。 許多屬性都有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
 本主題將列出及描述連接資料流程物件之路徑的自訂屬性。  
  
## <a name="path-properties"></a>路徑屬性  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件模型中，連接資料流程中元件的路徑會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 介面。  
  
 下表將描述資料流程中路徑的可設定屬性。 資料流程引擎也會將值指派給這裡未列出的其他唯讀屬性。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|PathAnnotation|整數 (列舉)|指出設計師介面上是否應該與路徑一起顯示註解的值。 可能的值為 `AsNeeded`、`SourceName`、`PathName` 和 `Never`。 預設值是 `AsNeeded`。|  
|DestinationName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>|與路徑相關聯的輸入。|  
|SourceName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>|與路徑相關聯的輸出。|  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 路徑](data-flow/integration-services-paths.md)   
 [通用屬性](../../2014/integration-services/common-properties.md)   
 [轉換自訂屬性](data-flow/transformations/transformation-custom-properties.md)   
 [可以使用運算式設定的資料流程屬性](../../2014/integration-services/data-flow-properties-that-can-be-set-by-using-expressions.md)  
  
  
