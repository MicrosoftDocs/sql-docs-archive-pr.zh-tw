---
title: 多個優先順序條件約束 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- multiple precedence constraints
- precedence executables [Integration Services]
- precedence constraints [Integration Services], multiple
- constrained executables [Integration Services]
ms.assetid: 71c53ead-3d19-4bc1-aafd-e5b32595b420
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 16fefbbf886818989131710876564fc9e147a56a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596098"
---
# <a name="multiple-precedence-constraints"></a>多個優先順序條件約束
  優先順序條件約束會連接兩個可執行檔：兩個工作、兩個容器，或一個工作和一個容器。 其稱為優先順序可執行檔與受條件約束的可執行檔。 條件約束可執行檔可包含多個優先順序條件約束。 如需詳細資訊，請參閱 [優先順序條件約束](control-flow/precedence-constraints.md)。  
  
 藉由群組條件約束來組裝複雜的條件約束案例，可讓您在封裝中實作複雜的控制流程。 例如，在下圖中，工作 D 按 `Success` 條件約束連結到工作 A、按 `Failure` 條件約束連結到工作 B，同時按 `Success` 條件約束連結到工作 C。 工作 D 與工作 A、工作 D 與工作 B，以及工作 D 與工作 C 之間的優先順序條件約束會參與邏輯 *and* 關聯性。 因此，工作 A 必須成功執行、工作 B 必須失敗，而且工作 C 必須成功執行，才可以執行工作 D。  
  
 ![優先順序條件約束所連結的工作](media/precedenceconstraints.gif "優先順序條件約束所連結的工作")  
  
## <a name="logicaland-property"></a>LogicalAnd 屬性  
 如果工作或容器具有多個條件約束，則 `LogicalAnd` 屬性會指定是只評估優先順序條件約束，還是同時評估其他條件約束。  
  
 您可以 `LogicalAnd` 使用 [設計師] 中的 [**優先順序條件約束編輯器**] [!INCLUDE[ssIS](../includes/ssis-md.md)] ，或在提供的屬性視窗中設定屬性 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 。  
  
## <a name="related-tasks"></a>相關工作  
 [設定優先順序條件約束的屬性](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
  
