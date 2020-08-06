---
title: 內建的全域和使用者參考 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5f5e1149-c967-454d-9a63-18ec4a33d985
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8ada59244c2b1c49bc0be6f679b8eb4affc487ab
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599381"
---
# <a name="built-in-globals-and-users-references-report-builder-and-ssrs"></a>內建的全域和使用者參考 (報表產生器及 SSRS)
  內建欄位集合包含 `Globals` 和 `User` 集合，代表在處理報表時 Reporting Services 所提供的全域值。 `Globals` 集合提供的值包括報表名稱、開始處理報表的時間，以及報表頁首及頁尾的目前頁碼。 `User` 集合則提供使用者識別碼和語言設定。 您可以在運算式中使用這些值以在報表中篩選結果。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-globals-collection"></a>使用 Globals 集合  
 `Globals` 集合包含報表的全域變數。 這些變數在設計介面上會顯示為具有前置的 & (連字號)，例如 `[&ReportName]`。 下表描述 `Globals` 集合的成員。  
  
|**成員**|**型別**|**說明**|  
|----------------|--------------|---------------------|  
|ExecutionTime|`DateTime`|報表開始執行的日期和時間。|  
|PageNumber|`Integer`|相對於重設頁碼之分頁線的目前頁碼。 在開始處理報表時，初始值設為 1。 每個呈現之頁面的頁碼會遞增。<br /><br /> 若要針對矩形、資料區、資料區群組或地圖在分頁符號內的頁碼分頁，請在 PageBreak 屬性上將 ResetPageNumber 屬性設定為 `True` 。 在 Tablix 資料行階層群組上不支援。<br /><br /> PageNumber 只能用於頁首或頁尾中的運算式。|  
|ReportFolder|`String`|報表所在之資料夾的完整路徑。 這不包括報表伺服器 URL。|  
|ReportName|`String`|報表存放在報表伺服器資料庫的名稱。|  
|ReportServerUrl|`String`|執行報表之報表伺服器的 URL。|  
|TotalPages|`Integer`|相對於重設 PageNumber 之分頁線的總頁碼。 如果未設定任何分頁線，此值與 OverallTotalPages 相同。<br /><br /> TotalPages 只能用於頁首或頁尾中的運算式。|  
|PageName|`String`|頁面名稱。 在開始處理報表時，會從 InitialPageName 報表屬性設定初始值。 當每個報表項目都經過處理之後，此值會從矩形、資料區、資料區群組或地圖取代為 PageName 的對應值。 在 Tablix 資料行階層群組上不支援。<br /><br /> PageName 只能用於頁首或頁尾中的運算式。|  
|OverallPageNumber|`Integer`|整個報表之目前頁面的頁碼。 這個值不會受到 ResetPageNumber 的影響。<br /><br /> OverallPageNumber 只能用於頁首或頁尾中的運算式。|  
|OverallTotalPages|`Integer`|整個報表的總頁數。 這個值不會受到 ResetPageNumber 的影響。<br /><br /> OverallTotalPages 只能用於頁首或頁尾中的運算式。|  
|RenderFormat|`RenderFormat`|目前轉譯要求的相關資訊。<br /><br /> 如需詳細資訊，請參閱下一節中的＜RenderFormat＞。|  
  
 `Globals` 集合的成員會傳回變數。 如果要在需要特定資料類型的運算式中使用這個集合的成員，必須先轉換變數。 例如，若要將執行時間變數轉換成日期格式，請使用 `=CDate(Globals!ExecutionTime)`。 如需詳細資訊，請參閱 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)。  
  
### <a name="renderformat"></a>RenderFormat  
 下表描述 `RenderFormat` 的成員。  
  
|成員|類型|描述|  
|------------|----------|-----------------|  
|名稱|`String`|在 RSReportServer 組態檔中註冊之轉譯器的名稱。<br /><br /> 可在報表處理/呈現週期的特定部分使用。|  
|IsInteractive|`Boolean`|目前的轉譯要求是否使用互動式轉譯格式。|  
|DeviceInfo|唯讀名稱/值集合|目前轉譯要求之 deviceinfo 參數的索引鍵/值配對。<br /><br /> 您可以使用索引鍵或索引指定集合中的字串值。|  
  
### <a name="examples"></a>範例  
 下列範例說明如何在運算式中使用 `Globals` 集合的參考。  
  
-   這個放在報表頁尾之文字方塊中的運算式，會提供報表的頁碼與總頁數：  
  
     `=Globals.PageNumber & " of " & Globals.TotalPages`  
  
-   這個運算式提供報表的名稱及其執行時間。 時間的格式為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 簡短日期的格式字串：  
  
     `=Globals.ReportName & ", dated " & Format(Globals.ExecutionTime, "d")`  
  
-   這個放在所選資料行之 **[資料行可見性]** 對話方塊中的運算式，只會在報表匯出至 Excel 之後顯示資料行； 其他時候則會隱藏資料行。  
  
     `EXCELOPENXML` 是指 Office 2007 隨附的 Excel 格式。 `EXCEL` 是指 Office 2003 隨附的 Excel 格式。  
  
     `=IIF(Globals!RenderFormat.Name = "EXCELOPENXML" OR Globals!RenderFormat.Name = "EXCEL", false, true)`  
  
## <a name="using-the-user-collection"></a>使用 User 集合  
 `User` 集合包含正在執行報表之使用者的相關資料。 您可以利用此集合來篩選出現在報表中的資料 (例如，只顯示目前使用者的資料)，或是在報表標題中顯示 UserID 或其他項目。 這些變數在設計介面上會顯示為具有前置的 & (連字號)，例如 `[&UserID]`。  
  
 下表描述 `User` 集合的成員。  
  
|**成員**|**型別**|**說明**|  
|----------------|--------------|---------------------|  
|`Language`|`String`|執行報表之使用者的語言。 例如： `en-US` 。|  
|`UserID`|`String`|執行報表之使用者的識別碼。 如果您是使用 Windows 驗證，此值為目前使用者的網域帳戶。 這個值是由 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安全性延伸模組所決定，此延伸模組可使用 Windows 驗證或自訂驗證。|  
  
 如需在報表中支援多國語言的詳細資訊，請參閱《 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SQL Server 線上叢書 [》中](https://go.microsoft.com/fwlink/?LinkId=120955)文件集的＜適用於多語言或全域部署的解決方案設計考量＞。  
  
### <a name="using-locale-settings"></a>使用地區設定  
 若要決定對使用者顯示報表的方式，您可以利用運算式，透過 `User.Language` 值來參考用戶端電腦上的本機設定。 例如，您可以建立報表來使用以本機值為基礎的不同查詢運算式。 查詢可能會根據傳回的語言，從不同的資料行擷取當地語系化的資訊。 您也可以在報表的語言設定或根據此變數的報表項目中使用運算式。  
  
> [!NOTE]  
>  變更報表的語言設定時，您必須注意可能會造成的顯示問題。 例如，變更報表的地區設定可能會變更報表中的日期格式，也可能會變更貨幣格式。 除非有貨幣轉換程序，否則這可能會造成不正確的貨幣符號在報表中顯示。 若要避免這種狀況，請您為每個要變更的項目個別設定其語言資訊，或將項目的貨幣資料設定為特定的語言。  
  
### <a name="identifying-userid-for-snapshot-or-history-reports"></a>識別快照集或歷程記錄報表的 UserID  
 在某些情況下，包含 *User!UserID* 變數的報表將無法顯示正在檢視報表之目前使用者特定的報表資料。  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [運算式對話方塊 &#40;報表產生器&#41;](../expression-dialog-box-report-builder.md)   
 [運算式中的資料類型 &#40;報表產生器和 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [將數位和日期格式化 &#40;報表產生器和 SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  
