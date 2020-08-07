---
title: 未指定 (Upgrade Advisor) 的虛擬目錄 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 7d32b560-49d6-4558-b5d6-9127067f82d6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e20c48d0bf58d28cb2894baa26c2e11db26fab96
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595410"
---
# <a name="virtual-directories-are-unspecified-upgrade-advisor"></a>未指定虛擬目錄 (Upgrade Advisor)
  Upgrade Advisor 未偵測到報表伺服器 Web 服務或報表管理員的虛擬目錄設定。 升級完成之後，您必須使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員來設定報表伺服器的 URL 保留項目。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]原生模式。|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 升級 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝包括保留報表伺服器 Web 服務和報表管理員的新 URL。 Upgrade Advisor 未偵測到要升級之執行個體的報表伺服器或報表管理員的虛擬目錄，因此升級程序的資訊不足，無法建立升級報表伺服器的 URL 保留項目。 雖然升級可以繼續進行，但是在升級的安裝之後，報表伺服器或報表管理員虛擬目錄將處於未定義狀態。  
  
## <a name="corrective-action"></a>更正動作  
 升級完成之後，請使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員來設定報表伺服器和報表管理員的 URL。 您可以使用 IIS 管理員來移除任何不再需要的虛擬目錄。  
  
 如需詳細資訊，請參閱《線上叢書》中的[Configure a URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Upgrade Advisor Reporting Services 升級問題&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
