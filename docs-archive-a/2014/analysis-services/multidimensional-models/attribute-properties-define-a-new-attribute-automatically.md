---
title: 自動定義新屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- automatic attribute creation
- attributes [Analysis Services], creating
ms.assetid: 208a050a-5e2f-470c-b645-8d835e123db7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 40f9ae1f00dd0a6520c6d1b06111864fba02e8f2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708809"
---
# <a name="define-a-new-attribute-automatically"></a>自動定義新屬性
  您可以在 [維度設計師] 中使用拖放式編輯，在維度中建立新屬性。  
  
### <a name="to-create-a-new-attribute-automatically"></a>自動建立新屬性  
  
1.  在維度設計師中，開啟您要在其中建立屬性的維度。  
  
2.  在 **[維度結構]** 索引標籤上，從 **[資料來源檢視]** 窗格的資料表中選取想要繫結屬性的資料行，然後將該資料行拖曳至 **[屬性]** 窗格。  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會建立與所繫結之資料行相同名稱的新屬性。 如果有多個屬性使用相同資料行， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會在屬性名稱後面附加一個數字。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的維度](dimensions-in-multidimensional-models.md)   
 [維度屬性 (attribute) 屬性 (property) 參考](dimension-attribute-properties-reference.md)  
  
  
