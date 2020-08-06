---
title: 使用者資料庫上的對稱金鑰 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3333ab5b-2518-4753-a0a8-57df5e5af74f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ca0fb62ccb32ce244e1087281997dcd9929df89c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594001"
---
# <a name="symmetric-keys-on-user-databases"></a>使用者資料庫上的對稱金鑰
  此規則會檢查長度少於 128 個位元組的金鑰是否不使用 RC2 或 RC4 加密演算法。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 使用 AES 128 位元或更大的位元來建立對稱金鑰進行資料加密。 如果作業系統不支援 AES，請使用 3DES。  
  
## <a name="for-more-information"></a>詳細資訊  
 [選擇加密演算法](../security/encryption/choose-an-encryption-algorithm.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
