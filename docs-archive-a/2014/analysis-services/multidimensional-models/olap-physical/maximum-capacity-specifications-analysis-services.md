---
title: " (Analysis Services) 的最大容量規格 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], maximum number
- objects [Analysis Services], maximum size
ms.assetid: 49fe1673-b908-4c7a-88ff-415efd294d27
author: minewiskan
ms.author: owend
ms.openlocfilehash: d0495ed563585a5b7427655428a257174673fc02
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598593"
---
# <a name="maximum-capacity-specifications-analysis-services"></a>最大容量規格 (Analysis Services)
  下表指定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 元件中的不同伺服器部署模式下，所定義之各種物件的大小和數目上限。  
  
 本主題包含下列幾節：  
  
 [多維度和資料採礦 (DeploymentMode=0)](#bkmk_OLAP)  
  
 [SharePoint (DeploymentMode=1)](#bkmk_sharepoint)  
  
 [表格式 (DeploymentMode=2)](#bkmk_vertipaq)  
  
##  <a name="multidimensional-and-data-mining-deploymentmode0"></a><a name="bkmk_OLAP"></a>多維度和資料採礦 (DeploymentMode = 0)   
 MOLAP 儲存模式，會同時儲存資料和中繼資料，對於檔案大小另有實體限制。 字串存放檔案的預設大小上限為 4 GB。 如果您需要更大的字串存放檔案，可以指定不同的字串儲存體架構。 如需詳細資訊，請參閱[設定維度和資料分割的字串儲存體](../configure-string-storage-for-dimensions-and-partitions.md)。  
  
|Object|大小/數目上限|  
|------------|----------------------------|  
|執行個體中的資料庫|2^31-1 = 2,147,483,647|  
|資料庫中的維度|2^31-1 = 2,147,483,647|  
|維度中的屬性|2^31-1 = 2,147,483,647|  
|維度屬性中的成員|2^31-1 = 2,147,483,647|  
|維度中的使用者自訂階層|2^31-1 = 2,147,483,647|  
|使用者自訂階層中的層級|2^31-1 = 2,147,483,647|  
|資料庫中的 Cube|2^31-1 = 2,147,483,647|  
|Cube 中的量值群組|2^31-1 = 2,147,483,647|  
|量值群組中的量值|2^31-1 = 2,147,483,647|  
|Cube 中的計算|2^31-1 = 2,147,483,647|  
|Cube 中的 KPI|2^31-1 = 2,147,483,647|  
|Cube 中的動作|2^31-1 = 2,147,483,647|  
|Cube 中的資料分割|2^31-1 = 2,147,483,647|  
|Cube 中的翻譯|2^31-1 = 2,147,483,647|  
|資料分割中的彙總|2^31-1 = 2,147,483,647|  
|查詢傳回的資料格|2^31-1 = 2,147,483,647|  
|來源查詢的記錄大小|64K|  
|物件名稱的長度|100 個字元|  
|資料採礦模型屬性資料行中相異狀態數目的上限|2^31-1 = 2,147,483,647|  
|考量的屬性數目上限 (特徵選取)|2^31-1 = 2,147,483,647|  
  
 如需物件命名指導方針的詳細資訊，請參閱[ASSL 物件和物件特性](../scripting-language-assl/assl-objects-and-object-characteristics.md)。  
  
 如需有關線上分析處理 (OLAP) 和資料採礦之資料來源限制的詳細資訊，請參閱[支援的資料來源 &#40;ssas 多維度&#41;](../supported-data-sources-ssas-multidimensional.md)、 [&#40;ssas 多維度&#41;支援的資料](../supported-data-sources-ssas-multidimensional.md)源，以及[ASSL 物件和物件特性](../scripting-language-assl/assl-objects-and-object-characteristics.md)。  
  
##  <a name="sharepoint-deploymentmode1"></a><a name="bkmk_sharepoint"></a>SharePoint (DeploymentMode = 1)   
  
|Object|大小/數目上限|  
|------------|----------------------------|  
|執行個體中的資料庫|2^31-1 = 2,147,483,647|  
|資料庫中的資料表|2^31-1 = 2,147,483,647|  
|資料表中的資料行|2 ^ 31-1 = 2147483647**警告：** 資料表中的資料行總數取決於與同一個資料表相關聯的量值和匯出資料行總數。 資料表的「資料行 + 量值 + 導出資料行」的最大數目為 2^31-1 = 2,147,483,647|  
|資料表中的資料列|無限制的**警告：** 限制，沒有單一資料行可包含超過1999999997個相異值。|  
|資料表中的階層|2^31-1 = 2,147,483,647|  
|階層中的層級|2^31-1 = 2,147,483,647|  
|關聯性|2^31-1 = 2,147,483,647|  
|資料表中的索引鍵資料行|2^31-1 = 2,147,483,647|  
|資料表中的量值|2 ^ 31-1 = 2147483647**警告：** 資料表中的量值總數取決於與同一個資料表相關聯的資料行和計算資料行總數。 資料表的「資料行 + 量值 + 導出資料行」的最大數目為 2^31-1 = 2,147,483,647|  
|資料表中的導出資料行|2 ^ 31-1 = 2147483647**警告：** 資料表中的匯出資料行總數取決於與同一個資料表相關聯的資料行和量值總數。 資料表的「資料行 + 量值 + 導出資料行」的最大數目為 2^31-1 = 2,147,483,647|  
|查詢傳回的資料格|2^31-1 = 2,147,483,647|  
|來源查詢的記錄大小|64K|  
|物件名稱的長度|100 個字元|  
  
##  <a name="tabular-deploymentmode2"></a><a name="bkmk_vertipaq"></a>表格式 (DeploymentMode = 2)   
  
|Object|大小/數目上限|  
|------------|----------------------------|  
|執行個體中的資料庫|2^31-1 = 2,147,483,647|  
|資料庫中的資料表|2^31-1 = 2,147,483,647|  
|資料表中的資料行|2 ^ 31-1 = 2147483647**警告：** 資料表中的資料行總數取決於與同一個資料表相關聯的量值和匯出資料行總數。 資料表的「資料行 + 量值 + 導出資料行」的最大數目為 2^31-1 = 2,147,483,647|  
|資料表中的資料列|無限制**警告：** 具有資料表中的單一資料行不能有超過1999999997個相異值的限制。|  
|資料表中的階層|2^31-1 = 2,147,483,647|  
|階層中的層級|2^31-1 = 2,147,483,647|  
|關聯性|2^31-1 = 2,147,483,647|  
|資料表中的索引鍵資料行|2^31-1 = 2,147,483,647|  
|資料表中的量值|2 ^ 31-1 = 2147483647**警告：** 資料表中的量值總數取決於與同一個資料表相關聯的資料行和計算資料行總數。 資料表的「資料行 + 量值 + 導出資料行」的最大數目為 2^31-1 = 2,147,483,647|  
|資料表中的導出資料行|2 ^ 31-1 = 2147483647**警告：** 資料表中的匯出資料行總數取決於與同一個資料表相關聯的資料行和量值總數。 資料表的「資料行 + 量值 + 導出資料行」的最大數目為 2^31-1 = 2,147,483,647|  
|查詢傳回的資料格|2^31-1 = 2,147,483,647|  
|來源查詢的記錄大小|64K|  
|物件名稱的長度|100 個字元|  
  
## <a name="see-also"></a>另請參閱  
 [判斷 Analysis Services 實例的伺服器模式](../../instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [一般屬性](../../server-properties/general-properties.md)  
  
  
