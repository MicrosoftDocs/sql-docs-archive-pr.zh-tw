---
title: RS.exe 公用程式 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- automatic report server tasks
- rs utility
- command prompt utilities [Reporting Services]
- report servers [Reporting Services], automating tasks
- command prompt utilities [SQL Server], rs
- scripts [Reporting Services], command prompt
- deploying reports [Reporting Services]
ms.assetid: bd6f958f-cce6-4e79-8a0f-9475da2919ce
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bcf21a1bf2453d2bd1f0644e31ca46f3f94e6884
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704825"
---
# <a name="rsexe-utility-ssrs"></a>RS.exe Utility (SSRS)
  rs.exe 公用程式會處理您在輸入檔中所提供的指令碼。 使用此公用程式可自動化報表伺服器部署和管理工作。  
  
> [!NOTE]  
>  從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]開始，可支援 **rs** 公用程式，運作於設定 SharePoint 整合模式的報表伺服器以及以原生模式設定的伺服器中。 之前舊版只支援原生模式設定。  
  
 **本主題內容：**  
  
-   [檔案位置](#bkmk_filelocation)  
  
-   [引數](#bkmk_arguments)  
  
-   [權限](#bkmk_permissions)  
  
-   [範例](#bkmk_examples)  
  
## <a name="syntax"></a>語法  
  
```  
  
      rs {-?}  
{-i input_file=}  
{-s serverURL}  
{-u username}  
{-p password}  
{-e endpoint}  
{-l time_out}  
{-b batchmode}  
{-v globalvars=}  
{-t trace}  
```  
  
##  <a name="file-location"></a><a name="bkmk_filelocation"></a> 檔案位置  
 **RS.exe** 位在 **\Program Files\Microsoft SQL Server\110\Tools\Binn**。 您可以從檔案系統上的任何資料夾執行此公用程式。  
  
##  <a name="arguments"></a><a name="bkmk_arguments"></a> 引數  
 **-?**  
 (選擇性) 顯示 **rs** 引數的語法。  
  
 `-i`*input_file*  
 (必要) 指定要執行的 .rss 檔案。 這個值可以是 .rss 檔案的相對路徑或完整路徑。  
  
 `-s`*serverURL*  
 (必要) 指定要對其執行檔案的 Web 伺服器名稱和報表伺服器虛擬目錄名稱。 報表伺服器 URL 的範例為 `http://examplewebserver/reportserver`。 伺服器名稱開頭的前置詞 http:// 或 https:// 是選擇性的。 如果您省略前置詞，報表伺服器 Script Host 會先嘗試使用 https，而且如果 https 無法運作，則會使用 http。  
  
 `-u`[*網域* \\ ]使用者*名稱*  
 (選擇性) 指定用來連接到報表伺服器的使用者帳戶。 如果省略 `-u` 和 `-p`，則會使用目前的 Windows 使用者帳戶。  
  
 `-p`*密碼*  
 (如果已指定 `-u` 則是必要的) 指定要與 `-u` 引數一起使用的密碼。 此值區分大小寫。  
  
 `-e`  
 (選擇性) 指定要在其上執行指令碼的 SOAP 結束點。 有效的值如下：  
  
-   Mgmt2010  
  
-   Mgmt2006  
  
-   Mgmt2005  
  
-   Exec2005  
  
 如果未指定值，則會使用 Mgmt2005 端點。 如需有關 SOAP 端點的詳細資訊，請參閱＜ [Report Server Web Service Endpoints](../report-server-web-service/methods/report-server-web-service-endpoints.md)＞。  
  
 `-l`*time_out*  
  (選擇性) 指定連接到伺服器超時之前經過的秒數。預設值為60秒。 若未指定逾時值，則使用預設值。 `0` 的值指定連接永不逾時。  
  
 **-b**  
 (選擇性) 指定以批次方式執行指令碼檔案中的命令。 若有任何命令失敗，便會回復此批次。 有些命令無法批次處理，而會依平常方式執行。 只有在指令碼中發生未處理的例外狀況會導致批次復原。 如果指令碼處理例外狀況並從 `Main` 正常地傳回，則會認可該批次。 如果忽略此參數，則會執行此命令而不會建立批次。 如需詳細資訊，請參閱 [Batching Methods](../report-server-web-service-net-framework-soap-headers/batching-methods.md)。  
  
 `-v`*expr.globalvar*  
 (選擇性) 指定在指令碼中使用的全域變數。 如果指令碼使用全域變數，則必須指定此引數。 指定的值必須是 .rss 檔案中所定義的全域變數之有效值。 您必須為每個 **-v**引數指定一個全域變數。  
  
 會在命令列上指定 `-v` 引數，以及用於設定在執行階段定義於指令碼中的全域變數值。 例如，如果您的指令碼包含名為 *parentFolder*的變數，您就可以在命令列上指定該資料夾的名稱：  
  
 `rs.exe -i myScriptFile.rss -s http://myServer/reportserver -v parentFolder="Financial Reports"`  
  
 全域變數會使用給定的名稱來建立並設定為所提供的值。 例如， **-v a =**" `1` " **-v b =**"" 會 `2` 產生名為的變數，其值為 `a` " `1` "，而變數**b**的值為 " `2` "。  
  
 指令碼中的任何函數均可使用全域變數。 反斜線和引號 (「 ** \\ **) 會被視為雙引號。 只有當字串含有空格時才需要引號。 變數名稱必須是有效的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] ; 它們必須以字母字元或底線開頭，而且包含字母字元、數位或底線。 保留字不可以當做變數名稱使用。 如需使用全域變數的詳細資訊，請參閱[運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md)。  
  
 **-t**  
 (選擇性) 追蹤記錄的輸出錯誤訊息。 此引數沒有取得值。 如需詳細資訊，請參閱 [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md)。  
  
##  <a name="permissions"></a><a name="bkmk_permissions"></a> 權限  
 若要執行工具，您必須有足夠的權限，可以連接到要對其執行指令碼的報表伺服器執行個體。 您可以執行指令碼在本機電腦或遠端電腦執行變更。 若要對安裝在遠端電腦上的報表伺服器執行變更，請在 `-s` 引數中指定遠端電腦。  
  
##  <a name="examples"></a><a name="bkmk_examples"></a> 範例  
 下列範例說明如何指定指令碼檔案，其中包含您要執行的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET 指令碼和 Web 服務方法。  
  
```  
rs -i c:\scriptfiles\script_copycontent.rss -s http://localhost/reportserver  
```  
  
  如需詳細的範例，請參閱＜ [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)＞。  
  
 如需其他範例，請參閱 [執行 Reporting Services 指令碼檔案](run-a-reporting-services-script-file.md)  
  
## <a name="remarks"></a>備註  
 您可以定義指令碼來設定系統屬性、發行報表等等。 您可以建立的指令碼包括 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] API 的任何方法。 如需有關可供您使用的方法和屬性之詳細資訊，請參閱＜ [Report Server Web Service](../report-server-web-service/report-server-web-service.md)＞。  
  
 指令碼必須以 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET 程式碼撰寫，然後使用 .rss 副檔名將指令碼儲存在 Unicode 或 UTF-8 文字檔中。 您不可以使用 **rs** 公用程式來偵錯指令碼。 若要對腳本進行偵錯工具，請在中執行程式碼 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
> [!TIP]  
>   如需詳細的範例，請參閱＜ [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [執行 Reporting Services 指令檔](run-a-reporting-services-script-file.md)   
 [編寫部署和管理工作的腳本](script-deployment-and-administrative-tasks.md)   
 [使用 rs.exe 公用程式與 Web 服務編寫腳本](script-with-the-rs-exe-utility-and-the-web-service.md)   
 [報表伺服器命令提示字元公用程式 &#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)  
  
  
