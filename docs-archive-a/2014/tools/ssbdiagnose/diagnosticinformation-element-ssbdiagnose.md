---
title: DiagnosticInformation 元素 (ssbdiagnose) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose], diagnosticinformation element
- diagnosticinformation element
- ssbdiagnose
ms.assetid: 0cfda544-542c-4cf4-86d2-8031c91b10f6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 92d76a065c24ddc1fc8d85989ed3202308571951
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593255"
---
# <a name="diagnosticinformation-element-ssbdiagnose"></a>DiagnosticInformation 元素 (ssbdiagnose)
  **DiagnosticInformation** 元素包含報告此公用程式找到之診斷資訊的所有元素。 **DiagnosticInformation** 是 **ssbdiagnostic** XML 輸出檔的根元素。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DiagnosticInformation>   
    ...   
</DiagnosticInformation>  
```  
  
## <a name="element-attributes"></a>元素屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|`None`|N/A|  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|每個 **ssbdiagnose** XML 輸出檔發生一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|無。|  
|**子元素**|[Banner 元素 &#40;ssbdiagnose&#41;](banner-element-ssbdiagnose.md)<br /><br /> [Issue 元素 &#40;ssbdiagnose&#41;](issue-element-ssbdiagnose.md)|  
  
## <a name="remarks"></a>備註  
 如需有關 XML 命名空間的詳細資訊，請參閱 [MSDN Library 中的＜](https://go.microsoft.com/fwlink/?LinkId=7341) XML 文件中的命名空間 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ＞(英文)。  
  
## <a name="see-also"></a>另請參閱  
 [ssbdiagnose 公用程式 &#40;Service Broker&#41;](ssbdiagnose-utility-service-broker.md)  
  
  
