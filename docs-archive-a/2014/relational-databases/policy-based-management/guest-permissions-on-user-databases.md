---
title: 使用者資料庫的 Guest 權限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 540f1c6d-df51-497e-958a-3a0f429d2920
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 344c5fd0639876998f1585c32fac5f7599f664e7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591986"
---
# <a name="guest-permissions-on-user-databases"></a>使用者資料庫的 Guest 權限
  此規則會判斷 guest 使用者是否有權存取資料庫。 此規則只適用於使用者資料庫。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 撤銷 guest 使用者存取資料庫的權限 (如果不需要的話)。  
  
 雖然您不能卸除 guest 使用者，但是可以在 master、tempdb 或 msdb 以外的任何資料庫中執行 REVOKE CONNECT FROM GUEST 來撤銷其 CONNECT 權限，以停用 guest 使用者。  
  
## <a name="for-more-information"></a>詳細資訊  
 [保護 SQL Server 的安全](../security/securing-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
