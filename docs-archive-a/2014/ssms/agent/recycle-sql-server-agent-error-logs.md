---
title: 回收 SQL Server Agent 錯誤記錄檔 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2b30f0a2ba9a2d861d4a36a86489757cde512fea
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606563"
---
# <a name="recycle-sql-server-agent-error-logs"></a>回收 SQL Server Agent 錯誤記錄檔
  使用此頁面來回收 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 錯誤記錄檔。 回收記錄檔時會關閉目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 錯誤記錄檔，並在未重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務的情況下，啟動新的錯誤記錄檔。 請注意， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會保留九個最新的錯誤記錄檔。 如果已經有九個錯誤記錄檔存在，回收錯誤記錄檔會造成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 移除最舊的錯誤記錄檔。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 錯誤記錄檔](sql-server-agent-error-log.md)  
  
  
