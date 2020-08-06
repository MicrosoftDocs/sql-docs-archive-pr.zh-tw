---
title: 卸離資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.detachdatabase.f1
helpviewer_keywords:
- database detaching [SQL Server]
- detaching databases [SQL Server]
ms.assetid: f63d4107-13e4-4bfe-922d-5e4f712e472d
author: stevestein
ms.author: sstein
ms.openlocfilehash: b8acc809b881012d18f78995bb8e521337fb02ee
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606871"
---
# <a name="detach-a-database"></a>卸離資料庫
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中卸離資料庫。 卸離的檔案會保留下來，您可以使用 CREATE DATABASE 搭配 FOR ATTACH 或 FOR ATTACH_REBUILD_LOG 選項來重新附加它。 您可以將這些檔案移到另一部伺服器，將它附加在那裡。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目卸離資料庫：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
 如需限制事項的清單，請參閱 [資料庫卸離與附加 &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)中卸離資料庫。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要 db_owner 固定資料庫角色中的成員資格。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-detach-a-database"></a>若要卸離資料庫  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 物件總管中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體，然後展開執行個體。  
  
2.  展開 **[資料庫]** ，並選取您想要卸離的使用者資料庫名稱。  
  
3.  以滑鼠右鍵按一下資料庫名稱，並指向**工作**，然後按一下 [卸離]。 **[卸離資料庫]** 對話方塊隨即出現。  
  
     **要卸離的資料庫**  
     列出要卸離的資料庫。  
  
     **Database Name**  
     顯示要卸離的資料庫名稱。  
  
     **卸除連接**  
     中斷到指定資料庫的連接。  
  
    > [!NOTE]  
    >  您無法卸離具有使用中連接的資料庫。  
  
     **更新統計資料**  
     依預設，卸離作業會在卸離資料庫時保留任何過時的最佳化統計資料。若要更新現有的最佳化統計資料，請按一下此核取方塊。  
  
     **保留全文檢索目錄**  
     依預設，卸離作業會保留與該資料庫關聯的所有全文檢索目錄。 若要移除這些全文檢索目錄，請清除 **[保留全文檢索目錄]** 核取方塊。 只有當您從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]升級資料庫時，才會出現這個選項。  
  
     **狀態**  
     顯示下列其中一個狀態：[就緒] 或 [未就緒]。  
  
     **訊息**  
     **[訊息]** 資料行可以顯示有關資料庫的資訊，如下所示：  
  
    -   當資料庫涉及複寫時， **[狀態]** 為 **[尚未備妥]** 且 **[訊息]** 資料行會顯示 **[資料庫已複寫]** 。  
  
    -   當資料庫有一或多個使用中的連線時，[狀態] 為 [未就緒] 且 [訊息] 資料行顯示 [<使用中連線數目> 個使用中的連線]，例如：[1 個使用中的連線]。 您必須選取 **[卸除連接]** 中斷任何使用中的連接之後，才能卸離資料庫。  
  
     若要取得有關訊息的詳細資訊，請按一下超連結文字，以開啟活動監視器。  
  
4.  當您準備卸離資料庫時，請按一下 **[確定]** 。  
  
> [!NOTE]  
>  重新整理檢視之前，仍可在 [物件總管] 的 **[資料庫]** 節點中看見最新卸離的資料庫。 您可以隨時重新整理檢視：按一下 [物件總管] 窗格，並從功能表列選取 [檢視]，然後選取 [重新整理]。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-detach-a-database"></a>若要卸離資料庫  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例會以 skipchecks 設為 true 來卸離 AdventureWorks2012 資料庫。  
  
```  
EXEC sp_detach_db 'AdventureWorks2012', 'true';  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料庫卸離和附加 &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)   
 [sp_detach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql)  
  
  
