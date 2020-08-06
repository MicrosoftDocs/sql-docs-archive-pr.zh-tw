---
title: Excel 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7561361c6d4ab7e22282b25367906aa4b75e5bc7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595241"
---
# <a name="excel-connection-manager"></a>Excel 連接管理員
  Excel 連接管理員可讓封裝連接到現有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 活頁簿檔案。 包含的 excel 來源和 excel 目的地 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 使用 excel 連線管理員。  
  
 當您將 Excel 連接管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立一個連接管理員 (該連接管理員在執行階段會被解析為 Excel 連接)、設定連接管理員屬性，並將該連接管理員加入封裝上的 `Connections` 集合。  
  
 連接管理員的 `ConnectionManagerType` 屬性會設為 `EXCEL`。  
  
> [!NOTE]  
>  您不能連接到受密碼保護的 Excel 檔案。  
  
## <a name="configuration-of-the-excel-connection-manager"></a>設定 Excel 連接管理員  
 您可以利用下列方式設定 Excel 連接管理員：  
  
-   指定 Excel 活頁簿檔案的路徑。  
  
-   指定用於建立檔案的 Excel 版本。  
  
-   指出所選取工作表或範圍中第一個存取資料的資料列是否包含資料行名稱。  
  
 如果 Excel 來源使用 Excel 連接管理員，擷取的資料中便會包含資料行名稱。 如果 Excel 目的地使用 Excel 連接管理員，資料行名稱便會包含在寫入的資料中。  
  
 Excel 連接管理員會使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet 4.0 及其支援的 Excel ISAM (Indexed Sequential Access Method，索引循序存取方法) 驅動程式，連接和讀寫資料至 Excel 資料來源。 如需此提供者和驅動程式與 Excel 來源和 Excel 目的地搭配使用時之行為的詳細資訊，請參閱[Excel 來源](../data-flow/excel-source.md)和[excel 目的地](../data-flow/excel-destination.md)。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中設定之屬性的詳細資訊，請參閱 [Excel 連線管理員編輯器](../excel-connection-manager-editor.md)。  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
 如需循環使用 Excel 檔案群組的資訊，請參閱 [使用 Foreach 迴圈容器來循環使用 Excel 檔案和資料表](../control-flow/foreach-loop-container.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [使用 Foreach 迴圈容器來執行 Excel 檔案和資料表迴圈](../control-flow/foreach-loop-container.md)  
  
-   [使用 SQL Server Integration Services (SSIS) 從 Excel 匯入資料，或將資料匯出至 Excel](../load-data-to-from-excel-with-ssis.md)
  
  
