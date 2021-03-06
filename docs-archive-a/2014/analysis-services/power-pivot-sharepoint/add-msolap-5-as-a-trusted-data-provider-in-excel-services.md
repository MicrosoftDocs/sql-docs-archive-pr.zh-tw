---
title: 將 MSOLAP. 5 新增為 Excel Services 中受信任的 Data Provider |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c1f40fa4-de6d-41ee-8124-14b4d65988f5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 876ec613f18b2d91b5e06ab5fed4a7b258c30a36
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599218"
---
# <a name="add-msolap5-as-a-trusted-data-provider-in-excel-services"></a>加入 MSOLAP.5 做為 Excel Services 中受信任的資料提供者
  MSOLAP.5 是指 Analysis Services OLE DB Provider for SQL Server 2012。 Excel Services 必須信任此提供者，才能提出連接要求，在伺服器上產生 PowerPivot 資料。  
  
 如果您使用 PowerPivot 組態工具設定 PowerPivot for SharePoint，MSOLAP.5 可能已經是受信任的提供者，因為工具包含滿足此需求的動作。 不過，如果您使用 PowerShell、管理中心，或在組態工具中排除受信任的提供者動作，可能會缺少提供者，在此情況下，您應該立即加入它做為設定伺服器陣列的一部分，以進行 PowerPivot 資料存取。  
  
 只需要為每個 Excel Services 服務應用程式執行此步驟一次。  
  
 電腦上必須已安裝 OLE DB 提供者，PowerPivot for SharePoint 伺服器或 Excel Services 伺服器等實體伺服器才能處理 PowerPivot 資料要求。 PowerPivot for SharePoint 安裝永遠都會包含 OLE DB 提供者，但是如果在沒有 PowerPivot for SharePoint 的電腦上執行 Excel Services，您必須手動安裝此提供者。 如需詳細資訊，請參閱 [在 SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)。  
  
## <a name="add-a-trusted-provider-to-excel-services"></a>將受信任的提供者加入至 Excel Services  
  
1.  在 [管理中心]，按一下 **[管理服務應用程式]**，然後按一下 Excel Services 服務應用程式。  
  
2.  按一下 **[信任的資料提供者]** 。  
  
3.  確認 MSOLAP.5 出現在清單中。 根據您設定 PowerPivot for SharePoint 的方式，MSOLAP.5 可能已經是受信任的提供者。  
  
4.  如果未列出，請按一下 **[新增信任的資料提供者]**。  
  
5.  在 [提供者識別碼] 中，輸入 `MSOLAP.5`。  
  
6.  對於 [提供者類型]，請確認已選取 OLE DB。  
  
7.  在 [提供者描述] 中，輸入 **Microsoft OLE DB Provider for OLAP Services 11.0**。  
  
  
