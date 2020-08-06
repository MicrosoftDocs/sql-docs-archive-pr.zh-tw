---
title: 模型部署選項 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cf1b17b4-47d5-4eba-83f9-fb0555806867
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 25af38deef2a5476f64f364116dc5e9168345fb2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707657"
---
# <a name="model-deployment-options-master-data-services"></a>模型部署選項 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，當您要部署模型封裝檔案時，必須決定要部署新的或複製的模型，還是更新之前複製的模型。  
  
## <a name="workflows"></a>工作流程  
 在使用模型封裝時，有兩個主要工作流程。  
  
-   在測試環境中建立模型封裝，並且將模型的複製部署到實際執行環境。 經過一段時間後，從測試環境將更新部署到實際執行環境。  
  
-   建立模型封裝，並將它做為新模型部署到相同的環境。 在此情況下，您必須指定模型的新名稱。  
  
## <a name="options"></a>選項  
 在 MDS 資料庫中，每個模型物件都有唯一識別碼 (ID)。 這些識別碼包含在模型部署封裝中。 當您部署封裝時，必須選擇如何處理這些識別碼。  
  
 下表有助於您在使用系統管理模型部署精靈或 MDSModelDeploy 工具部署模型時，決定選擇。  
  
|選項|描述|注意|  
|------------|-----------------|-----------|  
|新增|建立具有唯一名稱的新模型。 將會建立所有模型物件的新識別碼。|如果建立具有新識別碼的新模型，稍後您無法使用模型部署工具將更新套用至此模型。 在 Web 應用程式中使用精靈來部署模型封裝時，只在已經有相同名稱或識別碼的模型時，您才可以選擇建立新的模型。|  
|複製|建立新的模型，它是封裝中模型的完整複製。 只在此模型不存在於目標環境中 (依名稱或識別碼) 時才有效。 如果要在多個環境中具有相同的模型，且經過一段時間後要更新複製的模式，請使用 [複製]。|這是在 Web 應用程式中精靈的預設行為。 如果已經有相同名稱或識別碼的模型，系統會提示您改為建立新的模型。|  
|更新|以封裝中的模型來更新現有模型。 這兩個模型中的識別碼必須相同。 這是用來更新之前複製的模型。|您只可以更新之前複製的模型 (名稱和識別碼必須相符)。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 MDSModelDeploy 部署模型部署封裝](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)   
 [使用 Wizard 部署模型部署封裝](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)   
 [部署模型 &#40;Master Data Services&#41;](deploying-models-master-data-services.md)  
  
  
