---
title: 設定屬性關聯性屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- flexible relationships (Analysis Services)
- attributes [Analysis Services], relationships
- relationships [Analysis Services], attributes
- properties [Analysis Services], attribute relationships
- rigid relationships (Analysis Services)
ms.assetid: fce511af-66d7-42fc-bb3a-6c516f16b10e
author: minewiskan
ms.author: owend
ms.openlocfilehash: 241fa2af16377fd2cacf657ec6f99c5ca4bd0c53
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585658"
---
# <a name="configure-attribute-relationship-properties"></a>設定屬性 (Attribute) 關聯性屬性 (Property)
  下表列出及描述屬性 (Attribute) 關聯性的屬性 (Property)。  
  
|屬性|描述|  
|--------------|-----------------|  
|屬性|包含屬性的名稱。|  
|基數|指出關聯性的基數。 值可為許多 (針對多對一的關聯性)，或是一 (針對一對一的關聯性)。 預設值是「許多」。 在中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，基數屬性沒有作用-它的用途是保留供未來的執行。|  
|名稱|包含屬性的易記名稱。|  
|RelationshipType|指出成員關聯性是否會隨時間變更。 值可為 Rigid，表示成員之間的關聯性並不會隨著時間變更；或為 Flexible，表示成員之間的關聯性會隨時間變更。 預設值是 Flexible。 如果將關聯性定義為彈性，彙總會進行卸除，並重新計算做為累加式更新的一部分 (如果只是加入新成員，就不會卸除)。 如果將關聯性定義為固定，當維度進行累加式更新時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會保留彙總。 如果定義為固定的關聯性變更了， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會在累加式處理期間產生錯誤。 指定適當的關聯性和關聯性屬性可增加查詢和處理效能。|  
|可見|決定屬性關聯性是否可見。 值為 True 或 False。 預設值是 True。|  
  
  
