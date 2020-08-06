---
title: 初始化訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.initializesubscriptions.f1
ms.assetid: 7b170e4e-470d-4828-a9ed-7435b0b03514
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f8c9388138ddec275dc1abd2b75e0b0c7fc99de4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585816"
---
# <a name="initialize-subscriptions"></a>初始化訂閱
  訂閱者必須先初始化，才能開始接收複寫的資料。 不需要有初始資料集，但訂閱者至少必須有每個複寫物件的結構描述，以及複寫所需的任何中繼資料表和程序。  
  
## <a name="options"></a>選項。  
 **訂閱屬性**  
 針對每個需要初始資料集的訂閱者，選取 **[初始化]** 資料行中的核取方塊。 如果清除此核取方塊，則只會初始化複寫中繼資料和程序。 如需不使用快照集初始化訂閱的詳細資訊，請參閱[不使用快照集初始化交易式訂閱](initialize-a-transactional-subscription-without-a-snapshot.md)。  
  
 在 **[初始化時機]** 資料行的下拉式清單方塊中，選取 **[立即]** ，即可使合併代理程式或散發代理程式在此精靈完成後，將快照集檔案傳送至訂閱者。 選取 **[第一次同步處理時]** ，即可使代理程式在下一個執行排程傳送檔案。   的提取訂閱無法使用 [立即][!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 選項。 合併代理程式或散發代理程式無法在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]的執行個體上執行；因此必須經由其他方法初始化訂閱。  
  
> [!NOTE]  
>  精靈可能會提示散發者的連接，以便為散發者代理程式或合併代理程式啟動適當的作業。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [初始化訂閱](initialize-a-subscription.md)   
 [訂閱發行集](subscribe-to-publications.md)  
  
  
