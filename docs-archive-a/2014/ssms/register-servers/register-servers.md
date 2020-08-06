---
title: 註冊伺服器
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqlserverregisteredserver.dhelp
helpviewer_keywords:
- connections [SQL Server], registered servers
- registering servers
- servers [SQL Server], registering
- server management [SQL Server], registering servers
- server registration [SQL Server]
ms.assetid: c2a2513e-fa09-419c-99e7-a12d57c5a0db
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f4b23ba127c6b000b0abbe832c4c072ada78c5e6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594314"
---
# <a name="register-servers"></a>註冊伺服器
  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中註冊伺服器可讓您儲存伺服器連接資訊，以供未來連接使用。在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中註冊伺服器的方法有三種。  
  
1.  在安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後，第一次啟動時就會自動註冊 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的本機執行個體。  
  
2.  您也可以隨時初始化自動註冊處理序，以還原本機伺服器執行個體的註冊。  
  
3.  最後，您還可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的 [已註冊的伺服器] 工具來註冊伺服器。  
  
## <a name="benefits-of-registered-servers"></a>已註冊伺服器的優點  
 您可以利用已註冊的伺服器來執行下列動作：  
  
-   註冊伺服器來保留連接資訊。  
  
-   判斷已註冊的伺服器是否在執行中。  
  
-   輕易將物件總管和查詢編輯器連接到已註冊的伺服器。  
  
-   編輯或刪除已註冊的伺服器之登錄資訊。  
  
-   建立伺服器群組。  
  
-   在有別於 [伺服器名稱] 清單的 [已註冊的伺服器名稱] 方塊中提供一個值，以提供已註冊的伺服器之使用者易讀的名稱。  
  
-   提供已註冊的伺服器的詳細說明。  
  
-   提供已註冊的伺服器群組的詳細說明。  
  
-   匯出已註冊的伺服器群組。  
  
-   匯入已註冊的伺服器群組。  
  
-   檢視線上或離線 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記錄檔。  
  
## <a name="related-tasks"></a>相關工作  
 若要開始使用已註冊的伺服器，請使用下列主題：  
  
|**說明**|**主題**|  
|---------------------|---------------|  
|註冊本機伺服器執行個體|[註冊連接的伺服器 &#40;SQL Server Management Studio&#41;](register-a-connected-server-sql-server-management-studio.md)|  
|註冊伺服器|[建立新的已註冊伺服器 &#40;SQL Server Management Studio&#41;](create-a-new-registered-server-sql-server-management-studio.md)|  
|檢視已註冊的伺服器|[在 SQL Server Management Studio 中檢視已註冊的伺服器](view-registered-servers-in-sql-server-management-studio.md)|  
|移除已註冊的伺服器|[移除已註冊的伺服器 &#40;SQL Server Management Studio&#41;](remove-a-registered-server-sql-server-management-studio.md)|  
|變更伺服器的註冊|[變更伺服器的註冊 &#40;SQL Server Management Studio&#41;](change-a-server-s-registration-sql-server-management-studio.md)|  
|連接到已註冊的伺服器|[連接至已註冊的伺服器 &#40;SQL Server Management Studio&#41;](connect-to-a-registered-server-sql-server-management-studio.md)|  
|中斷與已註冊伺服器的連接|[中斷與註冊伺服器的連接 &#40;SQL Server Management Studio&#41;](disconnect-from-a-registered-server-sql-server-management-studio.md)|  
|移動已註冊的伺服器或伺服器群組|[移動已註冊的伺服器或已註冊的伺服器群組 &#40;SQL Server Management Studio&#41;](move-a-registered-server-or-registered-server-group.md)|  
|變更已註冊伺服器或伺服器群組的名稱|[變更已註冊的伺服器或已註冊的伺服器群組名稱 &#40;SQL Server Management Studio&#41;](change-the-name-of-registered-server-or-registered-server-group.md)|  
|建立或編輯伺服器群組|[建立或編輯伺服器群組 &#40;SQL Server Management Studio&#41;](create-or-edit-a-server-group-sql-server-management-studio.md)|  
|移除伺服器群組|[移除伺服器群組 &#40;SQL Server Management Studio&#41;](remove-a-server-group-sql-server-management-studio.md)|  
|匯出已註冊的伺服器資訊|[匯出已註冊的伺服器資訊 &#40;SQL Server Management Studio&#41;](export-registered-server-information-sql-server-management-studio.md)|  
|匯入已註冊的伺服器資訊|[匯入已註冊的伺服器資訊 &#40;SQL Server Management Studio&#41;](import-registered-server-information-sql-server-management-studio.md)|  
|建立中央管理伺服器和伺服器群組|[建立中央管理伺服器與伺服器群組 &#40;SQL Server Management Studio&#41;](create-a-central-management-server-and-server-group.md)|  
|同時對多部伺服器執行陳述式|[同時針對多部伺服器執行陳述式 &#40;SQL Server Management Studio&#41;](execute-statements-against-multiple-servers-simultaneously.md)|  
  
## <a name="see-also"></a>另請參閱  
 [遠端伺服器](../../database-engine/configure-windows/remote-servers.md)  
  
  
