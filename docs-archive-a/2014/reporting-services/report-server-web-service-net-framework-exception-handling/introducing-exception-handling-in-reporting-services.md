---
title: Reporting Services 中的例外狀況處理簡介 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], exception handling
- errors [Reporting Services]
- exceptions [Reporting Services]
- Report Server Web service, exception handling
- XML Web service [Reporting Services], exception handling
ms.assetid: 54381870-ce67-482b-aa83-6a838cdbf9b9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 091b1f40d293515617e369b750a5f18dfe12951b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699319"
---
# <a name="introducing-exception-handling-in-reporting-services"></a>Reporting Services 中的例外狀況處理簡介
  如果您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式將要求傳送到報表伺服器 Web 服務，但是此服務無法處理，則服務會將 SOAP 例外狀況傳回用戶端。 報表伺服器 Web 服務擲回的處理例外狀況是所開發應用程式的重要部分之一，因為當錯誤發生時，可以傳回有用的資訊給使用者。  
  
 本節包含的特定資訊，是有關處理例外狀況以防止使用者的無效輸入，並將有意義的錯誤資訊傳回給使用者。 如需例外狀況處理的一般資訊，請參閱 SDK 檔中的「處理和擲回例外狀況」 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[處理 Reporting Services 中的例外狀況](handling-exceptions-in-reporting-services.md)|提供 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的例外狀況概觀以及從 Web 服務傳回錯誤的 SOAP 角色。|  
|[Reporting Services 例外處理的最佳作法](best-practices/best-practices-for-reporting-services-exception-handling.md)|提供如何處理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的例外狀況之建議。|  
|[Reporting Services SoapException 類別](soapexception-class/reporting-services-soapexception-class.md)|描述 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的 **SoapException** 類別。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和 .NET Framework 建置應用程式](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
