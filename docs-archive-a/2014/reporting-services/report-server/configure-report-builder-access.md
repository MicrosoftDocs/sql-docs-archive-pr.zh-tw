---
title: 設定報表產生器的存取 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, Report Builder
- Report Builder 1.0, configuring access
- configuring servers [Reporting Services]
ms.assetid: a79003d0-c905-4d4c-9560-93a7cc1e1dd4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ac18493044004a89b31c1cf19f169312ef648a3b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597594"
---
# <a name="configure-report-builder-access"></a>設定報表產生器的存取
  報表產生器是一個隨選報表工具，此工具會與設定原生模式或 SharePoint 整合模式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器一起安裝。  
  
 報表產生器的存取權會因下列因素而異：  
  
-   決定是否可以在報表伺服器上使用報表產生器的伺服器屬性。  
  
-   可將報表產生器提供給個別使用者或群組使用的角色指派或權限。  
  
-   驗證設定，可判斷使用者認證是否可以傳遞給報表伺服器，或是在應用程式檔案上設定匿名存取。  
  
 若要使用報表產生器，您必須具有要使用的已發行報表模型。  
  
## <a name="prerequisites"></a>先決條件  
 並非每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中都可使用報表產生器。 如需版本支援的功能清單 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱[SQL Server 2014 版本支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 用戶端電腦必須 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 安裝2.0。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 提供了執行 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 應用程式的基礎結構。  
  
 您必須使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 6.0 或更新版本。  
  
 報表產生器一定會在完全信任模式中執行；您不能設定它在部分信任模式中執行。 在舊版中，報表產生器可以在部分信任模式中執行，但是在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中則不支援這個選項。  
  
## <a name="enabling-and-disabling-report-builder"></a>啟用及停用報表產生器  
 預設會啟用報表產生器。 報表伺服器管理員可以選擇將報表伺服器系統屬性 `EnableReportDesignClientDownload` 設定為 `false`，以停用報表產生器功能， 設定這個屬性將會停用該報表伺服器的報表產生器下載功能。  
  
 若要設定報表伺服器系統屬性，您可以使用 Management Studio 或指令碼：  
  
-   若要使用 Management Studio，請連接到報表伺服器，並使用 [進階伺服器屬性] 頁面將 `EnableReportDesignClientDownload` 設定為 `false`。 如需如何開啟此頁面的詳細資訊，請參閱[設定報表伺服器屬性 &#40;Management Studio&#41;](../tools/set-report-server-properties-management-studio.md)。  
  
-   若要檢視設定報表伺服器屬性的範例指令碼，請參閱 [編寫部署和管理工作的指令碼](../tools/script-deployment-and-administrative-tasks.md)。  
  
## <a name="role-assignments-granting-report-builder-access-on-a-native-mode-report-server"></a>原生模式報表伺服器上授與報表產生器存取的角色指派  
 在原生模式報表伺服器上，建立使用者角色指派來包含使用報表產生器的工作。 您必須是內容管理員和系統管理員，才能建立或修改項目和網站層級的角色定義與角色指派。  
  
 下列指示假設您使用預先定義的角色。 如果您已修改角色定義或是從 SQL Server 2000 升級，請檢查這些角色，以確認它們有包含所需的工作。 如需建立角色指派的詳細資訊，請參閱[將報表伺服器的存取權授與使用者 &#40;報表管理員&#41;](../security/grant-user-access-to-a-report-server.md)。  
  
 在建立角色指派之後，使用者將有權執行以下作業：  
  
-   指派給「系統使用者」和「瀏覽者」角色的使用者可以檢視報表伺服器上的已發行報表產生器報表，而不需啟動報表產生器。  
  
-   指派給「系統使用者」和「報表產生器」角色的使用者可以產生模型、啟動報表產生器及建立報表，並將報表儲存到報表伺服器。  
  
-   指派給「系統使用者」和「發行者」角色的使用者可以從模型設計師將模型發行到報表伺服器。 模型會在報表產生器中當做資料來源使用。  
  
-   指派給「系統管理員」和「內容管理員」角色的使用者具有建立、檢視及管理報表產生器報表的完整權限。  
  
#### <a name="to-verify-required-tasks-are-in-the-role-definitions"></a>確認必要工作位於角色定義中  
  
1.  啟動 Management Studio，然後連接到報表伺服器。  
  
2.  開啟 [安全性]**** 資料夾。  
  
3.  開啟 [系統角色]**** 資料夾。  
  
4.  以滑鼠右鍵按一下 [系統管理員]****，然後選取 [屬性]****。  
  
5.  選取 [執行報表定義]****，然後按一下 [確定]****。  
  
6.  以滑鼠右鍵按一下 [系統使用者]****，然後選取 [屬性]****。  
  
7.  選取 [執行報表定義]****，然後按一下 [確定]****。  
  
8.  開啟 [角色]**** 資料夾。  
  
9. 以滑鼠右鍵按一下 [瀏覽器]****，然後選取 [屬性]****。  
  
10. 選取 [檢視模型]****，然後按一下 [確定]****。  
  
11. 以滑鼠右鍵按一下 [內容管理員]****，然後選取 [屬性]****。  
  
12. 選取 [檢視模型]****、[管理模型]****、[取用報表]****，然後按一下 [確定]****。  
  
13. 以滑鼠右鍵按一下 [發行者]****，然後選取 [屬性]****。  
  
14. 選取 [管理模型]****，然後按一下 [確定]****。  
  
15. 如果報表產生器角色不存在，請建立該角色：  
  
    1.  開啟 [安全性]**** 資料夾。  
  
    2.  以滑鼠右鍵按一下 [角色]****，並選取 [新增角色]****。  
  
    3.  在 [名稱] 中，輸入 **報表產生器**。  
  
    4.  在 [描述] 中，輸入角色的描述，好讓報表管理員中的使用者知道這個角色的目的。  
  
    5.  新增下列工作：[取用報表]****、[檢視報表]****、[檢視模型]****、[檢視資源]****、[檢視資料夾]**** 及 [管理個別訂閱]****。  
  
    6.  按一下 **[確定]** 以儲存角色。  
  
#### <a name="to-create-role-assignments-that-grant-access-to-report-builder"></a>建立角色指派來授與報表產生器的存取權  
  
1.  啟動報表管理員。  
  
2.  按一下 **[站台設定]** 。  
  
3.  按一下 **[安全性]** 。  
  
4.  如果您想要設定報表產生器存取的使用者或群組已經有角色指派，請按一下 [編輯]  。  
  
     否則請按一下 [新增角色指派]  。 在 [群組或使用者] 中，以下列格式輸入 Windows 網域使用者或群組帳戶： \<domain> \\<帳戶] \> 。 如果您要使用表單驗證或自訂安全性，請使用適用於部署的正確格式來指定使用者或群組帳戶。  
  
5.  選取 [系統使用者]  ，然後按一下 [確定]  。  
  
6.  按一下 [首頁]  。  
  
7.  按一下 [資料夾設定]  索引標籤。  
  
8.  按一下 [安全性]  索引標籤。  
  
9. 如果您想要設定報表產生器存取的使用者或群組已經有角色指派，請按一下 [編輯]  。  
  
     否則請按一下 [新增角色指派]  。 在 [群組或使用者] 中，以下列格式輸入 Windows 網域使用者或群組帳戶： \<domain> \\<帳戶] \> 。 如果您要使用表單驗證或自訂安全性，請使用適用於部署的正確格式來指定使用者或群組帳戶。  
  
10. 選取 [報表產生器]  ，然後按一下 [套用]  。  
  
11. 重複上述步驟，以便建立或修改其他使用者或群組的角色指派。  
  
## <a name="permissions-granting-report-builder-access-on-a-sharepoint-integrated-mode-report-server"></a>授與 SharePoint 整合模式報表伺服器之報表產生器存取的權限  
 在 SharePoint 整合模式報表伺服器上，報表產生器的存取會授與給具有「參與」或「完全控制」權限等級的 SharePoint 使用者。  
  
 如果您要使用自訂權限等級，您必須在此權限等級中包括「加入項目」和「編輯項目」。 如需透過內建權限層級存取報表產生器的詳細資訊，請參閱 [在 Windows SharePoint Services 中使用報表伺服器項目的內建安全性](../security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)。 如需自訂權限層級的權限需求詳細資訊，請參閱 [在 SharePoint Web 應用程式中設定報表伺服器作業的權限](../security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)。  
  
## <a name="authentication-considerations-and-credential-reuse"></a>驗證考量與認證重複使用  
 報表產生器會使用 ClickOnce 技術，將它的應用程式檔案下載及安裝到用戶端電腦上。 ClickOnce 技術要用於單向應用程式部署，這個部署會將程式檔案放在用戶端電腦上，並在預設使用者的識別之下以個別處理序的形式執行應用程式。 由於報表產生器必須連回報表伺服器，以取得應用程式檔案和報表伺服器資料，所以請務必了解 ClickOnce 如何設定安全性內容以及在不同狀況下對遠端電腦發出要求：  
  
-   ClickOnce 一定會在用戶端電腦上當做個別處理序來執行。 處理序識別是預設的 Windows 使用者認證。 ClickOnce 不會與 Internet Explorer 共用工作階段資料或是從 Internet Explorer 取得目前的使用者安全性內容。  
  
-   ClickOnce 會傳送要求，以便在驗證標頭中指定 Windows 整合式安全性。 如果伺服器設定了不同的驗證類型，伺服器將無法處理 ClickOnce 的要求，而且會產生驗證錯誤。 這個問題的解決方法如下：您必須針對 Windows 整合式安全性設定伺服器，或者必須啟用匿名存取來排除驗證檢查。  
  
-   報表產生器會開啟它自己與報表伺服器的連接。 如果您未搭配單一登入來使用 Windows 整合式安全性，使用者必須針對與報表伺服器的報表產生器連接重新輸入認證。  
  
 下表說明報表伺服器所支援的驗證類型，以及是否需要其他組態才能存取報表產生器。  
  
|報表伺服器驗證類型|報表產生器和 ClickOnce 應用程式啟動器的回應方式|  
|---------------------------------------|--------------------------------------------------------------------|  
|交涉 (預設值)<br /><br /> NTLM (預設值)|在 Windows 整合式安全性之下，如果用戶端和伺服器部署在相同的網域中、使用者使用有權存取報表產生器的網域帳戶來登入用戶端電腦，而且報表伺服器有設定 Windows 驗證時，來自 ClickOnce 和報表產生器的已驗證要求通常會成功。<br /><br /> 要求成功是因為 ClickOnce 以及與報表伺服器的瀏覽器連接具有相同的使用者識別。<br /><br /> 如果使用者使用 [執行身分] 開啟 Internet Explorer 而且指定了非預設的認證，要求將會失敗。 如果報表伺服器上的使用者工作階段是在特定的帳戶之下建立，而且 ClickOnce 會在不同的帳戶下執行，則報表伺服器將會拒絕檔案的存取。|  
|Kerberos|使用報表產生器所需的 Internet Explorer 並不會直接支援 Kerberos。|  
|基本驗證|ClickOnce 不支援基本驗證。 ClickOnce 將不會在驗證標頭中編寫用於指定基本驗證的要求， 也不會傳遞認證或是提示使用者提供認證。 您可以啟用報表產生器應用程式檔案的匿名存取來解決這些問題。<br /><br /> 如果您啟用報表產生器應用程式檔案的匿名存取，要求將會成功，因為報表伺服器會忽略驗證標頭。 如需如何啟用報表產生器匿名存取的詳細資訊，請參閱 [設定報表伺服器上的基本驗證](../security/configure-basic-authentication-on-the-report-server.md)。<br /><br /> 在 ClickOnce 擷取應用程式檔案之後，報表產生器會開啟與報表伺服器的個別連接。 使用者必須重新輸入認證，才能讓報表產生器連接報表伺服器。 報表產生器不會從 Internet Explorer 或 ClickOnce 收集認證。<br /><br /> 如果報表伺服器有設定基本驗證，而且您並未啟用報表產生器程式檔案的匿名存取，要求將會失敗。 要求失敗是因為 ClickOnce 會在它的要求中指定 Windows 整合式安全性。 如果報表伺服器有設定基本驗證，伺服器將會拒絕要求，因為它會指定無效的安全性封裝，而且它會缺少報表伺服器所預期的認證。<br /><br /> 此外，如果報表伺服器設定為使用 SharePoint 整合模式，而且 SharePoint 網站使用基本驗證，則當使用者嘗試使用 ClickOnce 在用戶端電腦上安裝報表產生器時，會出現 401 錯誤。 發生這個狀況的原因是 SharePoint 會使用 Cookie 讓使用者在工作階段期間維持驗證狀態，但是 ClickOnce 不支援 Cookie。 當使用者啟動 ClickOnce 應用程式 (例如報表產生器) 時，應用程式不會讓 Cookie 通過 SharePoint，因此 SharePoint 會拒絕存取並傳回 401 錯誤。<br /><br /> 您可以嘗試下列其中一個選項來解決這個問題：<br /><br /> 當您提供使用者認證時，請選取 [**記住我的密碼**] 選項。<br /><br /> 針對 SharePoint 網站集合啟用匿名存取。<br /><br /> 設定環境，讓使用者不提供認證。 例如，在內部網路環境中，您可能會將 SharePoint 伺服器設定為屬於某個工作群組，然後在本機電腦上建立使用者帳戶。|  
|自訂|當您設定報表伺服器使用自訂驗證時，報表伺服器上會啟用匿名存取，而且會接受要求而不執行驗證檢查。<br /><br /> 在 ClickOnce 擷取應用程式檔案之後，報表產生器會開啟與報表伺服器的個別連接。 使用者必須重新輸入認證，才能讓報表產生器連接報表伺服器。 報表產生器不會從 Internet Explorer 或 ClickOnce 收集認證。|  
  
## <a name="see-also"></a>另請參閱  
 [使用報表伺服器驗證](../security/authentication-with-the-report-server.md)   
 [規劃 Reporting Services 和 Power View 瀏覽器支援 &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)   
 [開始報表產生器 &#40;報表產生器&#41;](../report-builder/start-report-builder.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)   
 [連接到 Management Studio 中的報表伺服器](../tools/connect-to-a-report-server-in-management-studio.md)   
 [報表伺服器系統屬性](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)  
  
  
