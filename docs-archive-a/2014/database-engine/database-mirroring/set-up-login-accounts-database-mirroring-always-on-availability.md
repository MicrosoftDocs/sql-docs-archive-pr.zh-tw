---
title: 設定資料庫鏡像的登入帳戶，或 AlwaysOn 可用性群組 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- logins [SQL Server], database mirroring
ms.assetid: e9f5287b-1325-4cda-88a6-19eaaa52a652
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d149016dabd0239bd76eadc8655b6752afd916d9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87701767"
---
# <a name="set-up-login-accounts-for-database-mirroring-or-alwayson-availability-groups-sql-server"></a>設定資料庫鏡像或 AlwaysOn 可用性群組的登入帳戶 (SQL Server)
  若要讓兩個伺服器執行個體連接到對方的 [資料庫鏡像端點](the-database-mirroring-endpoint-sql-server.md) ，這兩個執行個體的登入帳戶都必須要有對方的存取權。 而且，這兩個登入帳戶都必須要有連接權限來連接到對方的資料庫鏡像端點。  
  
 此需求的影響視伺服器執行個體是否以相同網域使用者帳戶執行而定：  
  
-   如果伺服器執行個體是以相同的網域使用者帳戶執行，兩個 **master** 資料庫中都會自動存在正確的使用者登入。 這樣可簡化資料庫鏡像和 AlwaysOn 可用性群組的安全性組態。  
  
-   如果伺服器執行個體是以不同使用者帳戶執行，則裝載主體伺服器或主要複本的伺服器執行個體上的使用者登入必須以手動方式重新產生在裝載鏡像伺服器的伺服器執行個體或裝載次要複本的每個伺服器執行個體上。 如需詳細資訊，請參閱本主題稍後的 [＜為不同的帳戶建立登入＞](#CreateLogin) 和 [＜授與連接權限＞](#GrantConnect)。  
  
    > [!IMPORTANT]  
    >  若要建立更安全的環境，請考慮針對每個伺服器執行個體使用不同的網域帳戶。  
  
##  <a name="create-a-login-for-a-different-account"></a><a name="CreateLogin"></a>為不同的帳戶建立登入  
 如果兩個伺服器執行個體是以不同的帳戶執行，系統管理員必須使用 CREATE LOGIN [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，為每個伺服器執行個體之遠端執行個體的啟動服務帳戶建立登入。 如需詳細資訊，請參閱 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)。  
  
> [!IMPORTANT]  
>  如果您是在非網域帳戶之下執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用憑證。 如需詳細資訊，請參閱[使用資料庫鏡像端點憑證 &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)。  
  
 例如，若要讓伺服器執行個體 sqlA (在 loginA 之下執行) 連接到伺服器執行個體 sqlB (在 loginB 之下執行)，則 loginA 必須在 sqlB 中，而 loginB 必須在 sqlA 中。 此外，若資料庫鏡像工作階段中包含見證伺服器執行個體 (sqlC)，而且其中的三個伺服器執行個體都是在不同的網域帳戶下執行，則必須建立下列登入：  
  
|在執行個體|建立登入及授與連接權限給...|  
|--------------------|--------------------------------------------------------------|  
|sqlA|sqlB 和 sqlC|  
|sqlB|sqlA 和 sqlC|  
|sqlC|sqlA 與 sqlB|  
  
> [!NOTE]  
>  您也可以利用電腦帳戶代替網域使用者，與網路服務帳戶連接。 如果使用電腦帳戶，則必須將該帳戶新增為其他個伺服器執行個體的使用者。  
  
##  <a name="grant-connect-permission"></a><a name="GrantConnect"></a>Grant Connect 許可權  
 一旦在伺服器執行個體上建立登入，就必須授權該登入來連接伺服器執行個體的資料庫鏡像端點。 系統管理員可使用 GRANT [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式來授與連接權限。 如需詳細資訊，請參閱 [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)的相關資訊。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [建立登入](../../relational-databases/security/authentication-access/create-a-login.md)  
  
-   [允許使用 Windows 驗證 &#40;SQL Server&#41;，對資料庫鏡像端點進行網路存取](../database-mirroring-allow-network-access-windows-authentication.md)。  
  
-   [使用資料庫鏡像端點憑證 &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料庫鏡像端點 &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [為資料庫鏡像組態進行疑難排解 &#40;SQL Server&#41; &#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)   
 [針對 AlwaysOn 可用性群組 Configuration &#40;SQL Server&#41;進行疑難排解](../availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
