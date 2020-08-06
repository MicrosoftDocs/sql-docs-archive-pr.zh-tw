---
title: 表格式模型方案部署 (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: aff96558-e5e5-4b95-8ddf-ee0709c842fb
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8ff2bb4e8afbea010d4377654fc862415a81aefb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593613"
---
# <a name="tabular-model-solution-deployment-ssas-tabular"></a>表格式模型方案部署 (SSAS 表格式)
  撰寫表格式模型專案之後，您必須部署專案，以便讓使用者可以使用報表用戶端應用程式來瀏覽模型。 此主題描述在您的環境中部署表格式模型方案時可使用的各種屬性和方法。  
  
 本主題的章節：  
  
-   [優點](#bkmk_benefits)  
  
-   [從 SQL Server 資料工具 (SSDT) 部署表格式模型](#bkmk_deploying_bism)  
  
-   [部署屬性](#bkmk_deploy_props)  
  
-   [部署方法](#bkmk_meth)  
  
-   [設定部署伺服器並連接至已部署的模型](#bkmk_connecting)  
  
-   [相關工作](#bkmk_rt)  
  
##  <a name="benefits"></a><a name="bkmk_benefits"></a> 優點  
 部署表格式模型會在測試、暫存或實際執行環境中建立模型資料庫。 然後，使用者可以透過 Sharepoint 中的 .bism 連接檔案，或者直接從報表用戶端應用程式 (例如 Microsoft Excel、 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]或自訂應用程式) 使用資料連接，連接到已部署的模型。 當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中建立新的表格式模型專案時，所建立可用來撰寫模型的模型工作空間資料庫，會保留在工作空間伺服器執行個體上，讓您可以對模型專案進行變更，並在需要時，重新部署到測試、預備或生產環境。  
  
##  <a name="deploying-a-tabular-model-from-sql-server-data-tools-ssdt"></a><a name="bkmk_deploying_bism"></a>從 SQL Server Data Tools (SSDT 部署表格式模型)   
 部署是一個簡單的程序，不過，必須採取某些步驟來確認您的模型已使用正確的組態選項，部署到正確的 Analysis Services 執行個體。  
  
 表格式模型是由數個部署特定屬性所定義。 部署時，會建立在 [伺服器]**** 屬性中指定之 Analysis Services 執行個體的連接。 接著會在該執行個體上建立具有 [資料庫]**** 屬性中指定之名稱的新模型資料庫 (如果尚未存在)。 模型專案的 model.bim 檔案中的中繼資料是用來設定部署伺服器上 model 資料庫中的物件。 透過 [處理選項]****，您可以指定是否只要部署模型中繼資料，並建立模型資料庫；或者如果指定 [預設]**** 或 [完整]****，用來連接到資料來源的模擬認證就會從記憶體中的模型工作空間資料庫傳遞到已部署的模型資料庫。 接著，Analysis Services 會執行處理，以便將資料擴展到已部署的模型中。 一旦部署程序完成，用戶端應用程式就可以使用資料連接或 SharePoint 中的 .bism 連接檔案，來連接模型。  
  
##  <a name="deployment-properties"></a><a name="bkmk_deploy_props"></a>部署屬性  
 專案的 [部署選項] 與 [部署伺服器] 屬性會指定將模型部署到暫存或實際執行之 Analysis Services 環境的方式和位置。 針對所有模型專案定義預設的屬性設定時，您可以根據特定部署需求，變更每個專案的這些屬性設定。 如需設定預設部署屬性的詳細資訊，請參閱[設定預設的資料模型和部署屬性&#40;SSAS 表格式&#41;](properties-ssas-tabular.md)。  
  
### <a name="deployment-options-properties"></a>部署選項屬性  
 [部署選項] 屬性包括：  
  
|屬性|預設值|描述|  
|--------------|---------------------|-----------------|  
|**處理選項**|**預設值**|此屬性會指定部署物件變更時所需的處理類型。 此屬性具有以下選項：<br /><br /> **預設值**：此設定會指定 Analysis Services 將決定所需的處理類型。 將會處理未處理的物件，並且根據需要重新計算屬性關聯性、屬性階層、使用者階層和導出資料行。 此設定通常會造成比使用 [完整] 處理選項更快的部署時間。<br /><br /> 不**處理**-此設定只會指定要部署的中繼資料。 部署後，您可能必須在已部署的模型上執行處理作業，以更新及重新計算資料。<br /><br /> **Full** -這項設定會指定兩個中繼資料都已部署，並執行完整的處理常式作業。 如此可確保已部署模型的中繼資料和資料為最新。|  
|**交易式部署**|**False**|此屬性會指定部署是否為交易式。 依預設，在處理這些已部署的物件時，所有物件或已變更之物件的部署並不是交易式。 即使處理失敗，部署仍可以成功，並持續存在。 您可以變更這項預設值，在單一交易中併入部署和處理。|  
|**查詢模式**|**記憶體內部**|此屬性會指定傳回查詢結果的來源模式執行記憶體 (快取) 模式或 DirectQuery 模式。 此屬性具有以下選項：<br /><br /> **DirectQuery** ：此設定會指定模型的所有查詢都應該只使用關聯式資料來源。<br /><br /> **搭配使用 DirectQuery 和 InMemory** ：根據預設，此設定會指定應該透過關聯式來源來回應查詢，除非在用戶端的連接字串中指定其他項目。<br /><br /> **InMemory** ：此設定會指定僅透過快取來回應查詢。<br /><br /> **搭配使用 InMemory 和 DirectQuery** ：根據預設，此設定會指定 應該透過快取來回應查詢，除非在用戶端的連接字串中指定其他項目。<br /><br /> <br /><br /> 如需詳細資訊，請參閱 [DirectQuery 模式 &#40;SSAS 表格式&#41;](directquery-mode-ssas-tabular.md)。|  
  
### <a name="deployment-server-properties"></a>部署伺服器屬性  
 [部署伺服器] 屬性包括：  
  
|屬性|預設值|描述|  
|--------------|---------------------|-----------------|  
|**Server**<br /><br /> 在建立專案時設定。|**localhost**|在建立專案時設定的此屬性，會依部署模型的目標名稱來指定 Analysis Services 執行個體。 依預設，模型將會部署到本機電腦上的預設 Analysis Services 執行個體。 不過，您可以變更這項設定，以便在本機電腦上或是您有權建立 Analysis Services 物件之任何遠端電腦上的任何執行個體上指定具名執行個體。|  
|**版本(Edition)**|與工作空間伺服器所在之執行個體的版本相同。|此屬性會指定將模型部署到哪一個版本的 Analysis Services 伺服器。 這些伺服器版本會定義可以納入專案中的多種功能。 根據預設，此版本將屬於本機 Analysis Services 伺服器。 如果您指定不同的 Analysis Services 伺服器 (例如，實際 Analysis Services 伺服器)，請務必指定該 Analysis Services 伺服器的版本。|  
|**Database**|**\<projectname>**|此屬性會指定一旦部署之後，模型物件會立刻具現化所在的 Analysis Services 資料庫名稱。 此名稱也將在報表用戶端資料連接或 .bism 資料連接檔案中指定。<br /><br /> 您可以在製作模型時，隨時變更此名稱。 如果您在部署模型之後變更名稱，您在部署後所進行的變更將不會影響您先前部署的模型。 例如，如果您開啟名稱為 `TestDB` 的方案，並使用預設的模型資料庫物件名稱 Model 部署您的方案，然後修改方案並將模型資料庫重新命名為 `Sales`，在其上部署方案的 Analysis Services 執行個體將會顯示不同的資料庫，一個名為 Model，另一個名為 Sales。|  
|**Cube 名稱**|**型號**|此屬性會以用戶端工具 (例如 Excel) 和 AMO (分析管理物件) 中顯示的名稱來指定 Cube 名稱。|  
  
### <a name="directquery-options-properties"></a>DirectQuery 選項屬性  
 [部署選項] 屬性包括：  
  
|屬性|預設值|描述|  
|--------------|---------------------|-----------------|  
|**模擬設定**|**預設值**|此屬性會指定在 DirectQuery 模式下執行的模型連接到資料來源時所使用的模擬設定。 查詢記憶體中快取時，不會使用模擬認證。 此屬性設定具有以下選項：<br /><br /> **預設值**：此設定會指定當使用 [資料表匯入嚮導] 建立資料來源連接時，Analysis Services 將使用 [模擬資訊] 頁面上指定的選項。<br /><br /> **ImpersonateCurrentUser** -此設定會指定在連接到所有資料來源時，將使用目前登入之使用者的使用者帳戶。|  
  
##  <a name="deployment-methods"></a><a name="bkmk_meth"></a>部署方法  
 有數種方法可用於部署表格式模型專案。 可用於其他 Analysis Services 專案 (例如多維度) 的大多數部署方法也可用於部署表格式模型專案。  
  
|方法|描述|連結|  
|------------|-----------------|----------|  
|**SQL Server 資料工具中的部署命令**|部署命令提供從 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 撰寫環境部署表格式模型專案的一種簡單又直覺的方法。<br /><br /> ** \* \* 請 \* 注意 \* ** ，這個方法不應該用來部署到實際執行伺服器。 使用此方法可以覆寫現有模型中的某些屬性。|[從 SQL Server Data Tools 部署 &#40;SSAS 表格式&#41;](deploy-from-sql-server-data-tools-ssas-tabular.md)|  
|**分析管理物件 (AMO) 自動化**|AMO 提供 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]完整命令集的程式設計介面，包括可用於方案部署的命令。 AMO 自動化是方案部署的方法之一，雖然彈性最高，但是也需要撰寫程式。  使用 AMO 自動化的主要優點在於，您可以搭配 AMO 應用程式使用 SQL Server Agent，根據預設排程執行部署。|[使用分析管理物件 &#40;AMO&#41; 來開發](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)|  
|**XMLA**|使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，即可針對現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中繼資料產生 XMLA 指令碼，然後在另一部伺服器上執行該指令碼來重新建立初始資料庫。 透過定義部署處理，然後在 XMLA 指令碼中編纂和儲存部署處理，可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中輕易地形成 XMLA 指令碼。 一旦儲存的檔案中具有 XMLA 指令碼後，您就可以輕易地根據排程來執行指令碼，或在直接連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體的應用程式中內嵌指令碼。<br /><br /> 您也可以使用 SQL Server Agent，在預設的基礎上執行 XMLA 指令碼，但是使用 XMLA 指令碼的彈性不如 AMO。 AMO 會裝載完整的管理命令範圍，提供較廣泛的功能。|[使用 XMLA 部署模型方案](../multidimensional-models/deploy-model-solutions-using-xmla.md)|  
|**部署精靈**|使用 [部署精靈]，即可使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案產生的 XMLA 輸出檔來部署專案的中繼資料至目的地伺服器。 使用 [部署精靈] 時，您可以直接從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 檔案進行部署，如同由專案建置的輸出目錄所建立的一樣。<br /><br /> 使用 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈] 的主要優點在於其便利性。 就像是您可以儲存 XMLA 指令碼以供 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]稍後使用一樣，您也可以儲存 [部署精靈] 指令碼。 您可以透過部署公用程式，在命令提示字元處以互動方式執行 [部署精靈]。|[使用部署精靈部署模型解決方案](../multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|  
|**部署公用程式**|部署公用程式可讓您在命令提示字元之下啟動 Analysis Services 部署引擎。|[使用部署公用程式部署模型方案](../multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|  
|**同步處理資料庫精靈**|使用 [同步處理資料庫精靈]，即可同步處理任何兩個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫之間的中繼資料和資料。<br /><br /> [同步處理精靈] 可以從來源伺服器，將資料和中繼資料複製到目的地伺服器。 如果目的地伺服器沒有您要部署的資料庫複本，則會將新資料庫複製到目的地伺服器。 如果目的地伺服器已經有相同資料庫的複本，則會更新目的地伺服器上的資料庫，以使用來源資料庫的中繼資料和其他資料。|[同步處理 Analysis Services 資料庫](../multidimensional-models/synchronize-analysis-services-databases.md)|  
|**備份與還原**|備份提供傳送 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫最簡單的方式。 從 [備份]**** 對話方塊，您可以設定選項的組態，並可隨後從對話方塊本身來執行備份。 或者，您可建立可依需求頻率來儲存和執行的指令碼。<br /><br /> 備份和還原不像其他部署方法一般常用，但卻是可在最小基礎結構需求內快速完成部署的方法。|[備份與還原 Analysis Services 資料庫](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)|  
  
##  <a name="configuring-the-deployment-server-and-connecting-to-a-deployed-model"></a><a name="bkmk_connecting"></a> 設定部署伺服器並連接至已部署的模型  
 部署模型之後，保護模型資料存取、備份，以及可透過 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]在 Analysis Services 伺服器上設定的處理作業會有其他考量。 雖然這些屬性和組態設定超出本主題的範圍，但儘管如此，它們在確保已部署之模型資料安全、維持最新狀態上非常重要，而且會針對組織中的使用者，提供寶貴的資料分析資源。  
  
 部署模型並設定選擇性伺服器設定之後，就可以透過報表用戶端應用程式連接模型，並將其用來瀏覽及分析模型中繼資料。 從用戶端應用程式連接到已部署的模型資料庫超出本主題的範圍。 若要深入了解如何從用戶端應用程式連接到模型資料庫，請參閱 [表格式模型資料存取](tabular-model-data-access.md)。  
  
##  <a name="related-tasks"></a><a name="bkmk_rt"></a> 相關工作  
  
|Task|描述|  
|----------|-----------------|  
|[從 SQL Server Data Tools 部署 &#40;SSAS 表格式&#41;](deploy-from-sql-server-data-tools-ssas-tabular.md)|描述如何透過使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中的 [部署] 命令設定部署屬性及部署表格式模型專案。|  
|[使用部署精靈部署模型解決方案](../multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|本節的主題描述如何使用 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈] 來部署表格式和多維度模型方案。|  
|[使用部署公用程式部署模型方案](../multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|描述如何使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署公用程式來部署表格式和多維度模型方案。|  
|[使用 XMLA 部署模型方案](../multidimensional-models/deploy-model-solutions-using-xmla.md)|描述如何使用 XMLA 來部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格式和多維度方案。|  
|[同步處理 Analysis Services 資料庫](../multidimensional-models/synchronize-analysis-services-databases.md)|描述如何使用 [同步處理資料庫精靈]，同步處理任何兩個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格式或多維度資料庫之間的中繼資料和資料。|  
  
## <a name="see-also"></a>另請參閱  
 [連接到表格式模型資料庫 &#40;SSAS&#41;](connect-to-a-tabular-model-database-ssas.md)  
  
  
