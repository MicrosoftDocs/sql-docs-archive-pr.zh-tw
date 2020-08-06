---
title: 建立資料庫 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 617b3fe10a17ae2d8659b51e85cdb3fed4470506
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597938"
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>建立資料庫 (SQL Server 匯入和匯出精靈)
  使用 [**建立資料庫**] 頁面，即可為目的地檔案定義新的資料庫。  
  
 這個頁面提供建立新資料庫之可用選項的子集。 若要查看所有選項，請使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
 若要深入瞭解此嚮導，請參閱[SQL Server 匯入和匯出嚮導](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要瞭解啟動精靈的選項，以及成功執行嚮導所需的許可權，請參閱[執行 SQL Server 匯入和匯出嚮導](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>選項。  
 **名稱**  
 為目的地 SQL Server 資料庫提供唯一的名稱。 當您命名此資料庫時，請確認有遵循 SQL Server 慣例。  
  
 **資料檔名稱**  
 檢視資料檔的名稱。 這是從您在先前提供的資料庫名稱衍生的。  
  
 **記錄檔名稱**  
 檢視記錄檔的名稱。 這是從您在先前提供的資料庫名稱衍生的。  
  
 **初始大小 (資料檔)**  
 指定資料檔的初始大小 (以 MB 為單位)。  
  
 **不允許成長 (資料檔)**  
 指出資料檔是否可以成長超過指定的初始大小。  
  
 **成長百分比 (資料檔)**  
 指定資料檔可以成長的百分比。  
  
 **成長大小 (資料檔)**  
 指定資料檔可以成長的大小 (以 MB 為單位)。  
  
 **初始大小 (記錄檔)**  
 指定記錄檔的初始大小 (以 MB 為單位)。  
  
 **不允許成長 (記錄檔)**  
 指出記錄檔是否可以成長超過指定的初始大小。  
  
 **成長百分比 (記錄檔)**  
 指定記錄檔可以成長的百分比。  
  
 **成長大小 (記錄檔)**  
 指定記錄檔可以成長的大小 (以 MB 為單位)。  
  
  
