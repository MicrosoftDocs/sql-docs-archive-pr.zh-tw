---
title: SharePoint 伺服器陣列 (Upgrade Advisor) 所需的網域帳戶 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 90cd6d3e-a271-4cb8-81f2-fc555b2d3cab
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7d180fbc12a264256156c878916838f7caeec723
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606606"
---
# <a name="domain-accounts-required-for-sharepoint-farm-upgrade-advisor"></a>SharePoint 伺服陣列所需的網域帳戶 (Upgrade Advisor)
  針對伺服陣列環境設定的 SharePoint 產品需要使用網域帳戶。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式。|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRS](../../includes/ssrs.md)]  
  
### <a name="description"></a>描述  
 針對伺服陣列環境設定的 SharePoint 產品需要將網域帳戶用於服務和資料庫連接。 其中包括您為 Reporting Services 服務帳戶指定的帳戶。  
  
 如果您並未在 Reporting Services 中使用網域使用者帳戶，您就會在 SharePoint 2010 管理中心頁面中看到問題。 當您嘗試設定 Reporting Services 整合時，您會看到類似底下的錯誤訊息：  
  
 「報表伺服器是以內建的 NT AUTHORITY\NETWORK SERVICE 帳戶執行，但 SharePoint 伺服陣列安裝不支援該帳戶。 請將報表伺服器重新設定成以網域帳戶執行。」  
  
## <a name="corrective-action"></a>更正動作  
 若是 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和舊版，請使用 Reporting Services 組態管理員來變更指派為報表伺服器服務帳戶的帳戶。  
  
#### <a name="to-change-the-service-account-from-configuration-manager"></a>若要從組態管理員變更服務帳戶  
  
1.  從 [**開始**] 功能表選取 [**所有程式**]，然後按一下 [ **Microsoft SQL Server 2008 R2**]。  
  
2.  選取 [**組態工具**]，然後按一下 [ **Reporting Services 組態管理員**]。  
  
3.  在 Configuration Manager 中，選取 [**服務帳戶**] 索引標籤。  
  
4.  選取 [**使用其他帳戶**]，然後輸入網域帳戶的認證。  
  
5.  按一下 [套用]。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器服務帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
  
  
