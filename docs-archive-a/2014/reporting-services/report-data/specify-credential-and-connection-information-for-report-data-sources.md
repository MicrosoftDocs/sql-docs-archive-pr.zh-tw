---
title: 指定報表資料來源的認證及連線資訊 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- no credentials option [Reporting Services]
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- Windows authentication [Reporting Services]
- data sources [Reporting Services], security
- connection strings [Reporting Services]
- unattended report processing [Reporting Services]
- reports [Reporting Services], security
- remote data sources [Reporting Services]
- credentials [Reporting Services]
- authentication [Reporting Services]
- external data sources [Reporting Services]
- prompted credentials [Reporting Services]
- multiple connections
- stored credentials [Reporting Services]
- security [Reporting Services], data sources
- Windows integrated security [Reporting Services]
ms.assetid: fee1a663-a313-424a-aed2-5082bfd114b3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2d1e804282459972b21303cf795a9c3a88ea93d5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598235"
---
# <a name="specify-credential-and-connection-information-for-report-data-sources"></a>指定報表資料來源的認證及連接資訊
  報表伺服器使用認證以連接到外部資料來源，其中提供內容給報表或提供收件者資訊給資料驅動訂閱。 您可以指定認證來使用 Windows 驗證、資料庫驗證、無驗證或自訂驗證。 透過網路傳送連接要求時，報表伺服器會模擬使用者帳戶或自動執行帳戶。 如需安全性內容 (連接要求會在其底下進行) 的詳細資訊，請參閱本主題之後的 [資料來源組態和網路連接](#DataSourceConfigurationConnections) 。  
  
> [!NOTE]  
>  認證也用於驗證存取報表伺服器的使用者。 有關報表伺服器驗證使用者的資訊，會在另一個主題中提供。  
  
 當您建立報表時，會定義與外部資料來源之間的連接。 當報表發行之後，可以個別管理此連接。 您可以指定靜態連接字串或運算式，好讓使用者可以從動態清單中選取資料來源。 如需如何指定資料來源類型和連接字串的詳細資訊，請參閱[Reporting Services 中的資料連線、資料來源和連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
## <a name="using-remote-data-sources"></a>使用遠端資料來源  
 如果報表會從遠端資料庫伺服器擷取資料，請確認下列項目：  
  
-   提供給資料庫伺服器的認證有效。 如果您要使用 Windows 使用者認證，請確定該使用者擁有伺服器和資料庫的權限。  
  
-   資料庫伺服器所使用的通訊埠是開啟的。 如果您要存取外部電腦上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料庫，或者報表伺服器資料庫位於外部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上，您就必須開啟外部電腦上的通訊埠 1433 和 1434。 開啟這些通訊埠之後，請務必重新啟動伺服器。 如需詳細資訊，請參閱 [設定用於 Database Engine 存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)。  
  
-   遠端連接必須已啟用。 如果您要存取外部電腦上的 SQL Server 關聯式資料庫，可以使用 SQL Server 組態管理員工具來確認透過 TCP 進行遠端連接的功能是否已啟用。  
  
## <a name="ways-to-specify-credentials-for-connecting-to-remote-data-sources"></a>指定認證以便連接至遠端資料來源的方式  
 提供內容給報表的資料來源，通常是在遠端伺服器上主控。 若要擷取報表的資料，報表伺服器必須利用您事先提供或在執行階段取得的一組認證來連接到伺服器。 設定資料來源時，您可以採用下列方式來指定認證：  
  
-   提示使用者提供認證。  
  
-   儲存認證。  
  
-   使用 Windows 整合式安全性。  
  
-   不使用認證。  
  
 網路環境決定您可以支援的連接類型。 例如，如果 Kerberos 第 5 版通訊協定已啟用，您可以使用 Windows 驗證中提供的委派和模擬功能來支援跨多部伺服器的連接。 如果您的網路不支援這些安全性功能，您就必須解決連接條件約束。 如果委派和模擬尚未啟用，您可以在 Windows 認證過期之前，透過單一電腦連接傳遞這些認證。 用戶端電腦與報表伺服器電腦的使用者連接會當成第一個連接。 如果使用者開啟從遠端伺服器擷取資料的報表，該登入會當成第二個連接，而如果您在未啟用委派時指定要使用整合式安全性的連接，則連接會失敗。  
  
 如果需要多個連接來完成從用戶端電腦至外部報表資料來源的往返，請從下列策略中選擇，讓連接能夠成功。  
  
-   在網域中啟用模擬和委派功能，使認證能夠無限制地委派給其他電腦。  
  
-   使用預存認證或提示認證，即可查詢報表資料的外部資料來源。 認證可以是 Windows 網域帳戶或資料庫登入。  
  
### <a name="prompted-credentials"></a>提示認證  
 當您將報表資料來源連接設定為使用提示認證時，存取此報表的每位使用者都必須輸入使用者名稱和密碼，才能擷取資料。 此方法建議用於包含機密資料的報表。 提示認證只能用於視需要執行的報表上。 提示認證可以是 Windows 帳戶或資料庫登入。 若要使用 Windows 驗證，必須選取 [連線到資料來源時作為 Windows 認證]****。 否則，報表伺服器會將認證傳遞至資料庫伺服器以供使用者驗證。 如果資料庫伺服器無法驗證您所提供的認證，連接將會失敗。  
  
### <a name="windows-integrated-security"></a>Windows 整合式安全性  
 當您使用 [Windows 整合式安全性]**** 選項時，報表伺服器會將存取報表之使用者的安全性權杖，傳遞至主控外部資料來源的伺服器。 在此情況下，不會提示使用者輸入使用者名稱或密碼。 如果模擬和委派功能已啟用，建議您使用此方法。 如果這些功能未啟用，只有當所有您想要存取的伺服器都位於相同電腦上時，才應該使用此方法。  
  
### <a name="stored-credentials"></a>預存認證  
 您可以儲存用於存取外部資料來源的認證。 認證是以可回復加密的方式，儲存在報表伺服器資料庫中。 您可以為用於報表中的每一個資料來源，指定一組預存認證。 您提供的認證會為執行報表的每一個使用者擷取相同的資料。  
  
 建議存取遠端資料庫伺服器時，將預存認證當成策略的一部分。 如果您想要支援訂閱、產生排程報表記錄，或重新整理報表快照集，就需要預存認證。 以背景處理序執行報表時，報表伺服器為執行報表的代理程式。 因為沒有使用者內容，所以報表伺服器必須從報表伺服器資料庫取得認證資訊，以便連接到資料來源。  
  
 您指定的使用者名稱和密碼可以是 Windows 認證或資料庫登入。 如果您指定 Windows 認證，則報表伺服器會將認證傳遞至 Windows 以供後續驗證。 否則，它會將認證傳遞至資料庫伺服器以供驗證。  
  
#### <a name="how-to-grant-allow-log-on-locally-permissions-to-domain-user-accounts"></a>如何將「允許本機登入」權限授與網域使用者帳戶  
 如果您使用預存認證來連接至外部資料來源，Windows 網域使用者帳戶就必須擁有本機登入的權限。 這個權限可讓報表伺服器模擬報表伺服器的使用者，而且以該模擬使用者的身分將要求傳送至外部資料來源。  
  
 若要授與此權限，請執行下列動作：  
  
1.  在報表伺服器電腦的 [系統管理工具]**** 中，開啟 [本機安全性原則]****。  
  
2.  在 [安全性設定]**** 底下，展開 [本機原則]****，然後按一下 [使用者權限指派]****。  
  
3.  在詳細資料窗格中，以滑鼠右鍵按一下 [允許本機登入]****，然後以滑鼠右鍵按一下 [內容]****。  
  
4.  按一下 [新增使用者或群組]****。  
  
5.  按一下 [位置]****，指定要搜尋的網域或其他位置，然後按一下 [確定]****。  
  
6.  輸入允許互動式登入的 Windows 帳戶，然後按一下 [確定]****。  
  
7.  在 [允許本機登入內容]**** 對話方塊中，按一下 [確定]****。  
  
8.  確定您選取的帳戶沒有拒絕權限：  
  
    1.  以滑鼠右鍵按一下 [拒絕本機登入]****，然後以滑鼠右鍵按一下 [內容]****。  
  
    2.  如果帳戶列於其中，請選取帳戶，然後按一下 [移除]****。  
  
#### <a name="using-impersonation-with-stored-credentials"></a>以預存認證使用模擬  
 您也可以使用認證來模擬其他使用者的身分。 針對 SQL Server 資料庫，使用模擬選項會設定 [SETUSER](/sql/t-sql/statements/setuser-transact-sql) 函數。  
  
> [!IMPORTANT]  
>  針對支援訂閱的報表，或者使用排程來產生報表記錄或重新整理報表執行快照集的報表，都不要使用模擬。  
  
### <a name="no-credentials"></a>無認證  
 您可以設定資料來源連接，以使用無認證。 Microsoft 建議您永遠利用認證來存取資料來源；不建議使用無認證。 不過，在下列情況下，您可以選擇使用無認證來執行報表：  
  
-   遠端資料來源不需要認證。  
  
-   認證會在連接字串中傳遞 (僅建議用於保護連接的安全)。  
  
-   報表是使用父報表之認證的子報表。  
  
 在這些狀況下，報表伺服器會使用您必須事先定義的自動執行帳戶連接到遠端資料來源。 報表伺服器未利用它的服務認證連接到遠端伺服器，因此，您必須指定帳戶，讓報表伺服器能夠用於進行連接。 如需建立此帳戶的詳細資訊，請參閱[設定自動執行帳戶 &#40;SSRS 設定管理員&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
##  <a name="data-source-configuration-and-network-connections"></a><a name="DataSourceConfigurationConnections"></a> 資料來源組態和網路連接  
 下表顯示如何為認證類型和資料處理延伸模組的特定組合進行連接。 如果您要使用自訂資料處理延伸模組，請參閱 [為自訂資料處理延伸模組指定連接](specify-connections-for-custom-data-processing-extensions.md)。  
  
|**型別**|**網路連接的內容**|**資料來源類型**<br /><br /> **(SQL Server、Oracle、ODBC、OLE DB、Analysis Services、XML、SAP NetWeaver BI、Hyperion Essbase)**|  
|--------------|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|  
|整合式安全性|模擬目前的使用者|針對所有資料來源類型，利用目前的使用者帳戶來連接。|  
|Windows 認證|模擬指定的使用者|若為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Oracle、ODBC 和 OLE DB：使用模擬使用者帳戶進行連接。|  
|資料庫認證|模擬自動執行帳戶或服務帳戶。<br /><br /> (利用服務識別傳送連接要求時，Reporting Services 會移除管理員權限)。|若為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Oracle、ODBC 和 OLE DB：<br /><br /> 將使用者名稱和密碼附加至連接字串。<br /><br /> 針對 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]：<br /><br /> 使用 TCP/IP 通訊協定時，連接會成功，否則會失敗。<br /><br /> 如果是 XML：<br /><br /> 使用資料庫認證時，會使報表伺服器上的連接失敗。|  
|None|模擬自動執行帳戶。|若為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Oracle、ODBC 和 OLE DB：<br /><br /> 使用連接字串中定義的認證。 如果未定義自動執行帳戶，報表伺服器上的連接會失敗。<br /><br /> 針對 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]：<br /><br /> 指定無認證或定義自動執行帳戶時，永遠會使連接失敗。<br /><br /> 如果是 XML：<br /><br /> 如果已定義自動執行帳戶，則以匿名使用者連接；否則會使連接失敗。|  
  
## <a name="setting-credentials-programmatically"></a>以設計程式的方式設定認證  
 您可以在您的程式碼中設定認證，來控制報表和報表伺服器的存取。 如需詳細資訊，請參閱 [資料來源和連接方法](../report-server-web-service/methods/data-sources-and-connection-methods.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services &#40;SSRS 支援的資料來源&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Reporting Services 中的資料連線、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [管理報表資料來源](../../integration-services/connection-manager/data-sources.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)   
 [建立、刪除或修改共用資料來源 &#40;報表管理員&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [設定報表的資料來源屬性 &#40;報表管理員&#41;](configure-data-source-properties-for-a-report-report-manager.md)  
  
  
