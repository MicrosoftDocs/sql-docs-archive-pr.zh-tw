---
title: 變更資料庫嚮導 (SSRS 原生模式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.changedatabase.F1
helpviewer_keywords:
- Change Database Wizard
- report server database, create
ms.assetid: 1a2e8d18-5997-482f-a9c1-87d99f7407b8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c1ca83e3e09ffd1aa452c5253db5d7d9347490ba
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595523"
---
# <a name="change-database-wizard-ssrs-native-mode"></a>變更資料庫精靈 (SSRS 原生模式)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員提供了變更資料庫精靈，可引導您建立新的報表伺服器資料庫或是選取要搭配目前報表伺服器執行個體使用之現有報表伺服器資料庫的步驟。  
  
 如果您選取舊版中的報表伺服器資料庫，該資料庫將會升級，以符合它連接之報表伺服器執行個體的版本。 當此服務啟動時，它會檢查資料庫版本，並自動將它升級為目前的結構描述。  
  
 若要啟動此精靈，請按一下 **組態管理員內 [資料庫] 頁面上的** [變更資料庫] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 如需有關如何啟動 Configuration Manager 的指示 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]原生模式。  
  
## <a name="options"></a>選項。  
 **動作**  
 選取您要執行的工作。 您可以在原生或 SharePoint 整合模式中建立新的資料庫。 或者，您可以選取要搭配目前報表伺服器執行個體使用的現有報表伺服器資料庫。  
  
 **資料庫伺服器**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 主控報表伺服器資料庫之實例的名稱。 也可以在本機或遠端電腦上使用預設或具名的執行個體。 如果您要連接到已命名的實例，請以下列格式輸入伺服器名稱： \<*server*> \\ < *實例*>。  
  
 若要連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，您必須使用有權登入伺服器及更新資料庫資訊的認證。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員會使用目前的 Windows 認證，但是如果您沒有登入或資料庫權限，您就必須指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫登入。 您不能指定不同的 Windows 認證。 如果您想要以不同的 Windows 使用者身分連接，請以該使用者身分登入，然後啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員。  
  
 連接到遠端執行個體時，需要先啟用該執行個體進行遠端連接。 某些版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 依預設並不會啟用遠端連接。 若要確認是否允許遠端連接，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員並確認 TCP/IP 和具名管道通訊協定是否已啟用。 如果遠端執行個體也是具名執行個體，請確認 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務已啟用，而且在目標伺服器上執行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 提供了 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員的具名執行個體所要使用的通訊埠編號。  
  
 **Database**  
 指定儲存伺服器資料之報表伺服器資料庫的名稱。 您可以指定現有的資料庫或建立新的資料庫。  
  
 當您在 [動作] 頁面上選取 **[建立新的資料庫]** 時，精靈中會出現用來建立新資料庫的屬性。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員會建立依名稱繫結的兩個資料庫：包含靜態資料的資料庫以及儲存工作階段和工作資料的暫存資料庫。 如需詳細資訊，請參閱《線上叢書》中的 [報表伺服器資料庫 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 您也可以選擇現有的報表伺服器資料庫。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員不會篩選出無效的資料庫。 有效的資料庫是根據報表伺服器資料庫結構描述 (您無法選取遺失必要資料表、檢視表或預存程序的資料庫)。 如果您選擇針對舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]所建立的資料庫，此資料庫將會升級為目前的格式。  
  
 **語言**  
 只有當您要建立新的報表伺服器資料庫時，才會設定這個值。  
  
 您可以使用這個值來指定建立角色定義和描述所用的語言。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了以角色為基礎的授權模型，其中包含一組預先定義的角色。 這些角色會使用您指定的語言建立一次。 角色名稱和描述絕對不會以其他語言的形式出現，即使當您使用具有伺服器支援之文化特性或語言設定的瀏覽器來連接報表伺服器時，也是如此。 您所指定的語言也會決定用來建立 [我的報表] 資料夾名稱和 [我的報表] 功能之一部分的使用者資料夾名稱的語言。  
  
 **伺服器模式**  
 報表伺服器資料庫會支援原生模式或 SharePoint 整合模式。 這兩個模式互斥。  
  
 如果您要建立新的報表伺服器資料庫，您必須指定一個模式。 您所選取的模式會決定報表伺服器資料庫的結構，並將 `SharePointIntegrated` 報表伺服器系統屬性設定為 `true` 或 `false`。  
  
 如果您選取不同的報表伺服器資料庫，目前資料庫的模式會顯示在畫面上，好讓您知道目前資料庫的使用方式。  
  
 **認證**  
 指定用來將報表伺服器連接到報表伺服器資料庫的帳戶。 有效的值包括報表伺服器 Web 服務的服務帳戶、用來主控報表伺服器之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上定義的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 資料庫登入，或是 Windows 帳戶。 如果您使用的是 Windows 帳戶，您可以指定本機帳戶 (* \<computername> \\<使用者名稱 \> *) 如果報表伺服器和資料庫位於相同的電腦上，或者如果網域使用者帳戶位於相同網域的不同電腦上，則 (* \<domain> \\<使用者名稱 \> *) 。  
  
 報表伺服器將會建立資料庫登入，並為您指定的帳戶指派資料庫權限。  
  
 報表伺服器不會建立帳戶本身。 您所指定的帳戶必須已經存在，而且對部署組態必須是有效的。 具體而言，如果資料庫位於遠端電腦上，而且您想要使用 Windows 帳戶，您就必須指定在該電腦上具有登入權限的帳戶。  
  
 如果此電腦位於不同的網域或不信任的網域中，請考慮使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫登入。 如需有關選擇帳戶的詳細資訊，請參閱 [&#40;SSRS 設定報表伺服器資料庫連接 Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
 **總結**  
 在安裝程式設定連接之前先確認設定。  
  
 **進度和完成**  
 監視每項工作的進度。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫 &#40;SSRS 原生模式&#41;](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [變更認證 Wizard &#40;SSRS 原生模式&#41;](../../../2014/sql-server/install/change-credentials-wizard-ssrs-native-mode.md)   
 [建立原生模式報表伺服器資料庫 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Reporting Services 組態管理員 &#40;SSRS 原生模式的 F1 說明主題&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
