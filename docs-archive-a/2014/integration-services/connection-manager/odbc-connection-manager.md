---
title: ODBC 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e1069e31f3f8ffaf14dde091d913ff6d9f8fa7cc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594633"
---
# <a name="odbc-connection-manager"></a>ODBC 連接管理員
  ODBC 連接管理員可使用「開放式資料庫連接 (ODBC)」規格，讓封裝連接到各種資料庫管理系統。  
  
 當您將 ODBC 連接加入封裝並設定連線管理員屬性時，會建立連線管理員， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 並將連線管理員加入 `Connections` 封裝的集合。 在執行階段，連接管理員會解析為實體 ODBC 連接。  
  
 連接管理員的 `ConnectionManagerType` 屬性會設為 `ODBC`。  
  
 您可以利用下列方式設定 ODBC 連接管理員：  
  
-   提供參考使用者或系統資料來源名稱的連接字串。  
  
-   指定要連接的伺服器。  
  
-   指示在執行階段是否保留連接。  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>設定 ODBC 連接管理員  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [ODBC 連線管理員 UI 參考](../odbc-connection-manager-ui-reference.md)  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連接](integration-services-ssis-connections.md)  
  
  
