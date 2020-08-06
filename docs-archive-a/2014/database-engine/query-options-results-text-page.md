---
title: 查詢選項結果 (Text 頁面) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.text.f1
ms.assetid: fd2fb409-58f9-4ede-8349-ce007126b68d
author: rothja
ms.author: jroth
ms.openlocfilehash: 45019450c8fc959b440aac5bf1e9098e59cecefc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599164"
---
# <a name="query-options-results-text-page"></a>查詢選項結果 (文字頁面)
  使用此頁面，即可指定以文字格式顯示查詢結果集的選項。 選取 **[將結果存檔]** 時，此頁面上的設定也適用。  
  
 **輸出格式**  
 根據預設，輸出會顯示在以空格填補結果所建立的資料行中。 其他選項包括使用逗號、索引標籤，或空格來分隔資料行。 選取 **[自訂分隔符號]** 核取方塊，即可在 **[自訂分隔符號]** 方塊中指定不同的分隔字元。  
  
 **[自訂分隔符號]**  
 指定您要用來分隔資料行的字元。 唯有在 **[輸出格式]** 方塊中選取了 **[自訂分隔符號]** 核取方塊之後，此選項才可以使用。  
  
 **在結果集內包含資料行標頭**  
 如果您不要每個資料行均標示有資料行標題，請清除此核取方塊。  
  
 **收到結果時捲動**  
 選取此核取方塊，即可將顯示焦點保持在最近傳回的底部記錄上。 清除此核取方塊，即可將作用中的顯示保持為接收到的第一組資料列。  
  
 **數值靠右對齊**  
 選取此核取方塊，即可將數值靠資料行的右邊對齊。 如此可便於檢閱有固定小數位數的數字。  
  
 **執行查詢之後捨棄結果**  
 在螢幕上顯示查詢結果之後即將其捨棄，以釋放記憶體。  
  
 **在其他索引標籤中顯示結果**  
 選取此核取方塊，即可在新的文件視窗中顯示結果集，而非在查詢文件視窗的下方顯示。  
  
 **執行查詢後，切換至結果索引標籤**  
 按一下以自動將螢幕焦點設定為結果集。  
  
 **每個資料行中顯示的最大字元數**  
 這個值預設為 256。 增加這個值即可顯示較大的結果集而不會截斷。  
  
 **重設為預設值**  
 將此頁面上的所有值重設為原始預設值。  
  
## <a name="saving-a-text-result-set-with-headers"></a>儲存具標頭的文字結果集  
 若要將查詢結果儲存為具標頭的文字檔案，請選取 **[在結果集內包含資料行標頭]** 核取方塊，以及輸出的分隔格式。 當您按一下工具列上的 [將結果存檔]**** 時；或以滑鼠右鍵按一下任何查詢結果，按一下 [儲存結果]****，輸入檔案名稱，然後按一下 [儲存]**** 時；此報表檔就會包含標頭。  
  
  