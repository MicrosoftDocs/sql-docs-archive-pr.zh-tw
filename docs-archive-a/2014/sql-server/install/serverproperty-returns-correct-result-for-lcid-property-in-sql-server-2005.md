---
title: SERVERPROPERTY 會針對 SQL Server 2005 中的 LCID 屬性傳回正確的結果 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SERVERPROPERTY function
ms.assetid: 833a2fc9-b480-4697-aa7b-9677e78ee0b4
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ebb125a86e6e30f2c3638004593da7657f02f1a6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87700624"
---
# <a name="serverproperty-returns-correct-result-for-lcid-property-in-sql-server-2005"></a>在 SQL Server 2005 中，SERVERPROPERTY 會傳回 LCID 屬性的正確結果
  如果 SERVERPROPERTY('LCID') 是在二進位定序伺服器上執行，則此函數會傳回對應於伺服器定序的 Windows 地區設定識別碼 (LCID)。  
  
> [!NOTE]  
>  對於包含 SERVERPROPERTY ('LCID') 的參考且在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之其他執行個體上執行的批次和追蹤檔案，只有在其他執行個體具有與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之目前執行個體相同的定序時，Upgrade Advisor 才會偵測此行為變更。  
  
## <a name="corrective-action"></a>更正動作  
 請修改應用程式以預期 SERVERPROPERTY('LCID') 會傳回對應至伺服器定序的 Windows LCID。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
