---
title: " (Partition Wizard) 的處理和儲存位置 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.specifyprocessingandstorage.f1
ms.assetid: dda2dc57-923d-4db9-93a7-38e95770f3df
author: minewiskan
ms.author: owend
ms.openlocfilehash: 00ab88bac184f57bd2b4dcfdb8d00909a85ece4f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708713"
---
# <a name="processing-and-storage-locations-partition-wizard"></a>處理與儲存位置 (資料分割精靈)
  使用 [處理與儲存位置]**** 頁面，即可指定擁有資料分割之 Cube 的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體，以及儲存該資料分割之資料的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體。 藉由指定遠端 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體或指定預設儲存位置以外的儲存位置，即可將資料分割定義為遠端資料分割。 如需遠端資料分割的詳細資訊，請參閱 [遠端資料分割](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)。  
  
## <a name="processing-location-options"></a>處理位置選項  
 **目前伺服器執行個體**  
 使目前的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體負責處理資料分割。  
  
 **遠端 Analysis Services 資料來源**  
 使遠端 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體負責處理此資料分割。  
  
 從下拉式清單中，選取代表負責處理資料分割之遠端 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的資料來源。  
  
> [!NOTE]  
>  如果您選取的資料來源之 `Initial Catalog` 連接字串屬性並未設定為有效的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，或是如果 `Initial Catalog` 連接字串屬性中所指定的資料庫並不支援遠端資料分割 (換言之，指定之資料庫的 `MasterDatasourceID` 屬性並未設定為有效值)，就會發生錯誤。  
  
 **新增**  
 建立代表負責處理資料分割之遠端 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的新資料來源。  
  
## <a name="storage-location-options"></a>儲存位置選項  
 **預設伺服器位置**  
 使目前 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體資料的資料夾，成為資料分割之彙總與索引資料的儲存位置。  
  
 **指定的資料夾**  
 指定資料分割之彙總與索引資料的儲存位置。  
  
 **...**  
 顯示 [瀏覽遠端資料夾]**** 對話方塊，您可以在其中為 [指定的資料夾]**** 選取資料夾。  
  
## <a name="see-also"></a>另請參閱  
 [分割區 Wizard F1 說明 &#40;Analysis Services-多維度資料&#41;](partition-wizard-f1-help-analysis-services-multidimensional-data.md)   
 [分割區 &#40;Analysis Services 多維度資料&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [[流覽遠端資料夾] 對話方塊 &#40;Analysis Services-多維度資料&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)  
  
  
