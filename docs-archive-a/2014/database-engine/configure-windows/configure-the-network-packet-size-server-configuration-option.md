---
title: 設定 network packet size 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default packet size
- size [SQL Server], packets
- packets [SQL Server], size
- network packet size option
ms.assetid: 236985bf-fc4a-4a57-98f7-a71ef977fd7b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 69e5963675349bceff6a0ee022f6dc28da03db59
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87700210"
---
# <a name="configure-the-network-packet-size-server-configuration-option"></a>設定 network packet size 伺服器組態選項
  本主題描述如何 `network packet size` 使用或，在中設定 server configuration 選項 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 `network packet size`選項會設定在整個網路上使用的封包大小 (位元組) 。 封包是在用戶端與伺服器之間傳送要求與結果的固定大小資料區塊。 預設的封包大小為 4096 個位元組。  
  
> [!NOTE]  
>  除非確信有助於提升效能，否則請勿變更封包大小。 對於大部分應用程式而言，預設封包大小是最適當的大小。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用下列方法設定 network packet size 選項：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **後續操作：** [設定網路封包大小 選項之後](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   加密連接的最大 network packet size 為 16,383 個位元組。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   這個選項是進階選項，只有有經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術人員才可變更。  
  
-   如果應用程式進行大量複製作業，或是傳送或接收大量的文字或影像資料，則使用大於預設值的封包有助於改善效能，因為這樣可以減少網路讀取與寫入的作業。 如果應用程式傳送與接收的資訊量很少，可以將封包大小設定為 512 位元組，這對大部分資料傳輸而言已經足夠。  
  
-   在使用不同網路通訊協定的系統上，請將 [網路封包大小] 設定為最常用通訊協定的大小。 當網路通訊協定支援大型封包時，network packet size 選項可以改善網路效能。 用戶端應用程式可以覆寫此值。  
  
-   您也可以呼叫 OLE DB、開放式資料庫連接 (ODBC) 及 DB-Library 函數來要求變更封包大小。 如果伺服器無法支援要求的封包大小， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 將會傳送警告訊息給用戶端。 在某些情況下，變更封包大小可能會導致通訊連結失敗，例如以下狀況：  
  
     `Native Error: 233, no process is on the other end of the pipe.`  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-network-packet-size-option"></a>設定 network packet size 選項  
  
1.  在物件總管中，請以滑鼠右鍵按一下伺服器，然後選取 [屬性]。  
  
2.  按一下 **[進階]** 節點。  
  
3.  在 **[網路]** 下，為 **[網路封包大小]** 方塊選取一個值。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-network-packet-size-option"></a>設定 network packet size 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例示範如何使用 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 將 `network packet size` 選項的值設定為 `6500` 個位元組。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'network packet size', 6500 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)伺服器組態選項。  
  
##  <a name="follow-up-after-you-configure-the-network-packet-size-option"></a><a name="FollowUp"></a> 後續操作：設定網路封包大小選項之後  
 設定會立即生效，不需要重新啟動伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
