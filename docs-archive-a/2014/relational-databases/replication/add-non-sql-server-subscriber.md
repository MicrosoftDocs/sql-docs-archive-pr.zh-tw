---
title: 新增非 SQL Server 訂閱者 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.addnonsqlsubscriber.f1
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e36d048b11fcc71b27ab0ab2ee815b0284187c4d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596667"
---
# <a name="add-non-sql-server-subscriber"></a>加入非 SQL Server 訂閱者
  複寫可以支援為 Oracle 和 IBM DB2 訂閱者建立快照式和交易式發行集的發送訂閱。  
  
## <a name="options"></a>選項。  
 **要加入的訂閱者類型**  
 選取 Oracle 訂閱者或 IBM DB2 訂閱者。 如需這些訂閱者支援的詳細資訊，請參閱[非 SQL Server 訂閱者](non-sql/non-sql-server-subscribers.md)。  
  
 **資料來源名稱**  
 在用來尋找網路上之資料庫的名稱。 複寫會使用資料來源名稱，結合登入、密碼及您在此精靈的 **[散發代理程式安全性]** 頁面中指定的任何連接選項，來產生資料庫的連接字串。  
  
> [!NOTE]  
>  在散發代理程式嘗試初始化訂閱之前， [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會驗證資料來源名稱和連接字串。  
  
## <a name="see-also"></a>另請參閱  
 [為非 SQL Server 訂閱者建立訂閱](create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md)   
 [訂閱發行集](subscribe-to-publications.md)  
  
  
