---
title: 以線上模式連接到 Analysis Services 資料庫 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, connecting
ms.assetid: 33041234-7106-404f-a289-8e904f32aff2
author: minewiskan
ms.author: owend
ms.openlocfilehash: 363beb7132eae92907198979fe2d9892c5d07b79
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705645"
---
# <a name="connect-in-online-mode-to-an-analysis-services-database"></a>在連線模式下連接至 Analysis Services 資料庫
  您可以直接連接到現有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的資料庫，並直接修改該資料庫內的物件。 當您直接連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫時，對物件的變更會立即發生，而且 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中不會建立任何 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]專案。  
  
### <a name="to-connect-directly-to-an-analysis-services-database-by-using-sql-server-data-tools"></a>若要使用 SQL Server 資料工具直接連接到 Analysis Services 資料庫  
  
1.  開啟 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  
  
2.  指向 **[檔案]** 功能表上的 **[開啟舊檔]** ，再按一下 **[Analysis Services 資料庫]**。  
  
3.  選取 **[連接到現有的資料庫]**。  
  
4.  指定伺服器名稱和資料庫名稱。  
  
     您可以輸入資料庫名稱或是查詢伺服器，以檢視伺服器上現有的資料庫。  
  
5.  按一下 [確定]  。  
  
     您現在可以直接編輯 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中的任何物件。  
  
## <a name="see-also"></a>另請參閱  
 [在開發階段使用 Analysis Services 專案和資料庫](work-with-analysis-services-projects-and-databases-in-development.md)   
 [使用 SQL Server 資料工具 &#40;SSDT&#41; 建立多維度模型](creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)  
  
  
