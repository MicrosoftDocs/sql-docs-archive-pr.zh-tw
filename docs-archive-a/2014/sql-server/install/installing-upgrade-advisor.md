---
title: 安裝 Upgrade Advisor |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- Upgrade Advisor [SQL Server], installing
ms.assetid: 1b7d6eca-1df1-47df-bbba-0fc485706a95
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 40f214b01f3e2066708a060c5f3ad1e8aa4a0a23
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688449"
---
# <a name="installing-upgrade-advisor"></a>安裝 Upgrade Advisor
  安裝 SQL Server 2014 Upgrade Advisor 的位置會因您要分析的項目而不同。 Upgrade Advisor 支援所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的遠端分析，但 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]除外。 如果您未掃描的實例 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，您可以在任何可連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 且符合[Upgrade advisor 必要條件](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)的電腦上安裝 Upgrade Advisor。 如果您要掃描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的執行個體，則必須將 Upgrade Advisor 安裝在報表伺服器上。  
  
 執行 **SQLUA.msi** 檔，以便安裝 Upgrade Advisor。 您可以從命令提示字元進行自主式且自動化安裝。 請參閱＜ [Installing Upgrade Advisor from the Command Prompt](../../../2014/sql-server/install/installing-upgrade-advisor-from-the-command-prompt.md) ＞，以取得語法和範例。  
  
 取得 SQLUA.msi：  
  
-   在 **產品媒體的** redist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料夾中。  
  
-   作為 [SQL 2014 功能套件下載](https://www.microsoft.com/download/details.aspx?id=42295)的一部分。  
  
## <a name="uninstalling-upgrade-advisor"></a>解除安裝 Upgrade Advisor  
 您可以使用 **[新增或移除程式]** 來解除安裝 Upgrade Advisor。 命令提示字元語法也支援移除/解除安裝。  
  
  
