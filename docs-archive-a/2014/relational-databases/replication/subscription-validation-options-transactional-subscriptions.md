---
title: 訂閱驗證選項 (交易式訂閱) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.options.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: fd66ad1f-df01-4240-9e89-8f41bff12c1e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 40a617dd1beff24f8f072f5d139bec7c1ca65f33
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709114"
---
# <a name="subscription-validation-options-transactional-subscriptions"></a>訂閱驗證選項 (交易式訂閱)
  使用 [**訂閱驗證選項**] 對話方塊，即可指定驗證應該只使用資料列計數，或資料列計數與二進位總和檢查碼。  
  
## <a name="options"></a>選項  
 **確認訂閱者與發行者的複寫資料列數相同。**  
 選取要執行之資料列計數驗證的類型。 對於 Oracle 發行集，唯一可用的選項是 **[直接查詢資料表來計算實際資料列計數]**。  
  
 **比較總和檢查碼來確認資料列資料**  
 除了統計「發行者」與「訂閱者」上的資料列數量之外，也會使用二進位總和檢查碼演算法計算所有資料的總和檢查碼。 如果資料列計數失敗，就不會執行總和檢查碼。  
  
 **完成驗證之後停止散發代理程式。**  
 依預設，散發代理程式會持續執行。 選取此選項即可在執行驗證之後停止代理程式。 此選項可以讓您在繼續複寫資料至訂閱者之前，先檢查驗證是否已成功。  
  
## <a name="see-also"></a>另請參閱  
 [驗證訂閱者端的資料](validate-data-at-the-subscriber.md)   
 [驗證複寫的資料](validate-data-at-the-subscriber.md)  
  
  
