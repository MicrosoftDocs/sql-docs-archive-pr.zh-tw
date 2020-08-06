---
title: " (文字編輯器的選項-Transact-sql-索引標籤頁面) |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.SQL.Tabs
dev_langs:
- TSQL
ms.assetid: a4499784-67f7-46ef-9f7c-2d0fdd117a52
author: rothja
ms.author: jroth
ms.openlocfilehash: 6caa659d13f8089fdd9f990a55e503657ef72a43
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597992"
---
# <a name="options-text-editor---transact-sql---tabs-page"></a> (文字編輯器的選項-Transact-sql-索引標籤頁面) 
  使用這個對話方塊可以變更在 [!INCLUDE[ssDE](../includes/ssde-md.md)] 查詢編輯器中按下 Tab 鍵的移動行為，這個編輯器會用來撰寫 [!INCLUDE[tsql](../includes/tsql-md.md)] 指令碼。 若要顯示這些設定，請按一下 [工具]**** 功能表上的 [選項]****，並展開 [文字編輯器]**** 資料夾，再展開 [Transact-SQL]**** 子資料夾，然後按一下 [定位點]****。  
  
## <a name="setting-options-in-multiple-locations"></a>在多個位置設定選項  
 [!INCLUDE[ssDE](../includes/ssde-md.md)] 查詢編輯器的選項也可以在 [所有語言 - 索引標籤]**** 對話方塊中設定。 如果您使用 **[所有語言]** 對話方塊為其他 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 編輯器 (例如 DMX 或 MDX 編輯器) 設定不同的選項，則必須使用這個對話方塊重設 [!INCLUDE[ssDE](../includes/ssde-md.md)] 查詢編輯器選項。  
  
## <a name="indenting"></a>縮排  
 **None**  
 如果選取此選項，當您按下 ENTER 時所建立的新行就不會縮排。 資料指標會放在新行的第一個資料行上。  
  
 **封鎖**  
 如果選取此選項，當您按下 ENTER 鍵時所建立的新行就會自動縮排與上一行相同的距離。  
  
 **智慧型**  
 此選項無法使用。  
  
## <a name="tabs"></a>索引標籤  
 **定位點大小**  
 以空格數目，設定各定位點之間的距離。 預設值為四個空格。  
  
 **縮排大小**  
 以空格數目，設定自動縮排的大小。 預設值為四個空格。 會插入定位字元、空格字元或兩者，以填滿指定的大小。  
  
 **插入空格**  
 如果選取此選項，縮排作業僅會插入空格字元，而非定位字元。 例如，如果 [**縮排大小**] 設為5，則每當您按下 TAB 鍵或在主視窗的工具列上按一下 [**增加縮排**] 按鈕時，就會插入五個空白字元 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 。  
  
 **保留定位點**  
 如果選取此選項，縮排作業會儘可能插入最多的定位字元。 每個定位字元會填滿 **[定位點大小]** 中所指定的空格數目。 如果 **[縮排大小]** 不是 **[定位點大小]** 的倍數，就會加入空格字元以填滿差異。  
  
  
