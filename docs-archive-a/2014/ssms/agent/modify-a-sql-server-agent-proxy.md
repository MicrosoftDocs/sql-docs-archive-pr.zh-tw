---
title: 修改 SQL Server Agent Proxy | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- proxies [SQL Server Agent], modifying
- modifying SQL Server Agent proxy
ms.assetid: 6e1dfbaa-8089-4813-940c-d5a2e13d8552
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2f86793a8ddcc6fe8f981d6b367d2178c5a794ec
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594342"
---
# <a name="modify-a-sql-server-agent-proxy"></a>修改 SQL Server Agent Proxy
  本主題描述如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用或，在中修改 Agent proxy [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目修改 SQL Server Agent Proxy：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 使用認證來儲存 Windows 使用者帳戶的相關資訊。 認證中所指定的使用者，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行的電腦上必須要有「以批次工作登入」的權限。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會檢查 Proxy 的子系統存取權，而且每當作業步驟執行時，就會提供 Proxy 的存取權。 如果 Proxy 不再擁有子系統的存取權，作業步驟就會失效。 否則， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會模擬 Proxy 中所指定的使用者，並執行作業步驟。  
  
-   如果使用者的登入身分可以存取 Proxy，或者使用者隸屬於可存取 Proxy 的角色，該使用者就可以使用作業步驟中的 Proxy。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 只有 **sysadmin** 固定伺服器角色的成員才能建立、修改或刪除 Proxy 帳戶。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-a-ssnoversion-agent-proxy"></a>若要修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy  
  
1.  在 **[物件總管]** 中，按一下加號，展開包含要修改之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 帳戶的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  按一下加號展開 **[Proxy]** 資料夾。  
  
4.  按一下加號展開 Proxy 的子系統節點 (例如，[ActiveX Script]****)。  
  
5.  以滑鼠右鍵按一下要修改的 Proxy 帳戶，然後選取 [屬性]****。  
  
6.  在 [ _proxy_name_**proxy 帳戶屬性**] 對話方塊中，視需要對 proxy 帳戶進行變更。 如需有關此對話方塊之選項的詳細資訊，請參閱 [建立 SQL Server Agent Proxy](create-a-sql-server-agent-proxy.md)。  
  
7.  完成後，請按一下 **[確定]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-modify-a-ssnoversion-agent-proxy"></a>若要修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- Disables the proxy named 'Catalog application proxy'.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_proxy  
        @proxy_name = 'Catalog application proxy',  
        @enabled = 0;  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_update_proxy &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-update-proxy-transact-sql)。  
  
  
