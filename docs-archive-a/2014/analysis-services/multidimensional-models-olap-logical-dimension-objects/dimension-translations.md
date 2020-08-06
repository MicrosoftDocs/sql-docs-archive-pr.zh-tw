---
title: 維度翻譯 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], translations
- multiple language support [Analysis Services]
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- LCIDs
- translations [Analysis Services], dimensions
ms.assetid: 38fc1e05-2ac9-4816-b52b-dfd19c3a43a2
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6f31773ad871ef7e3fc8f99d57e7a9099335b899
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706889"
---
# <a name="dimension-translations"></a>維度翻譯
  翻譯是一種簡單的機制，用來將顯示的標籤和標題從某個語言變成另一個語言。 每一個翻譯都會定義成一組值：具有翻譯文字的字串以及具有語言識別碼的數字。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的所有物件都可使用翻譯。 維度也可以將屬性值翻譯。 用戶端應用程式負責尋找使用者已定義的語言設定，並將所有標題和標籤切換成以該語言顯示。 物件可以有您想要的任何翻譯數目。  
  
 簡單的 <xref:Microsoft.AnalysisServices.Translation> 物件是由語言識別碼和翻譯的標題所組成。 語言識別碼是具有語言識別碼的 `Integer`。 翻譯的標題則是翻譯的文字。  
  
 在中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，維度轉譯是維度名稱的特定語言標記法、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件名稱或其成員之一，例如標題、成員或階層層級。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]也支援 cube 物件的翻譯。  
  
 翻譯會針對可支援多種語言的用戶端應用程式，提供伺服器支援。 通常，檢視 Cube 及其維度的使用者來自許多不同國家 (地區)。 可將 Cube 及其維度的各種元素翻譯成不同語言則十分有用，如此這些使用者就可檢視和了解 Cube。 例如，法國的商務使用者使用法文地區設定的工作站存取 Cube 時，就可用法文查看物件屬性值。 而德國的商務使用者使用德文地區設定的工作站存取相同 Cube 時，就可用德文查看相同的物件屬性值。  
  
 用戶端電腦的定序和語言資訊是以地區設定識別碼 (LCID) 的格式予以儲存。 連接時，用戶端將 LCID 傳遞至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體。 執行個體會使用 LCID 來決定在提供 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的中繼資料時要使用的翻譯集。 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件不包含指定的翻譯，則使用預設語言來傳回內容給用戶端。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 翻譯](../multidimensional-models-olap-logical-cube-objects/cube-translations.md)   
 [翻譯 &#40;Analysis Services&#41;](../translations-analysis-services.md)   
 [全球化秘訣和最佳作法 &#40;Analysis Services&#41;](../globalization-tips-and-best-practices-analysis-services.md)  
  
  
