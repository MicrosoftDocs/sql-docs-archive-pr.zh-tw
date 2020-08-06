---
title: 步驟 2:確認部署配套 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 6c13f5c9-c75e-4e52-94dc-2d2db2c578fe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f452a87154175ac05a050761d8f12b6bfe61cd8b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592117"
---
# <a name="step-2-verifying-the-deployment-bundle"></a>步驟 2:確認部署套件組合
  在第 1 課中，您建立了「部署教學課程」專案，並且將封裝和輔助檔案加入至專案中。在上一項工作中，您為專案建立了部署公用程式。  
  
 在這項工作中，您會確認部署配套的內容。 部署配套就是您將要複製到目的地電腦上並且用來安裝封裝的資料夾。 如果您使用預設值 (bin\Deployment) 作為部署公用程式的位置，則部署配套就是 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案中 [部署教學課程] 資料夾內的 Bin\Deployment 資料夾。  
  
### <a name="to-verify-the-content-of-deployment-bundle"></a>若要確認部署配套的內容  
  
1.  在電腦上找到 bin\Deployment 資料夾。  
  
2.  確認下列檔案存在：  
  
    -   DataTransfer.dtsx  
  
    -   datatransferconfig.dtsconfig  
  
    -   Deployment Tutorial.SSISDeploymentManifest  
  
    -   LoadXMLData.dtsx  
  
    -   loadxmldataconfig.dtsconfig  
  
    -   NewCustomers.txt  
  
    -   orders.xml  
  
    -   orders.xsd  
  
    -   Readme.txt  
  
3.  以滑鼠右鍵按一下 Deployment Tutorial.SSISDeploymentManifest，並指向 [開啟方式]  ，然後按一下 [Internet Explorer]  。 您也可以在「記事本」之類的文字編輯器中開啟此檔案。 此檔案的 XML 程式碼應該如下所示：  
  
     `<?xml version="1.0"?><DTSDeploymentManifest GeneratedBy="Domain\UserName" GeneratedFromProjectName="Deployment Tutorial" GeneratedDate="2006-02-24T13:29:02.6537669-08:00" AllowConfigurationChanges="true"><Package>DataTransfer.dtsx</Package><Package>LoadXMLData.dtsx</Package><ConfigurationFile>datatransferconfig.dtsconfig</ConfigurationFile><ConfigurationFile>loadxmldataconfig.dtsconfig</ConfigurationFile><MiscellaneousFile>Readme.txt</MiscellaneousFile><MiscellaneousFile>orders.xml</MiscellaneousFile><MiscellaneousFile>NewCustomers.txt</MiscellaneousFile><MiscellaneousFile>orders.xsd</MiscellaneousFile></DTSDeploymentManifest>`  
  
4.  請確認屬性的值 `AllowConfigurationChanges` 為**true** ，而且 XML 包含兩個封裝的元素，分別是四個非封裝檔案的專案， `Package` `MiscellaneousFile` 以及兩個 `ConfigurationFile` XML 設定檔中每一個的元素。  
  
5.  結束 Internet Explorer 或文字編輯器。  
  
## <a name="next-lesson"></a>下一課  
 [第 3 課：安裝套件](../integration-services/lesson-3-install-ssis-package.md)  
  
![Integration Services 圖示 (小型) ](media/dts-16.gif "Integration Services 圖示 (小)")會**保持最**新狀態 Integration Services  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
  
