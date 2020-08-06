---
title: WSFC 叢集服務已離線 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp1WSFCquorum.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: d502548d-ece6-4a42-9ded-2157d33e3d21
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e6e7b48f96eb09638291b1d0655d385d606b1666
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87701905"
---
# <a name="wsfc-cluster-service-is-offline"></a>WSFC 叢集服務離線
    
## <a name="introduction"></a>簡介  
  
|||  
|-|-|  
|**原則名稱**|WSFC 叢集狀態|  
|**問題**|WSFC 叢集服務已離線。|  
|**類別目錄**|**嚴重**|  
|**Facet**|SQL Server 的執行個體|  
  
## <a name="description"></a>描述  
 這項原則檢查 Windows Server 容錯移轉叢集 (WSFC) 的狀態。 當 WSFC 叢集已離線或處於強制仲裁狀態時，原則為狀況不良並會引發警示。 此叢集中裝載的所有可用性群組都已離線或需要災害復原動作。  
  
 當叢集狀態為標準仲裁時，原則為狀況良好。  
  
> [!NOTE]  
>  在此版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]中，可能原因和解決方案的資訊位於 TechNet Wiki 上的 [WSFC 叢集服務已離線](https://go.microsoft.com/fwlink/p/?LinkId=220849) 。  
  
## <a name="possible-causes"></a>可能的原因  
 這個問題可能是叢集服務問題或叢集遺失仲裁所造成。  
  
## <a name="possible-solution"></a>可能的解決方案  
 使用叢集管理員工具來執行強制仲裁或災害復原工作流程。 如果您無法透過執行強制仲裁或災害復原來解決問題，請向您的叢集管理員尋求協助。 如需詳細資訊，請參閱《 [線上叢書》中的](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md) 在無仲裁情況下強制啟動 WSFC 叢集 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
