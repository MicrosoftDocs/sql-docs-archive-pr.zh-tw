---
title: 網路封包大小不應超過 8060 個位元組 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 86db5da1-afe4-4fbb-8bf8-33cedc7e4361
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 01b500cbe65107767d73bc2901b6d5e028b94ee9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594002"
---
# <a name="network-packet-size-should-not-exceed-8060-bytes"></a>網路封包大小不應超過 8060 個位元組
  如果為 sp_configure 'network packet size' 指定的值或是任何已登入使用者的網路封包大小超過 8060 個位元組， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會執行不同的記憶體配置作業。 這會造成未保留給緩衝集區的處理序虛擬位置空間增加。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 網路封包大小不應超過 8060 個位元組。  
  
## <a name="for-more-information"></a>詳細資訊  
 [Microsoft 知識庫文章 903002](https://go.microsoft.com/fwlink/?linkid=117749)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
