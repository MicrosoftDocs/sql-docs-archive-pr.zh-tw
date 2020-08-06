---
title: 升級會將 SQL Server Agent 的使用者 Proxy 帳戶變更為暫時的 UpgradedProxyAccount |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server Agent]
ms.assetid: cd2d08c3-4e56-4034-8b68-0c78df8b5471
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2bca80580a50f2acebed1b6fbea2dec1f6458dbc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584970"
---
# <a name="upgrading-will-change-the-sql-server-agent-user-proxy-account-to-the-temporary-upgradedproxyaccount"></a>升級會將 SQL Server Agent 使用者 Proxy 帳戶變更為暫時的 UpgradedProxyAccount
  升級之後，已啟用記錄傳送的資料庫維護計劃將無法啟用。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>描述  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供一組與資料庫維護計劃不直接相容的新記錄傳送功能。  
  
## <a name="corrective-action"></a>更正動作  
 擁有包含記錄傳送功能之資料庫維護計劃的 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 使用者應該使用新的功能來設定記錄傳送。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜記錄傳送＞。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 記錄傳送作業類別目錄會導致升級失敗](../../../2014/sql-server/install/sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail.md)   
 [升級之後，不會執行記錄傳送](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)  
  
  
