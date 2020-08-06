---
title: SharePoint 模式下 Analysis Services Server 的硬體和軟體需求 (SQL Server 2014) |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.topic: conceptual
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: ac169a334c2f375afb08ba9fdba4306ba11fd29e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606049"
---
# <a name="hardware-and-software-requirements-for-analysis-services-server-in-sharepoint-mode-sql-server-2014"></a>Analysis Services SharePoint 模式伺服器的硬體和軟體需求 (SQL Server 2014)

[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 同時支援 SharePoint 2010 和 SharePoint 2013。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 是在 SharePoint 伺服器陣列外執行，但是可以安裝於 SharePoint 伺服器上。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 是在 SharePoint 2010 伺服器陣列中的應用程式伺服器上執行，並使用 SharePoint 功能和基礎結構來支援伺服器作業。 若要安裝 SharePoint 任一版本的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]，請使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝精靈。 安裝完畢後，接著完成下列步驟：  
  
- 根據 SharePoint 版本執行適當版本的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 組態工具。  
  
- 若是 SharePoint 2013，請安裝[&#40;SharePoint 2013&#41;安裝或卸載 PowerPivot for SharePoint 增益集](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)。  

##  <a name="sql-server-edition-requirements"></a><a name="bkmk_sqleditions"></a> SQL Server Edition 需求  
 並非在所有版本的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中都提供商業智慧功能。 如需詳細資訊，請參閱[SQL Server 2014 版本支援的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)和[SQL Server 2014 的版本和元件](../editions-and-components-of-sql-server-2016.md)。  
  
 您可以在[Microsoft SQL Server 2014 版本](https://go.microsoft.com/fwlink/?LinkID=296445)資訊中找到目前的版本資訊。  
  

  
##  <a name="sql-server-licensing"></a><a name="bkmk_sqllicense"></a>SQL Server 授權  
 如需有關 SQL Server 授權的詳細資訊，請參閱下列主題：  
  
-   [SQL Server 2014 授權資料表](https://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf) (https://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf) 。  
  
-   [如何購買： SQL Server 授權模型支援](https://www.microsoft.com/licensing/product-licensing/sql-server-2014?activetab=sql-server-2014-pivot%3aprimaryr2) (https://www.microsoft.com/licensing/product-licensing/sql-server-2014?activetab=sql-server-2014-pivot%3aprimaryr2) 。  
  
##  <a name="analysis-services-installed-on-sharepoint-2013"></a><a name="bkmk_ssas__sharepoint_2013"></a>安裝在 SharePoint 2013 上的 Analysis Services  
 如果您將 SharePoint 模式的 Analysis Services 伺服器單獨安裝在某部伺服器上，則最低系統需求是以 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 而非 SharePoint Server 需求為基礎。  
  
 [安裝 SQL Server 2014 的硬體與軟體需求](hardware-and-software-requirements-for-installing-sql-server.md)  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 在新一代商務伺服器上執行效果最佳，這類伺服器提供更高的 RAM 臨界值和更強的處理能力。 系統會使用大量 RAM，將 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料儲存在記憶體中。 RAM 支援適應結構變更的能力。 額外的處理器支援執行未經處理及彙總之資料的長時間掃描。 資料會在動態環境中取得其結構，以回應透過 Excel 用戶端或前端介面初始化的使用者導向資料分析。  
  
> [!TIP]  
>  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 使用 L2 和 L3 快取。 為了提升效能，請考慮使用具有更大 L2 和 L3 快取的處理器。  
  
 下表描述不屬於 SharePoint 伺服器陣列一部分的 [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] 獨立伺服器適用的最低硬體和建議的硬體組態：  
  
|元件|最小值|建議|  
|---------------|-------------|-----------------|  
|處理器|64 位元雙核心處理器，3 GHz。|16 個核心|  
|RAM|8 GB 的 RAM|64 GB 的 RAM|  
|儲存體|80 GB 的儲存空間|80 GB 或以上|  
  
 如果您將 SharePoint 模式的 Analysis Services 伺服器安裝在 SharePoint 伺服器陣列的伺服器上，請透過下列連結檢閱 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 SharePoint Server 的最低系統需求：  
  
-   [安裝 SQL Server 2014 的硬體與軟體需求](hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [SharePoint 2013 的硬體和軟體需求](https://technet.microsoft.com/library/cc262485\(office.15\).aspx)。  
  
 標準的 SharePoint 2013 硬體與軟體建議適用於工作群組或小組的 Web 式文件管理解決方案。 由於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 處理需要大量資料，標準建議在整體工作負載很小的情況下就夠用。例如，使用者或活頁簿數目少於 100。 較大的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 部署需要更多運算能力。  
  
##  <a name="analysis-services-installed-on-a-sharepoint-2010-server"></a><a name="bkmk_ssas__sharepoint_2010"></a>Analysis Services 安裝在 SharePoint 2010 伺服器上  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 是在 SharePoint 2010 伺服器陣列中的應用程式伺服器上執行，並使用 SharePoint 功能和基礎結構來支援伺服器作業。 下表摘要說明與 SharePoint 2010 部署相關的需求：  
  
|元件|需求|  
|---------------|-----------------|  
|SharePoint 版本|SharePoint 2010 Enterprise，並且與 Excel Services、Secure Store Service，以及對 Windows Token Service 的宣告設定在相同的伺服陣列中。<br /><br /> SharePoint 必須使用 SharePoint 安裝程式中的伺服陣列選項安裝 (不支援 SharePoint 的獨立安裝選項)。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 會要求伺服器陣列基礎結構必須支援系統管理和資料存取。 獨立安裝不提供這些服務。<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器安裝不支援在 Windows 7 或 Windows Vista 上執行的 Developer Edition。|  
|Service Pack|需要 SharePoint Server 2010 Service Pack 1 (SP1)。<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 功能需要 SharePoint 2010 Service Pack 1。<br /><br /> 將舊版 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 升級為 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 需要 SharePoint 2010 的 2010 年 8 月份累計更新或更新版本。 2010 年 8 月份累計更新或更新版本應在安裝 SharePoint Service Pack 1 之後安裝。 的新安裝 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 不需要累計更新。 如需詳細資訊，請參閱已[發行 SharePoint 的2010年8月累計更新](https://blogs.technet.com/b/stefan_gossner/archive/2010/09/02/august-2010-cumulative-update-for-sharepoint-has-been-released.aspx)。|  
|SharePoint Web 應用程式|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2010 只支援設定成使用傳統模式驗證的 SharePoint Web 應用程式。 您如要將 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 加入至現有的伺服器陣列，請務必將您計劃與之搭配使用的 Web 應用程式設定成使用傳統模式驗證。 如需如何檢查驗證模式的指示，請參閱將[PowerPivot 方案部署到 SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint)中的「驗證 Web 應用程式是否使用傳統模式驗證」一節。|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器端資料重新整理所需的資料提供者|伺服器端資料重新整理會重複原本用來匯入資料的相同資料擷取步驟。 這表示，在用戶端工作站上用來匯入資料的資料提供者必須同樣存在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 伺服器上。<br /><br /> 此外，您必須有 ADO.NET Data Services 才能在 SharePoint 伺服器上使用資料摘要。 SharePoint 必要條件安裝程式不會自動安裝此軟體。 下列軟體必須手動安裝。<br /><br /> ADO.NET Data Services 3.5 SP1 執行階段元件，用來將 SharePoint 清單當做資料摘要匯出。 下載及安裝符合作業系統的版本：<br /><br /> 針對 Windows Server 2008 R2，請使用適用于[windows 7 和 Windows Server 2008 R2 的 .NET Framework 3.5 SP1 的 ADO.NET 資料服務更新](https://www.microsoft.com/download/details.aspx?id=2343)。 Windows Server 2008 R2 **SP1**已包含更新的提供者。<br /><br /> 針對 Windows Server 2008，請使用適用于[.NET Framework 3.5 SP1 的 ADO.NET 資料服務更新，windows 2000、Windows Server 2003、WINDOWS XP、Windows Vista 和 Windows https://go.microsoft.com/fwlink/?LinkId=158125) server 2008 (](https://www.microsoft.com/download/details.aspx?id=22734)。|  
  
 [判斷 (SharePoint 2010) 的硬體和軟體需求 (https://go.microsoft.com/fwlink/?LinkId=169734)](https://go.microsoft.com/fwlink/?LinkId=169734)  
  
## <a name="additional-information"></a>其他資訊  

