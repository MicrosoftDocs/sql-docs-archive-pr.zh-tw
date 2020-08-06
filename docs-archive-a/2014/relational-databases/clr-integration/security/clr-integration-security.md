---
title: CLR 整合安全性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- authorization [CLR integration]
- common language runtime [SQL Server], security
- database objects [CLR integration], security
ms.assetid: 05d7a471-c5d5-4730-b903-e4edc8157bb4
author: rothja
ms.author: jroth
ms.openlocfilehash: 0d99d32a061d8fe78a8ac3642a503cceb45f3809
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594585"
---
# <a name="clr-integration-security"></a>CLR 整合安全性
  通用語言執行平臺 (CLR) 的安全性模型，可 [!INCLUDE[ssNoVersion](../../../includes/dnprdnshort-md.md)] 管理及保護在 [!INCLUDE[ssNoVersion](../../../includes/tsql-md.md)] 語句或伺服器中執行之另一個 clr 物件的不同類型 clr 和非 CLR 物件之間的存取。 這些物件之間的呼叫稱為連結。 針對這些物件所執行的安全性檢查類型會因所涉及的連結類型而不同。  
  
 CLR 整合安全性模型具有下列目標：  
  
-   根據預設，在上執行 managed 使用者程式碼 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 執行可能危害 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 健全性的作業應該透過適當的高層級權限保護。  
  
-   Managed 使用者程式碼不應該取得資料庫中使用者資料或其他使用者程式碼的未經授權存取權。 使用者定義程式碼應該在叫用它之使用者工作階段的安全性內容底下執行，而且使用該安全性內容的正確權限執行。  
  
-   應該要有一些控制項來限制使用者程式碼存取伺服器外部的任何資源，並且針對本機資料存取和計算嚴格使用。  
  
-   使用者定義程式碼不應該透過在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 處理序中執行，取得系統資源的未經授權存取權。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 CLR 以程式碼存取為基礎的安全性模型。 本節將討論這種結合方法對於安全性的一些優點。  
  
 下表列出本節的主題。  
  
 [CLR 整合程式碼存取安全性](clr-integration-code-access-security.md)  
 討論 Managed 程式碼的程式碼存取安全性 (CAS) 模型。  
  
 [主機保護屬性和 CLR 整合程式設計](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)  
 提供不允許在 SAFE 和 EXTERNAL_ACCESS 組件中使用之主機保護屬性 (HPA) 值的相關資訊。  
  
 [CLR 整合安全性中的連結](../../../database-engine/dev-guide/links-in-clr-integration-security.md)  
 描述使用者程式碼片段如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中彼此呼叫。  
  
 [模擬和 CLR 整合安全性](../../../database-engine/dev-guide/impersonation-and-clr-integration-security.md)  
 討論 Managed 程式碼如何使用模擬來存取外部資源。  
  
 [允許部分信任的呼叫端](../../../database-engine/dev-guide/allowing-partially-trusted-callers.md)  
 討論 Managed 方法叫用其他組件所包含之類別中的方法時所引發的問題。  
  
 [應用程式網域和 CLR 整合安全性](../../../database-engine/dev-guide/application-domains-and-clr-integration-security.md)  
 描述如何將組件載入應用程式網域中。  
  
## <a name="see-also"></a>另請參閱  
 [管理 CLR 整合組件](../assemblies/managing-clr-integration-assemblies.md)  
  
  
