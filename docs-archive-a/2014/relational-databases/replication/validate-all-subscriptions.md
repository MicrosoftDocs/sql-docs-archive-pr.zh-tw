---
title: 驗證所有訂閱 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.allsubscriptions.f1
helpviewer_keywords:
- Validate All Subscriptions dialog box
ms.assetid: 32e31469-36e4-42d9-a57a-12388bfd229d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 27a7a4f5e5c3c303d5a1cbe257c0a0e9b531e824
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598266"
---
# <a name="validate-all-subscriptions"></a>驗證所有訂閱
  使用 **[驗證所有訂閱]** 對話方塊來指定下次執行每個訂閱的合併代理程式時，應驗證合併發行集的所有訂閱。 驗證的結果會在複寫監視器中顯示。 如需詳細資訊，請參閱 [Validate Data at the Subscriber](validate-data-at-the-subscriber.md)。  
  
 您也可以用滑鼠右鍵按一下 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的訂閱，然後按一下 **[驗證訂閱]** ，藉以驗證單一訂閱。  
  
## <a name="options"></a>選項。  
 **只確認資料列計數**  
 選取以驗證訂閱者端之資料表的資料列數目是否與發行者端之資料表的資料列數目相同。 此方法不會驗證資料列的內容是否相符。 資料列計數驗證提供一種輕量型驗證方法，可讓您發現資料中的問題。  
  
 **確認資料列計數並比較總和檢查碼，來確認資料列資料**  
 除了統計「發行者」與「訂閱者」上的資料列數量之外，也會使用二進位總和檢查碼演算法計算所有資料的總和檢查碼。 如果資料列計數失敗，就不會執行總和檢查碼。 這個選項對於 [!INCLUDE[ssEW](../../includes/ssew-md.md)]無效。  
  
## <a name="see-also"></a>另請參閱  
 [驗證複寫的資料](validate-data-at-the-subscriber.md)  
  
  
