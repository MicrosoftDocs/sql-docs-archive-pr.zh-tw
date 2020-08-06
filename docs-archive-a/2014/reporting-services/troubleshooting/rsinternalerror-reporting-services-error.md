---
title: rsInternalError - Reporting Services 錯誤 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsInternalError
ms.assetid: 52613d52-fc78-4870-93f0-7d393ab9c335
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 85b88519df810f60c580ad2d6eb355dde236d081
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596461"
---
# <a name="rsinternalerror---reporting-services-error"></a>rsInternalError - Reporting Services 錯誤
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|rsInternalError|  
|事件來源|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|元件|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|訊息文字|報表伺服器發生內部錯誤。 請參閱錯誤記錄以取得更多詳細資料。|  
  
## <a name="explanation"></a>說明  
 這是一般錯誤訊息，後面通常會跟隨更具描述性的錯誤訊息，提供更多詳細資料。  
  
 內部錯誤並不常見。 如果您收到這個錯誤，可以在報表伺服器追蹤記錄內取得詳細資訊。 除此之外，如果您是以本機管理員的身分在發生錯誤的電腦上執行，則可以檢視呼叫堆疊，以取得詳細資訊。  
  
## <a name="user-action"></a>使用者動作  
 若要判斷此訊息的特定原因，請參閱位於 \Microsoft SQL Server\MSRS12. \<instancename > 的報表伺服器記錄檔。\Reporting Services\logfiles 如需詳細資訊，請參閱 [Reporting Services 記錄檔和來源](../report-server/reporting-services-log-files-and-sources.md)。  
  
 若要檢視呼叫堆疊，請以滑鼠右鍵按一下發生錯誤的頁面，然後指向 [檢視來源]  。 檢視呼叫堆疊時，將需要錯誤發生所在之相同電腦上的系統管理員權限。  
  
 如果沒有其他資訊可用，您可以再次嘗試您的要求。  
  
## <a name="internal-only"></a>僅供內部使用  
  
## <a name="see-also"></a>另請參閱  
 [啟動與停止報表伺服器服務](../report-server/start-and-stop-the-report-server-service.md)  
  
  
