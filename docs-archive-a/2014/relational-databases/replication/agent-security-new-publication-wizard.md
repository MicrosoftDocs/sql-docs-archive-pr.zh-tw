---
title: 代理程式安全性 (新增發行集精靈) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.agentsecurity.articles.f1
ms.assetid: 05ae44df-8e9f-46ea-95f6-972ad109c6c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6a0da30cb49a73024ca83d8587a4f6477d21c49c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593964"
---
# <a name="agent-security-new-publication-wizard"></a>代理程式安全性 (新增發行集精靈)
  **[代理程式安全性]** 頁面可讓您指定執行下列代理程式的帳戶，並與複寫拓撲中的電腦建立連接。  
  
-   所有發行集的快照集代理程式。  
  
-   所有交易式發行集的記錄讀取器代理程式。  
  
-   允許可更新訂閱的交易式發行集之佇列讀取器代理程式。 如果您在 [發行集類型] 頁面上指定 [具有可更新訂閱的交易式發行集]，則不論您所使用可更新訂閱類型為何都會建立此代理程式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。 如需有關可更新訂閱的詳細資訊，請參閱＜ [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)＞。  
  
 如需有關代理程式所需權限和複寫安全性的最佳做法的詳細資訊，請參閱＜ [Replication Agent Security Model](security/replication-agent-security-model.md) ＞和＜ [Replication Security Best Practices](security/replication-security-best-practices.md)＞。  
  
## <a name="options"></a>選項。  
 **快照集代理程式**  
 所有發行集都會顯示。 按一下 **[安全性設定]** ，即可在 **[快照集代理程式安全性]** 對話方塊中指定安全性設定。  
  
 如需有關快照集代理程式所使用帳戶需要之權限的詳細資訊，請在 **[快照集代理程式安全性]** 對話方塊中按一下 **[說明]** 。  
  
 **記錄讀取器代理程式**  
 所有交易式發行集都會顯示。 按一下 **[安全性設定]** ，即可在 **[記錄讀取器代理程式安全性]** 對話方塊中指定安全性設定。  
  
 如需有關記錄讀取器代理程式所使用帳戶需要之權限的詳細資訊，請在 **[記錄讀取器代理程式安全性]** 對話方塊中按一下 **[說明]** 。  
  
> [!NOTE]  
>  每一個使用異動複寫發行的資料庫都有一個記錄讀取器代理程式。 如果交易式發行集已存在資料庫中，則安全性設定是唯讀的。 您可以在 **[發行集屬性]** 對話方塊中變更設定，但變更會影響資料庫中的所有交易式發行集。  
  
 **佇列讀取器代理程式**  
 允許可更新訂閱的交易式發行集都會顯示。 按一下 **[安全性設定]** ，即可在 **[佇列讀取器代理程式安全性]** 對話方塊中指定安全性設定。 此精靈完成時就會建立佇列讀取器代理程式作業；與您是否建立任何佇列更新訂閱無關。 如果您不要建立任何佇列更新訂閱，就可以停用此作業。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的 [Jobs] 資料夾中，以滑鼠右鍵按一下作業 (以下列格式命名： *[\<Publisher>].\<integer>* .)，然後按一下 [停用]。  
  
 如需有關佇列讀取器代理程式所使用的帳戶所需之權限的詳細資訊，請在 **[佇列讀取器代理程式安全性]** 對話方塊上按一下 **[說明]** 。  
  
> [!NOTE]  
>  針對每個散發資料庫 (及其服務的所有發行者) 都有一個佇列讀取器代理程式。 在使用給定散發資料庫的任何發行者上，如果已存在允許佇列更新訂閱的交易式發行集，則安全性設定是唯讀的。 您可以在 **[散發者屬性]** 對話方塊中，變更用於執行佇列讀取器代理程式和建立連接的帳戶，但變更會影響使用散發資料庫之所有發行者的發行集。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](publish/create-a-publication.md)   
 [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [檢視及修改散發者和發行者屬性](view-and-modify-distributor-and-publisher-properties.md)   
 [檢視及修改發行集屬性](publish/view-and-modify-publication-properties.md)   
 [管理複寫的登入與密碼](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [發行資料和資料庫物件](publish/publish-data-and-database-objects.md)   
 [複寫代理程式概觀](agents/replication-agents-overview.md)  
  
  
