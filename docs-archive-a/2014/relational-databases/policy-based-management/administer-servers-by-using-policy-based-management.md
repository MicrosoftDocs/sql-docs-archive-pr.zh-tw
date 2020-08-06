---
title: 使用原則式管理來管理伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- facet See facets
- Declarative Management Framework See Policy-Based Management
- surface area configuration [SQL Server], Policy-Based Management
- Policy-Based Management
- facets [Policy-Based Management]
- Policy-Based Management, administering
- conditions [Policy-Based Management]
- facets [Policy-Based Management], about facets
- PolicyAdministratorRole role
ms.assetid: ef2a7b3b-614b-405d-a04a-2464a019df40
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c0f415ffbc10b93cee2037da78daef3b7ee5aba9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87697981"
---
# <a name="administer-servers-by-using-policy-based-management"></a>使用原則式管理來管理伺服器
  以原則為基礎的管理是用於管理一或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的系統。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原則管理員使用原則式管理時，他們會使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 建立管理伺服器上實體的原則，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體、資料庫或其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件。  
  
## <a name="benefits-of-policy-based-management"></a>原則式管理的優點  
 原則式管理在解決下列狀況所呈現的問題方面很有用：  
  
-   公司原則禁止啟用 Database Mail 或 SQL Mail。 因此，建立原則來檢查這兩項功能的伺服器狀態。 管理員會比較伺服器狀態與此原則。 如果伺服器狀態不符合規範，管理員就會選擇設定模式，而且此原則會讓伺服器狀態符合規範。  
  
-   [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫具有要求所有預存程序都以字母 AW_ 為開頭的命名慣例。 因此，建立原則來強制執行此原則。 管理員會測試此原則，並且收到不符合規範之預存程序的清單。 如果未來的預存程序不符合此命名慣例，預存程序的建立陳述式就會失敗。  
  
> [!NOTE]  
>  請注意，原則可能會影響某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能之運作方式。 例如，異動資料擷取和異動複寫都會使用沒有索引的 systranschemas 資料表。 如果您啟用了所有資料表都必須擁有索引的原則，則強制此原則的合規性將會造成這些功能失敗。  
  
 原則利用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 加以建立及管理。 此程序包含下列步驟：  
  
1.  選取包含要設定之屬性的以原則為基礎的管理 Facet。  
  
2.  定義指定管理 Facet 狀態的條件。  
  
3.  定義包含此條件、可篩選目標集的其他條件及評估模式的原則。  
  
4.  檢查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體是否符合此原則。  
  
 若為失敗的原則，[物件總管] 會指出嚴重健全狀況警告成為目標旁的紅色圖示以及 [物件總管] 樹狀結構中較高的節點。  
  
> [!NOTE]  
>  當系統計算原則的物件集時，根據預設會排除系統物件。  例如，如果原則的物件集是指所有資料表，則原則不會套用至系統資料表。 如果使用者想要對系統物件評估原則，可以明確地將系統物件加入至物件集。 不過，雖然 **check on schedule** 評估模式支援所有原則，但基於效能的考量， **check on change** 評估模式並未支援所有原則與任意物件集搭配使用。 如需詳細資訊，請參閱[https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx](https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx)  
  
## <a name="policy-based-management-concepts"></a>原則式管理概念  
 原則式管理有三個元件：  
  
-   原則管理  
  
     原則管理員會建立原則。  
  
-   明確管理  
  
     管理員會選取一或多個 Managed 目標並且明確檢查這些目標是否符合特定原則，或明確讓這些目標符合原則。  
  
-   評估模式  
  
     有四種評估模式式，其中三種模式可以自動化：  
  
    -   **視需要**。 這種模式會在使用者直接指定時評估原則。  
  
    -   **變更時: 避免**。 這種自動模式會使用 DDL 觸發程序來防止原則違規。  
  
        > [!IMPORTANT]  
        >  如果停用了巢狀觸發程序伺服器組態選項，[變更時: 避免]**** 將無法正確運作。 以原則為基礎的管理會依賴 DDL 觸發程序來偵測及回復不符合使用此評估模式之原則的 DDL 作業。 移除以原則為基礎的管理 DDL 觸發程序或停用巢狀觸發程序時，將會造成這個評估模式失敗或以非預期的方式執行。  
  
    -   **變更時：僅限記錄**檔。 這種自動模式會在發生相關變更時使用事件通知來評估原則。  
  
    -   **按排程時間**。 這種自動模式會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業來定期評估原則。  
  
     未啟用自動原則時，原則式管理將不會影響系統效能。  
  
## <a name="policy-based-management-terms"></a>原則式管理條款  
 原則式管理 Managed 目標  
 以原則為基礎之管理所管理的實體，例如 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體、資料庫、資料表或索引。 伺服器執行個體中的所有目標都會構成目標階層。 目標集是指將一組目標篩選套用至目標階層所產生的目標集，例如 HumanResources 結構描述所擁有之資料庫中的所有資料表。  
  
 以原則為基礎的管理 Facet  
 針對特定 Managed 目標類型建立行為或特性模型的一組邏輯屬性。 屬性的數目和特性會建立在 Facet 中，而且只能由 Facet 的建立者加入或移除。 一個目標類型可以實作一或多個管理 Facet，而一個管理 Facet 可以由一或多個目標類型實作。 Facet 的某些屬性只能套用至特定版本。  
  
 以原則為基礎的管理條件  
 一種布林運算式，可指定以原則為基礎之管理 Managed 目標所允許的一組狀態 (與管理 Facet 有關)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在評估條件時嘗試觀察定序。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序不完全符合 Windows 定序時，請測試您的條件，以決定演算法如何解決衝突。  
  
 以原則為基礎的管理原則  
 以原則為基礎的管理條件和預期的行為，例如評估模式、目標篩選和排程。 一個原則只能包含一個條件。 您可以啟用或停用原則。 原則會儲存在 msdb 資料庫中。  
  
 以原則為基礎的管理原則類別目錄  
 協助管理原則的使用者定義類別目錄。 使用者可以將原則分類至不同的原則類別目錄中。 一個原則只能屬於一個原則類別目錄。 原則類別目錄會套用至資料庫和伺服器。 下列條件會在資料庫層級套用：  
  
-   資料庫擁有者可以讓資料庫訂閱一組原則類別目錄。  
  
-   只有來自其訂閱類別目錄的原則可以管理資料庫。  
  
-   所有資料庫都會隱含訂閱預設的原則類別目錄。  
  
 原則類別目錄可以在伺服器層級上套用到所有資料庫。  
  
 有效原則  
 目標的有效原則就是管理此目標的這些原則。 只有在滿足下列所有條件時，原則對於目標而言才有效：  
  
-   此原則已啟用。  
  
-   目標屬於此原則的目標集。  
  
-   目標或其中一個目標上階，訂閱了包含此原則的原則群組。  
  
## <a name="policy-based-management-tasks"></a>原則式管理工作  
 原則式管理是用於管理一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的原則式系統。 您可以使用以原則為基礎的管理來建立包含條件運算式的條件。 然後，建立將這些條件套用至資料庫目標物件的原則。  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述原則式管理原則的儲存方式。|原則式管理原則儲存|  
|描述如何設定警示，在原則失敗時通知原則管理員。|[設定警示以便向原則管理員通知原則失敗](configure-alerts-to-notify-policy-administrators-of-policy-failures.md)|  
|描述如何建立、檢視、修改及刪除原則式管理條件。|[建立新的原則式管理條件](create-a-new-policy-based-management-condition.md)<br /><br /> [刪除原則式管理條件](delete-a-policy-based-management-condition.md)<br /><br /> [檢視或修改原則式管理條件的屬性](view-or-modify-the-properties-of-a-policy-based-management-condition.md)|  
|描述如何建立、檢視、修改與刪除原則式管理原則。|[建立原則式管理原則](create-a-policy-based-management-policy.md)<br /><br /> [刪除原則式管理原則](delete-a-policy-based-management-policy.md)<br /><br /> [檢視或修改原則式管理原則的屬性](view-or-modify-the-properties-of-a-policy-based-management-policy.md)|  
|描述如何匯出及匯入原則式管理原則。|[匯出原則式管理原則](export-a-policy-based-management-policy.md)<br /><br /> [匯入原則式管理原則](import-a-policy-based-management-policy.md)|  
|描述如何確認伺服器執行個體、資料庫、伺服器物件或資料庫物件符合原則。|[根據物件評估原則式管理原則](evaluate-a-policy-based-management-policy-from-an-object.md)<br /><br /> [根據原則式管理原則評估該原則](evaluate-a-policy-based-management-policy-from-that-policy.md)<br /><br /> [依照排程評估原則式管理原則](evaluate-a-policy-based-management-policy-on-a-schedule.md)|  
|描述如何檢視及複製原則式管理 Facet 狀態至檔案|[使用原則式管理 Facet](working-with-policy-based-management-facets.md)|  
|提供一組原則檔可讓您將其做為最佳作法原則進行匯入，然後說明如何針對包含執行個體、執行個體物件、資料庫或資料庫物件的目標集，評估原則。|[使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)|  
|在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中提供物件總管的 [原則管理]**** 節點之 F1 說明主題。|[原則管理節點 &#40;物件總管&#41;](../../ssms/object/object-explorer.md)|  
  
## <a name="see-also"></a>另請參閱  
 [以原則為基礎的管理檢視 &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/policy-based-management-views-transact-sql)  
  
  
