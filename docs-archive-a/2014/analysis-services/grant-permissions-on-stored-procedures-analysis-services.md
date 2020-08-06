---
title: 授與預存程式的許可權 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 01793166-a3e5-4856-8302-21b82d494e69
author: minewiskan
ms.author: owend
ms.openlocfilehash: 13d75ca8b6ff6e7d482e9d69894091518aa9469e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594258"
---
# <a name="grant-permissions-on-stored-procedures-analysis-services"></a>授與預存程序 (Analysis Services) 的權限
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中的預存程序 (或組件) 是以 [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET 程式語言撰寫的外部常式，用於擴充 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的功能。 組件可讓開發人員利用跨語言整合、例外狀況處理、版本控制支援、部署支援和偵錯支援等優點。  
  
 您必須是伺服器管理員，才能註冊組件。 請參閱[&#40;Analysis Services&#41;授與伺服器管理員許可權](instances/grant-server-admin-rights-to-an-analysis-services-instance.md)。  
  
## <a name="security-context-for-stored-procedure-execution"></a>預存程序執行的安全性內容  
 所有使用者都可以呼叫預存程序。 視預存程序的設定方式而定，程序可在呼叫程序之使用者的內容中，或是在匿名使用者的內容中執行。 因為匿名使用者沒有安全性內容，請使用此功能及設定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的執行個體來允許匿名存取。  
  
 在使用者呼叫預存程序之後，但在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行預存程序之前，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會在預存程序內評估動作。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會根據已授與使用者的權限以及用來執行此程序的權限集合之間的交集，評估預存程序中的動作。 如果預存程序包含資料庫角色無法為使用者執行的動作，就不會執行該動作。  
  
 以下是用來執行預存程序的權限集合：  
  
-   **安全**在安全許可權集合中，預存程式無法存取 .NET Framework 中受保護的資源 [!INCLUDE[msCoName](../includes/msconame-md.md)] 。 此權限集合只允許計算。 這是最安全的權限集合；資訊不會洩露到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 之外，權限無法提高，使資料遭到竄改的風險降至最低。  
  
-   **外部存取**使用外部存取權限集時，預存程式就可以使用受控碼來存取外部資源。 將預存程序設定為此權限集合不會造成可能導致伺服器不穩定的程式設計錯誤。 不過，此權限集合可能會導致資訊洩露到伺服器之外，而且權限有可能提高及資料遭到竄改的風險。  
  
-   不**受限制**有了不受限制的許可權集合，預存程式就可以使用任何程式碼來存取外部資源。 使用此權限集合，就無法保證預存程序的安全性或可靠性。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型組件管理](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
