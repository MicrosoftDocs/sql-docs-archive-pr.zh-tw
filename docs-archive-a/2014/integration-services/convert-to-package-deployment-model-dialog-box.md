---
title: 轉換成封裝部署模型對話方塊 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.bids.converttolegacydeployment.f1
ms.assetid: 9e60a34a-10f7-48d1-966f-b3ff236ab4b7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b52932ad26f8cebd2e67b0025f4b881241119f6e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596841"
---
# <a name="convert-to-package-deployment-model-dialog-box"></a>轉換成封裝部署模型對話方塊
  **[轉換成封裝部署模型]** 命令可讓您在檢查專案和專案中的每個封裝是否與該模型相容之後，將封裝轉換成封裝部署模型。 如果某個封裝使用專案部署模型獨有的功能 (例如參數)，則無法轉換該封裝。  
  
## <a name="task-list"></a>工作清單  
 將封裝轉換成封裝部署模型需要兩個步驟。  
  
1.  當您從 **[專案]** 功能表選取 **[轉換成封裝部署模型]** 命令時，會檢查專案和每個封裝是否與此模型相容。 結果會顯示在 **[結果]** 資料表中。  
  
     如果專案或封裝無法通過相容性測試，按一下 **[結果]** 資料行中的 **[失敗]** ，可取得詳細資訊。 按一下 **[儲存報表]** ，將此資訊的副本儲存到文字檔中。  
  
2.  如果專案和所有封裝通過相容性測試，則按一下 **[確定]** 以轉換封裝。  
  
> [!NOTE]  
>  若要將專案轉換為專案部署模型，請使用 **[Integration Services 專案轉換精靈]**。 如需相關資訊，請參閱 [Integration Services Project Conversion Wizard](../../2014/integration-services/integration-services-project-conversion-wizard.md)。  
  
## <a name="see-also"></a>另請參閱  
 [專案和套件的部署](packages/deploy-integration-services-ssis-projects-and-packages.md)   
 [&#40;SSIS&#41;的套件部署](packages/legacy-package-deployment-ssis.md)   
 [Integration Services 專案轉換精靈](../../2014/integration-services/integration-services-project-conversion-wizard.md)  
  
  
