---
title: 存取 CDC 設計工具主控台 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- accMsDes
ms.assetid: b168c64e-c1b5-42d4-a92a-84de1dd0324e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7f4f6e4df0a514cb29e36bcd1270b2537dc3ba68
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708561"
---
# <a name="access-the-cdc-designer-console"></a>存取 CDC 設計工具主控台
  您可以從安裝 CDC 設計工具主控台的電腦來存取此主控台。 如需有關安裝的詳細資訊，請參閱＜安裝＞。  
  
 當您開啟 CDC 設計工具主控台時，隨即開啟 [連接到 SQL Server] 對話方塊。  
  
 存取 [CDC 設計工具] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入必須擁有 MSXDBCDC 資料庫的 UPDATE 權限。 此外，此登入也必須擁有 `dbcreator` 固定伺服器角色，才能建立新的 Oracle CDC 執行個體。 建議最好讓此登入也具備正在使用之 CDC 資料庫的 SELECT 權限，否則使用者將無法檢視這些資料庫的狀態。  
  
 在 [連接到 SQL Server] 對話方塊中輸入以下資訊。  
  
### <a name="server-name"></a>伺服器名稱  
 輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所在的伺服器名稱。  
  
### <a name="authentication"></a>驗證  
 選取下列其中一個：  
  
-   **Windows 驗證**  
  
-   **SQL Server 驗證**：如果您選取這個選項，必須針對您所連接之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的使用者輸入**登入**和**密碼**。  
  
 此登入擁有的資料庫角色必須允許存取 MSXCDCDB 資料庫。 建議最好讓此登入也能存取正在使用的其他任何資料庫，否則使用者將無法檢視這些資料庫中的資料。  
  
### <a name="options"></a>選項。  
 按一下箭頭即可檢視要設定的可用選項。 您可以選擇保留這些選項的預設值。 可用的選項如下：  
  
 **連接逾時**  
 輸入 Oracle CDC 服務在逾時之前等候連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的時間 (以秒數為單位)。預設值為 **15**。  
  
 **執行逾時**  
 輸入 Oracle CDC Windows 服務在逾時之前，等候執行命令的時間 (以秒數為單位)。預設值是 **30**。  
  
 **加密連接**  
 針對 Oracle CDC 服務與使用加密連線之目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間的通訊選取 [加密連線]  。**進階**：按一下 [進階]  ，並在必要時，於 [進階連接屬性] 對話方塊中輸入其他任何連接屬性。  
  
 **進階**  
 按一下 [進階]  ，並在必要時，於 [進階連接屬性] 對話方塊中輸入其他任何連接屬性。  
  
 如需 [進階連接屬性] 對話方塊的資訊，請參閱 [進階連接屬性](advanced-connection-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 連接所需的 CDC 設計工具權限](sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  
