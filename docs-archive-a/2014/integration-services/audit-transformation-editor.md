---
title: Audit 轉換編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.audittransformation.f1
helpviewer_keywords:
- Audit Transformation Editor
ms.assetid: 32786a34-5870-4fde-83c7-ec74d62404b8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: af6490643a0bef60cca961dc9a0564c5f6b46484
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707737"
---
# <a name="audit-transformation-editor"></a>稽核轉換編輯器
  稽核轉換可讓封裝中的資料流程包含有關封裝執行的環境資料。 例如，可以將封裝、電腦與操作員的名稱加入資料流程。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包括提供此資訊的系統變數。  
  
 若要深入了解稽核轉換，請參閱＜ [Audit Transformation](data-flow/transformations/audit-transformation.md)＞。  
  
## <a name="options"></a>選項  
 **輸出資料行名稱**  
 提供包含稽核資訊之新輸出資料行的名稱。  
  
 **Audit 類型**  
 選取可用的系統變數以提供稽核資訊。  
  
|值|描述|  
|-----------|-----------------|  
|**執行執行個體 GUID**|插入唯一識別封裝之執行執行個體的 GUID。|  
|**封裝識別碼**|插入唯一識別封裝的 GUID。|  
|**封裝名稱**|插入封裝名稱。|  
|**版本識別碼**|插入唯一識別封裝版本的 GUID。|  
|**執行開始時間**|插入封裝開始執行的時間。|  
|**電腦名稱**|插入啟動封裝的電腦名稱。|  
|**使用者名稱**|插入啟動封裝之使用者的登入名稱。|  
|**工作名稱**|插入與稽核轉換相關聯之資料流程工作的名稱。|  
|**工作識別碼**|插入唯一識別與稽核轉換相關聯之資料流程工作的 GUID。|  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
