---
title: 使用檢查點來重新啟動套件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- checkpoints [Integration Services]
- restarting packages
- starting packages
ms.assetid: 48f2fbb7-8964-484a-8311-5126cf594bfb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa0e0e9ad1da67bfc70dec61396ab026df62d3ee
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597192"
---
# <a name="restart-packages-by-using-checkpoints"></a>使用檢查點來重新啟動封裝
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可以從失敗點重新啟動失敗的封裝，而無需重新執行整個封裝。 如果封裝設定為使用檢查點，則封裝執行的相關資訊會寫入檢查點檔案。 當失敗的封裝重新執行時，檢查點檔案會用於從失敗點重新啟動封裝。 如果封裝順利執行，則會刪除檢查點檔案，然後在下次封裝執行時重新建立檢查點檔案。  
  
 在封裝中使用檢查點有下列優點。  
  
-   避免重複下載和上傳大型檔案。 例如，對每個下載使用 FTP 工作來下載多個大型檔案的封裝，在下載單一檔案失敗後可以重新啟動，然後只下載該單一檔案。  
  
-   避免重複載入大量資料。 例如，如果封裝針對每個維度使用不同「大量插入」工作向資料倉儲中的維度資料表執行大量插入，則當一個維度資料表的插入失敗時，該封裝會重新啟動，且只重新載入該維度。  
  
-   避免重複彙總值。 例如，使用資料流程工作執行每個彙總以計算許多彙總 (例如，平均和總和) 的封裝，可以在計算一個彙總失敗之後重新啟動，且只重新計算該彙總。  
  
 如果封裝設定為使用檢查點，則 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會擷取檢查點檔案中的重新啟動點。 失敗的容器類型和功能的實作 (例如，交易) 會影響檢查點檔案中記錄的重新啟動點。 檢查點檔案中也會擷取變數目前的值。 然而，具有 `Object` 資料類型之變數的值不會儲存於檢查點檔案中。  
  
## <a name="defining-restart-points"></a>定義重新啟動點  
 封裝單一工作的工作主機容器是可以重新啟動的最小基本單位工作。 「Foreach 迴圈」容器和交易容器也會視為最小基本單位工作。  
  
 如果封裝在交易容器執行時停止，則交易會結束，且該容器執行的任何工作都會回復。 當封裝重新啟動時，會重新執行失敗的容器。 如果交易容器的任何子容器完成，則不會在檢查點檔案中記錄。 因此，當封裝重新啟動時，交易容器及其子容器都會重新執行。  
  
> [!NOTE]  
>  在相同的封裝中使用檢查點與交易可能會造成非預期的結果。 例如，當封裝失敗並從檢查點重新啟動時，封裝可能會重複已經過成功認可的交易。  
  
 不會儲存 For 迴圈和 Foreach 迴圈容器的檢查點資料。 當封裝重新啟動時，For 迴圈和 Foreach 迴圈容器及其子容器會再次執行。 如果迴圈中的子容器順利執行，則不會在檢查點檔案中記錄它，而是重新執行。 如需詳細資訊和因應措施，請參閱 [For 迴圈或 Foreach 迴圈容器項目都不接受 SSIS 檢查點](https://go.microsoft.com/fwlink/?LinkId=241633)。  
  
 如果封裝重新啟動，則不會重新載入封裝組態，該封裝會使用寫入檢查點檔案的組態資訊。 這會確保封裝在重新執行時使用與其失敗時相同的組態。  
  
 封裝只可以在控制流程層級重新啟動。 您無法在資料流程中間重新啟動封裝。 為避免重新執行整個資料流程，封裝可能會設計成包含多個資料流程，每個都使用不同的資料流程工作。 如此一來，重新啟動封裝時就只需重新執行一個資料流程工作。  
  
## <a name="configuring-a-package-to-restart"></a>設定重新啟動的封裝  
 檢查點檔案包含所有完成之容器的執行結果、系統和使用者自訂之變數的目前值，以及封裝組態資訊。 該檔案還包含封裝的唯一識別碼。 若要順利重新啟動封裝，檢查點檔案中的封裝識別碼必須與封裝中的識別碼相符，否則重新啟動會失敗。 這會防止封裝使用不同封裝版本寫入的檢查點檔案。 如果封裝順利執行，則在其重新啟動後，會刪除檢查點檔案。  
  
 下表列出設定用以實作檢查點的封裝屬性。  
  
|屬性|描述|  
|--------------|-----------------|  
|CheckpointFileName|指定檢查點檔案的名稱。|  
|CheckpointUsage|指定是否使用檢查點。|  
|SaveCheckpoints|指出封裝是否儲存檢查點。 必須將此屬性設為 True，才能從失敗點重新啟動封裝。|  
  
 此外，您必須 `true` 針對封裝中要識別為重新啟動點的所有容器，將 FailPackageOnFailure 屬性設定為。  
  
 可以使用 ForceExecutionResult 屬性來測試封裝中檢查點的使用。 將工作或容器的 ForceExecutionResult 設為 [Failure]，可以模擬即時失敗。 當重新執行封裝時，會重新執行失敗的工作和容器。  
  
### <a name="checkpoint-usage"></a>檢查點使用方式  
 CheckpointUsage 屬性可以設為下列值：  
  
|值|描述|  
|-----------|-----------------|  
|`Never`|指定不使用檢查點檔案，且封裝從封裝工作流程的開始點執行。|  
|`Always`|指定總是使用檢查點檔案，且封裝從上一個執行失敗點重新啟動。 如果找不到檢查點檔案，則封裝會失敗。|  
|`IfExists`|指定如果存在檢查點檔案，就使用該檔案。 如果存在檢查點檔案，則封裝會從上一個執行失敗點重新啟動，否則，封裝會從封裝工作流程的開始點執行。|  
  
> [!NOTE]  
>  Dtexec 的 **/checkpointing on**選項相當於將封裝的屬性設定 `SaveCheckpoints` 為 `True` ，並將屬性設 `CheckpointUsage` 為 Always。 如需詳細資訊，請參閱 [dtexec Utility](dtexec-utility.md)。  
  
## <a name="securing-checkpoint-files"></a>保護檢查點檔案  
 封裝等級保護並不包括檢查點檔案的保護，因此您必須個別保護這些檔案。 檢查點資料只能儲存在檔案系統中，而且您應該使用作業系統存取控制清單 (ACL) 來保護儲存檔案之位置或資料夾的安全。 請務必保護檢查點檔案的安全，因為它們包含有關封裝狀態的資訊，包括變數目前的值。 例如，變數包含的資料錄集可能具有許多私密資料 (例如電話號碼) 的資料列。 如需詳細資訊，請參閱 [對封裝使用之檔案的存取權](../access-to-files-used-by-packages.md)。  
  
### <a name="to-configure-the-checkpoint-properties"></a>設定檢查點屬性  
  
-   [設定檢查點以重新啟動失敗的封裝](../configure-checkpoints-for-restarting-a-failed-package.md)  
  
## <a name="external-resources"></a>外部資源  
  
-   位於 social.technet.microsoft.com 的技術文件： [發生容錯移轉或失敗之後 SSIS 封裝自動重新啟動](https://go.microsoft.com/fwlink/?LinkId=200407)。  
  
-   support.microsoft.com 上的技術支援文件： [For 迴圈或 Foreach 迴圈容器項目都不接受 SSIS 檢查點](https://go.microsoft.com/fwlink/?LinkId=241633)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
