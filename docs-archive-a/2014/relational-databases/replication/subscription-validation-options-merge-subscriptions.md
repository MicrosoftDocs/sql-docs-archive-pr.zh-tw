---
title: 訂閱驗證選項 (合併訂閱) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.mergeoptions.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: 4958c4ab-2025-42ce-b836-6fb4e9e6f24d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 458da0387dbaa1b366348c374748c42946893feb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709118"
---
# <a name="subscription-validation-options-merge-subscriptions"></a>訂閱驗證選項 (合併訂閱)
  使用 **[訂閱驗證選項]** 對話方塊來指定驗證應該只使用資料列計數，或使用資料列計數與二進位總和檢查碼。  
  
## <a name="options"></a>選項  
 **只確認資料列計數**  
 選取以驗證訂閱者端之資料表的資料列數目是否與發行者端之資料表的資料列數目相同。 此方法不會驗證資料列的內容是否相符。 資料列計數驗證提供一種輕量型驗證方法，可讓您發現資料中的問題。  
  
 **確認資料列計數並比較總和檢查碼，來確認資料列資料**  
 除了統計「發行者」與「訂閱者」上的資料列數量之外，也會使用二進位總和檢查碼演算法計算所有資料的總和檢查碼。 如果資料列計數失敗，就不會執行總和檢查碼。 此選項對無效 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] 。  
  
## <a name="see-also"></a>另請參閱  
 [驗證訂閱者端的資料](validate-data-at-the-subscriber.md)   
 [驗證複寫的資料](validate-data-at-the-subscriber.md)  
  
  
