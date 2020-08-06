---
title: 報表組件 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10543"
ms.assetid: 957f664c-8a7a-4532-b5a6-5f859c5840bd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eb709f33b208f5bef56cbd6bf5ebf72e735d9433
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87702418"
---
# <a name="report-parts-report-builder-and-ssrs"></a>報表組件 (報表產生器及 SSRS)
  資料表、矩陣、圖表和影像等報表項目都可以當做 *「報表組件」* (Report Part) 發行。 報表組件是指已經個別發行至報表伺服器，而且可以在其他報表中重複使用的報表項目。 報表組件的副檔名為 .rsc。  
  
 有了報表組件，工作群組現在能夠利用其小組成員各不相同的優點與角色。 例如，如果您負責建立圖表，可以將圖表儲存為個別的組件，讓您和您的同事可以在其他報表中共用那些組件。 您可以在報表伺服器或與報表伺服器整合的 SharePoint 網站上發行報表組件。 您可以重複使用多個報表中的報表組件，也可以在伺服器上更新。  
  
 您加入至報表的報表組件藉由唯一識別碼，與網站或伺服器上的報表組件執行個體維持關聯性。 將報表組件從網站或伺服器加入至報表後，不管原始的報表組件位於網站或伺服器上，您都可以修改它們。 您可以接受其他人針對網站或伺服器上之報表組件所進行的更新，而且您可以將修改過的報表組件，透過加入新的報表組件或覆寫原始報表組件，存回網站或伺服器 (如果您有足夠的權限)。  
  
 若要立即開始使用報表組件，請參閱以下影片： [SQL Server 2008 R2 中報表產生器 3 的報表組件](https://technet.microsoft.com/edge/Video/ff711300) 和 [如何：使用 SQL Server 報表產生器建立可重複使用的報表組件](https://technet.microsoft.com/sqlserver/ff634166.aspx)。  
  
##  <a name="life-cycle-of-a-report-part"></a><a name="ComponentWorkflow"></a> 報表組件的生命週期  
 ![rs_ComponentCreation](media/rs-componentcreation.gif "rs_ComponentCreation")  
  
1.  某甲使用與內嵌資料集相依的圖表建立報表。  
  
2.  某甲選擇將圖表發行至報表伺服器。 報表產生器會將唯一的識別碼指派給已發行的圖表。 某甲選擇不共用資料集，因此資料集仍然內嵌在圖表中。  
  
3.  某乙建立空白報表、搜尋報表組件庫、尋找圖表，然後將該圖表加入至報表中。 現在，該圖表加上內嵌資料集都是某乙報表的一部分。 某乙可以修改報表中的圖表執行個體與資料集。 這項作業對報表伺服器上的圖表執行個體和資料集不會有任何影響，也不會中斷報表中與報表伺服器上執行個體之間的關聯性。  
  
     ![rs_componentupdate](media/rs-componentupdate.gif "rs_componentupdate")  
  
4.  某丙將圖表加入至報表，然後將報表中的這個圖表從橫條圖變成圓形圖。  
  
5.  某丙擁有在伺服器上覆寫圖表的權限，而且也這麼做了，並將其重新發行到伺服器。 這樣會更新伺服器上已發行的圖表複本。 某丙也選擇不共用資料集，因此該資料集仍然內嵌在圖表中。  
  
6.  某乙接受來自伺服器的已更新圖表。 這會覆寫某乙在自己報表中對圖表所做的變更。  

##  <a name="publishing-report-parts"></a><a name="PublishingComponents"></a> 發行報表組件  
 當您發行報表組件時，報表產生器會為它指派一個不同於報表組件名稱的唯一識別碼。 不論您變更了報表組件的什麼內容，報表產生器都會維護該識別碼。 識別碼會連結您報表中的原始報表項目至報表組件。 當其他報表作者重複使用此報表組件時，該識別碼也會將其報表中的報表組件連結到報表伺服器上的報表組件。  
  
 以下是您可以發行為報表組件的報表項目：  
  
-   圖表  
  
-   量測計  
  
-   影像  
  
-   地圖  
  
-   參數  
  
-   矩形  
  
-   資料表  
  
-   矩陣  
  
-   清單  
  
 當您發行顯示資料 (例如資料表、矩陣或圖表) 的報表項目時，報表項目相依的資料集會與其儲存在一起，做為內嵌在其中的資料集。 您也可以個別儲存資料集，做為您和其他人可以當做其他報表組件基礎使用的共用資料集。 如需詳細資訊，請參閱 [報表產生器中的報表組件和資料集](report-data/report-parts-and-datasets-in-report-builder.md)。  
  
 有些報表組件可以包含其他報表項目。 例如，資料表可以包含圖表，而矩形可以包含矩陣或圖表。 當您發行包含其他報表項目的報表項目時，會儲存為一個單位。 內嵌在容器報表組件中的其他報表項目會一併儲存。 您無法個別更新它們，而且您無法將容器中的項目儲存為個別的報表組件。  
  
 如需發行報表組件的詳細資訊，請參閱 [發行與重新發行報表組件 &#40;報表產生器及 SSRS&#41;](report-parts-report-builder-and-ssrs.md)(Report Part) 發行。  
  
### <a name="modifying-report-part-metadata"></a>修改報表組件中繼資料  
 您可以使用預設值將報表組件發行至預設位置，或者您可以將每個報表組件儲存至不同的位置，然後修改中繼資料 (例如標題和描述)。  
  
 當您發行報表組件時，最好提供報表組件一個清楚的名稱和描述，以協助使用者在搜尋時識別它。 您可以在網站或伺服器上得到具有類似名稱的大量報表組件。 請考慮使用命名慣例，以說明報表組件及其相依項目之間的關聯性。  
  
 此外，請考慮將共用資料來源、共用資料集，以及相依的報表組件儲存在相同的資料夾中。  
  
 您也可以編輯 [屬性] 窗格中的描述。  

##  <a name="reusing-report-parts"></a><a name="ReusingComponents"></a> 重複使用報表組件  
 建立報表最簡單的方式，就是將現有的報表組件 (如資料表和圖表) 從報表組件庫加入到您的報表。 當您將報表組件加入至報表之後，您可以盡量修改它，或接受來自伺服器的更新。 變更報表中的報表項目不會影響在網站或伺服器上發行之報表組件的執行個體，也不會中斷報表中的執行個體與網站或伺服器上的執行個體之間的關聯性。 如果您足夠的權限，可以將更新的複本存回網站或伺服器。 如果有其他人修改網站或伺服器上的複本，您可以決定要將複本保留原狀，或是更新它，使它成為網站或伺服器上的複本。  
  
### <a name="searching-for-report-parts"></a>搜尋報表組件  
 您會尋找報表組件，以便加入至報表組件庫中的報表。 您可以依下列方式篩選報表組件：報表的全部或部分名稱、建立者、上次修改報表組件者、上次修改時間、儲存位置，或報表組件的類型。 例如，您可以依其中一個同事，搜尋上星期建立的所有圖表。  
  
 您可以以縮圖或清單方式檢視搜尋結果，並依名稱、建立和修改日期，以及建立者來排序搜尋結果。 如需詳細資訊，請參閱 [瀏覽報表組件及設定預設資料夾 &#40;報表產生器及 SSRS&#41;](report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)(Report Part) 發行。  
  
### <a name="what-comes-with-a-report-part"></a>報表組件隨附的內容  
 當您將報表組件加入到報表時，您也會加入此組件運作所必須擁有的所有項目。 例如，顯示資料的任何物件都取決於資料集，也就是資料來源的查詢和連接。 它也有一個或多個參數。 相依的所有項目都是它的 *「相依性」*(Dependency)，而且當您將報表組件加入至報表時，所有相依性或其指標都隨附在報表組件中。 資料集和參數會列在您報表的 [報表資料] 窗格中。  
  
 報表組件的資料集可能會內嵌在報表組件中，或者，它可能是報表組件所指向的個別、共用資料集。 如果資料集內嵌在報表組件中，您可以修改它。 如果是共用資料集，則它是您需要權限的個別物件。 如需共用和內嵌資料集的詳細資訊，請參閱[將資料加入報表 &#40;報表產生器和 SSRS&#41;](report-data/report-datasets-ssrs.md)。  
  
### <a name="resolving-naming-conflicts"></a>解決命名衝突  
 當您加入報表組件時，報表產生器會修正所有名稱衝突。 例如，如果您的報表中已經有一個 Chart1，然後又加入一個稱為 Chart1 的報表組件，報表產生器就會自動將新的報表組件重新命名為 Chart2。 如果您的報表中已經有一個 Dataset1，然後您又加入一個參考不同資料集 (也稱為 Dataset1) 的報表組件，報表產生器會將新的資料集重新命名為 Dataset2，並更新參考。  
  
### <a name="adding-more-than-one-report-part"></a>加入一個以上的報表組件  
 您可以將不限數目的報表組件加入至報表中。 不過，您一次只可以加入一個報表組件。 您甚至可以將一個報表組件的多個執行個體加入至相同的報表中。 這些執行個體全都有唯一的名稱，但全部都是伺服器上相同報表組件的執行個體，而且有相同的唯一識別碼。  
  
 當您加入其他報表組件 (使用與報表中已有之資料集相同的資料集) 時，精靈不會將該資料集的其他版本加入至報表中；它會重新導向報表組件中的參考以移至現有的資料集中。 如需詳細資訊，請參閱 [報表產生器中的報表組件和資料集](report-data/report-parts-and-datasets-in-report-builder.md)。  

##  <a name="updating-report-parts-with-changes-from-the-server"></a><a name="UpdatingComponents"></a> 使用來自伺服器的變更更新報表組件  
 每當您開啟報表時，報表產生器都會檢查伺服器上是否已經更新該報表中之報表組件的伺服器執行個體。 它也會檢查報表組件的相依項目 (如資料集和參數) 是否有變更。 如果伺服器上已經更新任何已發行的報表組件或其相依性，報表中的資訊列會顯示已經更新的數目。 您可以選擇檢視並接受或拒絕更新，或是解除資訊列。 如果選擇檢視更新，您會看到報表組件的縮圖、上次修改者，以及上次修改時間。 接著，您可以接受任何或所有更新的項目。  
  
> [!NOTE]  
>  您可以停用資訊列，如此當報表組件變更時，您就不會收到通知。 當您將報表組件加入至報表時，可設定此選項。 即使您停用了資訊列，還是可以檢查更新。 如需詳細資訊，請參閱[檢查更新或關閉 &#40;報表產生器和 SSRS&#41;的更新](../../2014/reporting-services/check-for-updates-or-turn-updates-off-report-builder-and-ssrs.md)。  
  
 報表產生器會檢查報表組件上次在伺服器上更新的日期，與您上次同步處理報表組件與伺服器的日期之間的差異。 它不會檢查您修改報表中之報表組件的日期。 因此，報表中的報表組件和伺服器上的報表組件差異可能很大，但是報表產生器檢查更新時，將不會發現任何差異。  
  
### <a name="accepting-updates"></a>接受更新  
 當您接受報表組件的更新時，它會完全取代已經在報表中的報表組件複本。 您無法結合報表中的報表組件功能與伺服器上已發行之報表組件的功能。 不過，如果您已經變更其中一個報表組件的相依性 (例如內嵌的資料集)，報表產生器就不會覆寫已經在報表中的相依性。 它會下載一份新的相依性複本，並更新報表組件，以指向新的複本。  
  
### <a name="reverting-to-a-previous-version-of-a-report-part"></a>還原到先前版本的報表組件  
 如果您已經變更報表中的報表組件版本，而且決定要以伺服器上的版本取代它，則您無法使用 **[更新]** 對話方塊來進行這個動作。 更新僅針對您下載報表組件之後，在伺服器上變更的報表組件進行。  
  
 若要還原到伺服器上的版本，只要刪除您在報表中擁有的版本，然後再加入一次即可。  

##  <a name="updating-report-parts-already-on-the-server"></a><a name="RepublishingComponents"></a> 更新已經在伺服器上的報表組件  
 您可以選擇更新伺服器上的現有報表組件，或將其發行為新的報表組件，而不取代現有的報表組件。 當您更新伺服器上的報表組件時，它不會自動修改其他報表中的報表組件複本。 如果其他報表作者已經將該報表組件加入至報表中，下次開啟該報表時就會接到變更的通知。 他們可以選擇接受您所做的變更與否。  
  
 如果您選擇將其發行為新的報表組件，報表產生器會為它提供一個新的唯一識別碼，而且不會再連結到原始的報表組件。  
  
 如果資料集內嵌在報表組件中，則每次發行報表組件時，資料集將會顯示在 **[發行報表組件]** 對話方塊中。 共用資料集不會顯示在 **[發行報表組件]** 對話方塊中。  

##  <a name="working-with-report-parts-in-report-designer"></a><a name="RptPartsRptDesigner"></a> 在報表設計師中使用報表組件  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的報表設計師中，報表組件的運作方式稍有不同。 在報表設計師中，發行作業是單向的：您可以從報表設計師發行報表組件，但不能在報表設計師中重複使用現有的報表組件。 如需詳細資訊，請參閱[報表設計師中的報表組件 &#40;SSRS&#41;](report-design/report-parts-in-report-designer-ssrs.md)。  
  
##  <a name="how-to-topics"></a><a name="HowTo"></a>How to 主題  
 [發行與重新發行報表組件 &#40;報表產生器及 SSRS&#41;](report-parts-report-builder-and-ssrs.md)  
  
 [瀏覽報表組件及設定預設資料夾 &#40;報表產生器及 SSRS&#41;](report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)  
  
 [檢查是否有更新，或關閉 &#40;報表產生器和 SSRS 的更新&#41;](../../2014/reporting-services/check-for-updates-or-turn-updates-off-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>另請參閱  
 [報表產生器中的報表元件和資料集](report-data/report-parts-and-datasets-in-report-builder.md)   
 [&#40;報表產生器和 SSRS&#41;疑難排解報表元件](../../2014/reporting-services/troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [管理報表元件](report-design/managing-report-parts.md)   
 [SQL Server 2008 R2 (影片) 中的報表產生器3個報表元件](https://technet.microsoft.com/edge/Video/ff711300)   
 [如何：使用 SQL Server 報表產生器建立可重複使用的報表組件 (影片)](https://technet.microsoft.com/sqlserver/ff634166.aspx)  
  
  
