---
title: 記錄讀取器代理程式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.logreaderagent.f1
helpviewer_keywords:
- Log Reader Agent dialog box
ms.assetid: 300a3c46-0e48-4334-99c0-9ee690d2ef4f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2b908e43cf97350fee2913e8cc6bab30a1bcd0dd
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707365"
---
# <a name="log-reader-agent"></a>記錄讀取器代理程式
  **[記錄讀取器代理程式]** 對話方塊會顯示記錄讀取器代理程式的詳細資訊，包括狀態、記錄、參考訊息，以及任何錯誤訊息。  
  
## <a name="options"></a>選項。  
 從 **[檢視]** 功能表選取要檢視的記錄讀取器代理程式工作階段，然後在標示為 **[記錄讀取器代理程式的工作階段]** 的方格中，選取一個特定的工作階段。 有關這個工作階段的詳細資訊，會顯示在標示為 **[所選取工作階段中的動作]** 之方格中。 如果選取的工作階段結束時發生錯誤， **[所選取之工作階段的錯誤詳細資料或訊息]** 的文字區域也會顯示。  
  
 **檢視**  
 選取要檢視的記錄讀取器代理程式工作階段。 記錄讀取器代理程式通常會連續執行，因此可能只會有一個工作階段可供檢視。  
  
 **狀態**  
 記錄讀取器代理程式的狀態。 下列清單顯示可能的狀態值：  
  
-   錯誤  
  
-   正在重試失敗的命令  
  
-   未執行  
  
-   執行中  
  
 **Start Time**  
 工作階段的開始時間。  
  
 **結束時間**  
 工作階段的結束時間。 如果代理程式未停止，則這個欄位是空的。  
  
 **有效期間**  
 記錄讀取器代理程式已在這個工作階段執行的時間量。 如果代理程式目前正在執行，則時間代表經過時間，如果代理程式工作階段已結束，則時間代表工作階段總共花費的時間。  
  
 **錯誤訊息**  
 如果工作階段因發生錯誤而結束，這個欄位會顯示記錄讀取器代理程式所記錄的最後錯誤訊息。 如果工作階段結束時沒有錯誤，這個欄位會是空白。  
  
 **動作訊息**  
 記錄讀取器代理程式在所選取工作階段過程中已記錄的所有參考訊息與錯誤訊息。  
  
 **動作時間**  
 執行 **[動作訊息]** 資料行所描述之動作的時間。  
  
 **[所選取之工作階段的錯誤詳細資料或訊息]**  
 唯有所選取工作階段在 **[狀態]** 資料行中顯示的值為 **[錯誤]** 時，才會顯示。 此文字區域會顯示詳細錯誤資訊和發生錯誤時所嘗試的命令。 它也會包括與錯誤相關之其他內容的連結。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](monitor/start-the-replication-monitor.md)   
 [使用複寫監視器來檢視資訊及執行工作](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [監視複寫](monitoring-replication.md)   
 [複寫代理程式概觀](agents/replication-agents-overview.md)  
  
  
