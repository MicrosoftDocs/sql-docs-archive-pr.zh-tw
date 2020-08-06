---
title: 原生至 SharePoint 移轉 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c5b15bec-6fde-4174-bcde-d043307244dd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2377a3cb8c267c083cec6985f57fa07a734f875f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87710313"
---
# <a name="native-to-sharepoint-migration-ssrs"></a>原生至 SharePoint 移轉 (SSRS)
  您無法從一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 伺服器模式升級或轉換至另一個模式。 例如，您無法將原生模式報表伺服器升級或轉換為 SharePoint 模式。 您無法在兩種模式之間複製報表伺服器資料庫，因為它們使用不同的資料庫結構描述。 您可以將內容從一部報表伺服器移轉至另一部報表伺服器。 您使用的工具取決於為來源和目的地伺服器設定的報表伺服器模式類型。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式  
  
##  <a name="reporting-services-migration-tool"></a><a name="bkmk_native_to_sharepoint"></a> Reporting Services 移轉工具  
 此工具支援將內容從原生模式部署移轉至 SharePoint 模式部署。 此工具不支援從 SharePoint 模式移轉至 SharePoint 模式，或是從 SharePoint 模式移轉至原生模式。  
  
 如需詳細資訊，請參閱 [Reporting Services 移轉工具](https://www.microsoft.com/download/details.aspx?id=29560) (https://www.microsoft.com/download/details.aspx?id=29560) \(英文\)。  
  
## <a name="use-script-to-migrate-content"></a>使用指令碼來移轉內容  
 如果移轉工具不符合您的需求，您可以手動移轉報表伺服器資料。 下面為將報表項目從一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 部署移轉至另一個部署之步驟的摘要。 此方法支援以原生模式或 SharePoint 模式做為來源或目的地伺服器。  
  
1.  備份與還原加密金鑰。 這是用於加密資料的金鑰。 加密金鑰也用於加密密碼，例如，針對資料來源連接儲存的密碼。 不過，密碼無法移轉，因此您必須在目的地環境中再次輸入密碼。  
  
2.  **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] RSS 指令碼：** 撰寫呼叫報表伺服器 Web 服務 SOAP 方法的 Visual Basic 指令碼，以便在資料庫之間複製資料。 使用 **RS.exe** 公用程式來執行指令碼。 Rs.exe 會與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]一起安裝。  
  
    -   [在報表伺服器之間遷移內容的範例 Reporting Services rs.exe 腳本](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)。 本主題說明如何使用您可以從 CodePlex 下載的範例指令碼。  
  
    -   CodePlex 上的 rss 指令碼範例， [可將內容從一個報表伺服器移轉至另一個報表伺服器的 Reporting Services RS.exe 指令碼](https://azuresql.codeplex.com/releases/view/115207)。  
  
    -   [指令碼與 PowerShell 搭配 Reporting Services](../tools/scripting-and-powershell-with-reporting-services.md)  
  
 下表概述可以用指令碼來移轉的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 物件：  
  
|Object|可撰寫指令碼|註解|  
|------------|---------------------|--------------|  
|報表|是|在移轉之後，重新輸入資料來源的密碼。|  
|資料來源|是|在移轉之後，將報表重新連結至資料來源。|  
|模型|是||  
|資料集|是||  
|報表組件||在移轉之後，驗證或更新報表組件的路徑。|  
|排程|是|[Subscription and Delivery Methods](../report-server-web-service/methods/subscription-and-delivery-methods.md)請參閱 ListSchedules 方法|  
|訂用帳戶|是|請參閱列出訂閱者法[訂閱和傳遞方法](../report-server-web-service/methods/subscription-and-delivery-methods.md)和 ChangeSubscriptionOwner 方法<xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>|  
|快照集|||  
||||  
  
