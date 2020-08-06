---
title: 資料夾和檔案權限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- security [Master Data Services], file and folder
- folders [Master Data Services]
- files [Master Data Services]
ms.assetid: 6402d81d-7349-47b1-95ca-99b0c0f4f373
author: lrtoyou1223
ms.author: lle
robots: noindex,nofollow
ms.openlocfilehash: 6dc356e074574a4c520b1f4de2f41db0e983c4df
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699934"
---
# <a name="folder-and-file-permissions-master-data-services"></a>資料夾和檔案的權限 (Master Data Services)
  當您安裝 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]時，資料夾和檔案會安裝在檔案系統中針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 共用功能所指定的安裝路徑。 如果您使用共用功能的預設安裝路徑 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，的安裝路徑為 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] *drive*： \Program Files\Microsoft SQL Server\120\Master 資料服務。 雖然您可以變更共用功能的安裝路徑，但請注意繼承自父資料夾的權限以及為 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]明確設定的權限。  
  
## <a name="inherited-permissions"></a>繼承的權限  
 **Microsoft SQL Server** 資料夾、 **Master Data Services** 資料夾，以及大部分子資料夾和檔案都會從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝程式中指定的父資料夾繼承權限。 如果您選擇預設安裝位置，則會從下列父資料夾繼承權限： *drive*:\Program Files。 下表描述 **Program Files**的預設權限。  
  
> [!NOTE]  
>  如果您修改 **Program Files**的預設權限或選擇不同的安裝位置， [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料夾和檔案會跟著從其父資料夾繼承權限，而這些權限可能不同於下表所描述的權限。  
  
###### <a name="program-files-default-permissions"></a>Program Files 的預設權限  
  
|群組或帳戶名稱|權限|  
|---------------------------|-----------------|  
|CREATOR OWNER|特殊權限|  
|系統|特殊權限|  
|Administrators|特殊權限|  
|使用者|讀取與執行、列出資料夾內容、讀取|  
|TrustedInstaller|列出資料夾內容、特殊權限|  
  
## <a name="explicit-permissions"></a>明確權限  
 **MDSTempDir** 資料夾和 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web.config 檔案 (在 **WebApplication** 資料夾中) 不會繼承權限。 它們的權限是在您安裝 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]時明確設定，無論所選安裝路徑為何。 請不要修改這些權限。  
  
###### <a name="mdstempdir-permissions"></a>MDSTempDir 的權限  
  
|群組或帳戶名稱|權限|  
|---------------------------|-----------------|  
|系統|修改、讀取與執行、列出資料夾內容、讀取、寫入|  
|Administrators|修改、讀取與執行、列出資料夾內容、讀取、寫入|  
|MDS_ServiceAccounts|修改、讀取與執行、列出資料夾內容、讀取、寫入|  
  
###### <a name="webconfig-permissions"></a>Web.config 的權限  
  
|群組或帳戶名稱|權限|  
|---------------------------|-----------------|  
|系統|完全控制、修改、讀取與執行、讀取、寫入|  
|Administrators|完全控制、修改、讀取與執行、讀取、寫入|  
|MDS_ServiceAccounts|讀取與執行、讀取|  
  
 如需 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web.config 檔案內容的詳細資訊，請參閱 [Web 組態參考 &#40;Master Data Services&#41;](web-configuration-reference-master-data-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Master Data Services](install-windows/install-master-data-services.md)  
  
  
