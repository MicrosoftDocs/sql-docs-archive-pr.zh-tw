---
title: 偵測到 (Upgrade Advisor) 的 IP 位址限制 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 9a154455-c68f-4403-a3a7-b90f4d35eecb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2028e59e91d42bfdced2d18fa6ce129dfb108302
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87700630"
---
# <a name="ip-address-restriction-detected-upgrade-advisor"></a>偵測到 IP 位址限制 (Upgrade Advisor)
  Upgrade Advisor 在主控報表伺服器或報表管理員虛擬目錄的 IIS 網站上偵測到一個或多個 IP 位址限制。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不會提供 IP 位址限制的原生支援。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]自有.|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 安裝程式無法針對升級報表伺服器所建立的 URL 定義 IP 位址限制。 雖然升級可以繼續進行，但是不會針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 定義 IP 位址限制。  
  
## <a name="corrective-action"></a>更正動作  
 升級之後，請使用 ISA Server、防火牆軟體或其他解決方案來允許或排除特定 IP 位址到報表伺服器的要求。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Upgrade Advisor Reporting Services 升級問題&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
