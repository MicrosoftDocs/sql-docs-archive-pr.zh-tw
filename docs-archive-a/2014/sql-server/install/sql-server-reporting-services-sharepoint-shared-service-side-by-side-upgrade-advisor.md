---
title: Microsoft SQL Server Reporting Services SharePoint 共用服務已並存安裝 (Upgrade Advisor) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6ae1017e-129b-4702-9ea7-00ac9b024062
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b8a26fedd892dfb26dea4616efd46d3b3748b508
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598119"
---
# <a name="microsoft-sql-server-reporting-services-sharepoint-shared-service-is-installed-side-by-side-upgrade-advisor"></a>已並存安裝 Microsoft SQL Server Reporting Services SharePoint 共用服務 (Upgrade Advisor)
  Upgrade Advisor 偵測到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 共用服務與舊版並存安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式。|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 Upgrade Advisor 偵測到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sharepoint 共用服務與舊版並存安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，而該版本不是以 SharePoint 共用服務架構為基礎。 由於電腦上已並存安裝新舊 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 相關技術，因此升級遭到封鎖。  
  
## <a name="corrective-action"></a>更正動作  
 若要繼續升級，您必須解除安裝其中一個現有的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝。 移除其中一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝之後，請重新執行 Upgrade Advisor，以便確認沒有其他升級問題。  
  
  
