---
title: 在同步處理期間執行指令碼 (複寫 Transact-SQL 程式設計) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- synchronization [SQL Server replication], scripts
- scripts [SQL Server replication], synchronization and
- sp_addscriptexec
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4bc217ad160a0238cc4247600d65eb32f156071f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585846"
---
# <a name="execute-scripts-during-synchronization-replication-transact-sql-programming"></a>在同步處理期間執行指令碼 (複寫 Transact-SQL 程式設計)
  複寫可支援視需要針對交易式與合併式發行集的訂閱者執行指令碼。 這項功能會將指令碼複製到複寫工作目錄，然後使用 **sqlcmd** 將指令碼套用到訂閱者。 依預設，如果針對交易式發行集的訂閱套用指令碼時發生失敗，則散發代理程式將會停止。 您可以使用複寫預存程序以程式設計的方式指定要執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。  
  
### <a name="to-specify-a-script-to-run-for-all-subscribers-to-a-snapshot-transactional-or-merge-publication"></a>針對快照式、交易式或合併式發行集的所有訂閱者指定要執行的指令碼  
  
1.  撰寫及測試將會視需要執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。  
  
2.  將指令碼檔案儲存到可由發行集之快照集代理程式存取的位置。  
  
3.  在發行集資料庫的發行者上，執行 [sp_addscriptexec &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql)。 針對** \@ scriptfile**指定** \@ 發行**集、在步驟2中為其建立完整 UNC 路徑的指令檔名，以及** \@ skiperror**的下列其中一個值：  
  
    -   **0** - 如果遇到錯誤，代理程式將會停止執行指令碼。  
  
    -   **1** - 如果遇到錯誤，代理程式將會記錄錯誤並繼續執行指令碼。  
  
4.  當下一次執行代理程式來同步處理訂閱時，指定的指令碼將會在每一個訂閱者上執行。  
  
## <a name="see-also"></a>另請參閱  
 [同步處理資料](synchronize-data.md)  
  
  
