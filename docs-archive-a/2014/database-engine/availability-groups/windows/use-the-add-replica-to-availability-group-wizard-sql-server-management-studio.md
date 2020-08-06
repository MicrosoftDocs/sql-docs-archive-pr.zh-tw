---
title: 使用將複本新增至可用性群組精靈 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.addreplicawizard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], wizards
ms.assetid: 60d962b6-2af4-4394-9190-61939a102bc0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e4d75372cd2388e88fcb3d3ce95975bdefa54c5c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593597"
---
# <a name="use-the-add-replica-to-availability-group-wizard-sql-server-management-studio"></a>使用 [將複本加入至可用性群組] 精靈 (SQL Server Management Studio)
  使用 [將複本加入至可用性群組精靈]，可協助您將新次要複本加入至現有的 AlwaysOn 可用性群組。  
  
> [!NOTE]  
>  如需使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 PowerShell 將次要複本加入可用性群組的資訊，請參閱 [將次要複本加入至可用性群組 &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)。  
  

  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
 如果您從未將任何可用性複本新增至可用性群組，請參閱[AlwaysOn 可用性群組 &#40;SQL Server&#41;的必要條件、限制和建議](prereqs-restrictions-recommendations-always-on-availability.md)中的「伺服器實例」和「可用性群組和複本」小節。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
  
-   您必須連接到裝載目前主要複本的伺服器執行個體。  
  
-   加入次要複本之前，請確認 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主機執行個體與現有複本位於相同 Windows Server 容錯移轉叢集 (WSFC) 叢集中，但位於不同的叢集節點上。 也請確認這個伺服器執行個體符合所有其他 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 必要條件。 如需詳細資訊，請參閱 [AlwaysOn 可用性群組的必要條件、限制和建議 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)。  
  
-   如果您選取來裝載可用性複本的伺服器執行個體是以網域使用者帳戶執行，且還沒有資料庫鏡像端點，則此精靈可以建立端點，並授與伺服器執行個體服務帳戶的 CONNECT 權限。 但是，如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務是以內建帳戶 (例如本機系統、本機服務或網路服務) 或非網域帳戶的身分執行，您就必須將憑證用於端點驗證，而且精靈無法在此伺服器執行個體上建立資料庫鏡像端點。 在此情況下，我們建議您先手動建立資料庫鏡像端點，然後再啟動 [將複本加入至可用性群組] 精靈。  
  
     `To use certificates for a database mirroring endpoint:`  
  
     [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)  
  
     [使用資料庫鏡像端點憑證 &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   **使用完整初始資料同步處理的必要條件**  
  
    -   每個裝載可用性群組複本之伺服器執行個體上的所有資料庫檔案路徑均須相同。  
  
    -   任何裝載次要複本的伺服器執行個體上皆不應存在主要資料庫名稱。 這表示目前還不可有任何新次要資料庫。  
  
    -   您必須指定網路共用，精靈才能建立及存取備份。 對於主要複本，用於啟動 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 的帳戶必須具有網路共用的讀取與寫入檔案系統權限。 如果是次要複本，此帳戶必須有網路共用的讀取權限。  
  
     如果您無法使用精靈執行完整初始資料同步處理，則必須手動準備次要資料庫。 您可以在執行精靈前後進行這項作業。 如需詳細資訊，請參閱 [針對可用性群組手動準備次要資料庫 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)中的 PowerShell，將次要資料庫聯結至 AlwaysOn 可用性群組。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
 如果您想要允許 [將複本加入至可用性群組精靈] 管理資料庫鏡像端點，也需要 CONTROL ON ENDPOINT 權限。  
  

  
##  <a name="using-the-add-replica-to-availability-group-wizard-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用將複本加入至可用性群組精靈 (SQL Server Management Studio)  
 **使用將複本加入至可用性群組精靈**  
  
1.  在 [物件總管] 中，連接到裝載可用性群組之主要複本的伺服器執行個體，然後展開伺服器樹狀目錄。  
  
2.  依序展開 **[AlwaysOn 高可用性]** 節點和 **[可用性群組]** 節點。  
  
3.  以滑鼠右鍵按一下您要加入次要複本的可用性群組，並選取 [加入複本] 命令。 這會啟動 [將複本加入至可用性群組] 精靈。  
  
4.  在 **[連接到現有次要複本]** 頁面上，連接到可用性群組中的每一個次要複本。 如需詳細資訊，請參閱[連接到現有的次要複本頁面 &#40;新增複本嚮導和加入資料庫 wizard&#41;](connect-to-existing-secondary-replicas-page.md)。  
  
5.  在 **[指定複本]** 頁面上，針對可用性群組指定並設定一個或多個新次要複本。 此頁面包含三個索引標籤。 下表將介紹這些索引標籤。 如需詳細資訊，請參閱[指定複本頁面 &#40;新增可用性群組精靈：新增複本精靈 &#41;](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md)。  
  
    |索引標籤|簡短描述|  
    |---------|-----------------------|  
    |**複本**|使用此索引標籤可指定將裝載新次要複本的每個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。|  
    |**端點**|使用此索引標籤來驗證每個新次要複本的現有資料庫鏡像端點 (如果有的話)。 如果在其服務帳戶使用 Windows 驗證的伺服器執行個體上缺少此端點，精靈會嘗試自動建立該端點。 **注意：** 如果有任何伺服器實例是在非網域使用者帳戶下執行，您必須先對伺服器實例進行手動變更，然後才能在嚮導中繼續進行。 如需詳細資訊，請參閱本主題前面的＜ [必要條件](#Prerequisites)＞。|  
    |**備份喜好設定**|使用此索引標籤可指定整個可用性群組的備份喜好設定，如果您希望修改目前設定，可指定個別可用性複本的備份優先權。|  
  
6.  在 **[選取初始資料同步處理]** 頁面上，選擇您要如何建立新的次要資料庫並將它聯結至可用性群組。 選擇下列其中一個選項：  
  
    -   **完整**  
  
         只有在您的環境符合自動啟動初始資料同步處理的需求時，才選取此選項 (如需詳細資訊，請參閱本主題稍早的 [必要條件、限制和建議](#Prerequisites))。  
  
         如果您選取 **[完整]** ，在建立可用性群組之後，精靈會將每個主要資料庫及其交易記錄備份至網路共用，並在裝載新次要複本的每個伺服器執行個體上還原這些備份。 然後精靈會將每個新次要資料庫聯結至可用性群組。  
  
         在 **[指定所有複本可存取的共用網路位置:]** 欄位中，指定裝載複本的所有伺服器執行個體都有讀寫存取的備份共用。 記錄備份將是記錄備份鏈結的一部分。 請適當地儲存記錄備份檔案。  
  
        > [!IMPORTANT]  
        >  如需檔案系統必要權限的資訊，請參閱本主題稍早的 [必要條件](#Prerequisites)。  
  
    -   **僅聯結**  
  
         如果您已經在將裝載新次要複本的伺服器執行個體上手動備妥次要資料庫，就可以選取此選項。 然後精靈會將這些新的次要資料庫聯結至可用性群組。  
  
    -   **略過初始資料同步處理**  
  
         如果要使用您自己的主要資料庫的資料庫和記錄備份，請選取此選項。 如需詳細資訊，請參閱[於 AlwaysOn 次要資料庫啟動資料移動 &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
7.  **[驗證]** 頁面會驗證您在此精靈中指定的值是否符合 [將複本加入至可用性群組] 精靈的需求。 若要進行變更，您可以按 **[上一步]** 返回先前的精靈頁面，以變更一個或多個值。 然後按 **[下一步]** 返回 **[驗證]** 頁面，再按一下 **[重新執行驗證]** 。  
  
8.  在 **[摘要]** 頁面上，檢閱您為新的可用性群組的選擇。 若要進行變更，請按 **[上一步]** 返回相關頁面。 進行變更之後，請按 **[下一步]** 返回 **[摘要]** 頁面。  
  
     如果您對所做的選擇感到滿意時，可以選擇按一下 [指令碼]，建立精靈將執行之步驟的指令碼。 然後，若要建立及設定新的可用性群組，請按一下 **[完成]** 。  
  
9. **[進度]** 頁面會顯示建立可用性群組之步驟的進度 (設定端點、建立可用性群組，並將次要複本加入群組中)。  
  
10. 當這些步驟完成時， **[結果]** 頁面會顯示每個步驟的結果。 如果所有這些步驟都成功，表示新的可用性群組已完成設定。 如果任何步驟導致錯誤，您可能需要手動完成設定。 如需有關給定錯誤原因的詳細資訊，請按一下 **[結果]** 資料行中相關聯的 [錯誤] 連結。  
  
     當精靈完成時，按一下 **[關閉]** 以結束。  
  
> [!IMPORTANT]  
>  新增複本之後，請參閱＜後續操作：新增複本之後＞一節，位於[將次要複本新增至可用性群組 &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)中。  
  

  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [將次要複本加入至可用性群組 &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  

  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server 的必要條件、限制和建議&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [將次要複本加入至可用性群組 &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
