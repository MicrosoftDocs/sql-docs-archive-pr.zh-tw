---
title: 設定 PowerPivot 無人看管的資料重新整理帳戶 (PowerPivot for SharePoint) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 81401eac-c619-4fad-ad3e-599e7a6f8493
author: minewiskan
ms.author: owend
ms.openlocfilehash: d6f53d7272dc48ed55ffb175e0ace3e97263946c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593033"
---
# <a name="configure-the-powerpivot-unattended-data-refresh-account-powerpivot-for-sharepoint"></a>設定 PowerPivot 無人看管的資料重新整理帳戶 (PowerPivot for SharePoint)
  PowerPivot 無人看管的資料重新整理帳戶是一個指定的帳戶，可在 SharePoint 伺服器陣列中執行 PowerPivot 資料重新整理作業。 藉由設定它，您可以在資料重新整理排程頁面中，啟用 [**使用系統管理員所設定的資料**重新整理帳戶] 選項 (如下) 所示。 若排程資料重新整理的活頁簿作者想要使用 PowerPivot 無人看管的資料重新整理帳戶執行資料重新整理作業，可以選擇此選項。 如需有關如何在資料重新整理排程中查看認證選項的詳細資訊，請參閱[排程資料重新整理 &#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)。  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 2010  
  
 根據您在設定伺服器時選取的選項而定，可能已經建立無人看管的資料重新整理帳戶。 在預設組態中，一開始會將無人看管的資料重新整理帳戶識別設定為伺服器陣列帳戶。 您可以將帳戶變更為以不同的使用者執行，藉以提高部署的安全性。 請依照下列指示來變更帳戶：[更新現有 PowerPivot 無人看管的資料重新整理帳戶所使用的認證](#bkmk_editUA)。  
  
 對於所有其他安裝情況，您必須使用下列指示手動設定此帳戶。  
  
 本主題包含下列幾節：  
  
 [先決條件](#bkmk_prereq)  
  
 [步驟 1：建立目標應用程式並設定認證](#bkmk_create)  
  
 [步驟 2：在 PowerPivot 伺服器組態頁面中，指定無人看管的帳戶](#bkmk_specifyUA)  
  
 [步驟3：授與帳戶的「參與」許可權](#bkmk_grant)  
  
 [步驟 4：授與資料重新整理期間存取外部資料來源時所需的讀取權限](#bkmk_dbread)  
  
 [步驟 5：在資料重新整理組態頁面中，確認帳戶可用性](#bkmk_verify)  
  
 [使用 PowerPivot 無人看管的資料重新整理帳戶](#bkmk_use)  
  
 [更新現有 PowerPivot 無人看管的資料重新整理帳戶所使用的認證](#bkmk_editUA)  
  
##  <a name="prerequisites"></a><a name="bkmk_prereq"></a> 必要條件  
 您必須啟用並設定 Secure Store Service，而且必須產生主要金鑰。 如需如何執行這種操作的指示，請參閱[使用 SharePoint 2010 的 PowerPivot 資料](powerpivot-data-refresh-with-sharepoint-2010.md)重新整理  
  
 您必須事先決定要將哪個 Windows 網域使用者帳戶當做 PowerPivot 無人看管的資料重新整理帳戶使用。 這應該是特別針對這個用途所建立的帳戶，讓您可以監視其使用方式。  
  
 您必須知道 PowerPivot 系統服務的應用程式識別。 當您在步驟1中為其建立目標應用程式時，您會將無人看管資料重新整理帳戶的 [**完全控制**] 許可權授與此服務帳戶。 這些權限允許 PowerPivot 系統服務在資料重新整理期間擷取無人看管資料重新整理帳戶的認證。 若要取得所需的服務帳戶資訊，請開啟 [管理中心] 中的 [**設定服務帳戶**] 頁面，然後選取 PowerPivot 服務應用程式所使用的服務應用程式集區。 根據預設，這是**服務應用程式集區-SharePoint Web 服務系統**。  
  
## <a name="configure-the-unattended-powerpivot-data-refresh-account"></a>設定無人看管的 PowerPivot 資料重新整理帳戶  
 每個 PowerPivot 服務應用程式僅能設定一個無人看管的 PowerPivot 資料重新整理帳戶。 帳戶資訊儲存在目標應用程式的 Secure Store Service 中，而且該服務設為預先定義的 Windows 網域使用者帳戶。 建立目標應用程式之後，您就可以在 PowerPivot 服務應用程式的組態頁面中，將其指定為 PowerPivot 資料重新整理帳戶。  
  
> [!NOTE]  
>  使用無人看管的資料重新整理帳戶執行資料重新整理時，使用方式報告與資料重新整理記錄會針對用於無人看管之資料重新整理的 Windows 使用者帳戶進行記錄。 如果您需要要求資料重新整理或擁有排程之個人的更正確記錄，請考慮用於執行資料重新整理的其中一個其他選項。 換句話說，讓使者指定自己的認證 (這是預設值)，或建立其他目標應用程式來儲存您要用於資料重新整理用途的所有 Windows 認證。 如需詳細資訊，請參閱[設定 PowerPivot 資料重新整理的預存認證 &#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。  
  
 建立無人看管的資料重新整理帳戶有五部分。  
  
-   在 Secure Store Service 中建立帳戶的目標應用程式，然後指定認證。  
  
-   在 PowerPivot 伺服器組態頁面中，針對無人看管的資料重新整理帳戶指定目標應用程式識別碼。  
  
-   授與「參與」權限給帳戶。  
  
-   授與帳戶讀取權限，以便在資料重新整理期間存取外部資料來源。  
  
-   針對已發行的 PowerPivot 活頁簿，確認在 [管理資料重新整理] 排程頁面中可以使用該帳戶。  
  
###  <a name="step-1-create-a-target-application-and-set-the-credentials"></a><a name="bkmk_create"></a>步驟1：建立目標應用程式並設定認證  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]** 。  
  
2.  按一下 [ **Secure Store Service**]。  
  
3.  在 [管理目標應用程式] 中，按一下 [**新增**]。  
  
4.  在 [目標應用程式識別碼] 中，輸入**PowerPivotDataRefresh**。  
  
5.  在 [顯示名稱] 中，輸入**PowerPivot Data Refresh**。  
  
6.  在 [連絡人電子郵件] 中，輸入您的電子郵件地址。  
  
7.  在 [目標應用程式類型] 中，選取 [**個人**]。  
  
    > [!NOTE]  
    >  在此案例中指定 [個別] 帳戶類型是正確的，因為只有 PowerPivot 服務應用程式才會要求 PowerPivot 無人看管的資料重新整理帳戶的認證。 在實際情況中，此服務應用程式是唯一會使用無人看管的資料重新整理帳戶的使用者，因此對於此目標應用程式而言，[個別] 帳戶類別是最佳的選擇。  
  
8.  略過目標應用程式的網頁 URL。 PowerPivot 資料重新整理不會使用它。  
  
9. 按 [下一步] 。  
  
10. 在 [**指定 Secure Store 目標應用程式的認證欄位**] 頁面中，接受預設值。 欄位名稱和類型應該是 Windows 使用者名稱和 Windows 密碼。  
  
11. 按 [下一步] 。  
  
12. 在 [目標應用程式管理員]，指定 PowerPivot 服務應用程式的應用程式集區識別。 服務需要 [**完全控制**] 許可權，才能在執行時間捕獲自動資料重新整理帳戶資訊。 此外，請針對應該擁有應用程式設定管理存取權的任何其他 SharePoint 使用者指定 Windows 網域使用者帳戶。  
  
13. 按一下 [確定]  。  
  
14. 選取您剛才建立的目標應用程式，按一下向下箭號，然後選取 [**設定認證]。**  
  
15. 在 [**認證擁有**者] 中，輸入您想要擁有更新認證之許可權的 Windows 網域使用者帳戶。 認證會用於資料的新動作，而**認證擁有**者具有修改認證的許可權。  
  
16. 按一下 [確定]  。  
  
###  <a name="step-2-specify-the-unattended-account-in-powerpivot-server-configuration-pages"></a><a name="bkmk_specifyUA"></a>步驟2：在 PowerPivot 服務器設定頁面中指定自動帳戶  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]** 。  
  
2.  尋找 PowerPivot 服務應用程式。 您可以依其類型來識別服務應用程式。 PowerPivot 服務應用程式類型為 **[PowerPivot 服務應用程式]**。  
  
3.  按一下 PowerPivot 服務應用程式名稱。 等待 PowerPivot 管理儀表板出現。  
  
4.  在 [動作] 中，按一下右上角的 [**設定服務應用程式設定**]。  
  
5.  在 [資料重新整理] 的 [PowerPivot 無人看管的資料重新整理帳戶] 中，輸入您在上一個步驟建立的目標應用程式識別碼： **PowerPivotDataRefresh**。  
  
6.  按一下 [確定]  。  
  
###  <a name="step-3-grant-contribute-permissions-to-the-account"></a><a name="bkmk_grant"></a>步驟3：授與帳戶的「參與」許可權  
 在您可以使用 PowerPivot 無人看管的資料重新整理帳戶之前，必須在該帳戶所使用的任何 PowerPivot 活頁簿上指派「參與」權限給它。 您需要這個權限等級才能從文件庫開啟活頁簿，然後在重新整理資料之後，將其存回文件庫。  
  
 指派權限是由網站集合管理員所執行的步驟。 您可以在根網站集合或根網站集合底下的任何層級 (包括個別文件和項目) 指派 SharePoint 權限。 設定權限的方式將隨著細緻程度而有所不同。 下列步驟示範授與權限的其中一個方法。  
  
1.  在 SharePoint 網站的 [網站動作] 中，按一下 [**網站許可權**]。  
  
2.  按一下 [授與權限]****。  
  
3.  在 [選取使用者] 中，輸入您指定為 PowerPivot 無人看管的帳戶之 Windows 網域使用者帳戶的名稱。 這是您在目標應用程式的 Secure Store Service 中指定之 Windows 網域使用者帳戶的名稱。  
  
4.  在 [授與許可權] 中，選取 **[直接授與使用者許可權**]。  
  
5.  選取 [**參與**]，然後按一下 **[確定]**。  
  
###  <a name="step-4-grant-read-permissions-to-access-external-data-sources-used-in-data-refresh"></a><a name="bkmk_dbread"></a>步驟4：授與讀取權限以存取資料重新整理時所使用的外部資料源  
 當資料匯入至 PowerPivot 活頁簿時，外部資料連接通常是以信任連接或是以使用目前使用者身分連接至資料來源的模擬連接為基礎。 這些類型的連接只能在目前使用者有讀取所匯入之資料的權限時使用。  
  
 在資料重新整理案例中，用來匯入資料的相同連接字串現在會重複使用來重新整理資料。 如果連接字串假設目前使用者 (例如，包含 Integrated_Security=SSPI 的字串)，PowerPivot 系統服務就會將 PowerPivot 無人看管資料重新整理帳戶的使用者身分當做目前使用者。 此連接只在 PowerPivot 無人看管的資料重新整理帳戶有讀取外部資料來源的權限時才會成功。  
  
 因此，您必須將 PowerPivot 無人看管的資料重新整理帳戶所執行之任何資料重新整理作業所要使用的所有外部資料來源的唯讀權限，授與此帳戶。  
  
 如果您是組織中使用的資料來源的系統管理員，可以建立登入並指定所需的權限。 否則，您必須連絡資料擁有者並提供帳戶資訊。 請務必指定對應至 PowerPivot 無人看管資料重新整理帳戶的 Windows 網域使用者帳戶。 這是您在本主題的「 (步驟 1) ：建立目標應用程式並設定認證」中指定的帳號。  
  
###  <a name="step-5-verify-account-availability-in-data-refresh-configuration-pages"></a><a name="bkmk_verify"></a>步驟5：在資料重新整理設定頁面中確認帳戶可用性  
  
1.  為包含 PowerPivot 資料之已發行的活頁簿，開啟資料重新整理組態頁面。 如需如何開啟頁面的指示，請參閱[排程資料重新整理 &#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)。  
  
2.  確認已在 [資料重新整理設定] 頁面中，啟用 [**使用系統管理員所設定的資料**重新整理帳戶] 選項。  
  
3.  選取 [**同時**儘快重新整理] 核取方塊，然後按一下 **[確定]**。  
  
4.  在包含活頁簿的文件庫中，選取活頁簿，按一下向右顯示的向下箭號，然後選取 [**管理 PowerPivot 資料**重新整理]。 若資料重新整理作業傳回的資料量十分龐大，可能需要等候數分鐘的時間。  
  
 如果發生錯誤，您可以按一下 [資料重新整理記錄] 頁面中的 [設定**排程**]，以嘗試不同的認證。 您也可能需要檢查原始活頁簿中的資料來源連接資訊，以查看資料重新整理期間所使用的連接字串。 連接字串所提供的伺服器位置與資料庫資訊，可讓您用於疑難排解問題。  
  
 如需有關疑難排解的詳細資訊，請參閱 TechNet Wiki 上的[疑難排解 PowerPivot 資料](https://go.microsoft.com/fwlink/p/?LinkID=223279)重新整理。  
  
##  <a name="using-the-powerpivot-unattended-data-refresh-account"></a><a name="bkmk_use"></a>使用 PowerPivot 無人看管的資料重新整理帳戶  
 在 PowerPivot 資料重新整理排程頁面上所提供的三個認證選項中，只有第一個選項會對應到無人看管的資料重新整理帳戶。 設定資料重新整理排程時，請務必選取此選項。  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 請勿使用第三個認證選項 (即需要您輸入目標應用程式識別碼的選項) 存取 PowerPivot 無人看管的資料重新整理帳戶。 此選項另外還會執行模擬檢查，若您嘗試將此選項用於 PowerPivot 無人看管的資料重新整理帳戶 (或任何使用 [個別] 帳戶類型的目標應用程式)，將會導致驗證錯誤。 如需如何使用第三個選項的詳細資訊，請參閱[設定 PowerPivot 資料重新整理的預存認證 &#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。  
  
##  <a name="update-the-credentials-used-by-an-existing-powerpivot-unattended-data-refresh-account"></a><a name="bkmk_editUA"></a>更新現有 PowerPivot 無人看管的資料重新整理帳戶所使用的認證  
 若安裝程式或管理員已設定了無人看管的資料重新整理帳戶，您即可藉由編輯儲存認證的目標應用程式來更新使用者名稱或密碼。 請注意，當您編輯 Secure Store Service 中的認證時，將不會顯示先前與 PowerPivot 無人看管的資料重新整理帳戶相關聯的原始 Windows 識別。 不論您要更新過期密碼，或要指定不同的帳戶，皆必須在 Secure Store Service 中重新輸入該目標應用程式的使用者名稱及密碼。  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]** 。  
  
2.  按一下 [ **Secure Store Service**]。  
  
3.  選取 [ **PowerPivotDataRefresh**] 旁的核取方塊。  
  
4.  在 [認證] 中，按一下 [**設定**]。  
  
5.  在 [**認證擁有**者] 中，輸入您想要擁有更新認證之許可權的 Windows 網域使用者帳戶。 認證會用於資料的新動作，而**認證擁有**者具有修改認證的許可權。  
  
6.  在 [使用者名稱] 中，輸入將成為自動資料重新整理認證一部分的 Windows 網域使用者帳戶。  
  
7.  在 [密碼] 中，輸入帳戶的密碼，然後重新輸入密碼進行確認。  
  
8.  按一下 [確定]  。  
  
 若同時變更了密碼與使用者名稱，您很可能需要執行其他的組態步驟 (例如授與外部資料來源的讀取權限及 SharePoint 權限)，才可更新 PowerPivot 活頁簿。 如需相關指示，請移至 PowerPivot 無人看管的資料重新整理帳戶設定中的這個步驟：[步驟3：授與帳戶的「參與」許可權](#bkmk_grant)，然後繼續進行所有剩餘的步驟，最後才會確認帳戶已正確設定。  
  
## <a name="see-also"></a>另請參閱  
 [PowerPivot 資料重新整理與 SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)   
 [排程資料重新整理 &#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [PowerPivot 資料重新整理](power-pivot-sharepoint/power-pivot-data-refresh.md)  
  
  
