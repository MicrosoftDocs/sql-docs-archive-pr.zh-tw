---
title: 建立、刪除或修改共用資料來源 (報表管理員) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- removing shared data sources
- data sources [Reporting Services], shared
- deleting shared data sources
- modifying shared data sources
ms.assetid: cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c6f4ff658e656b159995087df3121806b462e687
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596553"
---
# <a name="create-delete-or-modify-a-shared-data-source-report-manager"></a>建立、刪除或修改共用資料來源 (報表管理員)
  共用資料來源會指定資料來源的連接屬性。 如果您擁有大量報表、模型或資料驅動訂閱所使用的資料來源，請考慮建立共用資料來源，以便排除必須在多個位置維護相同連接資訊的負擔。  
  
 下列圖示會指出報表管理員資料夾階層中的共用資料來源：  
  
 ![共用資料來源圖示](media/hlp-16datasource.png "共用資料來源圖示")  
共用資料來源的圖示  
  
### <a name="to-create-a-shared-data-source"></a>若要建立共用資料來源  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)。  
  
2.  在報表管理員中，導覽至 **[內容]** 頁面。  
  
3.  按一下 **[新增資料來源]**。 [新增資料來源]**** 頁面隨即開啟。  
  
4.  輸入項目的名稱。 名稱必須至少包含一個字元，而且開頭必須為字母。 它也可以包含特定符號，但不能包含空格或下列字元：; ? ： \@ & = +，$/* \< > |" /.  
  
5.  選擇性地輸入描述，以提供使用者有關連接的資訊。 此描述會出現在報表管理員的 [內容]**** 頁面上。  
  
6.  在 [資料來源類型]**** 清單中，指定用來處理資料來源中之資料的資料處理延伸模組。  
  
7.  針對 [連接字串]****，指定報表伺服器用於連線到資料來源的連接字串。 建議您不要在連接字串中指定認證。  
  
     下列範例說明用來連接到本機資料庫的連接字串 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] ：  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  針對 **[使用下列方式連接]**，指定報表執行時要如何取得認證：  
  
    -   如果您要提示使用者輸入登入名稱和密碼，請按一下 **[執行報表的使用者所提供的認證]**。 若要使用使用者所輸入的認證作為 Windows 認證，請按一下 [連線到資料來源時作為 Windows 認證]****。 如果使用者名稱和密碼是資料庫認證，請勿選取此選項。  
  
    -   如果您打算將資料來源當作具有資料來源擁有者所管理之預存認證的共用資料來源，或是在支援訂閱或其他已排程之作業 (例如自動化報表記錄產生) 的報表中使用資料來源，請按一下 [安全地儲存在報表伺服器中的認證]****。 如果資料庫伺服器支援模擬或委派，您就可以選取 **[連接到資料來源後，模擬已驗證的使用者]**。  
  
    -   對於存取報表的使用者提供的認證，若要讓報表伺服器將認證傳送給主控外部資料來源的伺服器，請按一下 **[Windows 整合式安全性]**。 在此情況下，不會提示使用者輸入使用者名稱或密碼。  
  
    -   如果資料來源沒有使用認證 (例如，如果資料來源是從檔案系統存取的 XML 檔)，請按一下 [不需要認證]****。 只有當這種認證類型適用於資料來源時，您才應該指定此認證類型。 如果您針對需要驗證的資料來源選取此選項，連接將會失敗。 如果您選取此選項，請務必設定自動執行帳戶，以便在使用者認證無法使用時，允許報表伺服器連接至其他電腦以擷取資料或檔案。  
  
     如需設定認證的詳細資訊，請參閱 [指定報表資料來源的認證及連接資訊](report-data/specify-credential-and-connection-information-for-report-data-sources.md)。 如需自動執行帳戶的詳細資訊，請參閱[設定自動執行帳戶 &#40;SSRS 設定管理員&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
9. 按一下 [測試連線]**** 按鈕，驗證資料來源設定。  
  
    > [!NOTE]  
    >  [測試連接] 按鈕不支援 XML 資料來源類型。  
  
10. 按一下 [檔案] &gt; [新增] &gt; [專案]  
  
### <a name="to-modify-a-shared-data-source"></a>若要修改共用資料來源  
  
1.  在報表管理員中，導覽至 [內容] 頁面。  
  
2.  巡覽至共用資料來源項目，將滑鼠停留在該項目上，按一下下拉式清單，然後在操作功能表中按一下 [管理]****。 [屬性]**** 頁面隨即開啟。  
  
3.  修改資料來源，然後按一下 [套用]****。  
  
### <a name="to-delete-a-shared-data-source"></a>若要刪除共用資料來源  
  
-   在報表管理員中，巡覽至 [內容]**** 頁面，然後執行下列其中一個動作：  
  
    -   導覽至共用資料來源項目。  
  
         按一下項目來開啟它。 [一般屬性] 頁面隨即開啟。  
  
         按一下 [刪除]****，然後按一下 [確定]****。  
  
    -   在 [內容]**** 頁面中，巡覽至包含您要刪除之資料來源的資料夾。  
  
         將滑鼠停留在該項目上，按一下下拉式清單，然後在操作功能表中按一下 [刪除]****。  
  
         [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的資料連線、資料來源及連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [[內容] 頁面 &#40;報表管理員&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [建立、修改和刪除 &#40;SSRS&#41;的共用資料來源](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [管理報表資料來源](report-data/manage-report-data-sources.md)   
 [設定報表的資料來源屬性 &#40;報表管理員&#41;](report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  
