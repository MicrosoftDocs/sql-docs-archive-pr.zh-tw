---
title: 使用 OLE DB 目的地來載入資料 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- loading data
- OLE DB destination [Integration Services]
- destinations [Integration Services], OLE DB
ms.assetid: 78899498-725e-4300-a7af-f983f4ea384b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 43e8d1123ae91d9e68c00fbe3e05c490383afe0c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87700090"
---
# <a name="load-data-by-using-the-ole-db-destination"></a>使用 OLE DB 目的地來載入資料
  若要加入及設定 OLE DB 目的地，封裝必須已包括至少一個「資料流程」工作與來源。  
  
### <a name="to-load-data-using-an-ole-db-destination"></a>使用 OLE DB 目的地載入資料  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [資料流程]  索引標籤，然後將 OLE DB 目的地從 [工具箱]  拖曳至設計介面。  
  
4.  將連接子從資料來源或前一個轉換拖曳至目的地，以便將 OLE DB 目的地連接到資料流程。  
  
5.  按兩下 OLE DB 目的地。  
  
6.  在 [連接管理員] 頁面的 [OLE DB 目的地編輯器] 對話方塊中，選取現有的 OLE DB 連接管理員，或按一下 [新增] 以新建連接管理員。 如需相關資訊，請參閱 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md)。  
  
7.  選取資料存取方法：  
  
    -   **資料表或檢視** ：在資料庫中選取包含資料的資料表或檢視。  
  
    -   **資料表或檢視 - 快速載入**：在資料庫中選取包含資料的資料表或檢視，然後設定快速載入選項：[保留識別]  、[保留 Null]  、[資料表鎖定]  、[檢查條件約束]  、[每批次的資料列]  或 [插入認可大小上限]  。  
  
    -   **資料表名稱或檢視名稱變數** ：選取使用者自訂變數，該變數包含資料庫中資料表或檢視的名稱。  
  
    -   **資料表名稱或檢視名稱變數 - 快速載入** ：選取使用者自訂變數，該變數含有資料庫中包含該資料之資料表或檢視的名稱，然後設定快速載入選項。  
  
    -   **SQL 命令**：輸入 SQL 命令，或按一下 [建立查詢]  ，以使用 [查詢產生器]  來撰寫 SQL 命令。  
  
8.  按一下 **[對應]** ，然後將資料行從一個清單拖曳至另一個清單，使 **[可用的輸入資料行]** 清單中的資料行對應至 **[可用的目的地資料行]** 清單中的資料行。  
  
    > [!NOTE]  
    >  OLE DB 目的地會自動對應具有相同名稱的資料行。  
  
9. 若要設定錯誤輸出，請按一下 **[錯誤輸出]** 。 如需詳細資訊，請參閱 [在資料流程元件中設定錯誤輸出](../configure-an-error-output-in-a-data-flow-component.md)。  
  
10. 按一下 [確定]  。  
  
11. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 目的地](ole-db-destination.md)   
 [Integration Services 轉換](transformations/integration-services-transformations.md)   
 [Integration Services 路徑](integration-services-paths.md)   
 [資料流程工作](../control-flow/data-flow-task.md)  
  
  
