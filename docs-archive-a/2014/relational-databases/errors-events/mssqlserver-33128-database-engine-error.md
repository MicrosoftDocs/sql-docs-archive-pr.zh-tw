---
title: MSSQLSERVER_33128 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 33128 (Database Engine error)
ms.assetid: 12c1096f-d120-439b-85f3-f794859503c9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 158cc609a18cf3fe7b76708e351b78263cd80a9e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595059"
---
# <a name="mssqlserver_33128"></a>MSSQLSERVER_33128
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|33128|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SEC_DEPRECATED_ALGO|  
|訊息文字|加密失敗。 金鑰使用已被取代而不再受支援的演算法 ' %.* ls'。|  
  
## <a name="explanation"></a>說明  
 參照 RC4 (或 RC4_128) 加密演算法時，會出現此訊息。 RC4 與 RC4_128 加密演算法提供的保護很弱，已被取代。 請改用較強的演算法，例如其中一種 AES 演算法。  
  
 當資料庫相容性層級設定為 90 或 100 時，作業成功執行後會引發取代事件，接著只會於信號緩衝區中顯示此訊息。  
  
 當資料庫相容性層級為 110 以上時，取代作業成功後會引發取代事件，接著只會於信號緩衝區中顯示此訊息。 加密作業將會失敗並會引發取代事件，接著使用者會看見此訊息，而信號緩衝區中也會顯示此訊息。  
  
> [!NOTE]  
>  信號緩衝區是一個內部元件，不會進行完整記錄，也並非供客戶之用。 當您連絡 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客戶支援時，信號緩衝區中的訊息將提供有用協助。 若要檢視信號緩衝區，請查詢 sys.dm_os_ring_buffers 動態管理檢視。  
  
|State|描述|  
|-----------|-----------------|  
|1|內建的 encryptbykey() 函式中使用 RC4 金鑰。 內建函數傳回 NULL。 此訊息僅會顯示於信號緩衝區中。|  
|2|內建的 decryptbykey() 函式中使用 RC4 金鑰。 此訊息僅會顯示於信號緩衝區中。|  
|3|已被取代的 RC4 金鑰正由對稱金鑰加密中。 使用者可看見，也會顯示於信號緩衝區中。 已被取代的 RC4 對稱金鑰不能改變相容性層級為 110。 嘗試使用非 RC4 金鑰進行加密作業。 請視需要將回溯相容性層級設定為 90 或 100。|  
|4|非 RC4 金鑰正由已被取代的 RC4 對稱金鑰加密中。 使用者可看見，也會顯示於信號緩衝區中。 將應用程式修改為使用非 RC4 對稱金鑰，或將回溯相容性層級設定為 90 或 100。|  
|5|已被取代的 RC4 金鑰正由對稱金鑰解密中。 此訊息僅會顯示於信號緩衝區中。|  
|6|非 RC4 金鑰正由 RC4 對稱金鑰解密中。 此訊息僅會顯示於信號緩衝區中。|  
|7|RC4 對稱金鑰正由憑證加密中。 使用者可看見，也會顯示於信號緩衝區中。|  
|8|RC4 對稱金鑰正由憑證解密中。 此訊息僅會顯示於信號緩衝區中。|  
|9|RC4 對稱金鑰正由 EKM 金鑰加密中。|  
|10|RC4 對稱金鑰正由 EKM 金鑰解密中。 此訊息僅會顯示於信號緩衝區中。|  
  
## <a name="user-action"></a>使用者動作  
 請改用較強的演算法，例如其中一種 AES 演算法。 (建議使用)  
  
 使用 ALTER DATABASE SET COMPATIBILITY_LEVEL 將資料庫相容性層級設定為 100 (不建議使用)。  
  
  
