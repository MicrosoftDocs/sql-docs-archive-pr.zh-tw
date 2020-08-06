---
title: 安裝 Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, installing
- SSIS, installing
- installing Integration Services, about installing Integration Services
- SQL Server Integration Services, installing
- Setup [Integration Services], about installing Integration Services
- installing Integration Services
- Setup [Integration Services]
ms.assetid: bd20fd3a-414b-4581-959d-ebba4ddf5a55
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4a5d1e12af23c58ad42154455718d0e99cf8b399
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596191"
---
# <a name="install-integration-services"></a>安裝 Integration Services
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了單一安裝程式，以安裝它的任何或所有元件，包含 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]在內。 您可以使用安裝程式來安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ，不論單一電腦上是否有其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件。  
  
 本主題將強調幾個重要考量事項，在您安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]之前應該先了解這些事項。 本主題的資訊將可幫助您評估安裝選項，好讓您可以做出讓安裝成功的選擇。  
  
 本主題不包含啟動安裝程式、使用安裝精靈或是從命令列執行安裝程式的相關指示。 如需如何啟動安裝程式並選取要安裝之元件的逐步指示，請參閱[SQL Server 2014 的快速啟動安裝](../../getting-started/quick-start-installation-of-sql-server-2014.md)。 如需安裝之命令列選項的相關資訊 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ，請參閱[從命令提示字元安裝 SQL Server 2014](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
## <a name="preparing-to-install-integration-services"></a>準備安裝 Integration Services  
 在安裝之前 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ，請檢查下列需求：  
  
-   [安裝 SQL Server 2014 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [檢查 System Configuration Checker 的參數](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)  
  
-   [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
## <a name="selecting-an-integration-services-configuration"></a>選取 Integration Services 組態  
 您可以在以下組態中安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]：  
  
-   您可以將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 安裝在沒有舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的電腦上。  
  
-   您可以將 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 與 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 和 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]的現有執行個體並存安裝。  
  
     如果您在已安裝其中一個舊版 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 的電腦上升級到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ，則 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 會與舊版並存安裝。  
  
     如需升級 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的詳細資訊，請參閱 [升級 Integration Services](upgrade-integration-services.md)。 如需與舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]之回溯相容性的資訊，請參閱 [Integration Services 回溯相容性](../integration-services-backward-compatibility.md)。  
  
## <a name="installing-integration-services"></a>安裝 Integration Services  
 在檢閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的安裝需求並確認電腦符合這些需求之後，您就可以開始安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。  
  
> [!NOTE]  
>  在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，當您安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，Users 群組中的所有使用者預設都能存取 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務。 安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]時，使用者則無法存取 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務。 因此，服務預設是安全的。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝之後， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員必須執行 DCOM 設定工具 ( # A0) ，以授與特定使用者**SQL Server Integration Services 12.0**的存取權。  
>   
>  如需如何授與權限的指示，請參閱 [授與 Integration Services 服務的權限](../grant-permissions-to-integration-services-service.md)。  
  
 如果您要使用安裝精靈安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，您將會使用一連串的頁面來指定元件和選項。 以下是安裝程式中的頁面，其中選取的選項會影響您的安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ，並選取建議：  
  
-   **特徵選取**  
  
     選取 [Integration Services]****，即可安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務並在設計環境外面執行封裝。  
  
     如需 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的完整安裝，以及開發和管理封裝的工具與文件集，請同時選取 [Integration Services]**** 和下列 [共用功能]****：  
  
    -   [SQL Server Data Tools]****，以便安裝設計封裝的工具。  
  
    -   [管理工具 - 完整]****，以便安裝管理封裝的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
    -   [用戶端工具 SDK]****，以便安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 程式設計的 Managed 組件。  
  
     許多資料倉儲解決方案也需要安裝其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件，例如 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。  
  
    > [!NOTE]  
    >  [安裝精靈] 的 [功能選取]  頁面上提供一些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件供您選取安裝，以安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的部分元件。 這些元件對特定的工作有用，但 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的功能會受到限制。 例如，[Database Engine Services]  選項會安裝 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 所需的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件。 [SQL Server Data Tools]**** 選項會安裝設計封裝所需的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件，但是不會安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務，而且您無法在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 外部執行封裝。 為了確保 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 能完整安裝，您必須在 [功能選擇]  頁面上選取 [Integration Services]  。  
  
     **在 64 位元電腦上安裝**：在 64 位元電腦上，選取 [Integration Services]**** 只會安裝 64 位元的執行階段和工具。 如果您必須以 32 位元模式執行封裝，您也必須選取其他選項來安裝 32 位元的執行階段和工具：  
  
    -   如果64位電腦正在執行 x86 作業系統，請選取 [ **SQL Server Data Tools** ] 或 [**管理工具-完成**]。  
  
    -   如果64位電腦正在執行 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] 作業系統，請選取 [**管理工具-完成**]。  
  
     **在 ETL 的專用伺服器上安裝** ：若要使用擷取、轉換和下載 (ETL) 處理序的專用伺服器，我們建議您在安裝 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 時安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的本機執行個體。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 通常會將封裝儲存在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體中，而且它會仰賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來排程這些封裝。 如果此 ETL 伺服器沒有 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體，您就必須從具有 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體的伺服器排程或執行封裝。 這表示，雖然封裝無法在 ETL 伺服器上執行，但是它們會改在啟動封裝的伺服器上執行。 因此，系統將無法如預期方式使用專用 ETL 伺服器的資源。 此外，其他伺服器的資源可能會受到執行中 ETL 處理序的限制。  
  
-   **執行個體組態**  
  
     您在 [執行個體組態]**** 頁面上所做的任何選取都不會影響 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務。  
  
     您在電腦上只能安裝一個 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務執行個體。 您可以使用電腦名稱來連接此服務。  
  
     根據預設， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務設定為可管理儲存在 Database Engine 執行個體之 **msdb** 資料庫中的封裝，該執行個體與 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]同時安裝。 如果 Database Engine 執行個體並未與 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]同時安裝， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務會設定為可管理儲存在本機預設 **執行個體之** msdb [!INCLUDE[ssDE](../../includes/ssde-md.md)]資料庫中的封裝。 若要管理儲存在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]具名執行個體或遠端執行個體中的封裝，或儲存在多個 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體中的封裝，您就必須修改組態檔。 如需如何修改此組態檔的詳細資訊，請參閱[設定 Integration Services 服務 &#40;SSIS 服務&#41;](../service/integration-services-service-ssis-service.md)。  
  
-   **伺服器設定**  
  
     在 [伺服器組態]**** 頁面的 [服務帳戶]**** 索引標籤上，檢閱 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的設定。  
  
     如果已安裝 Windows 7 或 Windows Server 2008 R2， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務會註冊在 NT Services\MsDtsServer120 虛擬帳戶底下執行，而且**啟動類型**為 [**自動**]。  您不需要為此虛擬帳戶輸入密碼。 如果已安裝 Microsoft Vista 或 Windows Server 2008，系統會將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務註冊為在內建網路服務帳戶之下執行，而且 [啟動類型]**** 為 [自動]****。 您不需要針對內建的網路服務帳戶輸入密碼。  
  
 根據預設，在新的安裝中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會設定為不要將與封裝執行相關的事件記錄至應用程式事件記錄檔。 當您使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的資料收集器功能時，這個設定可避免產生過多的事件記錄項目。 不會記錄的事件包括 EventID 12288「封裝已啟動」和 EventID 12289「封裝已成功完成」。 若要將這些事件記錄到應用程式事件記錄檔，請開啟登錄進行編輯。 在登錄中找出 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS 節點，然後將 LogPackageExecutionToEventLog 設定的 DWORD 值從 0 變更為 1。  
  
## <a name="understanding-the-integration-services-service"></a>了解 Integration Services 服務  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務。  
  
 當您在 [功能選擇]**** 頁面上選取 [Integration Services]**** 選項時，就會安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務。 當您在 [伺服器組態]**** 頁面上接受預設設定時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務就會啟用而且其 [啟動類型]**** 是 [自動]****。  
  
 您在一部電腦上只能安裝單一 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的執行個體。 此服務並非特定 Database Engine 執行個體特有的。 您可以使用執行此服務所在的電腦名稱來連接此服務。  
  
## <a name="installing-integration-services-on-64-bit-computers"></a>在 64 位元電腦上安裝 Integration Services  
  
### <a name="integration-services-features-installed-on-64-bit-computers"></a>64 位元電腦上安裝的 Integration Services 功能  
 安裝程式會根據您所選取的安裝選項來安裝各種 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 功能：  
  
-   當您安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並選取 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 進行安裝時，安裝程式就會安裝所有可用的 64 位元 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 功能和工具。  
  
-   如果您需要 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 設計階段功能，就必須一併安裝 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  
  
-   如果您需要 32 位元版本的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行階段與工具，才能在 32 位元模式中執行特定的封裝，即必須一併安裝 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  
  
 64 位元的功能安裝於 [Program Files]**** 目錄下，而 32 位元的功能則另外安裝在 [Program Files (x86)]**** 目錄下。 (此行為不是 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的特有行為)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)](也就是 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的 32 位元開發環境) 在 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] 64 位元作業系統上不受支援，且不會安裝在 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] 伺服器上。  
  
  
