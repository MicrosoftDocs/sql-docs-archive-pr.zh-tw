---
title: 變更伺服器驗證模式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- authentication [SQL Server], changing modes
- server authentication mode [SQL Server]
- modifying server authentication mode
ms.assetid: 79babcf8-19fd-4495-b8eb-453dc575cac0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8bda31ca7d0c5949173a9a3e5ea656c1757c04f7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707878"
---
# <a name="change-server-authentication-mode"></a>變更伺服器驗證模式
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 變更 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的伺服器驗證模式。 在安裝期間， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會設為 **[Windows 驗證模式]** 或 **[SQL Server 及 Windows 驗證模式]** 。 安裝後，您可以隨時變更驗證模式。  
  
 如果您在安裝期間選取 [Windows 驗證模式]，sa 登入便會停用，且安裝程式會指派密碼。 即使稍後將驗證模式改成 [SQL Server 及 Windows 驗證模式]，sa 登入也會保持停用狀態。 若要使用 sa 登入，請使用 ALTER LOGIN 陳述式啟用 sa 登入並指派新密碼。 sa 登入只能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接到伺服器。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目變更伺服器驗證模式：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 sa 帳戶是已知的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，而且經常是惡意使用者的攻擊目標。 除非您的應用程式需要，否則請勿啟用 sa 帳戶。 請務必針對 sa 登入使用一個增強式密碼。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-change-security-authentication-mode"></a>變更安全性驗證模式  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的物件總管中，以滑鼠右鍵按一下伺服器，然後按一下 [屬性]。  
  
2.  在 **[安全性]** 頁面上的 **[伺服器驗證]** 中，選取新的伺服器驗證模式，然後按一下 **[確定]** 。  
  
3.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 對話方塊中，按一下 **[確定]** 以確認需要重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
4.  在物件總管中，以滑鼠右鍵按一下伺服器，然後按一下 [重新啟動]。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 正在執行，也必須將它重新啟動。  
  
#### <a name="to-enable-the-sa-login"></a>若要啟用 sa 登入  
  
1.  在物件總管中，依序展開 [**安全性**] 和 [登入]，以滑鼠右鍵按一下，然後按一下 [內容] `sa` 。 **Properties**  
  
2.  在 **[一般]** 頁面上，您可能需要為登入建立並確認密碼。  
  
3.  在 **[狀態]** 頁面的 **[登入]** 區段中按一下 **[已啟用]** ，然後按一下 **[確定]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要啟用 sa 登入**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 下列範例會啟用 sa 登入並設定新密碼。  
  
    ```  
    ALTER LOGIN sa ENABLE ;  
    GO  
    ALTER LOGIN sa WITH PASSWORD = '<enterStrongPasswordHere>' ;  
    GO  
  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [增強式密碼](../../relational-databases/security/strong-passwords.md)   
 [SQL Server 安裝的安全性考慮](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)   
 [當系統管理員遭到鎖定時連接到 SQL Server](connect-to-sql-server-when-system-administrators-are-locked-out.md)  
  
  
