---
title: MSSQL_ENG020574 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG02574 error
ms.assetid: 4e98f8de-287c-4090-81ee-dc8f80dfa6a1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8e224e9a87d40fa826a05c669216649c45185037
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606788"
---
# <a name="mssql_eng020574"></a>MSSQL_ENG020574
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|20574|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|訂閱者 '%s' 訂閱的發行項 '%s' (在發行集 '%s' 中)，未通過資料驗證。|  
  
## <a name="explanation"></a>說明  
 訂閱者端的資料是依據發行者端的資料進行驗證，而資料不相符，因此驗證失敗。 如需驗證的相關資訊，請參閱 [Validate Replicated Data](validate-data-at-the-subscriber.md)。  
  
## <a name="user-action"></a>使用者動作  
 建議您採取下列動作︰  
  
-   判斷驗證失敗的原因。  
  
-   更正導致失敗的根本問題。  
  
-   重新初始化訂閱或透過其他方法，讓資料聚合。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
