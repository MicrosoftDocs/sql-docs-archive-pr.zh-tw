---
title: 報表屬性對話方塊、參考 (報表產生器) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10082"
ms.assetid: 3414c857-8ea6-4fc4-a6d5-b4883c039efa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2c28e9053a1c13f8d0e0b7b44f3b1a037976c318
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87702402"
---
# <a name="report-properties-dialog-box-references-report-builder"></a>報表屬性對話方塊、參考 (報表產生器)
  選取 **[報表屬性]** 對話方塊上的 **[參考]** ，即可將參考加入報表定義中運算式所使用的自訂或其他外部組件以及自訂類別執行個體，或從中移除。 在報表產生器的本機模式中不支援自訂組件。 若要撰寫使用自訂群組件的報表，請使用中的報表設計師 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 。  
  
## <a name="options"></a>選項  
 **加入或移除組件**  
 列出報表參考的組件。 組件必須可以在安裝設計報表所使用之工具的電腦和報表伺服器上使用。 參考的名稱必須與 **\<CodeModule>** 報表定義語言中標記的內容完全相符 ( .rdl) 檔案。  
  
 **加入**  
 按一下即可加入組件。 按一下省略號 ( ... ) ] 按鈕以開啟 [**開啟**] 對話方塊，並選取完成報表處理和運算式評估所需的元件。  
  
 **移除**  
 若要從清單中移除組件參考，請選取組件名稱，再按一下 **[移除]** 按鈕。  
  
 **加入或移除類別**  
 列出報表所使用的類別執行個體。 類別清單僅供以執行個體為基礎的成員使用，並非供靜態成員使用。  
  
 **加入**  
 按一下即可加入類別參考。 按一下省略號 ( ... ) ] 按鈕以開啟 [**開啟**] 對話方塊，並選取完成報表處理和運算式評估所需的類別。  
  
 **移除**  
 若要刪除類別執行個體，請選取該執行個體，並按一下 **[移除]** 按鈕。  
  
 **設定**  
 若為具有相依性的類別，您可將這個參考移動至清單中的較高位置。  
  
 **Down**  
 若為具有相依性的類別，您可將這個參考移動至清單中的較低位置。  
  
## <a name="see-also"></a>另請參閱  
 [對話方塊、窗格和嚮導的報表產生器說明](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
  
