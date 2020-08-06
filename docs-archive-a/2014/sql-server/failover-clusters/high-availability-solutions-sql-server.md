---
title: 高可用性方案 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], solutions
- Database Engine [SQL Server], availability
- database availability [SQL Server]
- availability [SQL Server]
- server availability [SQL Server]
ms.assetid: b2eda634-0f8e-4703-801b-7ba895544ff5
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 83e7dde423fadcc0cd7d4d34dd4fd05b460cf453
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595600"
---
# <a name="high-availability-solutions-sql-server"></a>高可用性解決方案 (SQL Server)
  本主題會介紹幾個可增進伺服器或資料庫可用性的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 高可用性解決方案。 高可用性解決方案可遮蔽硬體或軟體失敗所造成的影響，並維護應用程式的可用性，進而讓使用者的停機時間減至最少。  
  
> [!NOTE]  
>  如需支援所指定高可用性解決方案之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的相關資訊，請參閱 [SQL Server 2014 版本支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)的＜高可用性 (AlwaysOn)＞一節。  
 ( # RecommendedSolutions)   
  
##  <a name="overview-of-sql-server-high-availability-solutions"></a><a name="TermsAndDefinitions"></a>SQL Server 高可用性解決方案的總覽  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供幾個選項用於建立伺服器或資料庫的高可用性。 高可用性選項包括下列各項：  
  
 AlwaysOn 容錯移轉叢集執行個體  
 AlwaysOn 容錯移轉叢集實例是 alwayson 供應專案的一部分，它會 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 利用 Windows Server 容錯移轉叢集 (WSFC) 功能，透過伺服器實例層級的冗余來提供本機高可用性-*容錯移轉叢集實例* (FCI) 。 FCI 是跨 Windows Server 容錯移轉叢集 (WSFC) 節點且可能跨多個子網路安裝的單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 在網路上，FCI 看似單一電腦上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，但是 FCI 提供容錯移轉，可以在目前的 WSFC 節點無法使用時，從該節點容錯移轉到另一個節點。  
  
 如需詳細資訊，請參閱 [AlwaysOn 容錯移轉叢集執行個體 (SQL Server)](windows/always-on-failover-cluster-instances-sql-server.md)。  
  
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 所導入的企業級高可用性災害復原方案，讓您可將一或多個使用者資料庫的可用性最大化。 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 要求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體必須位於 Windows Server 容錯移轉叢集 (WSFC) 節點上。 如需詳細資訊，請參閱[AlwaysOn 可用性群組 (SQL Server) ](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)。  
  
> [!NOTE]  
>  FCI 可以利用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 提供資料庫層級的遠端災害復原。 如需詳細資訊，請參閱[容錯移轉叢集和 AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)。  
  
 資料庫鏡像  
 > [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 我們建議您改用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 。  
  
 資料庫鏡像是支援近乎瞬間的容錯移轉，進而提高資料庫可用性的方案。 資料庫鏡像可用以維護實際執行的資料庫 (稱為 *「主體資料庫」*) 所對應的單一待命資料庫 (或稱 *「鏡像資料庫」*)。 如需詳細資訊，請參閱[資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
 記錄傳送  
 記錄傳送就像 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 與資料庫鏡像一樣，都是在資料庫層級運作。 您可以使用記錄傳送來針對單一實際執行資料庫 (稱為「主要資料庫」**) 維護一個或多個暖待命資料庫 (稱為「次要資料庫」**)。 如需記錄傳送作業的相關資訊，請參閱[關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)。  
  
##  <a name="recommended-solutions-for-using-sql-server-to-protect-data"></a><a name="RecommendedSolutions"></a> 使用 SQL Server 保護資料的建議方案  
 為您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境提供資料保護的建議如下：  
  
-   對於透過協力廠商共用磁碟方案 (SAN) 的資料保護，我們建議您使用 AlwaysOn 容錯移轉叢集執行個體。  
  
-   對於透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的資料保護，我們建議您使用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]。  
  
    > [!NOTE]  
    >  如果您執行不支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]版本，建議使用記錄傳送。 如需支援 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的相關資訊，請參閱 [SQL Server 2014 版本支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)的＜高可用性 (AlwaysOn)＞一節。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 的 Windows Server 容錯移轉叢集 &#40;WSFC&#41;](windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [資料庫鏡像：互通性與共存性 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-interoperability-and-coexistence-sql-server.md)   
 [SQL Server 2014 中已被取代的 Database Engine 功能](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)  
  
  
