---
title: 使用 MDSModelDeploy 建立模型部署套件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: c2687e39-dc20-494f-a707-2aa29f4c329e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c546d6398234dd43103d0e6c75822377e11de61a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606954"
---
# <a name="create-a-model-deployment-package-by-using-mdsmodeldeploy"></a>使用 MDSModelDeploy 建立模型部署封裝
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，使用 MDSModelDeploy 工具來建立封裝。 根據您指定的命令，此封裝可以包含：  
  
-   僅限模型物件。  
  
-   模型物件和資料。  
  
 如果您想要部署只包含模型物件的封裝，您可以在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式中改用模型部署精靈。 如需詳細資訊，請參閱 [使用精靈建立模型部署封裝](../../2014/master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)。  
> [!NOTE]  
> 這個版本的 MDSModelDeploy 工具無法使用超過 gb (GB 的記憶體) 。 當您使用**模型物件和資料**選項建立或部署大型模型時，可能會遇到「記憶體不足」或「資料流程太長」錯誤。 若要解決此問題，請使用 MDS 預備環境來部署資料;或升級至 MDS 2016 或更新版本，其中包含 MDSModelDeploy 工具的更新版本。
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
1.  執行 MDSModelDeploy 工作所需的基本權限如下：  
  
    -   與 MDS 組態管理員相同的 Windows 權限 (Windows 管理員)  
  
    -   MDS 資料庫的 DBA 權限。  
  
2.  使用 MDSModelDeploy 工作建立封裝所需的權限如下：  
  
    -   資料模型的 MDS 模型管理員權限。  
  
    -   MDS 整合管理功能權限。  
  
3.  使用 MDSModelDeploy 工作部署模型所需的權限如下：  
  
    -   MDS Explorer 功能權限  
  
    -   MDS 整合管理功能權限  
  
    -   MDS 系統管理功能權限。  
  
4.  使用 MDSModelDeploy 工作列出模型所需的權限如下：  
  
    -   MDS Explorer 功能權限  
  
    -   在訂單的資料模型上查看清單中模型的 MDS 模型管理員權限。  
  
 模型必須存在，才能建立其封裝。 如需詳細資訊，請參閱[建立模型 &#40;Master Data Services&#41;](create-a-model-master-data-services.md)。  
  
 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-create-a-model-deployment-package-by-using-mdsmodeldeploy"></a>若要使用 MDSModelDeploy 建立模型部署封裝  
  
1.  開啟命令提示字元。  
  
2.  導覽至 MDSModelDeploy.exe 的位置。  
  
    -   如果 MDS 已安裝在預設位置，檔案就會在*磁片磁碟機*： \PROGRAM Files\Microsoft SQL Server\120\Master Data services\configuration。中。  
  
    -   如果 MDS 未安裝在預設位置，請搜尋本機電腦中的 MDSModelDeploy.exe。  
  
3.  選擇性。 檢視選項和說明。  
  
    -   若要顯示所有可用的選項，請輸入 `MDSModelDeploy` ，然後按 Enter 鍵。  
  
    -   若要顯示某個選項的説明，請輸入 *，其中* OptionName `MDSModelDeploy help OptionName`是選項的名稱。  
  
4.  選擇性。 如果您有多個 Web 應用程式，請輸入以下命令並按 Enter 鍵，以判斷您要部署的目標服務名稱：  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     隨即傳回值的清單，例如 `MDS1, Default Web Site, MDS`。 此清單中的第一個值 (此案例中為 `MDS1`) 是部署模型所需的項目。  
  
5.  若要建立包含模型物件和資料的封裝，請輸入下列命令，其中 *ModelName*、 *VersionName*、 *ServiceName*和 *PackageName* 分別是模型、版本、服務和 .pkg 輸出檔的名稱：  
  
    ```  
    MDSModelDeploy createpackage -model ModelName -version VersionName -service ServiceName -package PackageName -includedata  
    ```  
  
     如果您不想要包含資料，請勿使用 `-version` 和 `-includedata` 參數。  
  
6.  按 Enter 鍵。 當成功建立套件之後，隨即顯示一則訊息，表示「MDSModelDeploy 作業已順利完成」。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [使用 MDSModelDeploy 部署模型部署封裝](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
## <a name="see-also"></a>另請參閱  
 [模型部署選項 &#40;Master Data Services&#41;](../../2014/master-data-services/model-deployment-options-master-data-services.md)   
 [部署模型 &#40;Master Data Services&#41;](../../2014/master-data-services/deploying-models-master-data-services.md)  
  
  
