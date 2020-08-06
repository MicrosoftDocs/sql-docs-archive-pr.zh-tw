---
title: 指定處理選項 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services deployments, processing options
- input files [Analysis Services]
- deploying [Analysis Services], processing options
- modifying processing options
- Analysis Services Deployment Wizard, processing options
ms.assetid: e9e50817-908e-4210-bc3d-8e2957568241
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9690aaa7e1d3b3870eb6ab01630b98027263655f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687285"
---
# <a name="specifying-processing-options"></a>指定處理選項
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署嚮導會從 d 檔案讀取處理選項 \<*project name*> 。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]當您建立專案時，會建立這個檔案 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]使用 [ **Deployment** *\<project name>* **屬性頁**] 對話方塊之 [部署] 頁面上指定的處理選項來建立 \<*project name*> d 檔案。  
  
## <a name="reviewing-the-processing-options-for-deployment"></a>檢閱部署的處理選項  
 儲存在 d 檔案中的設定會如下所示 \<*project name*> ：  
  
-   **處理方法** 此設定控制部署之後是否處理部署的物件，以及將要執行的處理類型。 有三個處理選項：  
  
    -   預設的處理 (預設值)  
  
    -   完整的處理  
  
    -   無  
  
-   **回寫資料表選項** 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中已啟用回寫，則此設定會定義如何處理回寫。 有三個回寫資料表選項：  
  
    -   依預設，如果有回寫資料表，就會使用回寫資料表。 如果沒有回寫資料表，則會建立新的回寫資料表。  
  
    -   如果已經存在回寫資料表，則部署會失敗。 如果沒有回寫資料表，則會建立新的回寫資料表。  
  
    -   無論是否已存在回寫資料表，都會建立新的回寫資料表。 在此情況下，[ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈] 將刪除任何現有的資料表，並以新的回寫資料表取代。  
  
-   **交易式部署** 此設定控制中繼資料變更與處理命令的部署是發生於單一交易或個別交易中。  
  
    -   如果此選項為 `True` (預設值)，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會在單一交易中部署所有的中繼資料變更與所有的處理命令。  
  
    -   如果此選項為 `False`，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會在單一交易中部署中繼資料變更，並在個別的交易中部署每個處理命令。  
  
## <a name="modifying-the-processing-options-for-deployment"></a>修改部署的處理選項  
 不過，您可能需要 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用不同于 d 檔案中儲存的處理選項，來部署專案 \<*project name*> 。 例如，您可能需要完整地處理所有的物件、或使用預設處理選項處理、或不進行處理。 如果 Cube 或維度是可寫入的，您可以指定使用新的或現有的回寫資料表。  
  
 若要修改部署期間使用的處理選項，您可以編輯並重建專案，或使用下列程序描述的方法之一，變更輸入檔中的處理選項。  
  
#### <a name="to-change-processing-options-after-the-input-files-have-been-generated"></a>若要在已產生輸入檔之後，變更處理選項  
  
-   以互動方式執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈。 在 [處理選項]**** 頁面上，指定正在部署之專案的處理選項。  
  
     -或-  
  
-   在命令提示字元下執行 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈]，並將精靈設定為以回應檔案模式執行。 如需回應檔案模式的詳細資訊，請參閱 [執行 Analysis Services 部署精靈](running-the-analysis-services-deployment-wizard.md)。  
  
     -或-  
  
-   \<*project name*>使用任何文字編輯器來修改 d 檔案。  
  
## <a name="see-also"></a>另請參閱  
 [指定安裝目標](deployment-script-files-specifying-the-installation-target.md)   
 [指定資料分割和角色部署選項](deployment-script-files-partition-and-role-deployment-options.md)   
 [指定方案部署的組態設定](deployment-script-files-solution-deployment-config-settings.md)  
  
  
