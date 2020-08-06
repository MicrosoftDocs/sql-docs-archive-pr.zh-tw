---
title: 集合 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services]
- collections [Master Data Services], about collections
ms.assetid: 5aa1d1e0-b4e5-4897-8e74-01dcf418df73
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ce49c57aad5da52dabba32a0f3fb9b6f4f45b209
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699997"
---
# <a name="collections-master-data-services"></a>集合 (Master Data Services)
  集合是一組來自單一實體的分葉成員和合併成員。 當您不需要完整的階層，而且想要檢視成員的不同群組進行報告或分析時，或當您不需要建立分類時，請使用集合。  
  
## <a name="what-collections-contain"></a>集合包含的內容  
 集合不會限制您可以包含的成員數目或類型，前提是這些成員都在同一實體內。 集合可以包含多個強制和非強制明確階層中的分葉成員與合併成員。  
  
 建立集合時，建立的不是階層結構，而是成員的一般清單。 當您從某個階層中選取一個節點，並將其加入至集合時，您所選取的合併成員是加入至集合中的唯一成員。  
  
 集合也可以包含其他集合。 您可以使用集合的集合來建立分類。  
  
 當您建立集合時，您會自動列為擁有者。 如果您是管理員，可以視需要建立集合的其他屬性。  
  
> [!NOTE]  
>  在您可以建立集合之前，實體必須啟用明確階層。 如需詳細資訊，請參閱[啟用明確階層和集合的實體 &#40;Master Data Services&#41;](enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md)。  
  
## <a name="subscription-views-for-collections"></a>集合的訂閱檢視  
 顯示集合的訂閱檢視有兩種。 [集合屬性]**** 格式會顯示集合的清單，以及與集合相關的任何屬性 (如描述或擁有者)。 [集合]**** 格式會顯示所有集合中的所有成員，以及每個成員加權和排序次序。 如需詳細資訊，請參閱[匯出資料 &#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)。  
  
 如果您為某個集合中的特定成員設定加權值，這些值則可以在相關的訂閱檢視中使用。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|啟用明確階層和集合的實體。|[啟用明確階層和集合的實體 &#40;Master Data Services&#41;](enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md)|  
|建立新集合。|[建立集合 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-collection-master-data-services.md)|  
|將成員加入至現有的集合。|[將成員加入至集合 &#40;Master Data Services&#41;](../../2014/master-data-services/add-members-to-a-collection-master-data-services.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [明確階層 &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [將資料匯出 &#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)  
  
  
