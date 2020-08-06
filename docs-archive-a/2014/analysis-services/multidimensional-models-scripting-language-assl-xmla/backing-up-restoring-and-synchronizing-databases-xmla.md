---
title: 備份、還原和同步處理資料庫 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- restoring databases [XML for Analysis]
- backing up databases [XML for Analysis]
- database backups [XML for Analysis]
- synchronization [XML for Analysis]
- database restores [XML for Analysis]
ms.assetid: 6c021b2e-6ad0-444e-b23f-4b5f72ce084b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 500435a585ffed84a8f16e2b3bd1c4db14509103
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687313"
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>備份、還原和同步處理資料庫 (XMLA)
  在 XML for Analysis 中，有三個命令分別可用來備份、還原和同步處理資料庫：  
  
-   [Backup](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)命令會 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 備份檔案 ( .abf) 來備份資料庫，如[備份資料庫](#backing_up_databases)一節所述。  
  
-   [Restore](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)命令會 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 從 .abf 檔案還原資料庫，如[還原資料庫](#restoring_databases)一節中所述。  
  
-   [Synchronize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)命令會同步 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 處理一個資料庫與另一個資料庫的資料和中繼資料，如[同步處理資料庫](#synchronizing_databases)一節中所述。  
  
##  <a name="backing-up-databases"></a><a name="backing_up_databases"></a>備份資料庫  
 如先前所述，`Backup` 命令會將指定的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫備份到備份檔案。 `Backup` 命令具有各種屬性，可讓您指定要備份的資料庫、要使用的備份檔案、如何備份安全性定義以及要備份的遠端資料分割。  
  
> [!IMPORTANT]  
>  Analysis Services 服務帳戶必須擁有針對每個檔案所指定之備份位置的寫入權限。 此外，使用者必須具有下列其中一個角色： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的管理員角色，或在要備份之資料庫上擁有「完整控制權 (管理員)」權限的資料庫角色成員。  
  
### <a name="specifying-the-database-and-backup-file"></a>指定資料庫與備份檔案  
 若要指定要備份的資料庫，請設定命令的[Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)屬性 `Backup` 。 `Object` 屬性必須包含資料庫的物件識別碼，否則就會發生錯誤。  
  
 若要指定備份程式所要建立及使用的檔案，請設定命令的[file](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/file-element-xmla)屬性 `Backup` 。 `File` 屬性應該設定成要建立的備份檔案之 UNC 路徑與檔案名稱。  
  
 除了指定用於備份的檔案之外，還可以為指定的備份檔案設定下列選項：  
  
-   如果您將[AllowOverwrite](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/allowoverwrite-element-xmla)屬性設定為 true，則此 `Backup` 命令會覆寫備份檔案（如果指定的檔案已存在）。 如果將 `AllowOverwrite` 屬性設定為 False，而指定的備份檔案已經存在時，就會發生錯誤。  
  
-   如果您將[ApplyCompression](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/applycompression-element-xmla)屬性設定為 true，則會在檔案建立之後壓縮備份檔案。  
  
-   如果您將[Password](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/password-element-xmla)屬性設定為任何非空白的值，則會使用指定的密碼來加密備份檔案。  
  
    > [!IMPORTANT]  
    >  如果未指定 `ApplyCompression` 與 `Password` 屬性，備份檔案會以純文字儲存包含在連接字串中的使用者名稱與密碼。 以純文字儲存的資料可能會被擷取。 為了提高安全性，請使用 `ApplyCompression` 與 `Password` 設定來壓縮和加密備份檔案。  
  
### <a name="backing-up-security-settings"></a>備份安全性設定  
 [Security](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla)屬性會決定命令是否會 `Backup` 備份資料庫上定義的安全性定義，例如角色和許可權 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 `Security` 屬性也會決定備份檔案是否包含定義為安全性定義成員的 Windows 使用者帳戶與群組。  
  
 `Security` 屬性值只能是下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*SkipMembership*|在備份檔案中納入安全性定義，但是排除成員資格資訊。|  
|*CopyAll*|在備份檔案中納入安全性定義與成員資格資訊。|  
|*IgnoreSecurity*|從備份檔案排除安全性定義。|  
  
### <a name="backing-up-remote-partitions"></a>備份遠端資料分割  
 若要備份資料庫中的遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料分割，請將命令的[BackupRemotePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/backupremotepartitions-element-xmla)屬性設定 `Backup` 為 true。 這個設定會造成 `Backup` 命令為每個遠端資料來源建立一個遠端備份檔案，用來儲存資料庫的遠端資料分割。  
  
 針對要備份的每個遠端資料源，您可以在命令的 [[位置](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/locations-element-xmla)] 屬性中包含[Location](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/location-element-xmla)元素，藉以指定其對應的備份檔案 `Backup` 。 `Location`元素應 `File` 將其屬性設定為遠端備份檔案的 UNC 路徑和檔案名，並將其[DataSourceID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)屬性設定為資料庫中所定義之遠端資料源的識別碼。  
  
##  <a name="restoring-databases"></a><a name="restoring_databases"></a>還原資料庫  
 `Restore` 命令會從備份檔案還原指定的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。 `Restore` 命令具有各種屬性，可讓您指定要還原的資料庫、要使用的備份檔案、如何還原安全性定義、要儲存的遠端資料分割以及重新放置關聯式 OLAP (ROLAP) 物件。  
  
> [!IMPORTANT]  
>  對於每個備份檔案，執行還原命令的使用者必須擁有從針對每個檔案所指定之備份位置讀取的權限。 若要還原沒有安裝在伺服器上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，使用者也必須是該 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員。 若要覆寫 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，使用者必須具有下列其中一個角色：[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員，或在要還原之資料庫上擁有「完整控制權 (管理員)」權限的資料庫角色成員。  
  
> [!NOTE]  
>  還原現有的資料庫之後，還原資料庫的使用者可能會喪失已還原資料庫的存取權。 如果在執行備份時，使用者不是伺服器角色的成員，也不是擁有完整控制權 (管理員) 權限的資料庫角色成員，就可能會發生存取權喪失的情況。  
  
### <a name="specifying-the-database-and-backup-file"></a>指定資料庫與備份檔案  
 `DatabaseName` 命令的 `Restore` 屬性必須包含資料庫的物件識別碼，否則就會發生錯誤。 如果指定的資料庫已經存在，`AllowOverwrite` 屬性會決定是否覆寫現有的資料庫。 如果將 `AllowOverwrite` 屬性設定為 False，而指定的資料庫已經存在時，就會發生錯誤。  
  
 您應該將 `File` 命令的 `Restore` 屬性設定成要還原至指定資料庫的備份檔案之 UNC 路徑與檔案名稱。 您也可以為指定的備份檔案設定 `Password` 屬性。 如果將 `Password` 屬性設定為任何非空白值，就會使用指定的密碼來解密備份檔案。 如果備份檔案未加密，或者如果指定的密碼不符合用以加密備份檔案的密碼，就會發生錯誤。  
  
### <a name="restoring-security-settings"></a>還原安全性設定  
 `Security` 屬性會決定 `Restore` 命令是否會還原在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫上定義的安全性定義，例如角色和權限。 `Security` 屬性也會決定 `Restore` 命令是否會將定義為安全性定義成員的 Windows 使用者帳戶和群組包含在還原程序中。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*SkipMembership*|在資料庫中納入安全性定義，但是排除成員資格資訊。|  
|*CopyAll*|在資料庫中納入安全性定義與成員資格資訊。|  
|*IgnoreSecurity*|從資料庫排除安全性定義。|  
  
### <a name="restoring-remote-partitions"></a>還原遠端資料分割  
 對於每個在前一個 `Backup` 命令期間建立的遠端備份檔案，您可以在 `Location` 命令的 `Locations` 屬性中包含 `Restore` 元素，以還原其關聯的遠端資料分割。 每個元素的[DataSourceType](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla)屬性都 `Location` 必須排除或明確設定為*Remote*。  
  
 對於每個指定的 `Location` 元素，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會連絡在 `DataSourceID` 屬性中指定的遠端資料來源，以還原在 `File` 屬性中指定的遠端備份檔案中定義的資料分割。 除了 `DataSourceID` 與 `File` 屬性之外，每個 `Location` 元素都可以使用下列屬性來還原遠端資料分割：  
  
-   若要覆寫在 `DataSourceID` 中指定的遠端資料來源連接字串，您可以將 `ConnectionString` 元素的 `Location` 屬性設定成不同的連接字串。 `Restore` 命令接著將會使用包含在 `ConnectionString` 屬性中的連接字串。 如果未指定 `ConnectionString`，`Restore` 命令會為指定的遠端資料來源，使用儲存在備份檔案中的連接字串。 您可以使用 `ConnectionString` 設定將遠端資料分割移到不同的遠端執行個體。 不過，您無法使用 `ConnectionString` 設定將遠端資料分割還原至含有已還原資料庫的相同執行個體。 換句話說，您無法使用 `ConnectionString` 屬性將遠端資料分割變成本機資料分割。  
  
-   針對用來在遠端資料源上儲存遠端資料分割的每個原始檔案夾，您可以指定[folder](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/folder-element-xmla)元素，指出要在其中還原所有儲存在原始檔案夾中之遠端分割區的新資料夾。 如果未指定 `Folder` 元素，`Restore` 命令會使用為遠端備份檔案中包含的遠端資料分割所指定的原始資料夾。  
  
### <a name="relocating-rolap-objects"></a>重新放置 ROLAP 物件  
 `Restore` 命令無法為使用 ROLAP 儲存的物件還原彙總或是資料，因為這樣的資訊是儲存在基礎關聯式資料來源的資料表中。 不過，可以還原 ROLAP 物件的中繼資料。 若要還原 ROLAP 物件的中繼資料，`Restore` 命令會在關聯式資料來源上重新建立資料表結構。  
  
 您可以在 `Location` 命令中使用 `Restore` 元素，重新放置 ROLAP 物件。 針對 `Location` 用來重新放置資料來源的每個元素， `DataSourceType` 必須將屬性明確設定為*Local*。 另外，您也必須將 `ConnectionString` 元素的 `Location` 屬性設定為新位置的連接字串。 在還原期間，`Restore` 將會使用 `DataSourceID` 元素的 `Location` 屬性值，取代 `ConnectionString` 元素的 `Location` 屬性所識別的資料來源連接字串。  
  
##  <a name="synchronizing-databases"></a><a name="synchronizing_databases"></a>同步處理資料庫  
 `Synchronize` 命令會將指定之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的資料和中繼資料與另一個資料庫同步處理。 `Synchronize` 命令具有各種屬性，可讓您指定來源資料庫、如何同步處理安全性定義、要同步處理的遠端資料分割，以及 ROLAP 物件的同步處理。  
  
> [!NOTE]  
>  只有伺服器管理員與資料庫管理員可以執行 `Synchronize` 命令。 來源與目的地資料庫都必須具有相同的資料庫相容性層級。  
  
### <a name="specifying-the-source-database"></a>指定來源資料庫  
 命令的[Source](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)屬性 `Synchronize` 包含兩個屬性： `ConnectionString` 和 `Object` 。 `ConnectionString` 屬性包括含有來源資料庫之執行個體的連接字串，而 `Object` 屬性包含來源資料庫的物件識別碼。  
  
 目的地資料庫是 `Synchronize` 命令執行的工作階段目前的資料庫。  
  
 如果 `ApplyCompression` 命令的 `Synchronize` 屬性是設定為 True，從來源資料庫傳送到目的地資料庫的資訊，會在傳送之前先壓縮。  
  
### <a name="synchronizing-security-settings"></a>同步處理安全性設定  
 [SynchronizeSecurity](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla)屬性會決定命令是否會同步處理在 `Synchronize` 源資料庫上定義的安全性定義，例如角色和許可權。 `SynchronizeSecurity` 屬性也會決定 `Sychronize` 命令是否包含定義為安全性定義成員的 Windows 使用者帳戶與群組。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*SkipMembership*|在目的地資料庫中納入安全性定義，但是排除成員資格資訊。|  
|*CopyAll*|在目的地資料庫中納入安全性定義與成員資格資訊。|  
|*IgnoreSecurity*|從目的地資料庫排除安全性定義。|  
  
### <a name="synchronizing-remote-partitions"></a>同步處理遠端資料分割  
 對於每個存在於來源資料庫的遠端資料來源，您可以在 `Location` 命令的 `Locations` 屬性中包含 `Synchronize` 元素，以同步處理每個關聯的遠端資料分割。 針對每個專案 `Location` ， `DataSourceType` 必須排除或明確將屬性設為*Remote*。  
  
 為了定義和連接到目的地資料庫中的遠端資料來源，`Synchronize` 命令會使用定義在 `ConnectionString` 元素中 `Location` 屬性的連接字串。 `Synchronize` 命令接著會使用 `DataSourceID` 元素的`Location` 屬性，以識別要同步處理哪些遠端資料分割。 命令會在 `Synchronize` 源資料庫的屬性中指定的遠端資料源上， `DataSourceID` 與目的地資料庫的屬性中指定的遠端資料源同步處理遠端資料分割 `DataSourceID` 。  
  
 對於每個用以儲存來源資料庫上遠端資料來源中之遠端資料分割的原始資料夾，您也可以指定 `Folder` 元素中的 `Location` 元素。 `Folder` 元素會指定目的地資料庫的新資料夾，在這個資料夾中，會同步處理儲存在遠端資料來源原始資料夾中的所有遠端資料分割。 如果未指定 `Folder` 元素，Synchronize 命令會使用針對來源資料庫中包含的遠端資料分割所指定的原始資料夾。  
  
### <a name="synchronizing-rolap-objects"></a>同步處理 ROLAP 物件  
 `Synchronize` 命令無法為使用 ROLAP 儲存的物件同步處理彙總或是資料，因為這樣的資訊是儲存在基礎關聯式資料來源的資料表中。 不過，可以同步處理 ROLAP 物件的中繼資料。 若要同步處理中繼資料，`Synchronize` 命令會在關聯式資料來源上重新建立資料表結構。  
  
 您可以在 Synchronize 命令中使用 `Location` 元素，同步處理 ROLAP 物件。 針對 `Location` 用來重新放置資料來源的每個元素， `DataSourceType` 必須將屬性明確設定為*Local*。 . 另外，您也必須將 `ConnectionString` 元素的 `Location` 屬性設定為新位置的連接字串。 在同步處理期間，`Synchronize` 命令將會使用 `DataSourceID` 元素的 `Location` 屬性值，取代 `ConnectionString` 元素的 `Location` 屬性所識別的資料來源連接字串。  
  
## <a name="see-also"></a>另請參閱  
 [Backup 元素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Restore 元素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [&#40;XMLA&#41;同步處理元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [備份與還原 Analysis Services 資料庫](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
