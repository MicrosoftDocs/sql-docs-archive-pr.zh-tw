---
title: 原則式管理原則儲存 | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, storage
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0e775d038c5bb4f7a467f2691e374296f1389d84
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699457"
---
# <a name="policy-based-management-storage"></a>原則式管理原則儲存
  原則會儲存在 msdb 資料庫中。 變更原則或條件之後，就應該備份 msdb。 如需詳細資訊，請參閱[系統資料庫的備份與還原 &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)。  
  
## <a name="storing-policies"></a>儲存原則  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 包含一些可用來監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的原則。 根據預設，這些原則不會安裝在上 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ; 不過，它們可以從 C:\Program 檔案的預設安裝位置匯入 (x86) \MICROSOFT SQL server\120\tools\policies\databaseengine\1033  
  
 您可以使用 [檔案/新增]  功能表來直接建立原則，然後將它們儲存至檔案。 當您沒有連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體時，這樣就可讓您建立原則。  
  
 在目前 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體中評估之原則的原則記錄會保存在 msdb 系統資料表中。 套用至其他 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體或套用至 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 之原則的原則記錄則不會保留。  
  
  
