---
title: 裝置內容 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.bnrdevicecontents.f1
ms.assetid: 95e1902e-8c7a-4830-bdf9-1a6aca414a24
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c904718eca671b1965a95d0d400f3f6fa075b500
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595136"
---
# <a name="device-contents-sql-server"></a>裝置內容 (SQL Server)
  使用此對話方塊來檢視備份資訊。 這個資訊描述裝置、媒體、媒體集，以及備份組。  
  
 **若要使用 SQL Server Management Studio 檢視備份裝置的內容**  
  
-   [檢視備份磁帶或檔案的內容 &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>選項。  
 **媒體**  
 儲存備份資訊的磁碟或磁帶集。  
  
 **媒體順序**  
 列出媒體序號、家族序號，以及鏡像識別碼 (如果有的話)。 各個實體備份媒體都標記有媒體序號，指出媒體使用時的順序。 初始備份媒體標記為 1，第二個媒體 (第一個接續磁帶) 則標記為 2，依此類推。 還原備份組時，媒體序號可以確定進行還原的操作員，會以正確的順序主控正確的媒體。  
  
 **建立於**  
 顯示媒體日期。  
  
 **媒體集**  
 媒體集是已排序的備份媒體集合，其中使用固定數目的備份裝置寫入一個或多個備份作業。  
  
 **名稱**  
 顯示媒體集的名稱。  
  
 **說明**  
 顯示媒體集的描述。  
  
 **媒體家族計數**  
 顯示媒體家族計數。 各個媒體集皆是一個或多個媒體家族的集合。 所有輸出到給定的單一備份裝置 (或鏡像的備份裝置群組)，即形成一個單一媒體家族。 每個媒體集的個別裝置 (或鏡像裝置的群組) 都包含一個媒體家族；例如，若媒體集使用兩個非鏡像備份裝置，則此媒體集會包含兩個媒體家族。  
  
 **備份組**  
 顯示有關媒體上包含的備份組的資訊。 備份組是成功備份作業的結果，其內容會在備份裝置組的媒體之間散發。  
  
|頁首|值|  
|------------|------------|  
|**名稱**|備份組的名稱。|  
|**型別**|執行的備份類型：[完整]、[差異] 或 [交易記錄]。|  
|**元件**|備份的元件：Database、File 或 *\<blank>* (適用於交易記錄)。|  
|**Server**|執行備份作業之 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的名稱。|  
|**Database**|已備份資料庫的名稱。|  
|**位置**|備份組在磁碟區中的位置。|  
|**日期**|備份作業完成時的日期和時間，會出現在用戶端的地區設定中。|  
|**大小**|備份組的大小 (以位元組為單位)。|  
|**使用者名稱**|執行備份作業的使用者名稱。|  
|**到期**|備份組過期的日期和時間。|  
  
## <a name="see-also"></a>另請參閱  
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
