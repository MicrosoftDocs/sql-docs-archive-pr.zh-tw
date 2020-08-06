---
title: MSSQLSERVER_3169 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "3169"
helpviewer_keywords:
- 3169 (Database Engine error)
ms.assetid: 7d4dbed6-bb94-4908-bc03-2040a9cf63bc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8b13d9c1c17eddb34648bc4a536e2fccf371b99a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596024"
---
# <a name="mssqlserver_3169"></a>MSSQLSERVER_3169
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|3169|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|NA|  
|訊息文字|資料庫是在執行 %ls 版的伺服器上備份。 該版本和此伺服器不相容，此伺服器目前執行 %ls 版。 請將資料庫還原到支援此備份的伺服器，或使用與此伺服器相容的備份。|  
  
## <a name="explanation"></a>說明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的某些功能會影響資料庫檔案的結構。 當您將資料庫還原到另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，檔案格式可能與不同的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 版本不相容。  
  
 例如，造成這項錯誤的原因可能是在較新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中使用 Vardecimal 儲存格式，然後嘗試在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 之前的版本中還原資料庫檔案。  
  
## <a name="user-action"></a>使用者動作  
 判斷原始伺服器上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 在中 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，以滑鼠右鍵按一下伺服器，然後按一下 [**屬性**] 或 [ `SELECT @@VERSION` 在查詢視窗中輸入]。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的原始版本開啟資料庫。 檢查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中原始資料庫上啟用的功能。 修改這些設定，以搭配用來還原資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。  
  
  
