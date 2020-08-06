---
title: 從多維度資料來源匯入 (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7f0793ea-a4c7-42e9-b722-2164a454ebca
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0b26cc8ed7237f87fa5e23c6a2fd47e18de2c165
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606477"
---
# <a name="import-from-a-multidimensional-data-source-ssas-tabular"></a>從多維度資料來源匯入 (SSAS 表格式)
  您可以使用 Analysis Services Cube 資料庫做為表格式模型的資料來源。 您必須定義 MDX 查詢選取要匯入的資料，才可以從 Analysis Services Cube 匯入資料。  
  
 包含在 SQL Server Analysis Services 資料庫中的任何資料，都可以匯入至模型中。 您可以擷取部分或全部的維度，或是從 Cube 取得配量和彙總，例如目前年度每個月的銷售總和等。但是請注意，您從 Cube 匯入的所有資料都會扁平化。 因此，如果您定義擷取量值及多維度的查詢，匯入資料的每個維度都會在個別的資料行中。  
  
 Analysis Services Cube 必須是 SQL Server 2005、SQL Server 2008、SQL Server 2008 R2、 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]版。  
  
### <a name="to-import-data-from-an-analysis-services-cube"></a>若要從 Analysis Services Cube 匯入資料  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，按一下 **[模型]** 功能表，然後按一下 **[從資料來源匯入]**。  
  
2.  在 **[連接到資料來源]** 頁面上，選取 **[Microsoft Analysis Services]**，然後按 **[下一步]**。  
  
3.  請遵循 [資料表匯入精靈] 中的步驟來進行。 您將能夠在 **[指定 MDX 查詢]** 頁面上，指定 MDX 查詢。 若要使用 MDX 查詢設計工具，請在 [指定 MDX 查詢] 頁面上，按一下 **[設計]**。  
  
## <a name="see-also"></a>另請參閱  
 [將資料匯入 &#40;SSAS 表格式&#41;](import-data-ssas-tabular.md)   
 [支援的資料來源 &#40;SSAS 表格式&#41;](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
