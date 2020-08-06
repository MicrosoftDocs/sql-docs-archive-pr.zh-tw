---
title: 第6課：搭配專案部署模型使用參數 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4bdc6b9dfc019822d6cf1bd9ec7d89ffcc5ea5e2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593434"
---
# <a name="lesson-6-using-parameters-with-the-project-deployment-model"></a>第 6 課：搭配專案部署模型使用參數
  SQL Server 2012 引進了新的部署模型，讓您可以將專案部署到 Integration Services 伺服器。 Integration Services 伺服器可讓您管理及執行封裝，以及設定封裝的執行值。  
  
 在這一課，您將修改在[第5課：新增封裝部署模型的封裝](lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)設定中所建立的封裝，以使用專案部署模型。 您會以參數取代組態值來指定範例資料位置。 您也可以複製此教學課程所包含之已完成的第 5 課封裝。  
  
 使用 Integration Services 專案組態精靈時，您可將專案轉換成專案部署模型，並可使用參數 (而非組態值) 來設定目錄屬性。 這一課的部分內容涵蓋了將現有的 SSIS 封裝轉換成新專案部署模型的步驟。  
  
 當您重新執行套件時，Integration Services 服務會使用參數來填入變數的值，然後此變數會更新目錄屬性。 因此，封裝會反覆執行此參數值所指定之新資料夾中的檔案，而不反覆執行封裝組態檔中所設定之資料夾中的檔案。  
  
> [!IMPORTANT]  
>  這個教學課程需要 **AdventureWorksDW2012** 範例資料庫。 如需如何安裝及部署 **AdventureWorksDW2012**的詳細資訊，請參閱 [安裝 SQL Server 範例和範例資料庫的考量](https://technet.microsoft.com/library/ms161556%28v=sql.105%29)。  
  
## <a name="lesson-tasks"></a>課程工作  
 這一課包含下列工作：  
  
1.  [步驟 1:複製第 5 課的封裝](lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [步驟 2:將專案轉換成專案部署模型](lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [步驟 3：測試第 6 課的封裝](lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [步驟 4：部署第 6 課的封裝](lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>開始課程  
 [步驟 1:複製第 5 課的封裝](lesson-6-1-copying-the-lesson-5-package.md)  
  
  
