---
title: SQL Server 2014 中管理工具功能的重大變更 |Microsoft Docs
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 3ff3fad8-b569-4516-bd58-5a3efeb537e2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0487b6ab0958e0b83d4e8e34be507b5b3211ac87
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597381"
---
# <a name="breaking-changes-to-management-tools-features-in-sql-server-2014"></a>SQL Server 2014 中管理工具功能的突破性變更
  此主題描述管理工具功能的突破性變更。 這些變更可能會中斷以舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]為根據的應用程式、指令碼或功能。 當您升級時可能會遇到這些問題。 如需詳細資訊，請參閱＜ [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)＞。  
  
## <a name="breaking-changes-in-sssql14"></a> 的最新變更  
 將於日後提供資訊。  
  
## <a name="breaking-changes-in-sssql11"></a> 的最新變更  
  
### <a name="you-cannot-use-sssql11-management-tools-to-create-a-utility-control-point-on-a-sskilimanjaro-instance-of-sql-server"></a>您無法在 SQL Server 的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 執行個體上，使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 管理工具建立公用程式控制點。  
 若要在 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]的執行個體上建立公用程式控制點，請使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 管理工具。  
  
### <a name="smo-has-been-reversioned-in-sssql11"></a>SMO 已經在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中還原  
 使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 或更早版本的 SMO 所開發的程式碼必須稍微修改，才能針對 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 進行建立。 如需詳細資訊，請參閱 [Backward Compatibility in SMO](../relational-databases/server-management-objects-smo/backward-compatibility-in-smo.md)。  

## <a name="breaking-changes-in-sql-server-2005"></a><a name="previous-versions"></a>SQL Server 2005 中的重大變更  

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>另請參閱  
 [回溯相容性](../../2014/getting-started/backward-compatibility.md)  
 [深入瞭解 SQL Server 2014 中管理工具功能的重大變更](breaking-changes-to-database-engine-features-in-sql-server-2016.md?view=sql-server-2014)  
  
  
