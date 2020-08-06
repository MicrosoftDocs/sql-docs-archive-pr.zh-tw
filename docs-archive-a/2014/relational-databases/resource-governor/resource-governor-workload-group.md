---
title: 資源管理員工作負載群組 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, workload group
- workload groups [SQL Server]
- workload groups [SQL Server], overview
ms.assetid: a84c3c3f-55b6-4a30-9c42-13f082d9281e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6c6fa8f6fe960571f10d6a8505329fbe8f400e6c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699376"
---
# <a name="resource-governor-workload-group"></a>資源管理員工作負載群組
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源管理員中，工作負載群組會當做有類似分類準則之工作階段要求的容器。 工作負載允許對工作階段進行彙總監視，並定義工作階段的原則。 每個工作負載群組都位於資源集區中，資源集區代表 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體的實體資源子集。 在工作階段啟動時，資源管理員分類會將此工作階段指派給特定的工作負載群組，並且此工作階段必須使用指派給該工作負載群組的原則以及為資源集區所定義的資源來執行。  
  
## <a name="workload-group-concepts"></a>工作負載群組概念  
 根據套用至每個要求的分類準則，工作負載群組會當做類似工作階段要求的容器。 工作負載群組允許進行資源耗用量的彙總監視，以及將統一原則套用至群組中的所有要求。 群組會針對其成員定義原則。  
  
> [!NOTE]  
>  您可以將使用者定義的工作負載群組從某個資源集區移至另一個資源集區。  
  
 資源管理員預先定義了兩個工作負載群組：內部群組和預設群組。 雖然使用者無法變更分類成內部群組的任何項目，但是能夠進行監視。 當下列條件存在時，要求就會分類至預設群組中：  
  
-   沒有分類要求的準則存在。  
  
-   嘗試將要求分類至不存在的群組中。  
  
-   發生一般分類失敗。  
  
 資源管理員也會提供建立、變更和卸除工作負載群組的 DDL 陳述式。  
  
## <a name="workload-group-tasks"></a>工作負載群組工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何建立工作負載群組。|[建立工作負載群組](create-a-workload-group.md)|  
|描述如何變更工作負載群組設定。|[變更工作負載群組設定](change-workload-group-settings.md)|  
|描述如何刪除工作負載群組。|[刪除工作負載群組](delete-a-workload-group.md)|  
  
## <a name="see-also"></a>另請參閱  
 [資源管理員](resource-governor.md)   
 [啟用資源管理員](enable-resource-governor.md)   
 [資源管理員資源集區](resource-governor-resource-pool.md)   
 [資源管理員分類函數](resource-governor-classifier-function.md)   
 [使用範本來設定資源管理員](configure-resource-governor-using-a-template.md)   
 [檢視資源管理員屬性](view-resource-governor-properties.md)  
  
  
