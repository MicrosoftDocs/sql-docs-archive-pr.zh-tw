---
title: 維護計畫 (報告與記錄頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.reportinglogging.f1
ms.assetid: 3a30b17a-3deb-446f-900a-62f88934a90f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7c7a95a7092ce2cdac4aa0540a5cb57d86b48497
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594529"
---
# <a name="maintenance-plan-reporting-and-logging-page"></a>維護計畫 (報告與記錄頁面)
  使用 **[報表與記錄]** 對話方塊設定執行維護計畫時產生的報表和記錄。  
  
## <a name="options"></a>選項。  
 **產生文字檔報表**  
 指定是否要 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 撰寫文字檔報表。  
  
 **建立新檔案**  
 每次執行維護計畫都建立新的報表檔案。 依預設，寫入報表檔案的電腦，是主控包含此維護計畫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的電腦，而寫入位置是安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，所建立的預設記錄檔資料夾。 若要指定其他資料夾，請在 [資料夾]  文字方塊中輸入資料夾的完整路徑，或者按一下瀏覽按鈕 ( **...** ) 並瀏覽至您要的資料夾。  
  
 **附加至檔案**  
 將來自每個計畫執行的報表附加至 [檔案名稱]  文字方塊中所指定的檔案。 您也可以按一下瀏覽按鈕並從對話方塊中選取檔案，以指定檔案。  
  
 **傳送報表至電子郵件收件者**  
 透過電子郵件傳送維護計畫執行的結果。 此選項只有在已啟用 Database Mail 並已正確設定之後才能使用。  
  
 **代理程式操作員**  
 從清單中選取代理程式操作員，以作為電子郵件的收件者。 此選項只有在郵件已啟用並已正確設定之後才能使用。  
  
 **記錄擴充資訊**  
 在記錄檔中包含更多資訊。 包含此選項會增加預存維護計畫記錄的大小。  
  
 **記錄到遠端伺服器**  
 將維護計畫記錄記錄到遠端伺服器。  
  
 **[連接]**  
 指定記錄到遠端伺服器使用的連接資訊。  
  
 **新增**  
 顯示 [連接屬性]  對話方塊。 用來設定記錄到遠端伺服器的新連接資訊。  
  
## <a name="see-also"></a>另請參閱  
 [維護計畫](maintenance-plans.md)   
 [Database Mail](../database-mail/database-mail.md)  
  
  
