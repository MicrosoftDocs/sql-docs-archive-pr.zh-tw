---
title: 未偵測到 IIS 回溯相容性元件 (Upgrade Advisor) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- IIS [Reporting Services]
ms.assetid: e794185a-0a77-480a-9aea-d09f8760a6b8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a5aad54a01b3840e121c6a63de0ea26f35921fa7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606029"
---
# <a name="iis-backward-compatibility-components-were-not-detected-upgrade-advisor"></a>未偵測到 IIS 回溯相容性元件 (Upgrade Advisor)
  Upgrade Advisor 並未偵測到可提供安裝程式用來建立新 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 之資訊的 IIS 元件和設定。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]原生模式。|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 IIS 包含可提供有關報表伺服器和報表管理員虛擬目錄之資訊的元件，而且這些元件未安裝在報表伺服器電腦上。 雖然升級可以繼續進行，但是升級將不會重建報表伺服器或報表管理員的 URL。  
  
## <a name="corrective-action"></a>更正動作  
 升級完成之後，請使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來設定報表伺服器或報表管理員的 URL。 您可以使用 IIS 管理員來移除不再需要的虛擬目錄。  
  
 如需詳細資訊，請參閱《線上叢書》中的[Configure a URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Upgrade Advisor Reporting Services 升級問題&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
