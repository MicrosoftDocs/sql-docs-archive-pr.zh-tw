---
title: 使用資料庫物件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
author: stevestein
ms.author: sstein
ms.openlocfilehash: 14dd0c0175a23f809fc925c5104ac15ac408805b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707350"
---
# <a name="working-with-database-objects"></a>使用資料庫物件
  建立 SMO 物件的階段如下：  
  
1.  建立物件的執行個體。  
  
2.  設定物件屬性。  
  
3.  建立子物件的執行個體。  
  
4.  設定子物件屬性。  
  
5.  建立物件。  
  
 在 SMO 應用程式中建立 SMO 物件的執行個體時，它們不會存在於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的執行個體上，直到發出 `Create` 方法。 不過，並非每個個別物件都需要發出 `Create` 方法。 如果某個物件包含一組子物件，只需要父物件才能執行 `Create` 方法。 例如，資料表的定義要求資料表至少要包含一個資料行才能存在。 同時，如果沒有資料表，資料行無法獨立存在。 在資料表及其資料行之間有一個共同相依的關聯性。  
  
  方法可讓您對物件進行變更。 對於物件的數個變更 (例如，將子物件加入到其中一個物件的集合，或變更屬性值)，會一起進行批次處理，並當做一個變更來執行。 `Alter` 方法會降低網路流量並改善整體效能。  
  
 `Drop` 陳述式用於移除一開始建立物件所需的物件及其所有共同相依的子物件。  
  
## <a name="see-also"></a>另請參閱  
 [SMO 物件模型](../smo-object-model.md)  
  
  
