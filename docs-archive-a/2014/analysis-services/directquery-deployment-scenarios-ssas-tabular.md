---
title: " (SSAS 表格式) 的 DirectQuery 部署案例 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2aaf5cb8-294b-4031-94b3-fe605d7fc4c7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2c90d90b40686b5953e26853ed9f53dcfd157f0f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606487"
---
# <a name="directquery-deployment-scenarios-ssas-tabular"></a>DirectQuery 部署案例 (SSAS 表格式)
  本主題提供 DirectQuery 模型設計和部署程序的逐步解說。 您可以設定 DirectQuery 只使用關聯式資料 (僅限 DirectQuery)，或者您可以將此模型設定為在使用快取資料與僅限關聯式資料之間切換 (混合模式)。 本主題說明這兩個模式的實作程序，並描述查詢結果中的可能差異 (視模型和安全性組態而定)。  
  
 [設計和部署步驟](#bkmk_DQProcedure)  
  
 [比較 DirectQuery 組態](#bkmk_Configurations)  
  
##  <a name="design-and-deployment-steps"></a><a name="bkmk_DQProcedure"></a>設計和部署步驟  
 **步驟1。建立解決方案**  
  
 不論您使用哪種模式，您都必須檢閱有關可用於 DirectQuery 模型中之資料的限制資訊。 例如，所有用於模型和報表的資料都必須來自單一 SQL Server 資料庫。 如需詳細資訊，請參閱 [DirectQuery 模式 &#40;SSAS 表格式&#41;](tabular-models/directquery-mode-ssas-tabular.md)。  
  
 您也可以檢閱量值和導出資料行的限制，並判斷您打算使用的公式是否與 DirectQuery 模式相容。 您可能需要移除或修改下列元素：  
  
-   不支援導出資料行。  
  
-   不能使用複製-貼上的資料。 如果您匯入 PowerPivot 模型來開始啟動方案，請務必先刪除連結資料表然後再匯入方案，因為此資料無法被刪除而且會阻擋 DirectQuery 驗證。  
  
 **步驟2。在模型設計師中啟用 DirectQuery 模式**  
  
 依預設，DirectQuery 為停用狀態。 因此，您必須設定設計環境來支援 DirectQuery 模式。  
  
 以滑鼠右鍵按一下方案總管中的 [ **model.bim** ] 節點，並將 [ **DirectQuery 模式]** 屬性設定為 `On` 。  
  
 您可以隨時開啟 DirectQuery，但是若要確保您不會建立與 DirectQuery 模式不相容的資料行或公式，我們建議您從一開始就啟用 DirectQuery 模式。  
  
 最初，即使是 DirectQuery 模型也一定會在記憶體中建立。 工作空間資料庫的預設查詢模式也會設定為 **[搭配使用 DirectQuery 和 In-Memory]**。 這個混和工作模式可讓您使用匯入資料的快取，以便在模型設計過程中提高效能，同時根據 DirectQuery 需求來驗證此模型。  
  
 **步驟3。解決驗證錯誤**  
  
 如果您在開啟 DirectQuery 時或在新增資料或公式時發生驗證錯誤，請開啟 Visual Studio **[錯誤清單]**，然後執行必要動作。  
  
-   如錯誤訊息所述，變更 DirectQuery 模式的所有必要屬性設定。  
  
-   移除導出資料行。 如果您需要特定量值的匯出資料行，您一律可以使用[關聯式查詢設計](relational-query-designer-ssas.md)工具來建立資料行，&#40;[資料表匯入] wizard 中提供的 SSAS&#41;。  
  
-   修改或刪除與 DirectQuery 模式不相容的公式。 如果計算需要使用特定函數，請考慮透過 Transact-SQL 來提供對應項目的方法。  
  
-   視需要新增資料。  如果您的模型之前使用複製-貼上資料或是來自 SQL Server 以外之提供者的資料，您可以在現有的連接中建立新的檢視表和衍生的資料行，或者使用分散式查詢。  DirectQuery 模型中使用的所有資料都必須可以透過單一 SQL Server 資料來源來存取。  
  
 **步驟4。在模型上設定用來回應查詢的慣用方法**  
  
|||  
|-|-|  
|**僅限 DirectQuery**|將此屬性設定為 **[DirectQuery]**。|  
|**混合模式**|將此屬性設定為 **[搭配使用 In-Memory 和 DirectQuery]** 或 **[搭配使用 DirectQuery 和 In-Memory]**。<br /><br /> 稍後您可以變更這個值來使用不同的喜好設定。<br /><br /> 請注意，用戶端可以覆寫連接字串中的慣用方法。|  
  
 **步驟5。指定 DirectQuery 資料分割**  
  
|||  
|-|-|  
|**僅限 DirectQuery**|選擇性。 僅限 DirectQuery 模型不需要資料分割。<br /><br /> 但是，如果您在設計階段於模型中建立資料分割，請記得只有一個資料分割可當做資料來源使用。 根據預設，您建立的第一個資料分割將會當做 DirectQuery 資料分割使用。<br /><br /> 若要確保模型所需的所有資料都可以從 DirectQuery 資料分割取得，請選擇 DirectQuery 資料分割並編輯 SQL 陳述式來取得整個資料集。|  
|**混合模式**|如果模型中的任何資料表有多個資料分割，您必須選擇單一資料分割當做 *「DirectQuery 資料分割」*(DirectQuery Partition)。 如果您未指派資料分割，則根據預設，之前建立的第一個資料分割將會當做 DirectQuery 資料分割使用。<br /><br /> 在 DirectQuery 除外的所有資料分割上設定處理選項。 通常絕對不會處理 DirectQuery 資料分割，因為資料是透過關聯式來源傳遞。<br /><br /> 如需詳細資訊，請參閱[&#40;SSAS 表格式&#41;的資料分割和 DirectQuery 模式](tabular-models/define-partitions-in-directquery-models-ssas-tabular.md)。|  
  
 **步驟6。設定模擬**  
  
 只有 DirectQuery 模型才支援模擬。 模擬選項 **[模擬設定]** 會定義在檢視指定的 SQL Server 資料來源資料時使用的認證。  
  
|||  
|-|-|  
|**僅限 DirectQuery**|針對  **[模擬設定]** 屬性，指定將用於連接至 SQL Server 資料來源的帳戶。<br /><br /> 如果您使用 **ImpersonateCurrentUser**值，則裝載此模型的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體會將此模型之目前使用者的認證傳遞給 SQL Server 資料庫。|  
|**混合模式**|針對 **[模擬設定]** 屬性，指定將用於存取 SQL Server 資料來源資料的帳戶。<br /><br /> 此設定不影響用於處理模型所用之快取的認證。|  
  
 **步驟7：部署模型**  
  
 當您準備好要部署模型時，請開啟 Visual Studio 的 [**專案**] 功能表，然後選取 [**屬性**]。 將 **[QueryMode]** 屬性設定為下表所述的其中一個值：  
  
 如需詳細資訊，請參閱[從 SQL Server Data Tools 部署 &#40;SSAS 表格式&#41;](tabular-models/deploy-from-sql-server-data-tools-ssas-tabular.md)。  
  
|||  
|-|-|  
|**僅限 DirectQuery**|**DirectQueryOnly**<br /><br /> 因為您已經指定僅限 DirectQuery，所以模型中繼資料會部署至伺服器，但是不會處理模型。<br /><br /> 請注意，工作空間資料庫使用的快取不會自動遭到刪除。 如果您想要確保使用者無法看到快取資料，最好清除設計階段快取。 如需詳細資訊，請參閱[清除 Analysis Services](instances/clear-the-analysis-services-caches.md)快取。|  
|**混合模式**|**[搭配使用 DirectQuery 和 In-Memory]**<br /><br /> **使用 DirectQuery 的記憶體內部**<br /><br /> 這兩個值都可讓您視需要使用快取或關聯式資料來源。 此順序定義在回應模型查詢時預設使用的資料來源。<br /><br /> 在混合模式中，必須在模型中繼資料部署至伺服器的同時處理快取。<br /><br /> 在部署後可以變更此設定。|  
  
 **步驟8。確認已部署的模型**  
  
 在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中，開啟部署模型的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體。 以滑鼠右鍵按一下資料庫名稱，然後選取 **[屬性]**。  
  
-   **[DirectQueryMode]** 屬性是在定義部署屬性時設定的。  
  
-   **[資料來源模擬資訊]** 屬性是在定義使用者模擬選項時設定的。 如需詳細資訊，請參閱[設定模擬選項 &#40;SSAS - 多維度&#41;](multidimensional-models/set-impersonation-options-ssas-multidimensional.md)。  
  
-   部署模型之後，您隨時可以變更這些屬性。  
  
##  <a name="comparing-directquery-options"></a><a name="bkmk_Configurations"></a>比較 DirectQuery 選項  
 **僅限 DirectQuery**  
 在您想要確保單一資料來源時，或者您的資料太大而無法放入記憶體中時，這是慣用選項。 如果您使用非常大的關聯式資料來源，可以在設計階段透過使用某個資料子集來建立模型。 當您在僅限 DirectQuery 模式下部署模型時，可以編輯資料來源定義來包含所有必要的資料。  
  
 如果您想要使用關聯式資料來源提供的安全性，以控制使用者對資料的存取，這也是慣用選項。 對於快取的表格式模型，您還可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 角色控制資料存取，但是儲存在快取中的資料必須也受到保護。 如果您的安全性內容要求應該永遠不快取資料，則應該永遠使用此選項。  
  
 下表描述僅限 DirectQuery 模式的可能部署結果：  
  
|||  
|-|-|  
|**無快取的 DirectQuery**|沒有資料會載入到快取中。 模型永遠不會處理。<br /><br /> 模型只能透過支援 DAX 查詢的用戶端進行查詢。 查詢結果永遠是從原始資料來源傳回。<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode**  = **DirectQuery**|  
|**DirectQuery 並且查詢僅針對快取**|部署失敗。 不支援這樣的設定。<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode**  = **記憶體**內部|  
  
 **混合模式**  
 部署混合模式的模型有許多好處：您可以根據需要從 SQL Server 資料來源取得最新資料，但保留快取讓您能夠使用記憶體中的資料，在設計報表或測試模型時增進效能。  
  
 如果您的模型非常大，DirectQuery 混和模式也會非常實用。 與其讓使用者取得過時資料或讓模型無法使用，您可以在處理進行中時將模型切換為 DirectQuery 模式。 使用者可能會感覺到效能稍慢，但將能夠直接從關聯式存放區取得資料，確保結果是最新狀態。  
  
 下表比較各個 DirectQuery 選項組合的部署結果。  
  
|||  
|-|-|  
|**快取為慣用的混合模式**|可以處理此模型，並且可以將資料載入至快取中。 查詢預設使用快取。  如果用戶端想要使用 DirectQuery 來源，必須在連接字串中插入參數。<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode**  = **使用 DirectQuery 的記憶體**內部|  
|**DirectQuery 為慣用的混合模式**|會處理模型，並且可以將資料載入至快取中。 但是，查詢預設使用 DirectQuery。 如果用戶端想要使用快取資料，必須在連接字串中插入參數。 如果模型中的資料表已分割，快取的主要資料分割也要設定為 **[搭配使用 In-Memory 和 DirectQuery]**。<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode**  = **具有記憶體**內部的 DirectQuery|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SSAS 表格式&#41;的 DirectQuery 模式](tabular-models/directquery-mode-ssas-tabular.md)   
 [表格式模型資料存取](tabular-models/tabular-model-data-access.md)  
  
  
