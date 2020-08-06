---
title: 使用現有的資料表建立維度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], dimensions
- main dimension tables
- dimensions [Analysis Services], standard
- standard dimensions [Analysis Services]
ms.assetid: edd96fbe-1b1c-445a-95d6-7a025e0ee868
author: minewiskan
ms.author: owend
ms.openlocfilehash: 42b236275a6e1543ec0b63cc09a9a1bc06b781f5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705609"
---
# <a name="create-a-dimension-by-using-an-existing-table"></a><span data-ttu-id="e5038-102">使用現有的資料表建立維度</span><span class="sxs-lookup"><span data-stu-id="e5038-102">Create a Dimension by Using an Existing Table</span></span>
  <span data-ttu-id="e5038-103">在中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，您可以使用中的 [維度 Wizard]， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 從現有的資料表建立維度。</span><span class="sxs-lookup"><span data-stu-id="e5038-103">In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], you can use the Dimension Wizard in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] to create a dimension from an existing table.</span></span> <span data-ttu-id="e5038-104">方法是，選取精靈之 [選取建立方法]\*\*\*\* 頁面的 [使用現有的資料表]\*\*\*\* 選項。</span><span class="sxs-lookup"><span data-stu-id="e5038-104">You do this by selecting the **Use an existing table** option on the **Select Creation Method** page of the wizard.</span></span> <span data-ttu-id="e5038-105">如果您選取此選項，精靈會以維度資料表、其資料行，以及在現有資料來源檢視中之資料行間的任何關聯性為基礎，</span><span class="sxs-lookup"><span data-stu-id="e5038-105">If you select this option, the wizard bases the dimension structure on the dimension tables, their columns, and any relationships between those columns in an existing data source view.</span></span> <span data-ttu-id="e5038-106">並以來源資料表和相關資料表中的資料為範例。</span><span class="sxs-lookup"><span data-stu-id="e5038-106">The wizard samples the data in the source table and related tables.</span></span> <span data-ttu-id="e5038-107">它會使用此資料，定義以維度資料表中資料行為基礎的屬性資料行，並定義屬性的階層 (稱為「使用者定義的」\*\* 階層)。</span><span class="sxs-lookup"><span data-stu-id="e5038-107">It uses this data to define attribute columns that are based on the columns in the dimension tables, and to define hierarchies of attributes (called *user-defined* hierarchies).</span></span> <span data-ttu-id="e5038-108">使用「維度精靈」建立維度之後，您可以使用 [維度設計師] 在維度中加入、移除和設定屬性與階層。</span><span class="sxs-lookup"><span data-stu-id="e5038-108">After you use the Dimension Wizard to create your dimension, you can use Dimension Designer to add, remove, and configure attributes and hierarchies in the dimension.</span></span>  
  
 <span data-ttu-id="e5038-109">使用現有的資料表建立維度時，「維度精靈」會引導您進行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e5038-109">When you are using an existing table to create a dimension, the Dimension Wizard guides you through the following:</span></span>  
  
-   <span data-ttu-id="e5038-110">指定來源資訊</span><span class="sxs-lookup"><span data-stu-id="e5038-110">Specifying the source information</span></span>  
  
-   <span data-ttu-id="e5038-111">選取相關資料表</span><span class="sxs-lookup"><span data-stu-id="e5038-111">Selecting related tables</span></span>  
  
-   <span data-ttu-id="e5038-112">選取維度屬性</span><span class="sxs-lookup"><span data-stu-id="e5038-112">Selecting dimension attributes</span></span>  
  
-   <span data-ttu-id="e5038-113">定義帳戶智慧</span><span class="sxs-lookup"><span data-stu-id="e5038-113">Defining account intelligence</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="e5038-114">如需與本節所述資訊相對應的逐步指示，請參閱 [使用維度精靈建立維度](create-a-dimension-using-the-dimension-wizard.md)。</span><span class="sxs-lookup"><span data-stu-id="e5038-114">For the step-by-step instructions that correspond to the information presented in this topic, see [Create a Dimension Using the Dimension Wizard](create-a-dimension-using-the-dimension-wizard.md).</span></span>  
  
## <a name="specifying-the-source-information"></a><span data-ttu-id="e5038-115">指定來源資訊</span><span class="sxs-lookup"><span data-stu-id="e5038-115">Specifying the Source Information</span></span>  
 <span data-ttu-id="e5038-116">您可以在 [指定來源資訊]\*\*\*\* 頁面上，指定來源資訊。</span><span class="sxs-lookup"><span data-stu-id="e5038-116">You specify the source information on the **Specify Source Information** page.</span></span> <span data-ttu-id="e5038-117">選取包含您要做為維度基礎之資料表的資料來源檢視，開始此程序。</span><span class="sxs-lookup"><span data-stu-id="e5038-117">You begin this process by selecting the data source view that contains the table on which you want the dimension to be based.</span></span> <span data-ttu-id="e5038-118">然後，您可以針對您要定義的維度來指定主維度資料表。</span><span class="sxs-lookup"><span data-stu-id="e5038-118">You then specify the main dimension table for the dimension that you are defining.</span></span> <span data-ttu-id="e5038-119">主維度資料表是直接連結到事實資料表的資料表。</span><span class="sxs-lookup"><span data-stu-id="e5038-119">The main dimension table is the table that is directly linked to the fact table.</span></span> <span data-ttu-id="e5038-120">例如，將 [產品] 資料表指定為 [產品] 維度的主資料表，或為 [員工] 維度指定 [員工] 資料表。</span><span class="sxs-lookup"><span data-stu-id="e5038-120">For example, specify a Product table as the main table for a Products dimension, or an Employee table for an Employees dimension.</span></span> <span data-ttu-id="e5038-121">精靈會在資料來源檢視中，自動選取以主索引鍵為基礎的索引鍵資料行。</span><span class="sxs-lookup"><span data-stu-id="e5038-121">The wizard automatically selects a key column that is based on the primary key in the data source view.</span></span> <span data-ttu-id="e5038-122">不過，您可以在適當的時機變更索引鍵資料行。</span><span class="sxs-lookup"><span data-stu-id="e5038-122">However, you can change the key column as appropriate.</span></span> <span data-ttu-id="e5038-123">此索引鍵資料行會決定維度的成員。</span><span class="sxs-lookup"><span data-stu-id="e5038-123">The key column determines the members of the dimension.</span></span> <span data-ttu-id="e5038-124">例如，您會將 [ProductKey] 定義為 [產品] 維度的索引鍵資料行。</span><span class="sxs-lookup"><span data-stu-id="e5038-124">For example, you would define ProductKey as the key column for a Product dimension.</span></span>  
  
 <span data-ttu-id="e5038-125">您可以選擇地定義包含成員名稱的資料行。</span><span class="sxs-lookup"><span data-stu-id="e5038-125">Optionally, you can define a column that contains the member name.</span></span> <span data-ttu-id="e5038-126">依預設，顯示給使用者的成員名稱就是此索引鍵資料行中的值。</span><span class="sxs-lookup"><span data-stu-id="e5038-126">By default, the member name that will be displayed to users is the value from the key column.</span></span> <span data-ttu-id="e5038-127">索引鍵資料行中的值 (例如，ProductID 或 EmployeeID) 通常是對使用者無意義，且是唯一的、系統產生的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e5038-127">The values in a key column, such as ProductID or EmployeeID, are often unique, system-generated keys that are meaningless to the user.</span></span> <span data-ttu-id="e5038-128">如果您將使用者看到的名稱變更為維度中其他資料行內的對應值，您通常可以提供更有意義的資訊給使用者。</span><span class="sxs-lookup"><span data-stu-id="e5038-128">You can often provide more meaningful information to the user if you change the name that users see to a corresponding value in some other column in the dimension.</span></span> <span data-ttu-id="e5038-129">例如，您可以定義包含產品或員工名稱的成員名稱資料行。</span><span class="sxs-lookup"><span data-stu-id="e5038-129">For example, you can define a member name column that contains product or employee names.</span></span> <span data-ttu-id="e5038-130">如果您變更成員名稱，使用者會看到更詳細描述的名稱，但是查詢仍會使用索引鍵資料行值，以便正確地分辨共用相同名稱的成員。</span><span class="sxs-lookup"><span data-stu-id="e5038-130">If you change the member name, users see a more descriptive name, but queries still use the key column values to correctly distinguish members that share the same name.</span></span> <span data-ttu-id="e5038-131">如果您為索引鍵資料行指定複合索引鍵，您也必須針對索引鍵屬性，指定提供成員值的資料行。</span><span class="sxs-lookup"><span data-stu-id="e5038-131">If you specify a composite key for the key column, you must also specify the column that provides the member values for the key attribute.</span></span> <span data-ttu-id="e5038-132">如需如何設定屬性的詳細資訊，請參閱 [維度屬性 (attribute) 屬性 (property) 參考](dimension-attribute-properties-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="e5038-132">For more information about how to configure attribute properties, see [Dimension Attribute Properties Reference](dimension-attribute-properties-reference.md).</span></span>  
  
## <a name="selecting-related-tables"></a><span data-ttu-id="e5038-133">選取相關資料表</span><span class="sxs-lookup"><span data-stu-id="e5038-133">Selecting Related Tables</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="e5038-134">如果主維度資料表在資料來源檢視中沒有定義與其他維度資料表之間的任何關聯性，則精靈會略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="e5038-134">The wizard skips this step if the main dimension table has no relationships defined in the data source view to other dimension tables.</span></span>  
  
 <span data-ttu-id="e5038-135">如果您要建立雪花維度，您可以在 [選取相關資料表]\*\*\*\* 頁面上，指定其他屬性定義所在的相關資料表。</span><span class="sxs-lookup"><span data-stu-id="e5038-135">If you are building a snowflake dimension, you specify the related tables from which additional attributes will be defined on the **Select Related Tables** page.</span></span> <span data-ttu-id="e5038-136">例如，您要建立想要在其中定義客戶地理位置資料表的客戶維度。</span><span class="sxs-lookup"><span data-stu-id="e5038-136">For example, you are building a customer dimension in which you want to define a customer geography table.</span></span> <span data-ttu-id="e5038-137">在此情況下，您可以將地理位置資料表定義為相關資料表。</span><span class="sxs-lookup"><span data-stu-id="e5038-137">In this case, you might define a geography table as a related table.</span></span>  
  
## <a name="selecting-dimension-attributes"></a><span data-ttu-id="e5038-138">選取維度屬性</span><span class="sxs-lookup"><span data-stu-id="e5038-138">Selecting Dimension Attributes</span></span>  
 <span data-ttu-id="e5038-139">選取維度資料表後，您可以使用 [選取維度屬性]\*\*\*\* 頁面，從這些資料表中選取您要包含在維度中的屬性。</span><span class="sxs-lookup"><span data-stu-id="e5038-139">After selecting the dimension tables, you use the **Select Dimension Attributes** page to select the attributes that you want to include in the dimension from these tables.</span></span> <span data-ttu-id="e5038-140">所有這些資料表中的所有基礎資料行都可以當做潛在的維度屬性使用。</span><span class="sxs-lookup"><span data-stu-id="e5038-140">All of the underlying columns from all these tables are available as potential dimension attributes.</span></span> <span data-ttu-id="e5038-141">您必須選取維度索引鍵屬性，並針對瀏覽啟用。</span><span class="sxs-lookup"><span data-stu-id="e5038-141">The dimension key attribute must be selected and enabled for browsing.</span></span>  
  
 <span data-ttu-id="e5038-142">根據預設，精靈會將屬性的類型設定為 `Regular`。</span><span class="sxs-lookup"><span data-stu-id="e5038-142">By default, the wizard sets the type of an attribute to `Regular`.</span></span> <span data-ttu-id="e5038-143">不過，您可能想要將特定的屬性對應到更能代表資料的不同屬性類型。</span><span class="sxs-lookup"><span data-stu-id="e5038-143">However, you might want to map specific attributes to a different attribute type that better represents the data.</span></span> <span data-ttu-id="e5038-144">例如， [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] DW 範例資料庫的 dbo.DimAccount 資料表包含可提供帳戶號碼的 AccountCodeAlternateKey 資料行。</span><span class="sxs-lookup"><span data-stu-id="e5038-144">For example, the dbo.DimAccount table in the [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] DW sample database contains an AccountCodeAlternateKey column that provides the account number.</span></span> <span data-ttu-id="e5038-145">`Regular`您可能想要將此屬性對應至類型，而不是將此屬性的類型設定為 `Account Number` 。</span><span class="sxs-lookup"><span data-stu-id="e5038-145">Instead of setting the type to `Regular` for this attribute, you might want to map this attribute to the `Account Number` type.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="e5038-146">如果建立維度時，尚未設定維度類型和標準屬性類型，請在建立維度後，使用「商業智慧精靈」設定這些值。</span><span class="sxs-lookup"><span data-stu-id="e5038-146">If the dimension type and standard attribute types are not set when you create the dimension, use the Business Intelligence Wizard to set these values after you create the dimension.</span></span> <span data-ttu-id="e5038-147">如需詳細資訊，請參閱 [將維度智慧加入至維度中](bi-wizard-add-dimension-intelligence-to-a-dimension.md) 或 [將帳戶智慧加入至維度中](bi-wizard-add-account-intelligence-to-a-dimension.md)(適用於帳戶類型維度)。</span><span class="sxs-lookup"><span data-stu-id="e5038-147">For more information, see [Add Dimension Intelligence to a Dimension](bi-wizard-add-dimension-intelligence-to-a-dimension.md) or (for an Accounts type dimension) [Add Account Intelligence to a Dimension](bi-wizard-add-account-intelligence-to-a-dimension.md).</span></span>  
  
 <span data-ttu-id="e5038-148">精靈會根據指定的屬性類型，自動設定維度類型。</span><span class="sxs-lookup"><span data-stu-id="e5038-148">The wizard automatically sets the dimension type based on the attribute types that are specified.</span></span> <span data-ttu-id="e5038-149">在精靈中指定的屬性類型會針對屬性 (Attribute) 設定 `Type` 屬性 (Property)。</span><span class="sxs-lookup"><span data-stu-id="e5038-149">The attribute types specified in the wizard set the `Type` property for the attributes.</span></span> <span data-ttu-id="e5038-150">維度及其屬性的 `Type` 屬性設定會提供關於維度內容的資訊給伺服器和用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="e5038-150">The `Type` property settings for the dimension and its attributes provide information about the contents of a dimension to server and client applications.</span></span> <span data-ttu-id="e5038-151">在某些情況下，這些 `Type` 屬性設定只會提供用戶端應用程式的指導，而且是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="e5038-151">In some cases, these `Type` property settings only provide guidance for client applications and are optional.</span></span> <span data-ttu-id="e5038-152">在其他情況下 (例如 [帳戶]、[時間] 或 [貨幣] 維度)，這些 `Type` 屬性設定會決定特定的伺服器型行為，且在實作某些 Cube 行為時可能會需要用到。</span><span class="sxs-lookup"><span data-stu-id="e5038-152">In other cases, as for Accounts, Time, or Currency dimensions, these `Type` property settings determine specific server-based behavior and might be required to implement certain cube behavior.</span></span>  
  
 <span data-ttu-id="e5038-153">如需維度和屬性類型的詳細資訊，請參閱 [維度類型](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)、 [設定屬性類型](attribute-properties-configure-attribute-types.md)。</span><span class="sxs-lookup"><span data-stu-id="e5038-153">For more information about dimension and attribute types, see [Dimension Types](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md), [Configure Attribute Types](attribute-properties-configure-attribute-types.md).</span></span>  
  
## <a name="defining-account-intelligence"></a><span data-ttu-id="e5038-154">定義帳戶智慧</span><span class="sxs-lookup"><span data-stu-id="e5038-154">Defining Account Intelligence</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="e5038-155">[維度精靈] 只有在精靈的 [選取維度屬性]\*\*\*\* 頁面上定義了 [帳戶類型]\*\*\*\* 維度屬性時，才會顯示此步驟。</span><span class="sxs-lookup"><span data-stu-id="e5038-155">The Dimension Wizard displays this step only if you defined an **Account Type** dimension attribute on the **Select Dimension Attributes** page of the wizard.</span></span>  
  
 <span data-ttu-id="e5038-156">您可以使用 [定義帳戶智慧]\*\*\*\* 頁面來建立 [帳戶類型] 維度。</span><span class="sxs-lookup"><span data-stu-id="e5038-156">You use the **Define Account Intelligence** page to create an Account type dimension.</span></span> <span data-ttu-id="e5038-157">如果您要建立 [帳戶類型] 維度，您必須將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所支援的標準帳戶類型對應到維度中帳戶類型屬性的成員。</span><span class="sxs-lookup"><span data-stu-id="e5038-157">If you are creating an Account type dimension, you have to map standard account types supported by [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] to members of the account type attribute in the dimension.</span></span> <span data-ttu-id="e5038-158">伺服器會使用這些對應，為各種類型的帳戶資料提供不同的彙總函式和別名。</span><span class="sxs-lookup"><span data-stu-id="e5038-158">The server uses these mappings to provide separate aggregation functions and aliases for each type of account data.</span></span>  
  
 <span data-ttu-id="e5038-159">若要對應這些帳戶類型，精靈會提供具有下列資料行的資料表：</span><span class="sxs-lookup"><span data-stu-id="e5038-159">To map these account types, the wizard provides a table with the following columns:</span></span>  
  
-   <span data-ttu-id="e5038-160">[來源資料表帳戶類型]\*\*\*\* 資料行會列出資料來源資料表中的帳戶類型。</span><span class="sxs-lookup"><span data-stu-id="e5038-160">The **Source Table Account Types** column lists account types from the data source table.</span></span>  
  
-   <span data-ttu-id="e5038-161">[內建帳戶類型]\*\*\*\* 資料行會列出伺服器所支援的對應標準帳戶類型。</span><span class="sxs-lookup"><span data-stu-id="e5038-161">The **Built-In Account Types** column lists the corresponding standard account types supported by the server.</span></span> <span data-ttu-id="e5038-162">如果來源資料使用標準名稱，精靈會將來源類型自動對應到伺服器類型，然後使用此資訊填入 [內建帳戶類型]\*\*\*\* 資料行。</span><span class="sxs-lookup"><span data-stu-id="e5038-162">If the source data uses standard names, the wizard automatically maps the source type to the server type, and populates the **Built-In Account Types** column with this information.</span></span> <span data-ttu-id="e5038-163">如果伺服器沒有對應帳戶類型，或者您想要變更對應，請從 [內建帳戶類型]\*\*\*\* 資料行的清單中選取不同的類型。</span><span class="sxs-lookup"><span data-stu-id="e5038-163">If the server does not map the account types or you want to change the mapping, select a different type from the list in the **Built-In Account Types** column.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="e5038-164">如果在精靈建立 [帳戶] 維度時，尚未對應帳戶類型，請在建立維度後，使用「商業智慧精靈」設定這些對應。</span><span class="sxs-lookup"><span data-stu-id="e5038-164">If the account types are not mapped when the wizard creates an Accounts dimension, use the Business Intelligence Wizard to configure these mappings after you create the dimension.</span></span> <span data-ttu-id="e5038-165">如需詳細資訊，請參閱 [將帳戶智慧加入至維度中](bi-wizard-add-account-intelligence-to-a-dimension.md)。</span><span class="sxs-lookup"><span data-stu-id="e5038-165">For more information, see [Add Account Intelligence to a Dimension](bi-wizard-add-account-intelligence-to-a-dimension.md).</span></span>  
  
## <a name="completing-the-wizard"></a><span data-ttu-id="e5038-166">正在完成精靈</span><span class="sxs-lookup"><span data-stu-id="e5038-166">Completing the Wizard</span></span>  
 <span data-ttu-id="e5038-167">精靈會掃描維度資料表，以偵測關聯性。</span><span class="sxs-lookup"><span data-stu-id="e5038-167">The wizard scans dimension tables to detect relationships.</span></span> <span data-ttu-id="e5038-168">精靈將會在雪花維度中，自動建立索引鍵屬性間的屬性關聯性。</span><span class="sxs-lookup"><span data-stu-id="e5038-168">The wizard will create attribute relationships between key attributes in snowflake dimensions automatically.</span></span>  
  
 <span data-ttu-id="e5038-169">精靈也會自動偵測維度中是否有父子式關聯性。</span><span class="sxs-lookup"><span data-stu-id="e5038-169">The wizard also automatically detects if a parent-child relationship exists in the dimension.</span></span> <span data-ttu-id="e5038-170">當父屬性參考到維度之索引鍵屬性的成員時，父子式關聯性就存在。</span><span class="sxs-lookup"><span data-stu-id="e5038-170">A parent-child relationship exists when a parent attribute references members of the key attribute of the dimension.</span></span> <span data-ttu-id="e5038-171">此關聯性會定義階層式關聯性，以及維度之分葉成員間的彙總路徑。</span><span class="sxs-lookup"><span data-stu-id="e5038-171">This relationship defines hierarchical relationships and aggregation paths between leaf members of the dimension.</span></span> <span data-ttu-id="e5038-172">如需父子式階層的詳細資訊，請參閱 [父子式階層中的屬性](parent-child-dimension-attributes.md)。</span><span class="sxs-lookup"><span data-stu-id="e5038-172">For more information about parent-child hierarchies, see [Attributes in Parent-Child Hierarchies](parent-child-dimension-attributes.md).</span></span>  
  
 <span data-ttu-id="e5038-173">在 [正在完成精靈]\*\*\*\* 頁面上，輸入新維度的名稱，然後檢閱維度的結構，即可完成精靈。</span><span class="sxs-lookup"><span data-stu-id="e5038-173">On the **Completing the Wizard** page, you complete the wizard by typing a name for the new dimension and reviewing the dimension structure.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e5038-174">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e5038-174">See Also</span></span>  
 <span data-ttu-id="e5038-175">[藉由在資料來源中產生非時間資料表來建立維度](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md) </span><span class="sxs-lookup"><span data-stu-id="e5038-175">[Create a Dimension by Generating a Non-Time Table in the Data Source](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md) </span></span>  
 <span data-ttu-id="e5038-176">[藉由產生時間資料表來建立時間維度](create-a-time-dimension-by-generating-a-time-table.md) </span><span class="sxs-lookup"><span data-stu-id="e5038-176">[Create a Time Dimension by Generating a Time Table](create-a-time-dimension-by-generating-a-time-table.md) </span></span>  
 <span data-ttu-id="e5038-177">[維度屬性屬性參考](dimension-attribute-properties-reference.md) </span><span class="sxs-lookup"><span data-stu-id="e5038-177">[Dimension Attribute Properties Reference](dimension-attribute-properties-reference.md) </span></span>  
 <span data-ttu-id="e5038-178">[藉由產生時間資料表來建立時間維度](create-a-time-dimension-by-generating-a-time-table.md) </span><span class="sxs-lookup"><span data-stu-id="e5038-178">[Create a Time Dimension by Generating a Time Table](create-a-time-dimension-by-generating-a-time-table.md) </span></span>  
 [<span data-ttu-id="e5038-179">在資料來源中產生非時間資料表來建立維度</span><span class="sxs-lookup"><span data-stu-id="e5038-179">Create a Dimension by Generating a Non-Time Table in the Data Source</span></span>](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  