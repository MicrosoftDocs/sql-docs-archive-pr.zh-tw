---
title: 選項 (文字編輯器-XML-一般頁面) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 46a9f913-d0b9-40ff-b382-9bbdec7461a6
author: rothja
ms.author: jroth
ms.openlocfilehash: 70d7f3130342a6b8ac7e92e1eaf3e89869ff4148
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686471"
---
# <a name="options-text-editor---xml---general-page"></a>選項 (文字編輯器 - XML - 一般頁面)
  使用這個對話方塊可以變更 XML 編輯器的一般編輯行為，這個編輯器會用來編輯 XML 文件。 若要顯示這些設定，請在 **[工具]** 功能表上按一下 **[選項]** ，展開 **[XML]** 子資料夾，然後按一下 **[一般]**。  
  
## <a name="setting-options-in-multiple-locations"></a>在多個位置設定選項  
 XML 編輯器的選項也可以在 **[所有語言 - 一般]** 對話方塊中設定。 如果您使用 **[所有語言]** 對話方塊為其他 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 編輯器 (例如 DMX 或 MDX 編輯器) 設定不同的選項，則必須使用這個對話方塊重設 XML 編輯器選項。  
  
## <a name="statement-completion"></a>陳述式完成  
 **自動列出成員**  
 選取此核取方塊時，可用的成員、屬性、值或方法的清單，會於編輯器內進行鍵入時顯示。 從快顯清單擇取任何項目，以將其插入程式碼。  
  
 **隱藏進階成員**  
 無法使用此核取方塊。  
  
 **參數資訊**  
 如果選取此核取方塊，目前宣告或程序的完整語法及其所有可用的參數，就會顯示在編輯器中插入點的左方。 您可以指派的下一個參數會以粗體顯示。  
  
## <a name="settings"></a>設定  
 **啟用虛擬空間**  
 如果選取此核取方塊，就會在每一行程式碼的結尾插入空間。 選取此核取方塊，即可在程式碼旁的一致位置上放置註解。  
  
 **自動換行**  
 如果選取此核取方塊，超出可檢視的編輯器區域的行之任何部份，就會自動顯示在下一行。 選取此核取方塊會啟用 **[顯示自動換行的視覺化圖像]** 核取方塊。  
  
 **顯示自動換行的視覺化圖像**  
 如果選取此核取方塊，就會顯示換行箭頭標記，其中過長的行就會自動換行到第二行。 如果您不想顯示這些標記，請清除此核取方塊。  
  
> [!NOTE]  
>  這些提醒箭頭不會加入您的程式碼中，且不會列印。 它們僅供參考。  
  
 **沒有選取項目時，請套用剪下/複製命令至空白行**  
 當您在空白行上放置插入點、不選取任何內容，然後按一下 **[複製]** 或 **[剪下]** 時，此核取方塊就會設定編輯器的行為。  
  
 如果選取此核取方塊，就會複製或剪下空白行。 接著，如果您按一下 **[貼上]**，就會插入一個新的空白行。  
  
 如果清除此核取方塊，就不會複製或剪下任何內容。 接著，您按一下 **[貼上]**，就會貼上最近複製的內容。 如果先前沒有進行複製，就不會有貼上動作。  
  
 當行不是空白時，此設定對 **[複製]** 或 **[剪下]** 沒有影響。 如果沒有選取內容，就會複製或剪下整個行。 接著，如果您按一下 **[貼上]**，就會貼上整行的文字與其結束字元。  
  
## <a name="display"></a>顯示  
 **行號**  
 如果選取此核取方塊，行號就會出現在每一行程式碼的旁邊。  
  
> [!NOTE]  
>  這些行號不會加入您的程式碼中，且不會列印。 它們僅供參考。  
  
 **啟用按一下方式的 URL 導覽**  
 如果選取此核取方塊，當游標在編輯器中的 URL 上方時會變成手指符號。 按一下 URL 即可在 Web 瀏覽器中顯示該頁面。  
  
 **巡覽列**  
 無法使用此核取方塊。  
  
  
