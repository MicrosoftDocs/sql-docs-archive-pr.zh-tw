---
title: 字元對應轉換編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.charactermaptransformation.f1
helpviewer_keywords:
- Character Map Transformation Editor
ms.assetid: 3f1dbcf9-9cca-4606-bdcc-7ea6ad48cdf3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c6cdcdba448dafc6ccf03774d4f611dee704b823
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593508"
---
# <a name="character-map-transformation-editor"></a>字元對應表轉換編輯器
  使用 [字元對應表轉換編輯器]**** 對話方塊，來選取要套用至資料行資料的字串函數，以及指定對應是就地變更或加入為新資料行。  
  
 若要深入了解字元對應表轉換，請參閱＜ [Character Map Transformation](data-flow/transformations/character-map-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **可用的輸入資料行**  
 使用此對話方塊來選取要使用字串函數轉換的資料行。 您的選擇會在下面的資料表中出現。  
  
 **輸入資料行**  
 從上述資料表檢視選取的輸入資料行。 您也可以藉由使用可用的輸入資料行之清單來變更或移除選擇。  
  
 **目的地**  
 指定字串作業之結果的儲存方式為就地儲存、使用現有的資料行儲存，或將修改的資料儲存為新的資料行。  
  
|值|描述|  
|-----------|-----------------|  
|新增資料行|將資料儲存在新的資料行中。 在 **[輸出別名]** 之下指派資料行名稱。|  
|就地變更|將修改的資料儲存在現有的資料行中。|  
  
 **作業**  
 從字串函數要套用至資料行資料的清單中選取。  
  
|值|描述|  
|-----------|-----------------|  
|小寫|轉換為小寫。|  
|大寫|轉換為大寫。|  
|位元組反轉|藉由反轉位元組的順序來進行轉換。|  
|平假名|將日文片假名字元轉換為平假名。|  
|片假名|將日文平假名字元轉換為片假名。|  
|半形|將全形字元轉換為半形。|  
|全形|將半形字元轉換為全形。|  
|語言大小寫|套用大小寫的語言規則 (突厥語系和其他地區設定的 Unicode 簡單大小寫對應) 來取代系統規則。|  
|簡體中文|將繁體中文字元轉換為簡體中文。|  
|繁體中文|將簡體中文字元轉換為繁體中文。|  
  
 **輸出別名**  
 輸入每一個輸出資料行的別名。 預設為輸入資料行的名稱，後面接著 **[的副本]** ；但是您也可以選擇任何唯一的描述性名稱。  
  
 **設定錯誤輸出**  
 使用 [設定錯誤輸出](../../2014/integration-services/configure-error-output.md) 對話方塊，即可指定此轉換的錯誤處理選項。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
