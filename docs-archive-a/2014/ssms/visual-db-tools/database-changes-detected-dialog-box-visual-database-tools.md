---
title: 偵測到資料庫變更對話方塊 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.schema.databasechangesdetected
- vdtsql.chm:65543
- vdtsql.chm:65554
ms.assetid: 91f13086-371f-46a2-9f46-804c1415f3ed
author: stevestein
ms.author: sstein
ms.openlocfilehash: 91d58e812b93f207d592d245d094b0fbeddcce72
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699067"
---
# <a name="database-changes-detected-dialog-box-visual-database-tools"></a>偵測到資料庫變更對話方塊 (Visual Database Tools)
  如果您嘗試儲存資料庫圖表或選取的資料表，但是儲存動作將影響的某些資料庫物件對於資料庫而言已經過期，這個對話方塊便會出現。 接受此對話方塊中顯示的變更，會更新資料庫，以符合您的圖表，並覆寫其他使用者的變更。  
  
> [!NOTE]  
>  雖然您無法復原對於資料表或資料庫圖表所做的變更，但是，在您儲存資料表或圖表之前，這些變更都不會儲存至資料庫中。 您可以選擇 [否]  以捨棄任何未儲存的變更，並關閉所有開啟的圖表，不予以儲存。  
  
## <a name="options"></a>選項。  
 **警告差異偵測**  
 指定下次您嘗試儲存資料庫圖表或選取的資料表時，此對話方塊是否出現。 核取表示每次您儲存對於資料庫而言已過期的圖表或資料表時，此對話方塊都會出現。 未核取表示對話方塊不會出現。 依照預設，此方塊為核取。 如果您取消核取此選項，可以在 [選項]  對話方塊中重新核取。  
  
 **是**  
 以清單中顯示的所有變更更新資料庫。  
  
 **否**  
 取消儲存動作。  
  
> [!NOTE]  
>  若要重新整理圖表以符合資料庫，可關閉圖表而不予以儲存，在 [伺服器總管] 的圖表上按一下滑鼠右鍵，並且按一下 [重新整理]，然後重新開啟圖表。  
  
 **儲存為文字檔**  
 顯示 [另存新檔]  對話方塊，讓您指定包含資料庫變更清單的文字檔位置。  
  
## <a name="see-also"></a>另請參閱  
 [使用修改過的資料庫協調資料庫關係圖 &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [多使用者環境 &#40;Visual Database Tools&#41;](multiuser-environments-visual-database-tools.md)  
  
  
