---
title: 合併成員暫存資料表 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- database [Master Data Services], attributes staging table
- attributes staging table [Master Data Services]
ms.assetid: 070681ed-be99-49ae-93bd-6402f2134ace
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7b2af1f783a6daa0b232e5e6970c72e4f5813435
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87701272"
---
# <a name="consolidated-member-staging-table-master-data-services"></a>合併成員暫存資料表 (Master Data Services)
  使用 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中的合併成員暫存資料表 (stg.name_Consolidated) 建立、更新、停用以及刪除合併成員。 您也可以用它來更新合併成員的屬性值。  
  
##  <a name="table-columns"></a><a name="TableColumns"></a>資料表資料行  
 下列資料表說明合併暫存資料表中各欄位的用途。  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|**識別碼**|自動指派的識別碼。 請勿在此欄位中輸入值。 如果尚未處理批次，這個欄位是空白。|  
|**ImportType**<br /><br /> 必要|決定在暫存資料符合 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中既存的資料時，該怎麼做。<br /><br /> **0**：建立新成員。 將現有的 MDS 資料取代為暫存資料，但唯有在暫存資料不是 NULL 的情況下。 系統會忽略 NULL 值。 若要將屬性值變更為 NULL，請使用 **~NULL~**。<br /><br /> **1**：只建立新成員。 對現有 MDS 資料的任何更新都將失敗。<br /><br /> **2**：建立新的成員。 將現有的 MDS 資料取代為暫存資料。 如果您匯入 NULL 值，它們會覆寫現有的 MDS 值。<br /><br /> **3**：依據字碼值停用成員。 將會維護所有屬性、階層和集合成員資格，以及交易，但已無法在使用者介面中使用。 如果成員當做另一個成員的網域屬性值使用，則停用將會失敗。<br /><br /> **4**：依據字碼值，永久刪除成員。 將會永久刪除所有屬性、階層和集合成員資格，以及交易。 如果成員當做另一個成員的網域屬性值使用，則刪除將會失敗。|  
|**ImportStatus_ID**<br /><br /> 必要|匯入程序的狀態。 可能的值包括：<br /><br /> **0**：您用來指定記錄已備妥，可供暫存。<br /><br /> **1**：自動指派，表示記錄的暫存處理序已成功。<br /><br /> **2**：自動指派，表示記錄的暫存處理序已失敗。|  
|**Batch_ID**<br /><br /> 只有 Web 服務需要|自動指派的識別碼，可用來將暫存的記錄分組。 批次中的所有成員都會被指派這個識別碼，這個識別碼會顯示在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 使用者介面的 **[識別碼]** 欄中。<br /><br /> 如果尚未處理批次，這個欄位是空白。|  
|**BatchTag**<br /><br /> 必要項，只有 Web 服務不需要|批次的唯一名稱 (最多 50 個字元)。|  
|**HierarchyName**<br /><br /> 必要|明確階層名稱。 每一個合併成員只能屬於一個階層。|  
|**ErrorCode**|顯示錯誤碼。 若要查詢 **ImportStatus_ID** 為 **2**的所有記錄，請參閱 [暫存處理序錯誤 &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md)。|  
|**Code**<br /><br /> 必要項，除非程式碼自動為 **ImportType1** 或 **2** 產生。如需詳細資訊，請參閱[自動建立代碼 &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md)。|成員的唯一代碼。|  
|**名稱**<br /><br /> 選擇性|成員的名稱。|  
|**NewCode**|唯有在您要變更成員代碼時才使用。|  
|\<Attribute name>|實體中的每個屬性都有一個資料行存在。 將其搭配 **ImportType****0** 或 **2**使用。 對於自由格式屬性，指定屬性的新文字或字串值。 對於網域屬性，指定將成為屬性之成員的代碼。 對於連結屬性，URL 開頭必須是 **http://**。<br /><br /> 注意：您無法暫存檔案屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [使用暫存進程在 Master Data Services 中載入或更新成員](add-update-and-delete-data-master-data-services.md)   
 [使用暫存進程 &#40;Master Data Services 來移動明確階層成員&#41;](add-update-and-delete-data-master-data-services.md)   
 [資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [查看暫存進程期間發生的錯誤 &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)   
 [暫存處理序錯誤 &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md)  
  
  
