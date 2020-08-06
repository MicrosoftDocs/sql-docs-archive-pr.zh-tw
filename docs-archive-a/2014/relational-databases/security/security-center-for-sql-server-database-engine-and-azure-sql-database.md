---
title: SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心 | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- Security [SQL Server]
helpviewer_keywords:
- SQL Server, security
- security [SQL Server]
- database security [SQL Server]
- databases [SQL Server], security
ms.assetid: dfb39d16-722a-4734-94bb-98e61e014ee7
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3eeea022cff74d2ca8ddb636d9f83e4d369529bc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688730"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心
  本頁提供的連結可協助您在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]及 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]中尋找有關於安全性及保護的資訊。  
  
> [!NOTE]  
>  [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] 的功能將持續改進。 如需了解 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]的最新資訊，請參閱本主題的最新版本 。  
  
|驗證：您的身分|授權：您可以執行的作業|加密：儲存機密資料|連線安全性：限制及保護|稽核：錄製存取權|  
|----------------------------------|-------------------------------------|-------------------------------------|---------------------------------------------------|--------------------------------|  
|**由誰驗證？**<br /><br /> [![資訊安全中心對應 Windows 驗證](../../database-engine/media/security-center-map-windows-authenticaion.png "資訊安全中心對應 Windows 驗證")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> <br /><br /> [![資訊安全中心對應 SQL Server 驗證](../../database-engine/media/security-center-map-sql-authenticaion.png "資訊安全中心對應 SQL Server 驗證")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> **驗證位置？**<br /><br /> [![資訊安全中心對應登入與使用者](../../database-engine/media/security-center-map-logins-users.png "資訊安全中心對應登入與使用者")](https://msdn.microsoft.com/library/aa337562.aspx)<br /><br /> <br /><br /> [![資訊安全中心自主資料庫使用者](../../database-engine/media/security-center-map-contained-users.png "資訊安全中心自主資料庫使用者")](https://msdn.microsoft.com/library/ff929188.aspx)<br /><br /> **使用其他身分識別**<br /><br /> [![資訊安全中心對應認證](../../database-engine/media/security-center-map-credentials.png "資訊安全中心對應認證")](https://msdn.microsoft.com/library/ms161950.aspx)<br /><br /> [![資訊安全中心對應 Execute As Login](../../database-engine/media/security-center-map-exec-as-login.png "資訊安全中心對應 Execute As Login")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> [![資訊安全中心對應 Execute As User](../../database-engine/media/security-center-map-exec-as-user.png "資訊安全中心對應 Execute As User")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")|**授與、撤銷和拒絕權限**<br /><br /> [![資訊安全中心的對應安全性實體類別](../../database-engine/media/security-center-map-securable-classes.png "資訊安全中心的對應安全性實體類別")](https://msdn.microsoft.com/library/ms190401.aspx)<br /><br /> [![資訊安全中心對應伺服器權限](../../database-engine/media/security-center-map-srv-perms.png "資訊安全中心對應伺服器權限")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> [![資訊安全中心對應資料庫權限](../../database-engine/media/security-center-map-db-perms.png "資訊安全中心對應資料庫權限")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> **安全性角色**<br /><br /> [![資訊安全中心對應伺服器角色](../../database-engine/media/security-center-map-srv-roles.png "資訊安全中心對應伺服器角色")](https://msdn.microsoft.com/library/ms188659.aspx)<br /><br /> [![資訊安全中心對應資料庫角色](../../database-engine/media/security-center-map-db-roles.png "資訊安全中心對應資料庫角色")](https://msdn.microsoft.com/library/ms189121.aspx)<br /><br /> `Restricting Data Access to Selected Data Elements`<br /><br /> [![資訊安全中心對應檢視表與程序](../../database-engine/media/security-center-map-view-procs.png "資訊安全中心對應檢視表與程序")](https://msdn.microsoft.com/library/ms175503.aspx)<br /><br /> [![資訊安全中心的對應資料列層級安全性](../../database-engine/media/security-center-map-row-level-sec.png "資訊安全中心的對應資料列層級安全性")](https://msdn.microsoft.com/library/dn765131.aspx)<br /><br /> [![資訊安全中心對應動態資料遮罩](../../database-engine/media/security-center-map-data-masking.png "資訊安全中心對應動態資料遮罩")](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)<br /><br /> [![資訊安全中心對應簽署的物件](../../database-engine/media/security-center-map-signed-objects.png "資訊安全中心對應簽署的物件")](https://msdn.microsoft.com/library/ms181700.aspx)<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")|**加密檔案**<br /><br /> [![資訊安全中心對應 BitLocker](../../database-engine/media/security-center-map-bitlocker.png "資訊安全中心對應 BitLocker")](https://support.microsoft.com/kb/2855131)<br /><br /> [![資訊安全中心對應 NTFS 加密](../../database-engine/media/security-center-map-ntfs-encryp.png "資訊安全中心對應 NTFS 加密")](https://msdn.microsoft.com/library/dd163562.aspx)<br /><br /> [![資訊安全中心對應 TDE](../../database-engine/media/security-center-map-tde.png "資訊安全中心對應 TDE")](https://msdn.microsoft.com/library/bb934049.aspx)<br /><br /> [![資訊安全中心對應備份加密](../../database-engine/media/security-center-map-backup-encryp.png "資訊安全中心對應備份加密")](https://msdn.microsoft.com/library/dn449489.aspx)<br /><br /> **加密的來源**<br /><br /> [![資訊安全中心對應 EKM](../../database-engine/media/security-center-map-ekm.png "資訊安全中心對應 EKM")](https://msdn.microsoft.com/library/bb895340.aspx)<br /><br /> [![資訊安全中心對應 Azure 金鑰保存庫](../../database-engine/media/security-center-map-key-vault.png "資訊安全中心對應 Azure 金鑰保存庫")](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)<br /><br /> **資料行，資料 & 金鑰加密**<br /><br /> [![依憑證資訊安全中心對應加密](../../database-engine/media/security-center-map-cert.png "依憑證資訊安全中心對應加密")](https://msdn.microsoft.com/library/ms188061.aspx)<br /><br /> [![資訊安全中心對應使用非對稱金鑰加密](../../database-engine/media/security-center-map-sym-key.png "資訊安全中心對應使用非對稱金鑰加密")](https://msdn.microsoft.com/library/ms174361.aspx)<br /><br /> [![非對稱金鑰將資訊安全中心對應加密](../../database-engine/media/security-center-map-asym-key.png "非對稱金鑰將資訊安全中心對應加密")](https://msdn.microsoft.com/library/ms186950.aspx)<br /><br /> [![資訊安全中心對應使用複雜密碼加密](../../database-engine/media/security-center-map-passphrase.png "資訊安全中心對應使用複雜密碼加密")](https://msdn.microsoft.com/library/ms190357.aspx)|**防火牆保護**<br /><br /> [![資訊安全中心對應 Windows 防火牆](../../database-engine/media/security-center-map-windows-firewall.png "資訊安全中心對應 Windows 防火牆")](https://msdn.microsoft.com/library/ms175043.aspx)<br /><br /> [![資訊安全中心對應服務防火牆](../../database-engine/media/security-center-map-service-firewall.png "資訊安全中心對應服務防火牆")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> [![資訊安全中心對應資料庫防火牆](../../database-engine/media/security-center-map-db-firewall.png "資訊安全中心對應資料庫防火牆")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> **在傳輸過程中的資料加密**<br /><br /> [![資訊安全中心對應強制 SSL](../../database-engine/media/security-center-map-forced-ssl.png "資訊安全中心對應強制 SSL")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> [![資訊安全中心對應非必要的 SSL](../../database-engine/media/security-center-map-opt-ssl.png "資訊安全中心對應非必要的 SSL")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")|**自動化稽核**<br /><br /> [![資訊安全中心對應 SQL Server Audit](../../database-engine/media/security-center-map-sql-audit.png "資訊安全中心對應 SQL Server Audit")](https://msdn.microsoft.com/library/cc280386.aspx)<br /><br /> [![資訊安全中心對應 SQL Database Audit](../../database-engine/media/security-center-map-sqldb-audit.png "資訊安全中心對應 SQL Database Audit")](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)<br /><br /> **自訂稽核**<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> [![資訊安全中心對應觸發程序](../../database-engine/media/security-center-map-triggers.png "資訊安全中心對應觸發程序")](https://msdn.microsoft.com/library/ms175941.aspx)<br /><br /> **遵循**<br /><br /> [![SecCtrCompliance](../../database-engine/media/secctrcompliance.png "SecCtrCompliance")](https://azure.microsoft.com/support/trust-center/services/)<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> ![預留位置](../../database-engine/media/security-center-map-blankplaceholder.png "預留位置")<br /><br /> ![資訊安全中心圖例](../../database-engine/media/security-center-map-legend.png "資訊安全中心圖例")|  
  
## <a name="links-to-specific-related-topics"></a>連結到特定的相關主題  
 ![小型檔案資料夾圖示](../../integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")**驗證：您是誰？**  
 **誰驗證？ (Windows 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) **  
  
-   [選擇驗證模式](choose-an-authentication-mode.md)  
  
 **在 master 資料庫上驗證** (登入和資料庫使用者)   
  
-   [建立 SQL Server 登入](authentication-access/create-a-login.md)  
  
-   [管理資料庫和 Azure SQL Database 中的登入](https://msdn.microsoft.com/library/ee336235.aspx)  
  
-   [建立資料庫使用者](authentication-access/create-a-database-user.md)  
  
 **在使用者資料庫進行驗證**  
  
-   [自主資料庫使用者 - 讓資料庫具有可攜性](contained-database-users-making-your-database-portable.md)  
  
 **使用其他身分識別**  
  
-   [認證 &#40;Database Engine&#41;](authentication-access/credentials-database-engine.md)  
  
-   [以另一個登入的方式執行](/sql/t-sql/statements/execute-as-transact-sql)  
  
-   [以另一個資料庫使用者的身分執行](/sql/t-sql/statements/execute-as-transact-sql)  
  
 ![小型檔案資料夾圖示](../../integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")**加密：儲存秘密資料**  
 **加密檔案**  
  
-   [BitLocker (磁碟機層級)](https://support.microsoft.com/kb/2855131)  
  
-   [NTFS 加密 (資料夾層級)](https://msdn.microsoft.com/library/dd163562.aspx)  
  
-   [透明資料加密 (檔案層級)](encryption/transparent-data-encryption.md)  
  
-   [備份加密 (檔案層級)](../backup-restore/backup-encryption.md)  
  
 **加密的來源**  
  
-   [可延伸金鑰管理模組](encryption/extensible-key-management-ekm.md)  
  
-   [儲存在 Azure 金鑰保存庫的金鑰](encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 **資料行、 資料和金鑰加密**  
  
-   [加密憑證](/sql/t-sql/functions/encryptbycert-transact-sql)  
  
-   [用非對稱金鑰來加密](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
  
-   [用對稱金鑰來加密](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [用複雜密碼來加密](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
  
 ![小型檔案資料夾圖示](../../integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")**授權：您可以執行什麼動作？**  
 **授與、撤銷和拒絕權限**  
  
-   [權限階層 &#40;Database Engine&#41;](permissions-hierarchy-database-engine.md)  
  
-   [權限](permissions-database-engine.md)  
  
-   [安全性實體](securables.md)  
  
 **安全性角色**  
  
-   [伺服器層級角色](authentication-access/server-level-roles.md)  
  
-   [資料庫層級角色](authentication-access/database-level-roles.md)  
  
 `Restricting Data Access to Selected Data Elements`  
  
-   限制資料存取使用 [檢視](../views/views.md) 和 [程序](../stored-procedures/stored-procedures-database-engine.md)  
  
-   [資料列層級安全性](https://msdn.microsoft.com/library/azure/dn765131.aspx)  
  
-   [動態資料遮罩](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)  
  
-   [簽署物件](/sql/t-sql/statements/add-signature-transact-sql)  
  
 ![小型檔案資料夾圖示](../../integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")**連接安全性：限制及保護**  
 **防火牆保護**  
  
-   [設定用於 Database Engine 存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
-   [Azure SQL Database 防火牆設定](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
-   [Azure 服務的防火牆設定](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
 **在傳輸過程中的資料加密**  
  
-   [資料庫引擎的安全通訊端層](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
  
-   [SQL Database 的安全通訊端層](https://msdn.microsoft.com/library/azure/ff394108.aspx)  
  
 ![小型檔案資料夾圖示](../../integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")**審核：錄製存取**  
 **自動化稽核**  
  
-   [SQL Server Audit &#40;Database Engine&#41;](auditing/sql-server-audit-database-engine.md)  
  
-   [SQL 資料庫稽核](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)  
  
 **實作自訂的稽核**  
  
-   建立 [DDL Triggers](../triggers/ddl-triggers.md) 和 [DML Triggers](../triggers/dml-triggers.md)  
  
 ![小型檔案資料夾圖示](../../integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")**合規性**  
 **SQL Server**  
  
-   [Common Criteria](https://go.microsoft.com/fwlink/?LinkId=616319)  
  
 **SQL Database**  
  
-   [Microsoft Azure Trust Center:Compliance by Feature](https://azure.microsoft.com/support/trust-center/services/) (Microsoft Azure 信任中心：功能符合規範的狀況)  
  
## <a name="see-also"></a>另請參閱  
 [保護 SQL Server 的安全](securing-sql-server.md)   
 [主體 &#40;Database Engine&#41;](authentication-access/principals-database-engine.md)   
 [SQL Server 憑證與非對稱金鑰](sql-server-certificates-and-asymmetric-keys.md)   
 [SQL Server 加密](encryption/sql-server-encryption.md)   
 [介面區組態](surface-area-configuration.md)   
 [增強式密碼](strong-passwords.md)   
 [TRUSTWORTHY 資料庫屬性](trustworthy-database-property.md)   
 [Database Engine 功能及工作](../../database-engine/database-engine-features-and-tasks.md)  
  
  
