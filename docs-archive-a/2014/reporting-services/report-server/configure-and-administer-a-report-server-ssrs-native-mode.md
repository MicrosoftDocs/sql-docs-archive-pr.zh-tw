---
title: 設定和管理報表伺服器 (SSRS 原生模式) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, components
- deploying [Reporting Services], component options
- report servers [Reporting Services], component options
- configuration options [Reporting Services]
- administering Reporting Services
- components [Reporting Services], configuring
- configuring servers [Reporting Services]
ms.assetid: cfec012b-56f1-4346-9814-247acf22351c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5164fd2f9170cb092a45394f64f06d7622253f2b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597599"
---
# <a name="configure-and-administer-a-report-server-ssrs-native-mode"></a>設定和管理報表伺服器 (SSRS 原生模式)
  本主題摘要列出您可以用來設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的方法， 也包含了主題清單，用來解釋如何設定特定的元件、功能或伺服器功能。 若要設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，您可以：  
  
-   使用 [Reporting Services 組態管理員]。 本節中的許多主題都包含了有關如何透過這個工具來設定特定功能的資訊。  
  
-   使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 來自訂伺服器屬性、啟用 [我的報表]、啟用追蹤記錄及設定網站範圍的預設值。 如需網站設定的詳細資訊，請參閱 Management Studio 的 [Reporting Services 報表伺服器 &#40;原生模式&#41;](reporting-services-report-server-native-mode.md) 。 請注意，您可以建立並執行以程式設計方式設定伺服器屬性的指令碼。 如需詳細資訊，請參閱 [編寫部署和管理工作的指令碼](../tools/script-deployment-and-administrative-tasks.md) 和 [報表伺服器系統屬性](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)。  
  
-   使用報表管理員來授與存取報表伺服器的權限。 這些權限是透過您針對每個使用者或群組帳戶定義的角色指派傳達的。 如需詳細資訊，請參閱[角色與權限 &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md)。  
  
-   (選擇性) 修改組態檔來變更應用程式設定。 如需每個檔案和修改它們之指導方針的詳細資訊，請參閱 [Reporting Services Configuration Files](reporting-services-configuration-files.md)(Reporting Services 組態檔)。  
  
## <a name="in-this-section"></a>本節內容  
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
 描述如何定義用來存取報表伺服器和報表管理員的 URL。  
  
 [設定報表伺服器服務帳戶 &#40;SSRS 組態管理員&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
 提供如何修改服務帳戶和密碼的建議與步驟。  
  
 [建立報表伺服器資料庫 &#40;SSRS 組態管理員&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)  
 描述如何建立儲存伺服器中繼資料和物件所需的報表伺服器資料庫。  
  
 [設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
 描述如何修改報表伺服器用來連接到報表伺服器資料庫的連接字串。  
  
 [針對 &#40;SSRS Configuration Manager 的電子郵件傳遞設定報表伺服器&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
 描述如何設定報表伺服器，以支援電子郵件報表散發。  
  
 [設定自動執行帳戶 &#40;SSRS 組態管理員&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
 描述如何設定使用者帳戶以自動模式處理報表。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表產生器存取](configure-report-builder-access.md)   
 [Reporting Services 組態檔](reporting-services-configuration-files.md)   
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Reporting Services 的安全性與保護](../security/reporting-services-security-and-protection.md)   
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](reporting-services-report-server-native-mode.md)  
  
  
