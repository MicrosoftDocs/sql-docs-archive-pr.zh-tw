---
title: 安全性角色 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], roles
- Analysis Services objects, roles
- security [Analysis Services], roles
- roles [Analysis Services], about roles
- server roles [Analysis Services]
- database roles [Analysis Services]
- roles [Analysis Services]
- storing data [Analysis Services], roles
- access rights [Analysis Services], roles
ms.assetid: 5b7e9cef-ff68-4d8e-99bc-e0094ced1baa
author: minewiskan
ms.author: owend
ms.openlocfilehash: e62abaab5a8f74dfee7d51962f2fb243dc6eb20a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705561"
---
# <a name="security-roles--analysis-services---multidimensional-data"></a>安全性角色 (Analysis Services - 多維度資料)
  在中，會使用角色 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 來管理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 物件和資料的安全性。 基本上，角色會與特定的 Microsoft Windows 使用者和群組的安全性識別碼 (SID) 相關聯，這些使用者和群組擁有針對 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體所管理物件定義的特定存取權限和權限。 在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中提供兩種角色類型：  
  
-   伺服器角色，這是一種固定角色，提供對 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體的管理員存取權。  
  
-   資料庫角色，這是管理員所定義的角色，用來控制非管理員使用者對物件和資料的存取。  
  
 安全性的安全性 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 是使用角色和許可權來管理。 角色是使用者的群組。 使用者 (也稱為成員) 可以在角色中加入或移除。 物件的權限是依角色指定，而角色中的所有成員都可以使用此角色具有權限的物件。 角色中的所有成員都具有物件的相同權限。 權限是物件所特有。 每一個物件都有權限集合 (包含該物件的授與權限)，可以對物件授與不同的權限集合。 每一個權限 (來自物件的權限集合) 都會被指派單一角色。  
  
## <a name="role-and-role-member-objects"></a>角色和角色成員物件  
 角色是使用者 (成員) 集合的包含物件。 角色定義會在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中建立使用者的成員資格。 由於權限是依角色指派，所以在使用者可存取任何物件之前，使用者必須是某個角色的成員。  
  
 <xref:Microsoft.AnalysisServices.Role> 物件是由參數名稱、識別碼和成員所組成。 成員是字串的集合。 每一個成員都包含 "domain\username" 格式的使用者名稱。 名稱是包含角色之名稱的字串。 識別碼是包含角色之唯一識別碼的字串。  
  
### <a name="server-role"></a>伺服器角色  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器角色定義 Windows 使用者和群組，對 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體的管理員存取權。 此角色的成員擁有 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上所有 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫和物件的存取權，並且可以執行下列工作：  
  
-   使用 SQL Server Management Studio 或 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]執行伺服器層級管理功能，其中包括建立資料庫和設定伺服器層級屬性。  
  
-   使用分析管理物件 (AMO)，以程式設計的方式執行管理功能。  
  
-   維護 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫角色。  
  
-   啟動追蹤 (除了處理事件之外，擁有 Process 存取權的資料庫角色就可以執行處理事件)。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的每個執行個體均有一個伺服器角色，該角色定義哪些使用者可以管理該執行個體。 此角色的名稱和識別碼是 Administrators，而且不能刪除伺服器角色，也不能加入或移除權限，這和資料庫角色不同。 換言之，使用者是或者不是 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體的管理員，這會視使用者是否包含在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體之伺服器角色中而定。  
  
### <a name="database-roles"></a>資料庫角色  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫角色，定義對 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫中之物件和資料的使用者存取。 資料庫角色會建立成 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫中的個別物件，且只適用於建立該角色的資料庫。 管理員將 Windows 使用者和群組包含在角色中，並且定義角色內的權限。  
  
 某個角色的權限除了能讓成員存取和管理資料庫內的物件與資料之外，也允許成員存取和管理資料庫。 每個權限有一或多個與其相關聯的存取權限，這些存取權限則會對資料庫之特定物件提供更細微的存取權限控制。  
  
## <a name="permission-objects"></a>Permission 物件  
 權限會與特定角色的物件 (Cube、維度等) 有關。 權限會指定該角色的成員可以在該物件上執行哪些作業。  
  
  類別是抽象類別， 因此，您必須使用衍生類別來定義對應物件的權限。 對於每一個物件而言，都會定義權限衍生類別。  
  
|Object|類別|  
|------------|-----------|  
|<xref:Microsoft.AnalysisServices.Database>|<xref:Microsoft.AnalysisServices.DatabasePermission>|  
|<xref:Microsoft.AnalysisServices.DataSource>|<xref:Microsoft.AnalysisServices.DataSourcePermission>|  
|<xref:Microsoft.AnalysisServices.Dimension>|<xref:Microsoft.AnalysisServices.DimensionPermission>|  
|<xref:Microsoft.AnalysisServices.Cube>|<xref:Microsoft.AnalysisServices.CubePermission>|  
|<xref:Microsoft.AnalysisServices.MiningStructure>|<xref:Microsoft.AnalysisServices.MiningStructurePermission>|  
|<xref:Microsoft.AnalysisServices.MiningModel>|<xref:Microsoft.AnalysisServices.MiningModelPermission>|  
  
 此清單中會顯示權限所啟用的可能動作：  
  
|動作|值|說明|  
|------------|------------|-----------------|  
|Process|{`true`, `false`}<br /><br /> 預設值=|如果為 `true`，成員可以處理此物件以及此物件中包含的任何物件。<br /><br /> 處理權限不會套用到採礦模型。 <xref:Microsoft.AnalysisServices.MiningModel> 權限一律是從 <xref:Microsoft.AnalysisServices.MiningStructure> 繼承而來。|  
|ReadDefinition|{`None`, `Basic`, `Allowed`}<br /><br /> 預設值=|指定成員是否可以讀取與此物件有關的資料定義 (ASSL)。<br /><br /> 如果為 `Allowed`，表示成員可以讀取與此物件有關的 ASSL。<br /><br /> `Basic` 和 `Allowed` 會由此物件中所包含的物件所繼承。 `Allowed` 會覆寫 `Basic` 和 `None`。<br /><br /> 物件上的 DISCOVER_XML_METADATA 需要 `Allowed`。 必須要有 `Basic`，才能建立連結物件和本機 Cube。|  
|讀取|{`None`, `Allowed`}<br /><br /> 預設值=`None` (DimensionPermission 例外，其預設值=`Allowed`)|指定成員是否具有結構描述資料列集和資料內容的讀取權。<br /><br /> `Allowed` 會提供資料庫的讀取權，這樣可讓您探索資料庫。<br /><br /> Cube 上的 `Allowed` 會提供結構描述資料列集中的讀取權及 Cube 內容的存取權 (除非受到 <xref:Microsoft.AnalysisServices.CellPermission> 和 <xref:Microsoft.AnalysisServices.CubeDimensionPermission> 的限制)。<br /><br /> 維度上的 `Allowed` 會授與此維度中所有屬性的讀取權限 (除非受到 <xref:Microsoft.AnalysisServices.CubeDimensionPermission> 的限制)。 讀取權限只會用於 <xref:Microsoft.AnalysisServices.CubeDimensionPermission> 的靜態繼承。 維度上的 `None` 會隱藏維度，並只針對可彙總屬性提供預設成員的存取；如果此維度包含不可彙總的屬性，則會引發錯誤。<br /><br /> <xref:Microsoft.AnalysisServices.MiningModelPermission> 上的 `Allowed` 會授與權限來查看結構描述資料列集中的物件以及執行預測聯結。<br /><br /> 必須有**NoteAllowed** ，才能讀取或寫入資料庫中的任何物件。|  
|寫入|{`None`, `Allowed`}<br /><br /> 預設值=|指定成員是否具有父物件資料的寫入權。<br /><br /> 也適用於 <xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.Cube> 和 <xref:Microsoft.AnalysisServices.MiningModel> 子類別。 它不會套用到資料庫 <xref:Microsoft.AnalysisServices.MiningStructure> 子類別，這樣會產生驗證錯誤。<br /><br /> <xref:Microsoft.AnalysisServices.Dimension> 上的 `Allowed` 會授與維度中所有屬性的寫入權限。<br /><br /> <xref:Microsoft.AnalysisServices.Cube> 上的 `Allowed` 會針對定義為 Type=writeback 之資料分割的 Cube 上的資料格授與其寫入權限。<br /><br /> <xref:Microsoft.AnalysisServices.MiningModel> 上的 `Allowed` 會授與修改模型內容的權限。<br /><br /> <xref:Microsoft.AnalysisServices.MiningStructure> 上的 `Allowed` 在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中沒有特定的意義。 **注意：** `Allowed`除非讀取也設定為，否則無法將寫入設定為`Allowed`|  
|管理**注意事項：** 僅在資料庫許可權中|{`true`, `false`}<br /><br /> 預設值=|指定成員是否可以管理資料庫。<br /><br /> `true` 會授與資料庫中所有物件的存取權。<br /><br /> 成員可以具有特定資料庫的管理權限，但不包含其他資料庫。|  
  
## <a name="see-also"></a>另請參閱  
 [物件和作業的存取權授權 &#40;Analysis Services&#41;](../authorizing-access-to-objects-and-operations-analysis-services.md)  
  
  
