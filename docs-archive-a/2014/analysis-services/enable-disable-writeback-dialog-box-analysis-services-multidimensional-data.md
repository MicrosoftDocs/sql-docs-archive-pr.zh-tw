---
title: 啟用-停用回寫對話方塊 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitiondesigner.writebackenabledisable.f1
ms.assetid: 2d254393-3f0d-4b70-8b98-87159f9f3639
author: minewiskan
ms.author: owend
ms.openlocfilehash: 54ee4597ee78f45682730bd0e8d7119d204eaf2b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607130"
---
# <a name="enable-disable-writeback-dialog-box-analysis-services---multidimensional-data"></a>啟用-停用回寫對話方塊 (Analysis Services-多維度資料) 
  [啟用/停用回寫]**** 對話方塊會啟用或停用 Cube 中之量值群組的回寫。 啟用量值群組的回寫會為該量值群組定義一個回寫資料分割，並建立一個回寫資料表。 停用量值群組的回寫會移除回寫資料分割，但是不會刪除回寫資料表，以避免非預期的資料遺失。 執行下列動作即可顯示 [啟用/停用回寫]**** 對話方塊：  
  
-   在 Cube 設計師中，於[資料分割]**** 的 [量值群組]**** 窗格中按一下 [回寫設定]****。  
  
-   在 Cube 設計師中，於 [資料分割]**** 索引標籤的 [量值群組]**** 窗格內，以滑鼠右鍵按一下 [資料分割]**** 方格中的資料分割，然後從內容功能表選取 [回寫設定]****。  
  
## <a name="options"></a>選項  
 **資料表名稱**  
 鍵入要為所選取資料分割建立之回寫資料表的名稱。 回寫資料表會儲存用戶端應用程式對量值群組所做的變更。  
  
> [!NOTE]  
>  如果未啟用回寫，此選項會是停用的。  
  
 **資料來源**  
 選取要包含回寫資料表的資料來源。  
  
> [!NOTE]  
>  如果未啟用回寫，此選項會是停用的。  
  
 **新增**  
 按一下即可顯示 [連線管理員]**** 對話方塊，並定義要包含回寫資料表的新資料來源。  
  
> [!NOTE]  
>  如果未啟用回寫，此選項會是停用的。  
  
  
