---
title: SQL Server Agent 記錄傳送作業類別目錄會導致升級失敗 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server Agent]
- job categories [SQL Server Agent]
ms.assetid: ef05ce53-c6ce-42ec-9df8-46c951626424
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2f5947e8fc8d459388fe35d86c75666e25b5d907
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87710138"
---
# <a name="sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail"></a><span data-ttu-id="60872-102">SQL Server Agent 記錄傳送作業類別目錄會造成升級失敗</span><span class="sxs-lookup"><span data-stu-id="60872-102">SQL Server Agent log shipping job category causes upgrade to fail</span></span>
  <span data-ttu-id="60872-103">如果您目前存在名為「記錄傳送」的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式作業類別，升級程序將會失敗。</span><span class="sxs-lookup"><span data-stu-id="60872-103">The upgrade process will fail if a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent job category named Log Shipping exists.</span></span>  
  
## <a name="component"></a><span data-ttu-id="60872-104">元件</span><span class="sxs-lookup"><span data-stu-id="60872-104">Component</span></span>  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="60872-105">Agent</span><span class="sxs-lookup"><span data-stu-id="60872-105">Agent</span></span>  
  
## <a name="description"></a><span data-ttu-id="60872-106">描述</span><span class="sxs-lookup"><span data-stu-id="60872-106">Description</span></span>  
 <span data-ttu-id="60872-107">有名為「記錄傳送」的系統作業類別。</span><span class="sxs-lookup"><span data-stu-id="60872-107">There is a system job category named Log Shipping.</span></span> <span data-ttu-id="60872-108">如果正在升級的安裝已經包含名為「記錄傳送」的使用者建立作業類別目錄，您就必須重新命名此作業類別目錄，然後再升級。否則，升級程序將會失敗。</span><span class="sxs-lookup"><span data-stu-id="60872-108">If an installation that is being upgraded already contains a user-created job category named Log Shipping, you must rename the job category before you upgrade; otherwise, the upgrade process will fail.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="60872-109">另請參閱</span><span class="sxs-lookup"><span data-stu-id="60872-109">See Also</span></span>  
 <span data-ttu-id="60872-110">[升級後將不會執行記錄傳送](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md) </span><span class="sxs-lookup"><span data-stu-id="60872-110">[Log shipping will not run after upgrading](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md) </span></span>  
 <span data-ttu-id="60872-111">[升級會將 SQL Server Agent 的使用者 Proxy 帳戶變更為暫時的 UpgradedProxyAccount](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md) </span><span class="sxs-lookup"><span data-stu-id="60872-111">[Upgrading will change the SQL Server Agent User Proxy Account to the temporary UpgradedProxyAccount](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md) </span></span>  
 [<span data-ttu-id="60872-112">SQL Server Agent 升級問題</span><span class="sxs-lookup"><span data-stu-id="60872-112">SQL Server Agent Upgrade Issues</span></span>](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
