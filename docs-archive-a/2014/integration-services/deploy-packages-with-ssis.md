---
title: SSIS 教學課程：部署封裝 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- deployment tutorial [Integration Services]
- deploying packages [Integration Services]
- SSIS, tutorials
- Integration Services, tutorials
- deploying packages [Integration Services], installing
- SQL Server Integration Services, tutorials
- walkthroughs [Integration Services]
- deployment utility [Integration Services]
- deploying packages [Integration Services], configurations
ms.assetid: de18468c-cff3-48f4-99ec-6863610e5886
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b6cb9ad6cc0932473ded07554f9f13d57879ccd9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599613"
---
# <a name="ssis-tutorial-deploying-packages"></a>SSIS 教學課程：部署封裝
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供數個工具，可讓您輕鬆地將套件部署到另一部電腦。 部署工具也可以用來管理任何相依性，例如封裝所需的組態和檔案。 在這個教學課程中，您會學到如何使用這些工具，將封裝及其相依性安裝到目標電腦上。

 首先，您會執行一些部署的準備工作。 您會在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中建立一個新的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 專案，並且將現有的封裝和資料檔加入至該專案中。 您不需要從頭開始建立新的封裝，而是使用針對這個教學課程所建立的已完成的封裝。 您在這個教學課程中並不會修改封裝的功能，不過，在您將封裝加入至專案之後，若能在 [ [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中開啟封裝並檢閱各個封裝的內容，可能會很有幫助。 因為您可以藉由檢查封裝，而了解封裝的相依性 (例如記錄檔) 以及封裝的其他有趣功能。

 在為部署做準備時，您還要更新封裝以使用組態。 組態會使封裝和封裝物件的屬性，在執行階段變成可更新的狀態。 在這個教學課程中，您會使用組態來更新記錄檔和文字檔的連接字串，以及封裝所使用之 XML 和 XSD 檔案的位置。 如需詳細資訊，請參閱 [封裝組態](../../2014/integration-services/package-configurations.md) 和 [建立封裝組態](../../2014/integration-services/create-package-configurations.md)。

 當您確認封裝可以在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中順利執行之後，就要建立用來安裝封裝的部署配套。 這個部署配套將會包含您已加入至 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案中的封裝檔案和其他項目、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 自動納入的封裝相依性，以及您所建立的部署公用程式。 如需詳細資訊，請參閱 [建立部署公用程式](../../2014/integration-services/create-a-deployment-utility.md)。

 接下來，您會將部署配套複製到目標電腦上，然後執行「封裝安裝精靈」來安裝封裝和封裝相依性。 封裝將會安裝在 msdb SQL Server 資料庫中，而支援檔案和輔助檔案則會安裝在檔案系統中。 由於部署的封裝會使用組態，因此您要更新組態使用新值，才能讓封裝在新的環境中順利執行。

 最後，您會使用「執行封裝公用程式」在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中執行封裝。

 這個教學課程的目標是，模擬在實際部署時可能遇到的各種問題的複雜性。 但是，如果您無法將封裝部署到其他電腦上，仍然可以進行這個教學課程，只要將封裝安裝在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]本機執行個體上的 msdb 資料庫中，然後從本機執行個體上的 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 執行封裝就可以了。

## <a name="what-you-will-learn"></a>學習內容
 若要熟悉中提供的新工具、控制項和功能，最好的方法 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 就是使用它們。 這個教學課程會逐步解說各個步驟，教您建立 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案，然後將封裝和其他必要檔案加入至專案中。 當專案完成之後，您還要建立部署配套、將部署配套複製到目的地電腦，然後將封裝安裝到目的地電腦上。

## <a name="requirements"></a>需求
 本教學課程的主要物件是已經熟悉基本檔案系統作業，但對提供的新功能有所限制的使用者 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 。 若要進一步瞭解 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 您將在本教學課程中使用的基本概念，您可能會發現，首先要完成下列 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 教學課程：[執行 SQL Server 匯入和匯出嚮導](import-export-data/start-the-sql-server-import-and-export-wizard.md)和[SSIS 教學課程：建立簡單的 ETL 封裝](../integration-services/ssis-how-to-create-an-etl-package.md)。

 **來源電腦。** 要用來建立部署配套的電腦必須安裝下列元件：

-   含有 AdventureWorks 資料庫的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 為了加強安全性，依預設，不會安裝範例資料庫。 您可以從[CodePlex](https://msftdbprodsamples.codeplex.com/releases/view/125550)下載範例資料庫。

-   您必須具有在 AdventureWorks 中建立和卸除資料表的權限。

-   這個教學課程也需要範例資料、完成的封裝、組態和讀我檔案。 這些項目的檔案會與範例一起安裝。 如果您找不到範例資料，請回到上面的程序，依所描述來完成安裝。

-   商業智慧開發環境 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。

 **目的地電腦。** 要用來部署封裝的電腦必須安裝下列元件：

-   含有 AdventureWorks 資料庫的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。

-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].

-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].

-   您必須具有在 AdventureWorks 中建立和卸除資料表以及在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中執行封裝的權限。

-   您必須具有 msdb 系統資料庫中 sysssispackages 資料表的 [讀取] 和 [寫入] 許可權 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。

 如果您計畫將封裝部署到建立部署配套時所使用的同一部電腦，則該部電腦必須同時符合來源電腦和目的地電腦的需求。

 **完成這個教學課程的估計時間：** 2 小時

## <a name="lessons-in-this-tutorial"></a>本教學課程中的課程
 [第1課：準備建立部署](../integration-services/lesson-1-preparing-to-create-the-deployment-bundle.md)配套在這一課，您將建立新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案，並將封裝和其他必要檔案加入至專案，以準備部署 ETL 解決方案。

 [第2課：建立部署](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)配套在這一課，您將建立部署公用程式，並確認部署配套包含必要的檔案。

 [第3課：安裝封裝](../integration-services/lesson-3-install-ssis-package.md)在這一課，您會將部署配套複製到目的電腦、安裝封裝，然後執行封裝。

![Integration Services 圖示 (小型) ](media/dts-16.gif "Integration Services 圖示 (小)")會**保持最**新狀態 Integration Services  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。

