---
title: 選取 (SSAS) 的資料表和 Views |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.seltablesviews.f1
ms.assetid: 5e8121cc-03f0-4168-98cf-63c5c032bb0b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 891da51478670122f5dbce8fdd7be55c98c898c7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706834"
---
# <a name="select-tables-and-views-ssas"></a><span data-ttu-id="4f771-102">選取資料表和檢視表 (SSAS)</span><span class="sxs-lookup"><span data-stu-id="4f771-102">Select Tables and Views (SSAS)</span></span>
  <span data-ttu-id="4f771-103">[資料表匯入精靈]\*\*\*\* 的這個頁面可讓您選取您要匯入資料的來源資料表和檢視表。</span><span class="sxs-lookup"><span data-stu-id="4f771-103">This page of the **Table Import Wizard** enables you to select the tables and views that you want to import data from.</span></span> <span data-ttu-id="4f771-104">若要從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]存取精靈，請按一下 **[模型]** 功能表上的 **[從資料來源匯入]**。</span><span class="sxs-lookup"><span data-stu-id="4f771-104">To access the wizard from the [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], on the **Model** menu, click **Import from Data Source**.</span></span>  
  
 <span data-ttu-id="4f771-105">此頁面之資料表和檢視表的外觀不保證匯入將會成功。</span><span class="sxs-lookup"><span data-stu-id="4f771-105">The appearance of tables and views on this page does not guarantee that import will succeed.</span></span> <span data-ttu-id="4f771-106">如果在 [模擬資訊] 頁面中指定的使用者未具備從所選資料庫讀取的權限，則匯入將會失敗。</span><span class="sxs-lookup"><span data-stu-id="4f771-106">If the user specified in the Impersonation Information page does not have sufficient privileges to read from the selected database, import will fail.</span></span>  
  
 <span data-ttu-id="4f771-107">針對使用 Windows 驗證的資料來源，目前使用者的認證會用來提取 [選取資料表和檢視表] 對話方塊中的資料表和檢視表。</span><span class="sxs-lookup"><span data-stu-id="4f771-107">For data sources using Windows authentication, the credentials of the current user are used to fetch the tables and views in the Select Tables and Views dialog.</span></span> <span data-ttu-id="4f771-108">至於其他資料來源，連接字串中提供的認證則用來提取資料。</span><span class="sxs-lookup"><span data-stu-id="4f771-108">For other data sources, the credentials supplied in the connection string are used to fetch the data.</span></span>  
  
## <a name="ui-element-list"></a><span data-ttu-id="4f771-109">UI 元素清單</span><span class="sxs-lookup"><span data-stu-id="4f771-109">UI element list</span></span>  
 <span data-ttu-id="4f771-110">**Server**</span><span class="sxs-lookup"><span data-stu-id="4f771-110">**Server**</span></span>  
 <span data-ttu-id="4f771-111">顯示您已連接的伺服器。</span><span class="sxs-lookup"><span data-stu-id="4f771-111">Displays the server that you are connected to.</span></span>  
  
 <span data-ttu-id="4f771-112">**Database**</span><span class="sxs-lookup"><span data-stu-id="4f771-112">**Database**</span></span>  
 <span data-ttu-id="4f771-113">顯示您已選取的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4f771-113">Displays the database that you selected.</span></span>  
  
 <span data-ttu-id="4f771-114">**資料表和檢視表**</span><span class="sxs-lookup"><span data-stu-id="4f771-114">**Tables and Views**</span></span>  
 <span data-ttu-id="4f771-115">列出資料庫中的資料表和檢視表。</span><span class="sxs-lookup"><span data-stu-id="4f771-115">Lists the tables and views in the database.</span></span> <span data-ttu-id="4f771-116">選取您要匯入之每個資料表和檢視表旁邊的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="4f771-116">Select the checkbox beside each table and view that you want to import.</span></span>  
  
 <span data-ttu-id="4f771-117">**來源資料表**</span><span class="sxs-lookup"><span data-stu-id="4f771-117">**Source Table**</span></span>  
 <span data-ttu-id="4f771-118">根據資料來源的類型指定來源資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="4f771-118">Specifies the name of the source table based on the type of data source.</span></span>  
  
 <span data-ttu-id="4f771-119">**結構描述**</span><span class="sxs-lookup"><span data-stu-id="4f771-119">**Schema**</span></span>  
 <span data-ttu-id="4f771-120">指定其中包含來源資料表的結構描述。</span><span class="sxs-lookup"><span data-stu-id="4f771-120">Specifies the schema in which the source table is contained.</span></span> <span data-ttu-id="4f771-121">視資料庫的類型而定，結構描述具有做為其他物件 (例如資料表) 之容器的作用，而且也表示這些物件的擁有權。</span><span class="sxs-lookup"><span data-stu-id="4f771-121">Depending on the type of database, a schema functions as a container for other objects, such as tables, and can also indicate ownership of those objects.</span></span>  
  
 <span data-ttu-id="4f771-122">**易記名稱**</span><span class="sxs-lookup"><span data-stu-id="4f771-122">**Friendly Name**</span></span>  
 <span data-ttu-id="4f771-123">指定來源資料表的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="4f771-123">Specifies the friendly name of the source table.</span></span> <span data-ttu-id="4f771-124">根據預設，此資料行會顯示出現在 [來源資料表]\*\*\*\* 資料行內的來源資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="4f771-124">By default, the column displays the name of the source table that appears in the **Source Table** column.</span></span> <span data-ttu-id="4f771-125">如果您要使用不同於來源資料庫中使用的名稱，請變更這個名稱。</span><span class="sxs-lookup"><span data-stu-id="4f771-125">Change the name if you want to use a different name than the name used in the source database.</span></span>  
  
 <span data-ttu-id="4f771-126">**篩選詳細資料**</span><span class="sxs-lookup"><span data-stu-id="4f771-126">**Filter Details**</span></span>  
 <span data-ttu-id="4f771-127">當篩選已經套用到正在匯入的資料時，在 [篩選詳細資料]\*\*\*\* 對話方塊中顯示資料匯入篩選。</span><span class="sxs-lookup"><span data-stu-id="4f771-127">When a filter has been applied to the data that is being imported, displays the data import filter in the **Filter Details** dialog box.</span></span> <span data-ttu-id="4f771-128">如需詳細資訊，請參閱[篩選詳細資料 &#40;SSAS&#41;](filter-details-ssas.md)。</span><span class="sxs-lookup"><span data-stu-id="4f771-128">For more information, see [Filter Details &#40;SSAS&#41;](filter-details-ssas.md).</span></span>  
  
 <span data-ttu-id="4f771-129">**預覽和篩選**</span><span class="sxs-lookup"><span data-stu-id="4f771-129">**Preview and Filter**</span></span>  
 <span data-ttu-id="4f771-130">顯示 [預覽選取的資料表]\*\*\*\* 對話方塊，此對話方塊是用來將篩選套用到匯入的資料。</span><span class="sxs-lookup"><span data-stu-id="4f771-130">Displays the **Preview Selected Table** dialog box that is used to apply a filter to the data that is being imported.</span></span> <span data-ttu-id="4f771-131">如需詳細資訊，請參閱[預覽選取的資料表 &#40;SSAS&#41;](preview-selected-table-ssas.md)。</span><span class="sxs-lookup"><span data-stu-id="4f771-131">For more information, see [Preview Selected Table &#40;SSAS&#41;](preview-selected-table-ssas.md).</span></span>  
  
 <span data-ttu-id="4f771-132">**選取相關資料表**</span><span class="sxs-lookup"><span data-stu-id="4f771-132">**Select Related Tables**</span></span>  
 <span data-ttu-id="4f771-133">選取以匯入與已選取之資料表和檢視表相關的資料表和檢視表。</span><span class="sxs-lookup"><span data-stu-id="4f771-133">Selects for import those tables and views that are related to the tables and views that you have already selected.</span></span>  
  
  