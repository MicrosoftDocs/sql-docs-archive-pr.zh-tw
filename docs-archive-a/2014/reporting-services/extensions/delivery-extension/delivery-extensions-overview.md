---
title: 傳遞延伸模組概觀 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- subscriptions [Reporting Services], delivery extensions
- delivery extensions [Reporting Services], about extensions
ms.assetid: a30600a9-bbed-4519-9426-3470ff2982e7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 61ad2879e2c449f9179670b3626e668eae92cfc1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87710385"
---
# <a name="delivery-extensions-overview"></a>傳遞延伸模組概觀
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 可讓使用者建立和發行報表，一旦建立和發行，就可以傳遞給各個位置。 除此之外，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包括數個傳遞延伸模組以及一個傳遞 API，可讓開發人員建立其他的傳遞延伸模組，以進一步擴充在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的傳遞功能。  
  
 下表列出 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 隨附的傳遞延伸模組。  
  
|傳遞延伸模組|描述|  
|------------------------|-----------------|  
|報表伺服器電子郵件|使用 SMTP 伺服器以電子郵件將報表寄到個別的使用者或群組。|  
|報表伺服器檔案共用|用以將組織中的報表散發到網路檔案共用。 提供依指定排程將報表自動複製到檔案共用的功能。|  
  
 ![Reporting Services 傳遞延伸模組架構](../../media/bk-reportservicedelivery.gif "Reporting Services 傳遞延伸模組架構")  
Reporting Services 傳遞延伸模組架構  
  
 傳遞延伸模組會與訂閱配對。 建立訂閱時，使用者可以選擇其中一個可用的傳遞延伸模組，以決定如何傳遞報表。 在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中，訂閱會位在報表伺服器資料庫中。 當事件發生時，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 會針對包含在報表伺服器資料庫中的訂閱與事件配對。 對於每個與事件繫結的訂閱，報表伺服器會建立通知。 對於資料驅動訂閱，會為每個收件者建立通知。 一旦建立通知，報表伺服器會叫用特定的傳遞延伸模組，並為在通知中指定的延伸模組設定傳遞值。 傳遞延伸模組會將通知傳遞給選取傳遞延伸模組所指定的使用者。  
  
 傳遞延伸模組會實作 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組 API。 透過支援 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組 API，傳遞延伸模組能夠從報表伺服器收到通知，並提供通知的狀態。  
  
 報表伺服器並不會管理通知和報表的傳遞目的地。 收集目的地資訊是透過在傳遞延伸模組中撰寫的程式碼來完成。  
  
## <a name="subscriptions-and-delivery-extensions"></a>訂閱與傳遞延伸模組  
 用戶端應用程式會使用報表伺服器 Web 服務的兩個方法，來建立使用傳遞延伸模組的訂閱：<xref:ReportService2010.ReportingService2010.CreateSubscription%2A> 與 <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>。 對於修改已經存在的訂閱，會使用 <xref:ReportService2010.ReportingService2010.SetSubscriptionProperties%2A> 與 <xref:ReportService2010.ReportingService2010.SetDataDrivenSubscriptionProperties%2A> 方法。 在建立訂閱時，使用者也會為訂閱選取傳遞延伸模組，並為必要的延伸模組設定輸入值。 當使用者儲存訂閱時，會將它儲存在報表伺服器資料庫中。 訂閱會根據排程或是事件來建立通知。 當傳遞開始時，選取的傳遞延伸模組會先從組態檔載入任何組態資料。 接下來，會擷取訂閱的延伸模組設定並設定值。 最後，會呼叫 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 方法，並傳送通知。  
  
## <a name="developer-requirements"></a>開發人員需求  
 開發 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組必須具有：  
  
-   安裝報表設計師的部署電腦。  
  
-   已安裝 [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] 或是 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 軟體開發套件 (SDK) 的開發電腦。  
  
-   對 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 特性與功能有深入的了解，特別是訂閱與傳遞。  
  
-   如果您計劃為報表管理員實作自訂的訂閱使用者介面，需要對 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 與 Web 控制項有深入的了解。  
  
-   [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 語言的開發經驗，例如 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET。  
  
## <a name="see-also"></a>另請參閱  
 [實作傳遞延伸模組](../delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
