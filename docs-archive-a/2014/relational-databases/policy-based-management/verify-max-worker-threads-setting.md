---
title: 驗證最大工作者執行緒設定 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 2d94adfd-3ba1-493a-b29a-b436f9d583df
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5dbffb87f58d2beb633f43ff18680222ea62cf5e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593986"
---
# <a name="verify-max-worker-threads-setting"></a>確認最大工作者執行緒設定
  此規則會檢查 max worker threads server 選項中是否可能有不正確的設定。 將 max worker threads 選項設定為很小的值可能會阻礙足夠的執行緒及時服務內送用戶端要求，而且可能會導致執行緒資源用盡。 但是，將此選項設定為較大的值可能會浪費位址空間，因為每一個使用中執行緒都會在 32 位元伺服器上耗用 512 KB 空間，並在 64 位元伺服器上最多耗用 4 MB 空間。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 將 max worker threads 選項設成 0。 如此可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 根據使用者要求來自動判斷 active worker threads 的正確數目。  
  
## <a name="for-more-information"></a>詳細資訊  
 [設定 max worker threads 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
