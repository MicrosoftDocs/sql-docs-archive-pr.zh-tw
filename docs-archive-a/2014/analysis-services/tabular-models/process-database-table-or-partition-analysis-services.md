---
title: 處理資料庫、資料表或資料分割 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- SQL12.ASVS.SSMS.PARTITIONS.PROCESSINGOPTIONS.IMBI.F1
ms.assetid: 307d69c3-cabb-4dfa-b90c-9852492c1213
author: minewiskan
ms.author: owend
ms.openlocfilehash: b5d3840be43798536f1bb517007a7974a1e08728
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687188"
---
# <a name="process-database-table-or-partition"></a>處理資料庫、資料表或資料分割
  本主題中的工作描述如何使用中的 [**處理 \<object> ** ] 對話方塊，手動處理表格式模型資料庫、資料表或資料分割 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
 如需表格式模型處理的詳細資訊，請參閱[處理資料 &#40;SSAS 表格式&#41;](../process-data-ssas-tabular.md)。  
  
##  <a name="tasks"></a><a name="bkmk_process_tasks"></a>任務  
  
###  <a name="to-process-a-database"></a><a name="bkmk_process_db"></a>若要處理資料庫  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下您想要處理的資料庫，然後按一下 [處理資料庫]****。  
  
2.  在 **[處理資料庫]** 對話方塊的 **[模式]** 清單方塊中，選取下列其中一個處理模式：  
  
    |[模式]|描述|  
    |----------|-----------------|  
    |**處理預設**|偵測資料庫物件的處理狀態，並且執行必要的處理，以便將尚未處理或部分處理的物件傳遞為完整處理的狀態。 載入空白資料表和資料分割的資料；建立或重新建立 (重新計算) 階層、導出資料行及關聯性。|  
    |**完整處理**|處理資料庫及其包含的所有物件。 對已處理過的物件執行完整處理時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會先卸除該物件中的所有資料，然後再處理該物件。 當物件已進行過任何結構性變更時，就需要這種處理。 此選項需要最多資源。|  
    |**處理清除**|從資料庫物件中移除所有資料。|  
    |**處理重新計算**|更新並重新計算階層、關聯性和導出資料行。|  
  
3.  在 **[處理]** 核取方塊資料行中，選取您想透過選取的模式處理的資料分割，然後按一下 **[確定]**。  
  
###  <a name="to-process-a-table"></a><a name="bkmk_process_table"></a>若要處理資料表  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，於包含您想要處理之資料表的表格式模型資料庫內，展開 [資料表]**** 節點、以滑鼠右鍵按一下您想要處理的資料表，然後按一下 [處理資料表]****。  
  
2.  在 **[處理資料表]** 對話方塊的 **[模式]** 清單方塊中，選取下列其中一個處理模式：  
  
    |[模式]|描述|  
    |----------|-----------------|  
    |**處理預設**|偵測資料表物件的處理狀態，並且執行必要的處理，以便將尚未處理或部分處理的物件傳遞為完整處理的狀態。 載入空白資料表和資料分割的資料；建立或重新建立 (重新計算) 階層、導出資料行及關聯性。|  
    |**完整處理**|處理資料表物件及其包含的所有物件。 對已處理過的物件執行完整處理時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會先卸除該物件中的所有資料，然後再處理該物件。 當物件已進行過任何結構性變更時，就需要這種處理。 此選項需要最多資源。|  
    |**處理資料**|將資料載入資料表，而不重新建立階層或關聯性，或重新計算導出資料行和量值。|  
    |**處理清除**|從資料表和任何資料表資料分割中移除所有資料。|  
    |**處理重組**|重組輔助資料表索引。|  
  
3.  在 [資料表] 核取方塊資料行中，確認資料表並選擇性地選取您想要處理的任何其他資料表，然後按一下 **[確定]**。  
  
###  <a name="to-process-one-or-more-partitions"></a><a name="bkmk_process_partition"></a> 若要處理一個或多個資料分割  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下含有您要處理之資料分割的資料表，然後按一下 [資料分割]****。  
  
2.  在 **[資料分割]** 對話方塊的 **[資料分割]** 中，按一下 [處理] 按鈕。  
  
3.  在 **[處理資料分割]** 對話方塊的 **[模式]** 清單方塊中，選取下列其中一個處理模式：  
  
    |[模式]|描述|  
    |----------|-----------------|  
    |**處理預設**|偵測資料分割物件的處理狀態，並且執行必要的處理，以便將尚未處理或部分處理的資料分割物件傳遞為完整處理的狀態。 載入空白資料表和資料分割的資料；建立或重新建立 (重新計算) 階層、導出資料行及關聯性。|  
    |**完整處理**|處理資料分割物件及其包含的所有物件。 對已處理過的物件執行完整處理時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會先卸除該物件中的所有資料，然後再處理該物件。 當物件已進行過任何結構性變更時，就需要這種處理。|  
    |**處理資料**|將資料載入資料分割或資料表，而不重新建立階層或關聯性，或重新計算導出資料行和量值。|  
    |**處理清除**|移除資料分割中的所有資料。|  
    |**處理加入**|以新資料累加地更新資料分割。|  
  
4.  在 **[處理]** 核取方塊資料行中，選取您想透過選取的模式處理的資料分割，然後按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型資料分割 &#40;SSAS 表格式&#41;](tabular-model-partitions-ssas-tabular.md)   
 [建立及管理表格式模型資料分割 &#40;SSAS 表格式&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
