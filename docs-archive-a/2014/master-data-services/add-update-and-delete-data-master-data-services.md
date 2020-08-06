---
title: 新增、更新和刪除資料 (Master Data Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b6295ead-bd2f-49dd-8756-35c6afb59648
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 5d3d0bf9460591a49cbaa2e5bcbfde6bc003d7a8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87703077"
---
# <a name="add-update-and-delete-data-master-data-services"></a><span data-ttu-id="83c38-102">加入、更新及刪除資料 (Master Data Services)</span><span class="sxs-lookup"><span data-stu-id="83c38-102">Add, Update and Delete Data (Master Data Services)</span></span>
  <span data-ttu-id="83c38-103">您可以將大量資料加入 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]的模型中，也可對模型中的資料進行大量變更。</span><span class="sxs-lookup"><span data-stu-id="83c38-103">You can add data and make data changes to a model in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], in bulk.</span></span>  
  
 <span data-ttu-id="83c38-104">**先決條件**</span><span class="sxs-lookup"><span data-stu-id="83c38-104">**Prerequisites**</span></span>  
  
-   <span data-ttu-id="83c38-105">您必須具有將資料插入 stg.< 的許可權。 \<name>_Leaf，stg.<。 \<name>_Consolidated，stg.<。 \<name>資料庫中 _Relationship 資料表 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="83c38-105">You must have permission to insert data into the stg.\<name>_Leaf, the stg.\<name>_Consolidated, stg.\<name>_Relationship table in the [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database.</span></span>  
  
-   <span data-ttu-id="83c38-106">您必須擁有在資料庫中執行 udp_ stg.< \<name> _Leaf、stg.< \_ \<name> _Consolidated 或 stg.< \_ \<name> _Relationship 預存 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 程式的許可權。</span><span class="sxs-lookup"><span data-stu-id="83c38-106">You must have permissions to execute either the stg.udp_\<name>_Leaf, stg.udp\_\<name>_Consolidated, or the stg.udp\_\<name>_Relationship stored procedure in the [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database.</span></span>  
  
-   <span data-ttu-id="83c38-107">模型的狀態不得為 [已認可] \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="83c38-107">The model must not have a status of **Committed**.</span></span>  
  
 <span data-ttu-id="83c38-108">**若要加入、更新和刪除資料庫中的資料 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]**</span><span class="sxs-lookup"><span data-stu-id="83c38-108">**To add, update, and delete data in the [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database**</span></span>  
  
1.  <span data-ttu-id="83c38-109">準備要匯入 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫之適當暫存資料表中的成員，這包括為必要欄位提供值。</span><span class="sxs-lookup"><span data-stu-id="83c38-109">Prepare the members for import into the appropriate staging table in the [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database, including providing values for the required fields.</span></span> <span data-ttu-id="83c38-110">如需臨時表的總覽，請參閱[資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)</span><span class="sxs-lookup"><span data-stu-id="83c38-110">For an overview of staging tables, see [Data Import &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)</span></span>  
  
    -   <span data-ttu-id="83c38-111">對於分葉成員，資料表為 stg.<。 \<name>_Leaf，其中 \<name> 指的是對應的實體。</span><span class="sxs-lookup"><span data-stu-id="83c38-111">For leaf members the table is stg.\<name>_Leaf, where \<name> refers to the corresponding entity.</span></span> <span data-ttu-id="83c38-112">如需必要欄位的資訊，請參閱[分葉成員暫存資料表 &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md)</span><span class="sxs-lookup"><span data-stu-id="83c38-112">For information about the required fields, see [Leaf Member Staging Table &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md)</span></span>  
  
    -   <span data-ttu-id="83c38-113">若為合併成員，則資料表為 stg.<。 \<name>_Consolidated。</span><span class="sxs-lookup"><span data-stu-id="83c38-113">For consolidated members, the table is stg.\<name>_Consolidated.</span></span> <span data-ttu-id="83c38-114">如需必要欄位的資訊，請參閱[合併成員暫存資料表 &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="83c38-114">For information about the required fields, see [Consolidated Member Staging Table &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md).</span></span>  
  
    -   <span data-ttu-id="83c38-115">若要在明確階層中移動成員的位置，資料表是 stg.<。 \<name>_Relationship。</span><span class="sxs-lookup"><span data-stu-id="83c38-115">For moving the location of members in explicit hierarchies, the table is stg.\<name>_Relationship.</span></span> <span data-ttu-id="83c38-116">如需必要欄位的資訊，請參閱[合併成員暫存資料表 &#40;Master Data Services&#41;](../../2014/master-data-services/relationship-staging-table-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="83c38-116">For information about the required fields, see [Relationship Staging Table &#40;Master Data Services&#41;](../../2014/master-data-services/relationship-staging-table-master-data-services.md).</span></span>  
  
         <span data-ttu-id="83c38-117">如需在明確階層中移動成員的總覽，請參閱[資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="83c38-117">For an overview on moving members in explicit hierarchies, see [Data Import &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).</span></span>  
  
    -   <span data-ttu-id="83c38-118">使用 **ImportType** 欄位值，指定您要建立新成員、停用成員或刪除成員。</span><span class="sxs-lookup"><span data-stu-id="83c38-118">Use the **ImportType** field value to specify that you're creating new members, deactivating members, or deleting members.</span></span> <span data-ttu-id="83c38-119">如需這些值的詳細資訊，請參閱[分葉成員暫存資料表 &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md) 和[合併成員暫存資料表 &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="83c38-119">For more information about the values, see [Leaf Member Staging Table &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md) and [Consolidated Member Staging Table &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md).</span></span>  
  
         <span data-ttu-id="83c38-120">如需停用及刪除成員的總覽，請參閱[資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="83c38-120">For an overview of deactivating and deleting members, see [Data Import &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).</span></span>  
  
2.  <span data-ttu-id="83c38-121">開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 並連接到您 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的 Database Engine 執行個體。</span><span class="sxs-lookup"><span data-stu-id="83c38-121">Open [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] and connect to the Database Engine instance for your [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database.</span></span>  
  
     <span data-ttu-id="83c38-122">如需詳細資訊，請參閱[SQL Server Management Studio](../ssms/sql-server-management-studio-ssms.md)。</span><span class="sxs-lookup"><span data-stu-id="83c38-122">For more information, see [SQL Server Management Studio](../ssms/sql-server-management-studio-ssms.md).</span></span>  
  
3.  <span data-ttu-id="83c38-123">使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 [匯入和匯出精靈]，將資料匯入暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="83c38-123">Import data into the staging tables by using the [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Import and Export wizard.</span></span>  
  
     <span data-ttu-id="83c38-124">如需詳細資訊，請參閱＜ [SQL Server Import and Export Wizard](../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)＞。</span><span class="sxs-lookup"><span data-stu-id="83c38-124">For more information, see [SQL Server Import and Export Wizard](../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).</span></span>  
  
4.  <span data-ttu-id="83c38-125">執行下列其中一項作業，將資料從暫存資料表載入 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料表：</span><span class="sxs-lookup"><span data-stu-id="83c38-125">Load the data from the staging tables to the [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] tables, by doing one of the following</span></span>  
  
    -   <span data-ttu-id="83c38-126">執行對應到資料所要移往之暫存資料表的暫存預存程序。</span><span class="sxs-lookup"><span data-stu-id="83c38-126">Run the staging stored procedure that corresponds to the staging table that you want to move data to.</span></span>  
  
         <span data-ttu-id="83c38-127">如需暫存預存程序和臨時表的總覽，請參閱[資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="83c38-127">For an overview of staging stored procedures and staging tables, see [Data Import &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).</span></span> <span data-ttu-id="83c38-128">如需暫存預存程序之參數及程式碼範例的詳細資訊，請參閱[暫存預存程序 &#40;Master Data Services&#41;](../../2014/master-data-services/staging-stored-procedure-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="83c38-128">For more information about parameters for staging stored procedures, and a code example, see [Staging Stored Procedure &#40;Master Data Services&#41;](../../2014/master-data-services/staging-stored-procedure-master-data-services.md).</span></span>  
  
    -   <span data-ttu-id="83c38-129">使用主資料管理的 **整合管理** 功能。</span><span class="sxs-lookup"><span data-stu-id="83c38-129">Use the **Integration Management** functional area of Master Data Management.</span></span>  
  
         <span data-ttu-id="83c38-130">在 [暫存批次] \*\*\*\* 頁面上，從下拉式清單中，選取要接收您所加入之資料的模型，然後按一下 [啟動批次] \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="83c38-130">On the **Staging Batches** page, select the model to which you're adding data to, in the drop-down list, and then click **Start Batches**.</span></span> <span data-ttu-id="83c38-131">批次處理的狀態會顯示在 [狀態] \*\*\*\* 欄位中。</span><span class="sxs-lookup"><span data-stu-id="83c38-131">The status of the batch processing is indicated in the **Status** field.</span></span> <span data-ttu-id="83c38-132">如需狀態的詳細資訊，請參閱[匯入狀態 &#40;Master Data Services&#41;](../../2014/master-data-services/import-statuses-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="83c38-132">For more information about the statuses, see [Import Statuses &#40;Master Data Services&#41;](../../2014/master-data-services/import-statuses-master-data-services.md).</span></span>  
  
         <span data-ttu-id="83c38-133">![主資料管理員中的暫存批次頁面](../../2014/master-data-services/media/mds-staging-batches.png "主資料管理員中的暫存批次頁面")</span><span class="sxs-lookup"><span data-stu-id="83c38-133">![Staging Batches Page in Master Data Manager](../../2014/master-data-services/media/mds-staging-batches.png "Staging Batches Page in Master Data Manager")</span></span>  
  
         <span data-ttu-id="83c38-134">暫存程序的啟動間隔，由 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中的 [暫存批次間隔]\*\*\*\* 設定決定。</span><span class="sxs-lookup"><span data-stu-id="83c38-134">The staging process  is started at intervals determined by the **Staging batch interval** setting in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].</span></span> <span data-ttu-id="83c38-135">如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="83c38-135">For more information, see [System Settings &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md).</span></span>  
  
5.  <span data-ttu-id="83c38-136">檢視暫存期間發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="83c38-136">View errors that occurred during staging.</span></span> <span data-ttu-id="83c38-137">如需詳細資訊，請參閱[在暫存進程期間發生的視圖錯誤 &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)和[臨時進程錯誤 &#40;Master Data Services&#41;](../../2014/master-data-services/staging-process-errors-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="83c38-137">For more information, see [View Errors that Occur During the Staging Process &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md) and [Staging Process Errors &#40;Master Data Services&#41;](../../2014/master-data-services/staging-process-errors-master-data-services.md).</span></span>  
  
6.  <span data-ttu-id="83c38-138">依據商務規則驗證資料。</span><span class="sxs-lookup"><span data-stu-id="83c38-138">Validate the data against business rules.</span></span>  
  
     <span data-ttu-id="83c38-139">在主資料管理員中，瀏覽至模型的 **Explorer** 功能區域，然後套用商務規則，以驗證資料。</span><span class="sxs-lookup"><span data-stu-id="83c38-139">In Master Data Manager, navigate to the **Explorer** functional area for your model, and then apply business rules to validate the data.</span></span> <span data-ttu-id="83c38-140">如需詳細資訊，請參閱[根據商務規則驗證特定成員 &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="83c38-140">For more information , see [Validate Specific Members against Business Rules &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md).</span></span> <span data-ttu-id="83c38-141">您也可以使用預存程序來驗證資料。</span><span class="sxs-lookup"><span data-stu-id="83c38-141">You can also use a stored procedure to validate the data.</span></span> <span data-ttu-id="83c38-142">如需詳細資訊，請參閱 [驗證預存程序 &#40;Master Data Services&#41;](../../2014/master-data-services/validation-stored-procedure-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="83c38-142">For more information, see [Validation Stored Procedure &#40;Master Data Services&#41;](../../2014/master-data-services/validation-stored-procedure-master-data-services.md).</span></span>  
  
     <span data-ttu-id="83c38-143">當您從暫存資料表載入資料時，不會自動依商務規則驗證該資料。</span><span class="sxs-lookup"><span data-stu-id="83c38-143">When you load data by from the staging tables, the data is not automatically validated against business rules.</span></span> <span data-ttu-id="83c38-144">如需何謂驗證和其發生時機的詳細資訊，請參閱[驗證 &#40;Master Data Services&#41;](../../2014/master-data-services/validation-master-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="83c38-144">For more information on what validation is and when it occurs, see [Validation &#40;Master Data Services&#41;](../../2014/master-data-services/validation-master-data-services.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="83c38-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="83c38-145">See Also</span></span>  
 [<span data-ttu-id="83c38-146">資料匯入 &#40;Master Data Services&#41;</span><span class="sxs-lookup"><span data-stu-id="83c38-146">Data Import &#40;Master Data Services&#41;</span></span>](overview-importing-data-from-tables-master-data-services.md)  
  
  