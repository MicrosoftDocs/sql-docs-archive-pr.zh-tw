---
title: File 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- File element
ms.assetid: 73dce835-9a80-4aef-8e0f-9dcf07dd5b80
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0eeb2bdcc9513ca6283447daca63c8bbc4fa1726
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704582"
---
# <a name="file-element-dta"></a>File 元素 (DTA)
  指定工作負載檔。 工作負載是針對需要微調的一或多個資料庫來執行的一組 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 工作負載檔可以是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼 (.sql) 或追蹤檔 (.trc)。 如需詳細資訊，請參閱 [啟動及使用 Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
  <Server>...</Server>  
  <Workload>  
    <File>...</File>  
  </Workload>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|請利用 `string` 資料類型來指定工作負載檔的目錄路徑。 例如：<br /><br /> `<File>C:\Tuning\tun.sql</File>`<br /><br /> 伺服器強制實施長度限制。|  
|**預設值**|無。|  
|**出現次數**|如果未指定任何其他工作負載類型，便需要使用這個元素一次。 您必須指定 **EventString**父系的 **File**、 **Database** 或 **Workload** 子元素，但只能使用一種類型。 例如，如果您利用 **File** 元素指定了工作負載，便不能在相同 XML 輸入檔中，同時利用 **Database** 元素來指定工作負載。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[Workload 元素 &#40;DTA&#41;](workload-element-dta.md)|  
|**子元素**|無。|  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[簡單 XML 輸入檔範例 &#40;DTA&#41;](simple-xml-input-file-sample-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
