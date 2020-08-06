---
title: 如何為 CDC 準備 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a327fa18-58f4-4e69-bb87-44faf47e20ef
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fbd285faaa55a28ad82beb673fa783570809bd04
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686459"
---
# <a name="how-to-prepare-sql-server-for-cdc"></a>如何為 CDC 準備 SQL Server
  Oracle CDC 服務要求所有目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體都必須包含 MSXDBCDC 資料庫。 您可在 CDC 服務組態主控台中使用「準備 SQL Server」動作來建立這個資料庫。每一個目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體只會執行這項工作一次。  
  
 以下描述如何使用 CDC 服務組態主控台針對 Oracle 異動資料擷取來準備 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 這個程序會建立 MSXDBCDC 資料庫，並定義所需的資料表、預存程序和其他必要成品。  
  
 為 Oracle CDC 準備 SQL Server 是由 Oracle CDC 服務管理員所執行。 如需 CDC 服務系統管理員角色的詳細資訊，請參閱[適用於 Oracle 的異動資料擷取服務的使用者角色（依 Attunity](user-roles.md)）。  
  
### <a name="to-enable-sql-server-for-cdc"></a>若要為 CDC 啟用 SQL Server  
  
1.  從 **[開始]** 功能表，選取 **[Oracle CDC 服務組態]** 。  
  
2.  從左窗格中選取 **[動作]** 窗格中的 **[本機 CDC 服務]** ，然後按一下 **[準備 SQL Server]** 。  
  
     您也可以用滑鼠右鍵按一下 [本機 CDC 服務]  ，並選取 [準備 SQL Server]  。  
  
3.  請在 [為 Oracle CDC 準備 SQL Server 執行個體] 對話方塊中輸入必要的資訊。 如需有關如何在此對話方塊中輸入必要資訊的詳細資訊，請參閱＜ [Prepare SQL Server for CDC](prepare-sql-server-for-cdc.md)＞。  
  
     若要為 Oracle CDC 準備 SQL Server 執行個體，登入必須擁有 MSXDBCDC 資料庫的寫入權限。 請輸入擁有 MSXDBCDC 資料庫寫入權限之登入的認證，例如 `sysasmin` 角色的成員。  
  
 **注意**：您可以按一下 [檢視指令碼]  ，檢視設定指令碼的唯讀版本。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員可以將此指令碼複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理主控台來編輯和執行 (必要的話)。  
  
## <a name="see-also"></a>另請參閱  
 [準備 SQL Server 以使用 CDC](prepare-sql-server-for-cdc.md)  
  
  
