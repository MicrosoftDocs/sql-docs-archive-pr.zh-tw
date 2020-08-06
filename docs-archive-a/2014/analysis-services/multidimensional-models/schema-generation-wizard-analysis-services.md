---
title: 架構產生嚮導 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- relational schema [Analysis Services]
ms.assetid: 68bf7ba3-d0cb-437f-9a3e-9edc0999af19
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2cd58ada8ea4c2dd17ba4427578ac1336a6bd353
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598026"
---
# <a name="schema-generation-wizard-analysis-services"></a>結構描述產生精靈 (Analysis Services)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 支援在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或資料庫內定義 OLAP 物件時，使用關聯式結構描述的兩個方法。 一般來說，您會根據 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或資料庫內資料來源檢視中所建構的邏輯資料模型來定義 OLAP 物件。 這個資料來源檢視是根據一個或多個關聯式資料來源中的結構描述元素所定義，如資料來源檢視中所自訂的方式一樣。  
  
 或者，您可以先定義 OLAP 物件，再產生支援這些 OLAP 物件的資料來源檢視、資料來源及基礎關聯式資料庫結構描述。 此關聯式資料庫稱為主題領域資料庫。  
  
 這個方法有時稱為由上而下設計，而且經常用於建立原型和分析模型。 當您使用這個方法時，您可以使用 [結構描述產生精靈] 根據 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或資料庫中定義的 OLAP 物件，來建立基礎資料來源檢視和資料來源物件。  
  
 這是一個反覆執行的方法。 您很有可能會隨變更維度和 Cube 的設計，多次重新執行精靈。 每次執行精靈時，精靈會將變更併入基礎物件，而且盡可能保留基礎資料庫中所包含的資料。  
  
 產生的結構描述是 SQL Server 關聯式資料庫引擎結構描述。 此精靈不會產生其他關聯式資料庫產品的結構描述。  
  
 在主題領域資料庫中擴展的資料，會使用您用來擴展 SQL Server 關聯式資料庫的任何工具和技術個別加入。 在大多數情況下，當您重新執行精靈時會保留資料，但是也有例外狀況。 例如，您若是刪除包含資料的維度或屬性，就必須捨棄某些資料。 如果因為結構描述變更，以致結構描述產生精靈必須捨棄某些資料，您會在捨棄資料之前收到警告，然後可以取消重新產生。  
  
 一般規則是結構描述產生精靈重新產生物件時，會覆寫您對結構描述產生精靈原來產生之物件所做的任何變更。 這個規則的主要例外狀況，是您將資料行加入至結構描述產生精靈所產生的資料表時。 在此情況下，[結構描述產生精靈] 會保留您加入至資料表的資料行，以及這些資料行裡的資料。  
  
## <a name="in-this-section"></a>本節內容  
 下表列出說明如何使用 [結構描述產生精靈] 的其他主題。  
  
|主題|描述|  
|-----------|-----------------|  
|[使用結構描述產生精靈 &#40;Analysis Services&#41;](schema-generation-wizard-analysis-services.md)|描述如何產生主題領域和暫存區域資料庫的結構描述。|  
|[了解資料庫結構描述](understanding-the-database-schemas.md)|描述針對主題領域和臨時區域資料庫產生的結構描述。|  
|[了解累加式產生](understanding-incremental-generation.md)|描述結構描述產生精靈的累加產生能力。|  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源視圖](data-source-views-in-multidimensional-models.md)   
 [多維度模型中的資料來源](data-sources-in-multidimensional-models.md)   
 [&#40;SSAS 多維度&#41;支援的資料來源](supported-data-sources-ssas-multidimensional.md)  
  
  
