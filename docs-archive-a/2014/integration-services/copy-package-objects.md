---
title: 複製封裝物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- control flow [Integration Services], copying objects
- copying package objects [Integration Services]
- data flow [Integration Services], copying objects
- connection managers [Integration Services], copying
ms.assetid: 99b85e5c-d6bd-4e7c-afe4-51f6ce151c2f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3219f0023c9a28ed270adeb6fd2b795e3459c3e0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593501"
---
# <a name="copy-package-objects"></a>複製封裝物件
  此主題描述如何在某個封裝內或兩個封裝之間複製控制流程項目、資料流程項目和連接管理員。  
  
### <a name="to-copy-control-and-data-flow-items"></a>若要複製控制和資料流程項目  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含要使用之封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下您要在其間進行複製的封裝。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中，按一下內含欲複製項目之封裝的索引標籤，然後按一下 [控制流程]  、[資料流程]  或 [事件處理常式]  索引標籤。  
  
4.  選取要複製的控制流程或資料流程項目。 您可以按住 Shift 鍵再按一下項目，逐一選取項目，也可以拖曳指標使其跨越您想選取的項目，以群組方式選項項目。  
  
    > [!IMPORTANT]  
    >  當您選取優先順序條件約束和路徑連接的兩個項目時，並不會自動選取連接項目的這些優先順序條件約束和路徑。 若要複製已排序的工作流程 (也就是控制流程或資料流程的區段)，請務必同時複製優先順序條件約束和路徑。  
  
5.  以滑鼠右鍵按一下選取的項目，然後按一下 [複製]  。  
  
6.  若要將項目複製到不同的封裝，請按一下要複製到其中的封裝，然後按一下適用於項目類型的索引標籤。  
  
    > [!IMPORTANT]  
    >  除非封裝中包含至少一項「資料流程」工作，否則您就不能將資料流程複製到封裝中。  
  
7.  按一下滑鼠右鍵，並按一下 [貼上]  。  
  
### <a name="to-copy-connection-managers"></a>若要複製連接管理員  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含要處理之封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中，按一下 [控制流程]  、[資料流程]  或 [事件處理常式]  索引標籤。  
  
4.  在 [連線管理員]  區域中，以滑鼠右鍵按一下連線管理員，然後按一下 [複製]  。 您一次僅能複製一個連接管理員。  
  
5.  若要將項目複製到不同的封裝，請按一下要複製到其中的封裝，然後按一下 [控制流程]  、[資料流程]  或 [事件處理常式]  索引標籤。  
  
6.  以滑鼠右鍵按一下 [連線管理員]  區域，然後按一下 [貼上]  。  
  
## <a name="see-also"></a>另請參閱  
 [控制流程](control-flow/control-flow.md)   
 [資料流程](data-flow/data-flow.md)   
 [Integration Services &#40;SSIS&#41; 連線](connection-manager/integration-services-ssis-connections.md)   
 [複製專案項目](../../2014/integration-services/copy-project-items.md)  
  
  
