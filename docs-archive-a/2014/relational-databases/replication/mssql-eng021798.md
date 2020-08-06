---
title: MSSQL_ENG021798 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021798 error
ms.assetid: 596f5092-75ab-4a19-8582-588687c7b089
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 327b4a373c28376701ea12400215ab00367df66a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87697924"
---
# <a name="mssql_eng021798"></a>MSSQL_ENG021798
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|21798|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|必須先透過 '%s' 新增 '%s' 代理程式工作，方可繼續。 請參閱 '%s' 的文件集。|  
  
## <a name="explanation"></a>說明  
 若要建立發行集，您必須是「發行者」上 **sysadmin** 固定伺服器角色的成員，或是發行集資料庫中 **db_owner** 固定資料庫角色的成員。 如果您是 **db_owner** 角色的成員，則以下情況會引發此錯誤：  
  
-   您會從 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]執行指令碼。 安全性模型在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中已變更，同時必須更新這些指令碼。  
  
-   執行預存程序 **sp_addpublication** 之後，再執行 [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql)。 適用於所有交易式發行集。  
  
-   執行預存程序 **sp_addpublication** 之後，再執行 [sp_addqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql)。 這適用于已針對佇列更新訂閱啟用的交易式發行集 (**@allow_queued_tran** **sp_addpublication**) 的參數值為 TRUE。  
  
 預存程序 **sp_addlogreader_agent** 和 **sp_addqreader_agent** 將分別建立一個代理程式作業，可讓您指定執行代理程式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶。 對於 **sysadmin** 角色的使用者，如果 **sp_addlogreader_agent** 和 **sp_addqreader_agent** 未執行，代理程式作業將以隱含的方式建立；代理程式會在「散發者」端的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶內容中執行。 儘管 **sysadmin** 角色的使用者不需要 **sp_addlogreader_agent** 和 **sp_addqreader_agent** ，但基於安全性考量，最好是為代理程式指定單獨的帳戶。 如需詳細資訊，請參閱 [複寫代理程式安全性模型](security/replication-agent-security-model.md)。  
  
## <a name="user-action"></a>使用者動作  
 確保您以正確的順序執行程序。 如需詳細資訊，請參閱[建立發行](publish/create-a-publication.md)集、更新這些腳本以包含 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本所需的預存程式和參數。 如需詳細資訊，請參閱[升級複寫指令碼 &#40;複寫 Transact-SQL 程式設計&#41;](administration/upgrade-replication-scripts-replication-transact-sql-programming.md)。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
