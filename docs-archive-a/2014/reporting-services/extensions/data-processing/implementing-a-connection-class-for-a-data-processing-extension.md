---
title: 為資料處理延伸模組實作連線類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- connections [Reporting Services], data processing extensions
- Connection class
- data processing extensions [Reporting Services], connections
ms.assetid: 7047d29e-a2c9-4e6f-ad02-635851a38ed7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 84caac40ec8df198d5c26ed89bf35fad71ad914f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708949"
---
# <a name="implementing-a-connection-class-for-a-data-processing-extension"></a>為資料處理延伸模組實作 Connection 類別
  **Connection** 物件代表資料庫連線或是類似的資源，而且是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組之使用者的起點。 它代表資料庫伺服器的連接，不過任何具有類似行為的實體都可以公開成 **Connection**。  
  
 若要實作 **Connection** 物件，請建立實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 的類別，並選擇性地實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>。  
  
 在您的實作中，您必須確保在執行命令之前先建立和開啟連接。 請確保實作要求用戶端明確地開啟和關閉連接，而不是讓您的實作隱含地為用戶端開啟和關閉連接。 在取得連接時執行您的安全性檢查。 在 [!INCLUDE[ssRS](../../../includes/ssrs.md)] 資料處理延伸模組中需要其他類別的現有連接，將可確保在與資料來源搭配使用時永遠執行安全性檢查。  
  
 所需連接的屬性是以連接字串來表示。 強烈建議 [!INCLUDE[ssRS](../../../includes/ssrs.md)] 資料處理延伸模組使用由 OLE DB 定義的熟悉名稱/值組系統來支援 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection.ConnectionString%2A> 屬性。  
  
> [!NOTE]  
>  **Connection** 物件通常需要大量資源才能取得，因此您可能會想要考慮共用連線或是其他技術來減輕這個問題。  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 繼承自 <xref:Microsoft.ReportingServices.Interfaces.IExtension>。 您必須將 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 介面實作為連接類別實作的一部分。 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 介面允許類別實作當地語系化的延伸模組名稱，並處理在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 組態檔中儲存的延伸模組特定組態資訊。  
  
 您的 **Connection** 物件透過其 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 的實作，包含 <xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A> 屬性。 強烈建議 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組支援 <xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A> 屬性，這樣使用者便會在使用者介面遇到熟悉且當地語系化的延伸模組名稱，例如報表管理員。  
  
 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 也允許您的 **Connection** 物件擷取和處理儲存在 RSReportServer.config 檔案中的自訂設定資料。 如需有關處理自訂組態資料的詳細資訊，請參閱＜<xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>＞方法。  
  
 當未卸載其餘的資料處理延伸模組類別時，實作 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 的類別不會從記憶體卸載。 因此，您可以使用 **Extension** 類別來儲存跨連線的狀態資訊，或是儲存可以在記憶體中快取的資料。 只要報表伺服器正在執行，您的 **Extension** 類別仍然會在記憶體中。  
  
 您可以透過實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> 來擴充 **Connection** 類別，以包含對 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中認證的支援。 當您實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> 介面的 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.IntegratedSecurity%2A>、<xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.UserName%2A> 和 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.Password%2A> 屬性時，可以啟用 [整合式安全性] 核取方塊，以及在報表設計師 [資料來源] 對話方塊的 [使用者名稱] 與 [密碼] 文字方塊。 這允許報表設計師儲存和擷取支援驗證的資料來源之認證。 會將認證安全地儲存並在預覽模式中轉譯報表時使用。  
  
> [!NOTE]  
>  若要隱含實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>，您必須實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 與 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 介面的成員。  
>   
>  如需範例 **Connection** 類別的實作，請參閱 [SQL Server Reporting Services 產品範例](https://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../reporting-services-extensions.md)   
 [實作資料處理延伸模組](implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
