---
title: PowerPivot 可用性和嚴重損壞修復 (SQL Server 2014) |Microsoft Docs
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4aaf008c-3bcb-4dbf-862c-65747d1a668c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 51a48470887f83515ddee8d01c1bb209dfa94008
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687261"
---
# <a name="powerpivot-availability-and-disaster-recovery-sql-server-2014"></a>PowerPivot 高可用性及災害復原 (SQL Server 2014)
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 的可用性和災害復原計畫主要取決於您的 SharePoint 伺服器陣列的設計、不同元件可接受的停機時間以及針對 SharePoint 可用性所實作的工具和最佳作法。 本主題摘要說明技術，並包含在規劃部署的可用性和嚴重損壞修復時所要考慮的範例拓撲圖表 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 。

||
|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|

 **本主題內容：**

-   [PowerPivot 高可用性的 SharePoint 2013 拓撲範例](#bkmk_sharepoint2013)

-   [PowerPivot 高可用性的 SharePoint 2010 拓撲範例](#bkmk_sharepoint2010)

-   [PowerPivot 服務應用程式資料庫及 SQL Server 可用性和復原技術](#bkmk_sql_server_technologies)

-   [詳細資訊連結](#bkmk_more_resources)

##  <a name="example-sharepoint-2013-topology-for-powerpivot-high-availability"></a><a name="bkmk_sharepoint2013"></a>PowerPivot 高可用性的 SharePoint 2013 拓撲範例
 在 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 部署中，您設計 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 可用性的方式有更大的彈性。 在 SharePoint 2013 中，以 SharePoint 模式部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體 (也稱為 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 伺服器) 會在 SharePoint 伺服器陣列外部執行，而且可以安裝在不同的伺服器上。 SharePoint 模式下的每個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體都會向 Excel Services 註冊。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 共用服務和服務應用程式會在 SharePoint 應用程式伺服器上執行。

 下圖描述 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 部署範例。 這個範例支援 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服務的正常可用性，並假設資料庫會定期備份。

 ![2013 中的 powerpivot 可用性](../media/ssas-powerpivot-services-2013.png "2013 中的 powerpivot 可用性")

-   **(1)** Web 前端伺服器。 使用 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 增益集，將資料提供者安裝在每部伺服器上。 如需詳細資訊，請參閱[安裝或卸載 PowerPivot for SharePoint 增益集 &#40;SharePoint 2013&#41;](../instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)。

-   **(2)**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 共用服務會在 **每部** 應用程式伺服器上執行，並允許服務應用程式 **跨** 應用程式伺服器來執行。 因此，如果單一應用程式伺服器離線， [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 應用程式依然可以使用。

-   **(3)** Excel Calculation Services 會在每部應用程式伺服器上執行，並允許服務應用程式跨應用程式伺服器來執行。 因此，如果單一應用程式伺服器離線，Excel Calculation Services 依然可以使用。

-   ** (4) **和** (6) **的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ins 實例 sharepoint 模式會在 sharepoint 伺服器陣列外部的伺服器上執行，這包括 Windows 服務**SQL Server Analysis Services (POWERPIVOT) **。 這些執行個體都會向 Excel Services 註冊 **(3)**。 Excel Services 會管理傳送給 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 伺服器之要求的負載平衡。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 架構可讓您擁有 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 適用的多部伺服器，好讓您可以視需要輕鬆地加入更多執行個體。 如需詳細資訊，請參閱 [Manage Excel Services data model settings (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780\(v=office.15\).aspx)(管理 Excel Services 資料模型設定 (SharePoint Server 2013))。

-   **(5)** 用於內容、組態和應用程式資料庫的 SQL Server 資料庫。 其中包括 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式資料庫。 您的 DR 計畫應該包括資料庫層。 在此設計中，資料庫會在其中一個 **執行個體上與** (4) [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 相同的伺服器上執行。 **(4)** 和 **(5)** 也可能會在不同的伺服器上。

-   **(7)** 某個形式的 SQL Server 資料庫備份或備援。

##  <a name="example-sharepoint-2010-topology-for-powerpivot-high-availability"></a><a name="bkmk_sharepoint2010"></a>PowerPivot 高可用性的 SharePoint 2010 拓撲範例
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 架構要求所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 元件都在相同的 SharePoint 應用程式伺服器上執行。 其中包括在 SharePoint 模式中部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體以及兩個共用服務 (相較於 SharePoint 2013 部署則只有一個)。

 下圖描述 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 部署範例。 這個範例支援 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服務的正常可用性，並假設資料庫會定期備份。

 ![sharepoint 2010 中的 powerpivot 可用性](../media/ssas-powerpivot-services-2010.png "sharepoint 2010 中的 powerpivot 可用性")

-   **(1)** Web 前端伺服器。 在每部伺服器上安裝資料提供者。 如需詳細資訊，請參閱 [在 SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)。

-   ** (2) **在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] SharePoint 應用程式伺服器上安裝的兩個共用服務和** (4) ** Windows 服務**SQL Server Analysis Services (POWERPIVOT) ** 。

     [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務會在 **每部** 應用程式伺服器上執行，並允許服務應用程式 **跨** 應用程式伺服器來執行。 如果單一應用程式伺服器離線， [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服務應用程式依然可以使用。

     若要提高 SharePoint 2010 中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 容量，請部署更多 SharePoint 應用程式伺服器來執行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務。

-   **(3)** Excel Calculation Services 會在每部應用程式伺服器上執行，並允許服務應用程式跨應用程式伺服器來執行。 因此，如果單一應用程式伺服器離線，Excel Calculation Services 依然可以使用。

-   **(5)** 用於內容、組態和應用程式資料庫的 SQL Server 資料庫。 其中包括 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式資料庫。 您的 DR 計畫應該包括資料庫層。

-   **(6)** 某個形式的 SQL Server 資料庫備份或備援。

##  <a name="powerpivot-service-application-database-and-sql-server-availability-and-recovery-technologies"></a><a name="bkmk_sql_server_technologies"></a>PowerPivot 服務應用程式資料庫和 SQL Server 可用性和修復技術
 在您的 SharePoint 高可用性規劃中包含 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服務應用程式資料庫。 這個資料庫的預設名稱為 `DefaultPowerPivotServiceApplicationDB-<GUID>`。 以下是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用性技術的摘要和搭配使用 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 資料庫時的建議。 如需詳細資訊，請參閱 [Supported high availability and disaster recovery options for SharePoint databases (SharePoint 2013)](https://technet.microsoft.com/library/jj841106.aspx)(SharePoint 資料庫支援的高可用性和災害復原選項 (SharePoint 2013))。

||註解|
|-|--------------|
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 同步鏡像的可用性。|支援，但不建議使用。 建議在同步認可模式中使用 AlwaysOn。|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)]在同步認可模式中|支援和建議。|
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 非同步鏡像或記錄傳送至另一個伺服器陣列以進行災害復原。|支援。|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)]針對嚴重損壞修復進行非同步認可|支援|

-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]

-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄傳送

 如需有關如何使用 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]規劃冷待命案例的詳細資訊，請參閱＜ [PowerPivot 災害復原](https://social.technet.microsoft.com/wiki/contents/articles/22137.sharepoint-powerpivot-disaster-recovery.aspx)＞。

## <a name="verification"></a>驗證
 如需指引和腳本，協助您在嚴重損壞 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 修復週期前後驗證部署，請參閱[檢查清單：使用 PowerShell 驗證 PowerPivot for SharePoint](../instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md)。

##  <a name="links-to-more-information"></a><a name="bkmk_more_resources"></a>詳細資訊的連結

-   [Supported high availability and disaster recovery options for SharePoint databases (SharePoint 2013)](https://technet.microsoft.com/library/jj841106.aspx)

-   [規劃嚴重損壞修復 (SharePoint Server 2010)](https://technet.microsoft.com/library/ff628971\(v=office.14\).aspx)




