---
title: 使用傳遞延伸模組的通知類別 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], notifications
- notifications [Reporting Services]
- retry queues
- Nofication class
ms.assetid: 549c40c4-d33d-46c2-9d6a-7bbb671ac67a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8b274eb50405a02f4995b953611e50a234b11eab
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607283"
---
# <a name="using-a-notification-class-for-a-delivery-extension"></a>使用傳遞延伸模組的通知類別
  <xref:Microsoft.ReportingServices.Interfaces.Notification> 類別是位於 <xref:Microsoft.ReportingServices.Interfaces> 命名空間中，並代表傳遞延伸模組用於傳遞報表的訂閱資訊。 <xref:Microsoft.ReportingServices.Interfaces.Notification> 類別提供一些屬性可用以轉譯要傳遞的報表、決定通知狀態以及設定使用者資料。

 ![報告通知進程](../../media/bk-ext-03.gif "報表通知程序")通知是任何傳遞的核心物件

 當所引發的事件是與使用自訂傳遞延伸模組的訂閱相關聯時，會建立包含 <xref:Microsoft.ReportingServices.Interfaces.Report> 物件的通知。 <xref:Microsoft.ReportingServices.Interfaces.Report> 物件會封裝將指定報表轉譯為支援的轉譯格式所需的功能，並包含報表特定的屬性，例如伺服器上報表的 URL以及報表的名稱。 如需 <xref:Microsoft.ReportingServices.Interfaces.Report> 類別的詳細資訊，請參閱[使用傳遞延伸模組的報表類別](../delivery-extension/using-the-report-class-for-a-delivery-extension.md)。

 您將 <xref:Microsoft.ReportingServices.Interfaces.Notification> 物件傳遞到傳遞延伸模組的 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 方法。 您的 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 方法應該包含特定的程式碼以處理通知和提供報表。

 如需如何使用 <xref:Microsoft.ReportingServices.Interfaces.Notification> 類別的範例，請參閱 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889) (SQL Server Reporting Services 產品範例)。

## <a name="retry-functionality"></a>重試功能
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 可讓您為無法立即傳遞的通知建立重試佇列。 在報表伺服器叫用傳遞延伸模組的 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 方法之後，傳遞延伸模組可以要求報表伺服器稍後再重試傳遞。 如果這個情形發生，報表伺服器會將通知放在內部佇列中，然後在經過一段特定時間之後重試傳遞。 系統管理員可以使用 **MaxNumberOfRetries** XML 項目與 **PeriodBetweenRetries** XML 項目，來設定報表伺服器嘗試執行的重試之最大數目，以及 RSReportServer.config 檔案的傳遞延伸模組區段中重試之間的週期。 如果傳遞稍後成功或是如果達到重試嘗試的最大數目，就會從重試佇列移除通知。 如果傳遞在達到重試的最大數目之後失敗，就會捨棄通知。

## <a name="see-also"></a>另請參閱
 [Reporting Services 延伸](../reporting-services-extension-library.md)模組程式庫中[執行傳遞延伸](../delivery-extension/implementing-a-delivery-extension.md)模組


