---
title: Reporting Services 的驗證擴充保護 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: eb5c6f4a-3ed5-430b-a712-d5ed4b6b9b2b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 66a3cf551b70fa564da3fa47eec015a5bbca7e43
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688502"
---
# <a name="extended-protection-for-authentication-with-reporting-services"></a>含有 Reporting Services 的驗證擴充保護
  「擴充保護」是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 作業系統最新版本的一組增強功能。 擴充保護會增強認證與驗證受到應用程式保護的方式。 此功能本身並不會針對認證轉送之類的特定攻擊直接提供保護，但是它會為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 之類的應用程式提供基礎結構，以增強驗證擴充保護。

 屬於擴充保護一部分的主要驗證增強功能為服務繫結與通道繫結。 通道繫結使用通道繫結 Token (CBT) 驗證兩點端點之間建立的通道是否未受到危害。 服務繫結使用服務主要名稱 (SPN) 驗證預期的驗證 Token 目的地。 如需擴充保護的詳細背景資訊，請參閱 [Integrated Windows Authentication with Extended Protection](https://go.microsoft.com/fwlink/?LinkId=179922)(具有擴充保護的整合式 Windows 驗證)。

 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]支援並強制執行已在作業系統中啟用，且在中設定的擴充保護 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 。 依預設， [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 會接受指定交涉或 NTLM 驗證的要求，因此可以在作業系統與 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 擴充保護功能中獲得擴充保護支援。

> [!IMPORTANT]
>  Windows 預設不會啟用 [擴充保護]。 如需如何在 Windows 中啟用 [擴充保護] 的資訊，請參閱 [驗證延伸保護](https://go.microsoft.com/fwlink/?LinkID=178431)。 作業系統與用戶端驗證堆疊必須同時支援擴充保護，驗證才會成功。 對於舊版作業系統，您可能需要針對完整具備擴充保護的電腦安裝多個更新。 如需擴充保護之最近開發狀況的詳細資訊，請參閱 [擴充保護的更新資訊](https://go.microsoft.com/fwlink/?LinkId=183362)。

## <a name="reporting-services-extended-protection-overview"></a>Reporting Services 擴充保護概觀
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]支援並強制執行已在作業系統中啟用的擴充保護。 如果作業系統不支援擴充保護，或者尚未啟用作業系統中的功能， [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 擴充保護功能將會無法驗證。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 擴充保護也需要 SSL 憑證。 如需詳細資訊，請參閱 [在原生模式報表伺服器上設定 SSL 連接](configure-ssl-connections-on-a-native-mode-report-server.md)

> [!IMPORTANT]
>  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 預設為不會啟用 [擴充保護]。 修改 `rsreportserver.config` 組態檔或使用 WMI API 更新組態檔，即可啟用該功能。 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 未提供可修改或檢視擴充保護設定的使用者介面。 如需詳細資訊，請參閱本主題中的 [組態設定](#ConfigurationSettings) 一節。

 因為擴充保護設定變更或進行之設定錯誤所造成的常見問題，不會以明顯的錯誤訊息或對話方塊視窗公開。 與擴充保護組態和相容性相關的問題會導致驗證失敗，並將錯誤記錄在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 追蹤記錄中。

> [!IMPORTANT]
>  某些資料存取技術可能不支援擴充保護。 資料存取技術可用於連接 SQL Server 資料來源與 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 目錄資料庫。 無法支援擴充保護的資料存取技術會以下列方式對 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 造成影響：
> 
>  -   執行 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 目錄資料庫的 SQL Server 無法啟用擴充功能，否則報表伺服器將無法成功連接至目錄資料庫，並傳回驗證錯誤。
> -   當作 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 報表資料來源使用的 SQL Servers 無法啟用擴充保護，否則報表伺服器為連接報表資料來源所做的嘗試將會失敗，並傳回驗證錯誤。
> 
>  資料存取技術的文件應具有支援擴充保護的資訊。

### <a name="upgrade"></a>升級

-   將 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 伺服器升級至 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 時，會將具有預設值的組態設定加入至 `rsreportserver.config` 檔。 如果設定已經存在， [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 安裝會將它們保留在檔案中 `rsreportserver.config` 。

-   將設定新增至 `rsreportserver.config` 設定檔時，預設行為是讓 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 擴充保護功能關閉，而且您必須啟用此功能，如本主題中所述。 如需詳細資訊，請參閱本主題中的 [組態設定](#ConfigurationSettings) 一節。

-   `RSWindowsExtendedProtectionLevel` 設定的預設值為 `Off`。

-   `RSWindowsExtendedProtectionScenario` 設定的預設值為 `Proxy`。

-   [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Upgrade Advisor 不會驗證作業系統或目前安裝的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 是否已啟用擴充保護支援。

### <a name="what-reporting-services-extended-protection-does-not-cover"></a>Reporting Services 擴充保護不涵蓋的功能
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 擴充保護功能不支援下列功能區與案例：

-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 自訂安全性延伸模組的作者必須將擴充保護的支援加入其自訂安全性延伸模組。

-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 安裝所加入或使用的協力廠商元件必須由協力廠商更新，才能支援擴充保護。 如需詳細資訊，請連絡協力廠商。

## <a name="deployment-scenarios-and-recommendations"></a>部署案例與建議
 下列案例說明不同的部署與拓撲，以及使用 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 擴充保護來保護其安全的建議組態。

### <a name="direct"></a>直接
 此案例描述直接連接至報表伺服器，例如內部網路環境。

|狀況|案例圖表|如何保護安全|
|--------------|----------------------|-------------------|
|直接 SSL 通訊。<br /><br /> 報表伺服器將會強制執行用戶端到報表伺服器的通道繫結。|![RS_ExtendedProtection_DirectSSL](../media/rs-extendedprotection-directssl.gif "RS_ExtendedProtection_DirectSSL")<br /><br /> 1) 用戶端應用程式<br /><br /> 2) 報表伺服器|不需要服務繫結，因為 SSL 通道將用於通道繫結。<br /><br /> 將 `RSWindowsExtendedProtectionLevel` 設定為 `Allow` 或 `Require`。<br /><br /> 將 `RSWindowsExtendedProtectionScenario` 設定為 `Direct`。|
|直接 HTTP 通訊。 報表伺服器將會強制執行用戶端到報表伺服器的服務繫結。|![RS_ExtendedProtection_Direct](../media/rs-extendedprotection-direct.gif "RS_ExtendedProtection_Direct")<br /><br /> 1) 用戶端應用程式<br /><br /> 2) 報表伺服器|沒有 SSL 通道，因此無法強制執行通道繫結。<br /><br /> 服務繫結可以經過驗證，不過，如果沒有自己的通道繫結和服務繫結，它將只能防範基本威脅，而不是完整的防禦。<br /><br /> 將 `RSWindowsExtendedProtectionLevel` 設定為 `Allow` 或 `Require`。<br /><br /> 將 `RSWindowsExtendedProtectionScenario` 設定為 `Any`。|

### <a name="proxy-and-network-load-balancing"></a>Proxy 與網路負載平衡
 用戶端應用程式所連接的裝置或軟體會執行 SSL 並通過伺服器的認證以進行驗證，例如外部網路、網際網路或安全的內部網路。 用戶端連接至 Proxy 或所有用戶端都使用 Proxy。

 這個情況與您使用網路負載平衡 (NLB) 裝置相同。

|狀況|案例圖表|如何保護安全|
|--------------|----------------------|-------------------|
|HTTP 通訊。 報表伺服器將會強制執行用戶端到報表伺服器的服務繫結。|![RS_ExtendedProtection_Indirect](../media/rs-extendedprotection-indirect.gif "RS_ExtendedProtection_Indirect")<br /><br /> 1) 用戶端應用程式<br /><br /> 2) 報表伺服器<br /><br /> 3) Proxy|沒有 SSL 通道，因此無法強制執行通道繫結。<br /><br /> 將 `RSWindowsExtendedProtectionLevel` 設定為 `Allow` 或 `Require`。<br /><br /> 將 `RSWindowsExtendedProtectionScenario` 設定為 `Any`。<br /><br /> 請注意，您必須將報表伺服器設定為知道 proxy 伺服器的名稱，以確保正確地強制執行服務系結。|
|HTTP 通訊。<br /><br /> 報表伺服器將會強制執行用戶端到 Proxy 的通道繫結與用戶端到報表伺服器的服務繫結。|![RS_ExtendedProtection_Indirect_SSL](../media/rs-extendedprotection-indirect-ssl.gif "RS_ExtendedProtection_Indirect_SSL")<br /><br /> 1) 用戶端應用程式<br /><br /> 2) 報表伺服器<br /><br /> 3) Proxy|SSL 通道到 Proxy 的連線可以使用，因此可以強制執行 Proxy 的通道繫結。<br /><br /> 也可以強制執行服務繫結。<br /><br /> 報表伺服器必須知道 Proxy 名稱，而且報表伺服器管理員應該為該 Proxy 建立一個包含主機標頭的保留 URL，或在 Windows 登錄項目 `BackConnectionHostNames` 中設定 Proxy 名稱。<br /><br /> `RSWindowsExtendedProtectionLevel` 到 `Allow` 或 `Require`。<br /><br /> 將 `RSWindowsExtendedProtectionScenario` 設定為 `Proxy`。|
|透過安全 Proxy 進行的間接 HTTPS 通訊。 報表伺服器將會強制執行用戶端到 Proxy 的通道繫結與用戶端到報表伺服器的服務繫結。|![RS_ExtendedProtection_IndirectSSLandHTTPS](../media/rs-extendedprotection-indirectsslandhttps.gif "RS_ExtendedProtection_IndirectSSLandHTTPS")<br /><br /> 1) 用戶端應用程式<br /><br /> 2) 報表伺服器<br /><br /> 3) Proxy|SSL 通道到 Proxy 的連線可以使用，因此可以強制執行 Proxy 的通道繫結。<br /><br /> 也可以強制執行服務繫結。<br /><br /> 報表伺服器必須知道 Proxy 名稱，而且報表伺服器管理員應該為該 Proxy 建立一個包含主機標頭的保留 URL，或在 Windows 登錄項目 `BackConnectionHostNames` 中設定 Proxy 名稱。<br /><br /> `RSWindowsExtendedProtectionLevel` 到 `Allow` 或 `Require`。<br /><br /> 將 `RSWindowsExtendedProtectionScenario` 設定為 `Proxy`。|

### <a name="gateway"></a>閘道
 此案例描述連接至執行 SSL 並驗證使用者之裝置或軟體的用戶端應用程式。 接著，裝置或軟體會模擬使用者內容或不同的使用者內容，之後才對報表伺服器發出要求。

|狀況|案例圖表|如何保護安全|
|--------------|----------------------|-------------------|
|間接 HTTP 通訊。<br /><br /> 閘道將會強制執行用戶端到閘道的通道繫結。 此處有閘道到報表伺服器的服務繫結。|![RS_ExtendedProtection_Indirect_SSL](../media/rs-extendedprotection-indirect-ssl.gif "RS_ExtendedProtection_Indirect_SSL")<br /><br /> 1) 用戶端應用程式<br /><br /> 2) 報表伺服器<br /><br /> 3) 閘道裝置|從用戶端到報表伺服器沒有通道繫結，因為閘道會模擬內容，並因而建立新的 NTLM Token。<br /><br /> 從閘道到報表伺服器沒有 SSL，因此無法強制執行通道繫結。<br /><br /> 可以強制執行服務繫結。<br /><br /> 將 `RSWindowsExtendedProtectionLevel` 設定為 `Allow` 或 `Require`。<br /><br /> 將 `RSWindowsExtendedProtectionScenario` 設定為 `Any`。<br /><br /> 系統管理員應該設定閘道裝置來強制執行通道繫結。|
|透過安全閘道進行的間接 HTTPS 通訊。 閘道將會強制執行用戶端到閘道的通道繫結，而且報表伺服器將會強制執行閘道到報表伺服器的通道繫結。|![RS_ExtendedProtection_IndirectSSLandHTTPS](../media/rs-extendedprotection-indirectsslandhttps.gif "RS_ExtendedProtection_IndirectSSLandHTTPS")<br /><br /> 1) 用戶端應用程式<br /><br /> 2) 報表伺服器<br /><br /> 3) 閘道裝置|從用戶端到報表伺服器沒有通道繫結，因為閘道會模擬內容，並因而建立新的 NTLM Token。<br /><br /> 從閘道到報表伺服器的 SSL 表示可以強制執行通道系結。<br /><br /> 不需要服務繫結。<br /><br /> 將 `RSWindowsExtendedProtectionLevel` 設定為 `Allow` 或 `Require`。<br /><br /> 將 `RSWindowsExtendedProtectionScenario` 設定為 `Direct`。<br /><br /> 系統管理員應該設定閘道裝置來強制執行通道繫結。|

### <a name="combination"></a>合併
 此案例描述用戶端連接 Proxy 的外部網路或網際網路環境。 這是合併用戶端連接報表伺服器的內部網路環境。

|狀況|案例圖表|如何保護安全|
|--------------|----------------------|-------------------|
|在用戶端到 Proxy 或用戶端到報表伺服器連線沒有 SSL 的情況下，從用戶端到報表伺服器服務的間接和直接存取。|1) 用戶端應用程式<br /><br /> 2) 報表伺服器<br /><br /> 3) Proxy<br /><br /> 4) 用戶端應用程式|可以強制執行從用戶端到報表伺服器的服務繫結。<br /><br /> 報表伺服器必須知道 Proxy 名稱，而且報表伺服器管理員應該為該 Proxy 建立一個包含主機標頭的保留 URL，或在 Windows 登錄項目 `BackConnectionHostNames` 中設定 Proxy 名稱。<br /><br /> 將 `RSWindowsExtendedProtectionLevel` 設定為 `Allow` 或 `Require`。<br /><br /> 將 `RSWindowsExtendedProtectionScenario` 設定為 `Any`。|
|在用戶端建立與 Proxy 或報表伺服器的 SSL 連接時，從用戶端到報表伺服器服務的間接和直接存取。|![RS_ExtendedProtection_CombinationSSL](../media/rs-extendedprotection-combinationssl.gif "RS_ExtendedProtection_CombinationSSL")<br /><br /> 1) 用戶端應用程式<br /><br /> 2) 報表伺服器<br /><br /> 3) Proxy<br /><br /> 4) 用戶端應用程式|可以使用通道繫結。<br /><br /> 報表伺服器必須知道 Proxy 名稱，而且報表伺服器管理員應該為該 Proxy 建立一個包含主機標頭的保留 URL，或在 Windows 登錄項目 `BackConnectionHostNames` 中設定 Proxy 名稱。<br /><br /> 將 `RSWindowsExtendedProtectionLevel` 設定為 `Allow` 或 `Require`。<br /><br /> 將 `RSWindowsExtendedProtectionScenario` 設定為 `Proxy`。|

## <a name="configuring-reporting-rervices-extended-protection"></a>設定 Reporting Services 擴充保護
 檔案 `rsreportserver.config` 包含控制擴充保護行為的設定值 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 。

 如需使用和編輯檔案的詳細資訊 `rsreportserver.config` ，請參閱[Rsreportserver.config Configuration file](../report-server/rsreportserver-config-configuration-file.md)。 擴充保護設定也可以透過 WMI API 變更與檢查。 如需詳細資訊，請參閱 [SetExtendedProtectionSettings 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)(具有擴充保護的整合式 Windows 驗證)。

 當組態設定的驗證失敗時，報表伺服器上會停用驗證類型 `RSWindowsNTLM`、`RSWindowsKerberos` 和 `RSWindowsNegotiate`。

###  <a name="configuration-settings-for-reporting-services-extended-protection"></a><a name="ConfigurationSettings"></a> Reporting Services 擴充保護的組態設定
 下表提供的資訊有關 `rsreportserver.config` 中顯示之擴充保護的組態設定。

|設定|描述|
|-------------|-----------------|
|`RSWindowsExtendedProtectionLevel`|指定擴充保護的強制執行程度。 有效值是 `Off`、`Allow` 和 `Require`。<br /><br /> 預設值是 `Off`。<br /><br /> 值為 `Off` 時，不會指定通道繫結或服務繫結驗證。<br /><br /> 值為 `Allow` 時，則支援擴充保護但並不需要它。 Allow 這個值會指定：<br /><br /> 擴充保護將會針對在支援擴充保護之作業系統上執行的用戶端應用程式強制執行。 您可以設定 `RsWindowsExtendedProtectionScenario` 來決定強制執行保護的方式。<br /><br /> 對於在不支援擴充保護之作業系統上執行的應用程式，不允許執行驗證。<br /><br />  這個值會指定：<br /><br /> 擴充保護將會針對在支援擴充保護之作業系統上執行的用戶端應用程式強制執行。<br /><br /> 對於在不支援擴充保護之作業系統上執行的應用程式，將**不**允許進行驗證。|
|`RsWindowsExtendedProtectionScenario`|指定要驗證的擴充保護形式：通道繫結、服務繫結或兩者。 有效值是 `Any`、`Proxy` 和 `Direct`。<br /><br /> 預設值是 `Proxy`。<br /><br />  這個值會指定：<br /><br /> \- Windows NTLM、Kerberos 和交涉驗證，而不需要通道繫結。<br /><br /> \- 服務繫結會強制執行。<br /><br />  這個值會指定：<br /><br /> \- Windows NTLM、Kerberos 和交涉驗證 (當通道繫結權杖存在時)。<br /><br /> \- 服務繫結會強制執行。<br /><br />  這個值會指定：<br /><br /> - Windows NTLM、Kerberos 和交涉驗證 (當 CBT 存在、目前服務的 SSL 連線存在，而且 SSL 連線的 CBT 與 NTLM、Kerberos 或交涉權杖的 CBT 相符時)。<br /><br /> \- 服務繫結不會強制執行。<br /><br /> <br /><br /> 注意：如果設定為，則會忽略此設定 `RsWindowsExtendedProtectionLevel` `OFF` 。|

 `rsreportserver.config` 組態檔中的範例項目：

```
<Authentication>
         <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>
         <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionLevel>
</Authentication>
```

## <a name="service-binding-and-included-spns"></a>服務繫結與隨附的 SPN
 服務繫結使用服務主要名稱或 SPN 驗證預期的驗證 Token 目的地。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 使用現有的 URL 保留資訊建立視為有效之 SPN 的清單。 使用 URL 保留資訊同時驗證保留的 SPN 和 URL 可讓系統管理員從單一位置同時進行管理。

 當報表伺服器啟動時、擴充保護的組態設定變更時，或應用程式定義域循環使用時，會更新有效 SPN 的清單。

 有效的 SPN 清單專屬於每個應用程式。 例如，報表管理員和報表伺服器會各自計算一份不同的有效 SPN 清單。

 針對應用程式計算的有效 SPN 清單取決於下列因素：

-   每個保留的 URL。

-   從 Reporting Services 服務帳戶之網域控制站擷取的每個 SPN。

-   如果保留的 URL 包括萬用字元 ('*' 或 '+')，則報表伺服器將會從主機集合加入每個項目。

### <a name="hosts-collection-sources"></a>主機集合來源。
 下表列出主機集合的潛在來源。

|來源類型|描述|
|--------------------|-----------------|
|ComputerNameDnsDomain|指派給本機電腦之 DNS 網域的名稱。 如果本機電腦是叢集中的一個節點，則會使用叢集虛擬伺服器的 DNS 網域名稱。|
|ComputerNameDnsFullyQualified|唯一識別本機電腦的完整 DNS 名稱。 此名稱結合 DNS 主機名稱與 DNS 網域名稱，其格式為 *HostName*.*DomainName*。 如果本機電腦是叢集中的一個節點，則會使用叢集虛擬伺服器的完整 DNS 名稱。|
|ComputerNameDnsHostname|本機電腦的 DNS 主機名稱。 如果本機電腦是叢集中的一個節點，則會使用叢集虛擬伺服器的 DNS 主機名稱。|
|ComputerNameNetBIOS|本機電腦的 NetBIOS 名稱。 如果本機電腦是叢集中的一個節點，則會使用叢集虛擬伺服器的 NetBIOS 名稱。|
|ComputerNamePhysicalDnsDomain|指派給本機電腦之 DNS 網域的名稱。 如果本機電腦是叢集中的一個節點，則會使用本機電腦的 DNS 網域名稱，而非叢集虛擬伺服器的名稱。|
|ComputerNamePhysicalDnsFullyQualified|唯一識別電腦的完整 DNS 名稱。 如果本機電腦是叢集中的一個節點，則會使用本機電腦的完整 DNS 名稱，而非叢集虛擬伺服器的名稱。<br /><br /> 完整的 DNS 名稱結合 DNS 主機名稱與 DNS 網域名稱，其格式為 *HostName*.*DomainName*。|
|ComputerNamePhysicalDnsHostname|本機電腦的 DNS 主機名稱。 如果本機電腦是叢集中的一個節點，則會使用本機電腦的 DNS 主機名稱，而非叢集虛擬伺服器的名稱。|
|ComputerNamePhysicalNetBIOS|本機電腦的 NetBIOS 名稱。 如果本機電腦是叢集中的一個節點，則會使用本機電腦的 NetBIOS 名稱，而非叢集虛擬伺服器的名稱。|

 如需詳細資訊，請參閱[為報表伺服器註冊服務主要名稱 &#40;SPN&#41;](../report-server/register-a-service-principal-name-spn-for-a-report-server.md) 和[關於 URL 保留項目和註冊 &#40;SSRS 組態管理員&#41;](../install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)。

## <a name="see-also"></a>另請參閱
 [使用擴充保護連接到資料庫引擎](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)[驗證擴充保護總覽](https://go.microsoft.com/fwlink/?LinkID=177943)[整合式 Windows 驗證與擴充保護](https://go.microsoft.com/fwlink/?LinkId=179922) [Microsoft 安全性摘要報告：驗證的擴充保護](https://go.microsoft.com/fwlink/?LinkId=179923)[報表伺服器服務追蹤記錄](../report-server/report-server-service-trace-log.md) [rsreportserver.config 設定檔](../report-server/rsreportserver-config-configuration-file.md)案[SetExtendedProtectionSettings 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)


