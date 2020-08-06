---
title: " (SSAS 多維度) 支援的資料來源 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Analysis Services, data sources
- data sources [Analysis Services], about data sources
- Analysis Services, data sources
- connections [Analysis Services]
- SSAS, data sources
ms.assetid: c97e0f8d-7ddd-4941-8b51-e7832f30fbbe
author: minewiskan
ms.author: owend
ms.openlocfilehash: 93c09424a7cc5fa6a17d84b7464798c0b4412612
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598017"
---
# <a name="data-sources-supported-ssas-multidimensional"></a> (SSAS 多維度) 支援的資料來源
  此主題描述可用於多維度模型的資料來源類型。  
  
##  <a name="supported-data-sources"></a><a name="bkmk_supported_ds"></a>支援的資料來源  
 您可以從下表的資料來源擷取資料。 當您安裝 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]時，安裝程式不會安裝所列每種資料來源的提供者。 某些提供者可能已經隨著其他應用程式安裝在您的電腦上。在其他情況下，您將需要下載和安裝提供者。  
  
> [!NOTE]  
>  協力廠商提供者 (如 Oracle OLE DB 提供者) 在這些協力廠商提供的支援之下，也可能會用於連接到協力廠商資料庫。  
  
|||||  
|-|-|-|-|  
|來源|版本|檔案類型|提供者<sup>1</sup>|  
|Access 資料庫|Microsoft Access 2007、2010、2013。|.accdb 或 .mdb|Microsoft Jet 4.0 OLE DB 提供者|  
|SQL Server 關係資料庫<sup>5</sup>|Microsoft SQL Server 2005、2008、2008 R2、2012、2014 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] <sup>2</sup>、SQL Server 平行處理資料倉儲 (PDW) <sup>3</sup>|(不適用)|OLE DB Provider for SQL Server<br /><br /> SQL Server Native Client OLE DB 提供者<br /><br /> SQL Server Native 11.0 Client OLE DB Provider<br /><br /> .NET Framework Data Provider for SQL Client|  
|Oracle 關聯式資料庫|Oracle 9i、10g、11g。|(不適用)|Oracle OLE DB Provider<br /><br /> .NET Framework Data Provider for Oracle Client<br /><br /> .NET Framework Data Provider for SQL Server<br /><br /> MSDAORA OLE DB 提供者<sup>4</sup><br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Teradata 關聯式資料庫|Teradata V2R6、V12|(不適用)|TDOLEDB OLE DB 提供者<br /><br /> .Net Data Provider for Teradata|  
|Informix 關聯式資料庫|V11.10|(不適用)|Informix OLE DB 提供者|  
|IBM DB2 關聯式資料庫|8.1|(不適用)|DB2OLEDB|  
|Sybase Adaptive Server Enterprise (ASE) 關聯式資料庫|15.0.2|(不適用)|Sybase OLE DB 提供者|  
|其他關聯式資料庫|(不適用)|(不適用)|OLE DB 提供者|  
  
 <sup>1</sup>多維度方案不支援 ODBC 資料來源。 雖然 Analysis Services 本身會處理連接，但是 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中用於建立方案的設計工具無法連接至 ODBC 資料來源，即使使用 MSDASQL 驅動程式亦然。 如果您的業務需求包含 ODBC 資料來源，請考慮改為建立表格式方案。  
  
 <sup>2</sup>如需詳細資訊，請參閱 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] [azure.microsoft.com](https://go.microsoft.com/fwlink/?LinkID=157856)上的。  
  
 <sup>3</sup>如需 PDW 的詳細資訊 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ，請參閱[SQL Server 平行處理資料倉儲](https://go.microsoft.com/fwlink/?LinkId=150895)。  
  
 <sup>4</sup>在某些情況下，使用 MSDAORA OLE DB 提供者可能會造成連接錯誤，特別是較新版本的 Oracle。 若一旦遭遇任何錯誤，建議您改用列於 Oracle 底下的任一其他提供者。  
  
 <sup>5</sup>部分功能需要在內部部署環境中執行 SQL Server 關係資料庫。 具體而言，回寫和 ROLAP 儲存會要求基礎資料來源為 SQL Server 關聯式資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SSAS 表格式&#41;支援的資料來源](../tabular-models/data-sources-supported-ssas-tabular.md)   
 [多維度模型中的資料來源](data-sources-in-multidimensional-models.md)   
 [多維度模型中的資料來源檢視](data-source-views-in-multidimensional-models.md)  
  
  
