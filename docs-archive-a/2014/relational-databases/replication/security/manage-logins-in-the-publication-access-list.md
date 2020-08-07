---
title: 管理發行集存取清單中的登入 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server replication], publication access list
- publications [SQL Server replication], publication access lists
- publication access list (PAL)
- PAL (publication access list)
- logins [SQL Server replication], managing
ms.assetid: fceb216b-0b18-4e3b-8ae0-13e35920dcbc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b96e6f46403cf3a482f00a3f5155527177920967
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593923"
---
# <a name="manage-logins-in-the-publication-access-list"></a>管理發行集存取清單中的登入
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中管理發行集存取清單內的登入。 發行集的存取是由發行集存取清單 (PAL) 所控制。 可以從 PAL 中加入及移除登入和群組。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [先決條件](#Prerequisites)  
  
-   **若要管理發行集存取清單中的登入，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
  
-   您必須先將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入與發行集資料庫中的資料庫使用者產生關聯，才能將該登入加入 PAL 中。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 您可利用發行集存取清單 (PAL) 來管理登入，此清單位於 [發行集屬性 - \<Publication>] 對話方塊的 [發行集存取清單] 頁面中。 如需存取這個對話方塊的詳細資訊，請參閱[檢視和修改發行集屬性](../publish/view-and-modify-publication-properties.md)。  
  
#### <a name="to-manage-logins-in-the-pal"></a>若要在 PAL 中管理登入  
  
1.  在 [發行集屬性 - \<Publication>] 對話方塊的 [發行集存取清單] 頁面中，使用 [新增]、[移除] 和 [全部移除] 按鈕在 PAL 新增及移除登入和群組。 請不要從 PAL 移除 **distributor_admin** 。 此帳戶由複寫使用。  
  
    > [!NOTE]  
    >  如果使用遠端散發者，則 PAL 中的帳戶在發行者和散發者兩端都必須是可以使用的。 該帳戶必須是在兩部伺服器都已定義的網域帳戶或本機帳戶。 與兩個登入相關聯的密碼必須是一樣的。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-groups-and-logins-that-belong-to-the-pal"></a>檢視屬於 PAL 的群組和登入  
  
1.  在發行集資料庫的發行者上，執行 [sp_help_publication_access](/sql/relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql)。 針對 [ ** \@ 發行**集]，指定發行集名稱。 這樣會顯示有關 PAL 中群組和登入的資訊。  
  
#### <a name="to-add-groups-and-logins-to-the-pal"></a>將群組和登入加入 PAL  
  
1.  在發行集資料庫的發行者上，執行 [sp_grant_publication_access](/sql/relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql)。 針對 [ ** \@ 發行**集] 指定發行集名稱，並針對** \@ [登**入] 指定要加入之登入或群組的名稱。  
  
#### <a name="to-remove-groups-and-logins-from-the-pal"></a>從 PAL 中移除群組和登入  
  
1.  在發行集資料庫的發行者上，執行 [sp_revoke_publication_access](/sql/relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql)。 針對 [ ** \@ 發行**集] 指定發行集名稱，並針對** \@ [登**入] 指定要移除之登入或群組的名稱。  
  
## <a name="see-also"></a>另請參閱  
 [複寫代理程式安全性模型](replication-agent-security-model.md)   
 [保護複寫拓撲](view-and-modify-replication-security-settings.md)   
 [保護發行者](secure-the-publisher.md)  
  
  
