---
title: Reporting Services 例外處理的最佳做法 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], best practices
ms.assetid: 72fecf28-f02e-4338-b50f-0b21f520302d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2e0561c19fbd3e709a0440a55f023f938eabf692
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594937"
---
# <a name="best-practices-for-reporting-services-exception-handling"></a>Reporting Services 例外處理的最佳作法
  當開發 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 應用程式時，您可以使用幾個方法來消除或是減少例外狀況的發生次數。 當例外狀況真的發生時，提供明確且精簡的錯誤訊息給使用者，並加入適當的例外狀況處理，以防止應用程式非預期地結束。  
  
 將要求傳送給報表伺服器 Web 服務的應用程式應該執行下列項目：  
  
-   透過盡可能防止無效的要求以避免造成例外狀況。  
  
-   盡可能快取例外狀況並提供特定的錯誤處理程式碼。  
  
-   處理未擲回例外狀況的錯誤案例。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[防止無效的要求](preventing-invalid-requests.md)|描述可用以防止將無效的要求傳送到報表伺服器的技術。|  
|[使用 Try 和 Catch 區塊](using-try-and-catch-blocks.md)|描述如何進一步使用 Try/Catch 區塊來增強應用程式的可靠性。|  
|[處理未造成例外狀況的警告與案例](handling-warnings-and-cases-that-do-not-cause-exceptions.md)|說明如何處理錯誤才不會造成 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 擲回例外狀況。|  
|[使用詳細資料屬性來處理特定的錯誤](using-the-detail-property-to-handle-specific-errors.md)|說明如何使用 **SoapException** 物件的 **Detail** 屬性，以程式設計的方式處理特定錯誤。|  
  
## <a name="see-also"></a>另請參閱  
 [Detail 屬性](../soapexception-class/detail-property.md)   
 [Reporting Services 中的例外狀況處理簡介](../introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 類別](../soapexception-class/reporting-services-soapexception-class.md)  
  
  
