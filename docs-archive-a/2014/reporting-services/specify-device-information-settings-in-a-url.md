---
title: 在 URL 中指定裝置資訊設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], URLs
- URL access [Reporting Services], device information settings
ms.assetid: cb7f7577-c6a8-4e6f-8e60-5ec0760f29c3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 00cd1fdc3b5fbe129ae4d51b220a11bc48b4744c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87703770"
---
# <a name="specify-device-information-settings-in-a-url"></a>在 URL 中指定裝置資訊設定
  裝置資訊設定是傳遞給轉譯延伸模組的參數。 如果您使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 報表伺服器 Web 服務的方法來轉譯報表，則會將 `DeviceInfo` XML 元素以輸入參數來傳遞。 `DeviceInfo` 元素的子元素是不同的轉譯延伸模組的裝置資訊設定所特有的。 您可以使用 *rc:tag=value* 參數字串，來包括 URL 中的裝置資訊設定，其中 *tag* 是要存取之裝置資訊設定元素的名稱。 如需 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中裝置資訊設定的詳細資訊，請參閱[將裝置資訊設定傳遞至轉譯延伸模組](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)。  
  
## <a name="example"></a>範例  
 下列範例使用影像轉譯延伸模組的 *OutputFormat* 裝置資訊來設定，以將指定報表的格式設定為 JPEG (已加入分行符號以利閱讀)：  
  
```  
http://servername/reportserver?/SampleReports  
/Employee Sales Summary&EmployeeID=38&rs:  
Command=Render&rs:Format=IMAGE&rc:OutputFormat=JPEG  
```  
  
## <a name="see-also"></a>另請參閱  
 [URL 存取 &#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 存取參數參考](url-access-parameter-reference.md)  
  
  
