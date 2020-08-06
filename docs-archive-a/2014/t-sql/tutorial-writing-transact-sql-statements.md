---
title: 教學課程：撰寫國際性通用的 Transact-SQL 陳述式 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL statements, tutorials
- Transact-SQL tutorials
- tutorials [Transact-SQL]
ms.assetid: 2addc9be-67d0-423d-a457-192fe9d7d058
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ac190d6099bca1a38ca2f286e6ce048fe5322e2a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708862"
---
# <a name="tutorial-writing-transact-sql-statements"></a>教學課程：撰寫國際性通用的 Transact-SQL 陳述式
  歡迎使用「撰寫 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式」教學課程。 本教學課程的主要對象是撰寫 SQL 陳述式的新手， 會透過檢閱一些建立資料表及插入資料的基本陳述式，協助新手上路。 本教學課程採用 [!INCLUDE[tsql](../includes/tsql-md.md)]，是 SQL 標準的 [!INCLUDE[msCoName](../includes/msconame-md.md)] 實作。 本教學課程的目的是用來概述 [!INCLUDE[tsql](../includes/tsql-md.md)] 語言，而非用來取代 [!INCLUDE[tsql](../includes/tsql-md.md)] 類別。 在本教學課程中的陳述式是有意經過簡化的，並無意呈現一般實際資料庫中所遇到的複雜問題。  
  
> [!NOTE]  
>  資料庫的新手通常會發現使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 處理 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 反而比撰寫 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式更容易。  
  
## <a name="finding-more-information"></a>尋找詳細資訊  
 若要尋找任何特定陳述式的詳細資訊，請在《SQL Server 線上叢書》中依名稱搜尋陳述式，或是使用 [內容] 瀏覽 [Transact-SQL 參考 &#40;Database Engine&#41;](/sql/t-sql/language-reference) 底下依字母順序排列的 1,800 個語言元素。 此外，搜尋與您有興趣的主題內容相關的關鍵字，也是另一種找出資訊的不錯方式。 例如，您想要知道如何傳回一部分的日期 (如月份)，您可以搜尋 **dates [SQL Server]** 的索引，然後選取 **dateparts**， 即會帶您前往 [DATEPART &#40;Transact-SQL&#41;](/sql/t-sql/functions/datepart-transact-sql) 主題。 例如若要找出如何使用字串，您可以搜尋 **字串函數**， 即會帶您前往[字串函數 &#40;Transact-SQL&#41;](/sql/t-sql/functions/string-functions-transact-sql) 主題。  
  
## <a name="what-you-will-learn"></a>學習內容  
 本教學課程會示範如何建立資料庫、在資料庫中建立資料表、插入資料至資料表、更新資料、讀取資料、刪除資料，然後刪除資料表。 您將建立檢視和預存程序，並將使用者設定到資料庫及資料。  
  
 本教學課程分成三個課程：  
  
 [課程 1：建立資料庫物件](lesson-1-creating-database-objects.md)  
 在這一課，您會建立資料庫、在資料庫中建立資料表、插入資料至資料表、更新資料以及讀取資料。  
  
 [課程 2：設定資料庫物件的權限](lesson-2-configuring-permissions-on-database-objects.md)  
 在這一課，您會建立登入及使用者， 也會建立檢視和預存程序，然後將使用者權授與預存程序。  
  
 [課程 3：刪除資料庫物件](lesson-3-1-deleting-database-objects.md)  
 在這一課，您會移除資料的存取、從資料表中刪除資料、刪除資料表，最後刪除資料庫。  
  
## <a name="requirements"></a>需求  
 為了完成本教學課程，您並不需要精通 SQL 語言，但必須了解基本資料庫概念 (如資料表)。 在進行本教學課程期間，您將建立資料庫以及建立 Windows 使用者。 這些工作需要高層權限，因此您必須以系統管理員的身份登入電腦。  
  
 另外，系統必須有安裝下列程式：  
  
-   任何版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或 Management Studio Express。  
  
-   Internet Explorer 6 或更新版本。  
  
> [!NOTE]  
>  當您查看教學課程時，建議您在檔檢視器工具列上加入 [**下一個]** 和 [**上一個**] 按鈕。  
  
  
