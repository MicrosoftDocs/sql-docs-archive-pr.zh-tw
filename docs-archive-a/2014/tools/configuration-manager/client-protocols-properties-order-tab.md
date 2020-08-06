---
title: 用戶端通訊協定屬性 (順序] 索引標籤) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- client protocols [SQL Server]
ms.assetid: 64fd7135-1756-4885-bed9-9ab8997ecc6c
author: stevestein
ms.author: sstein
ms.openlocfilehash: a367cff3495389d1a707ed108ba75e1e736538b8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688370"
---
# <a name="client-protocols-properties-order-tab"></a>用戶端通訊協定屬性 (順序索引標籤)
  您可以使用 [用戶端通訊協定內容]**** 對話方塊上的 [順序]**** 頁面來檢視與啟用用戶端通訊協定。  
  
 按一下通訊協定，然後按一下 [啟用]  或 [停用]  ，將選取的通訊協定移到 [停用通訊協定]  或 [啟用通訊協定]  清單中。  
  
 系統會以所列的順序嘗試通訊協定，亦即先嘗試使用第一順位的通訊協定，然後再嘗試使用第二順位的通訊協定，依此類推。若要上移或下移 [啟用的通訊協定]  清單中的通訊協定，請按一下向上箭頭或向下箭頭按鈕。 當您從該電腦上的用戶端連接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，一律會先嘗試使用**共用記憶體**通訊協定 (若已啟用)。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET SqlClient 不會使用這些設定。 .NET SqlClient 的通訊協定順序最先是 TCP，接著是具名管道，您無法變更此順序。  
  
## <a name="options"></a>選項。  
 **停用的通訊協定**  
 列出已安裝但目前未使用的通訊協定。  
  
 **啟用的通訊協定**  
 列出 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 此電腦上用戶端可用的通訊協定。  
  
 **>**  
 啟用目前 [停用的通訊協定]  方塊中反白顯示的通訊協定，並將它移到 [啟用的通訊協定]  方塊。  
  
 **\<**  
 停用目前 [啟用的通訊協定]  方塊中反白顯示的通訊協定，並將它移到 [停用的通訊協定]  方塊。  
  
 向上箭頭  
 在清單中將反白顯示的通訊協定向上移動。 這樣可以提高所選取通訊協定的優先順序，網路程式庫會優先使用選取的通訊協定來進行連接。  
  
 向下箭頭  
 在清單中將反白顯示的通訊協定向下移動。 這樣可以降低所選取通訊協定的優先順序，網路程式庫會優先使用順序較高的其他通訊協定來進行連接。  
  
 **啟用共用記憶體通訊協定**  
 當您從該電腦的用戶端連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，系統會啟用總是優先嘗試的共用記憶體通訊協定 (若已啟用該協定)。  
  
> [!NOTE]  
>  若通訊協定是以前置詞或連接字串的一部份來指定，則只會嘗試使用指定的通訊協定。  
  
## <a name="see-also"></a>另請參閱  
 [選擇網路通訊協定](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
