---
title: 使用指令碼元件建立來源 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], source components
- output columns [Integration Services]
- sources [Integration Services], components
ms.assetid: 547c4179-ea82-4265-8c6f-04a2aa77a3c0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7a352348f7f47157c5f2ec6d3ff01cea47de0ffb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596778"
---
# <a name="creating-a-source-with-the-script-component"></a><span data-ttu-id="84b15-102">以指令碼元件建立來源</span><span class="sxs-lookup"><span data-stu-id="84b15-102">Creating a Source with the Script Component</span></span>
  <span data-ttu-id="84b15-103">您在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的資料流程中使用來源元件，以從資料來源載入資料，進而將其傳遞至下游轉換與目的地。</span><span class="sxs-lookup"><span data-stu-id="84b15-103">You use a source component in the data flow of an [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] package to load data from a data source to pass on to downstream transformations and destinations.</span></span> <span data-ttu-id="84b15-104">通常您會透過現有的連接管理員來連接到資料來源。</span><span class="sxs-lookup"><span data-stu-id="84b15-104">Ordinarily you connect to the data source through an existing connection manager.</span></span>

 <span data-ttu-id="84b15-105">如需腳本元件的總覽，請參閱 [使用腳本元件擴充資料流程] (.。/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md.</span><span class="sxs-lookup"><span data-stu-id="84b15-105">For an overview of the Script component, see [Extending the Data Flow with the Script Component](../extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md.</span></span>

 <span data-ttu-id="84b15-106">指令碼元件以及它為您產生的基礎結構程式碼，可大幅簡化開發自訂資料流程元件的程序。</span><span class="sxs-lookup"><span data-stu-id="84b15-106">The Script component and the infrastructure code that it generates for you simplify significantly the process of developing a custom data flow component.</span></span> <span data-ttu-id="84b15-107">不過，若要了解指令碼元件如何運作，全部讀完開發自訂資料流程元件所需的步驟，可能會非常有用。</span><span class="sxs-lookup"><span data-stu-id="84b15-107">However, to understand how the Script component works, you may find it useful to read through the steps that are involved in developing a custom data flow component.</span></span> <span data-ttu-id="84b15-108">請參閱[開發自訂資料流程元件](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)一節，尤其是[開發自訂來源元件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)主題。</span><span class="sxs-lookup"><span data-stu-id="84b15-108">See the section [Developing a Custom Data Flow Component](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md), especially the topic [Developing a Custom Source Component](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md).</span></span>

## <a name="getting-started-with-a-source-component"></a><span data-ttu-id="84b15-109">開始使用來源元件</span><span class="sxs-lookup"><span data-stu-id="84b15-109">Getting Started with a Source Component</span></span>
 <span data-ttu-id="84b15-110">當您將指令碼元件新增至 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具的 [資料流程] 窗格時，就會開啟 [選取指令碼元件類型]  對話方塊，並提示您選取 [來源]、[目的地] 或是 [轉換] 指令碼。</span><span class="sxs-lookup"><span data-stu-id="84b15-110">When you add a Script component to the Data Flow pane of [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, the **Select Script Component Type** dialog box opens and prompts you to select a Source, Destination, or Transformation script.</span></span> <span data-ttu-id="84b15-111">在這個對話方塊中，選取 [來源]  。</span><span class="sxs-lookup"><span data-stu-id="84b15-111">In this dialog box, select **Source**.</span></span>

## <a name="configuring-a-source-component-in-metadata-design-mode"></a><span data-ttu-id="84b15-112">在中繼資料設計模式中設定來源元件</span><span class="sxs-lookup"><span data-stu-id="84b15-112">Configuring a Source Component in Metadata-Design Mode</span></span>
 <span data-ttu-id="84b15-113">選擇建立來源元件之後，您可以使用 [指令碼轉換編輯器]  來設定元件。</span><span class="sxs-lookup"><span data-stu-id="84b15-113">After selecting to create a source component, you configure the component by using the **Script Transformation Editor**.</span></span> <span data-ttu-id="84b15-114">如需詳細資訊，請參閱[在指令碼元件編輯器中設定指令碼元件](../extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。</span><span class="sxs-lookup"><span data-stu-id="84b15-114">For more information, see [Configuring the Script Component in the Script Component Editor](../extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).</span></span>

 <span data-ttu-id="84b15-115">資料流程來源元件沒有輸入，而且支援一或多個輸出。</span><span class="sxs-lookup"><span data-stu-id="84b15-115">A data flow source component has no inputs and supports one or more outputs.</span></span> <span data-ttu-id="84b15-116">設定元件的輸出是您必須在中繼資料設計模式下完成的其中一個步驟，方法是在撰寫自訂指令碼之前先使用 [指令碼轉換編輯器]  。</span><span class="sxs-lookup"><span data-stu-id="84b15-116">Configuring the outputs for the component is one of the steps that you must complete in metadata design mode, by using the **Script Transformation Editor**, before you write your custom script.</span></span>

 <span data-ttu-id="84b15-117">您也可以在 [指令碼轉換編輯器]  的 [指令碼]  頁面上設定 [ScriptLanguage]  屬性，來指定指令碼語言。</span><span class="sxs-lookup"><span data-stu-id="84b15-117">You can also specify the script language by setting the **ScriptLanguage** property on the **Script** page of the **Script Transformation Editor**.</span></span>

> [!NOTE]
>  <span data-ttu-id="84b15-118">若要為指令碼元件和指令碼工作設定預設指令碼語言，請使用 [選項]  對話方塊的 [一般]  頁面上的 [指令碼語言]  選項。</span><span class="sxs-lookup"><span data-stu-id="84b15-118">To set the default script language for Script components and Script Tasks, use the **Scripting language** option on the **General** page of the **Options** dialog box.</span></span> <span data-ttu-id="84b15-119">如需相關資訊，請參閱 [General Page](../general-page-of-integration-services-designers-options.md)。</span><span class="sxs-lookup"><span data-stu-id="84b15-119">For more information, see [General Page](../general-page-of-integration-services-designers-options.md).</span></span>

### <a name="adding-connection-managers"></a><span data-ttu-id="84b15-120">加入連接管理員</span><span class="sxs-lookup"><span data-stu-id="84b15-120">Adding Connection Managers</span></span>
 <span data-ttu-id="84b15-121">通常來源元件使用現有的連接管理員，以連接到它將資料載入資料流程的資料來源。</span><span class="sxs-lookup"><span data-stu-id="84b15-121">Ordinarily a source component uses an existing connection manager to connect to the data source from which it loads data into the data flow.</span></span> <span data-ttu-id="84b15-122">在 [指令碼轉換編輯器]  的 [連線管理員]  頁面上，按一下 [新增]  新增適當的連線管理員。</span><span class="sxs-lookup"><span data-stu-id="84b15-122">On the **Connection Managers** page of the **Script Transformation Editor**, click **Add** to add the appropriate connection manager.</span></span>

 <span data-ttu-id="84b15-123">然而，連接管理員只是一種便利的單位，用以封裝和儲存連接至特定類型的資料來源所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="84b15-123">However, a connection manager is only a convenient unit that encapsulates and stores the information that it must have to connect to a data source of a particular type.</span></span> <span data-ttu-id="84b15-124">您必須撰寫自己的自訂程式碼，以載入或是儲存資料，以及 (可能的話) 開啟和關閉連至資料來源的連接。</span><span class="sxs-lookup"><span data-stu-id="84b15-124">You must write your own custom code to load or save your data, and possibly to open and close the connection to the data source also.</span></span>

 <span data-ttu-id="84b15-125">如需如何利用指令碼元件以使用連線管理員的一般資訊，請參閱[在指令碼元件中連線至資料來源](../extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)。</span><span class="sxs-lookup"><span data-stu-id="84b15-125">For general information about how to use connection managers with the Script component, see [Connecting to Data Sources in the Script Component](../extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).</span></span>

 <span data-ttu-id="84b15-126">如需 [指令碼轉換編輯器]  之 [連線管理員]  頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;連線管理員頁面&#41;](../script-transformation-editor-connection-managers-page.md)。</span><span class="sxs-lookup"><span data-stu-id="84b15-126">For more information about the **Connection Managers** page of the **Script Transformation Editor**, see [Script Transformation Editor &#40;Connection Managers Page&#41;](../script-transformation-editor-connection-managers-page.md).</span></span>

### <a name="configuring-outputs-and-output-columns"></a><span data-ttu-id="84b15-127">設定輸出和輸出資料行</span><span class="sxs-lookup"><span data-stu-id="84b15-127">Configuring Outputs and Output Columns</span></span>
 <span data-ttu-id="84b15-128">來源元件沒有輸入，而且支援一或多個輸出。</span><span class="sxs-lookup"><span data-stu-id="84b15-128">A source component has no inputs and supports one or more outputs.</span></span> <span data-ttu-id="84b15-129">在 [指令碼轉換編輯器]  的 [輸入及輸出]  頁面上，預設已建立單一輸出，但是尚未建立輸出資料行。</span><span class="sxs-lookup"><span data-stu-id="84b15-129">On the **Inputs and Outputs** page of the **Script Transformation Editor**, a single output has been created by default, but no output columns have been created.</span></span> <span data-ttu-id="84b15-130">在編輯器的此頁面上，您可能會需要或想要設定下列項目。</span><span class="sxs-lookup"><span data-stu-id="84b15-130">On this page of the editor, you may need or want to configure the following items.</span></span>

-   <span data-ttu-id="84b15-131">您必須為每個輸出手動加入和設定輸出資料行。</span><span class="sxs-lookup"><span data-stu-id="84b15-131">You must add and configure output columns manually for each output.</span></span> <span data-ttu-id="84b15-132">為每個輸出選取 [輸出資料行] 資料夾，然後使用 [新增資料行]  和 [移除資料行]  按鈕，為來源元件的每個輸出管理輸出資料行。</span><span class="sxs-lookup"><span data-stu-id="84b15-132">Select the Output Columns folder for each output, and then use the **Add Column** and **Remove Column** buttons to manage the output columns for each output of the source component.</span></span> <span data-ttu-id="84b15-133">之後，您將在指令碼中使用這裡所指派的名稱來參考輸出資料行，方法是使用在自動產生的程式碼中為您建立的具有類型之存取子屬性。</span><span class="sxs-lookup"><span data-stu-id="84b15-133">Later, you will refer to the output columns in your script by the names that you assign here, by using the typed accessor properties created for you in the auto-generated code.</span></span>

-   <span data-ttu-id="84b15-134">您可能會想要建立一或多個其他輸出，例如含有非預期值的資料列之模擬錯誤輸出。</span><span class="sxs-lookup"><span data-stu-id="84b15-134">You may want to create one or more additional outputs, such as a simulated error output for rows that contain unexpected values.</span></span> <span data-ttu-id="84b15-135">使用 [新增輸出]  和 [移除輸出]  按鈕管理來源元件的輸出。</span><span class="sxs-lookup"><span data-stu-id="84b15-135">Use the **Add Output** and **Remove Output** buttons to manage the outputs of the source component.</span></span> <span data-ttu-id="84b15-136">所有的輸入資料列都會導向至所有可用的輸出，除非您也為那些輸出的 `ExclusionGroup` 屬性指定相同的非零值，也就是您想要將每個輸入資料列導向至有著相同 `ExclusionGroup` 值的其中一個輸出。</span><span class="sxs-lookup"><span data-stu-id="84b15-136">All input rows are directed to all available outputs unless you also specify an identical non-zero value for the `ExclusionGroup` property of those outputs where you intend to direct each row to only one of the outputs that share the same `ExclusionGroup` value.</span></span> <span data-ttu-id="84b15-137">至於選取哪一個特定的整數值以識別 `ExclusionGroup` 則無關緊要。</span><span class="sxs-lookup"><span data-stu-id="84b15-137">The particular integer value selected to identify the `ExclusionGroup` is not significant.</span></span>

    > [!NOTE]
    >  <span data-ttu-id="84b15-138">當您不想要輸出所有的資料列時，也可以使用具有單一輸出的非零 `ExclusionGroup` 屬性值。</span><span class="sxs-lookup"><span data-stu-id="84b15-138">You can also use a non-zero `ExclusionGroup` property value with a single output when you do not want to output all rows.</span></span> <span data-ttu-id="84b15-139">不過，在此情況下，您必須為要傳送至輸出的每個資料列，明確地呼叫 **DirectRowTo\<outputbuffer>** 方法。</span><span class="sxs-lookup"><span data-stu-id="84b15-139">In this case, however, you must explicitly call the **DirectRowTo\<outputbuffer>** method for each row that you want to send to the output.</span></span>

-   <span data-ttu-id="84b15-140">您可能會想要將易記名稱指派給輸出。</span><span class="sxs-lookup"><span data-stu-id="84b15-140">You may want to assign a friendly name to the outputs.</span></span> <span data-ttu-id="84b15-141">之後，您將在指令碼中使用輸出的名稱來加以參考，方法是使用在自動產生的程式碼中為您建立的具有類型之存取子屬性。</span><span class="sxs-lookup"><span data-stu-id="84b15-141">Later, you will refer to the outputs by their names in your script, by using the typed accessor properties created for you in the auto-generated code.</span></span>

-   <span data-ttu-id="84b15-142">通常，在相同 `ExclusionGroup` 中的多個輸出都有相同的輸出資料行。</span><span class="sxs-lookup"><span data-stu-id="84b15-142">Ordinarily multiple outputs in the same `ExclusionGroup` have the same output columns.</span></span> <span data-ttu-id="84b15-143">然而，如果您正在建立模擬的錯誤輸出，可能會想要加入更多的資料行以儲存錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="84b15-143">However, if you are creating a simulated error output, you may want to add more columns to store error information.</span></span> <span data-ttu-id="84b15-144">如需資料流程引擎如何處理錯誤資料列的資訊，請參閱[使用資料流程元件中的錯誤輸出](../extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)。</span><span class="sxs-lookup"><span data-stu-id="84b15-144">For information about how the data flow engine processes error rows, see [Using Error Outputs in a Data Flow Component](../extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md).</span></span> <span data-ttu-id="84b15-145">不過，在指令碼元件中，您必須撰寫自已的程式碼，以適當的錯誤資訊填入其他資料行。</span><span class="sxs-lookup"><span data-stu-id="84b15-145">In the Script component, however, you must write your own code to fill the additional columns with appropriate error information.</span></span> <span data-ttu-id="84b15-146">如需詳細資訊，請參閱[模擬指令碼元件的錯誤輸出](../extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)。</span><span class="sxs-lookup"><span data-stu-id="84b15-146">For more information, see [Simulating an Error Output for the Script Component](../extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).</span></span>

 <span data-ttu-id="84b15-147">如需 [指令碼轉換編輯器]  之 [輸入及輸出]  頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;輸入及輸出頁面&#41;](../script-transformation-editor-inputs-and-outputs-page.md)。</span><span class="sxs-lookup"><span data-stu-id="84b15-147">For more information about the **Inputs and Outputs** page of the **Script Transformation Editor**, see [Script Transformation Editor &#40;Inputs and Outputs Page&#41;](../script-transformation-editor-inputs-and-outputs-page.md).</span></span>

### <a name="adding-variables"></a><span data-ttu-id="84b15-148">加入變數</span><span class="sxs-lookup"><span data-stu-id="84b15-148">Adding Variables</span></span>
 <span data-ttu-id="84b15-149">如果有任何現有變數的值是您想要在腳本中使用的，您可以在 [ `ReadOnlyVariables` `ReadWriteVariables` **腳本轉換編輯器**] 的 [**腳本**] 頁面上，將它們加入和屬性欄位中。</span><span class="sxs-lookup"><span data-stu-id="84b15-149">If there are any existing variables whose values you want to use in your script, you can add them in the `ReadOnlyVariables` and `ReadWriteVariables` property fields on the **Script** page of the **Script Transformation Editor**.</span></span>

 <span data-ttu-id="84b15-150">當您在屬性欄位中輸入多個變數時，請用逗號分隔變數名稱。</span><span class="sxs-lookup"><span data-stu-id="84b15-150">When you enter multiple variables in the property fields, separate the variable names by commas.</span></span> <span data-ttu-id="84b15-151">您也可以按一下和屬性欄位旁邊的省略號 (**...**) ] 按鈕 `ReadOnlyVariables` `ReadWriteVariables` ，然後在 [**選取變數**] 對話方塊中選取變數，以輸入多個變數。</span><span class="sxs-lookup"><span data-stu-id="84b15-151">You can also enter multiple variables by clicking the ellipsis (**...**) button next to the `ReadOnlyVariables` and `ReadWriteVariables` property fields and selecting variables in the **Select variables** dialog box.</span></span>

 <span data-ttu-id="84b15-152">如需如何利用指令碼元件使用變數的一般資訊，請參閱[在指令碼元件中使用變數](../extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。</span><span class="sxs-lookup"><span data-stu-id="84b15-152">For general information about how to use variables with the Script component, see [Using Variables in the Script Component](../extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).</span></span>

 <span data-ttu-id="84b15-153">如需 [指令碼轉換編輯器]  的 [指令碼]  頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;指令碼頁面&#41;](../script-transformation-editor-script-page.md)。</span><span class="sxs-lookup"><span data-stu-id="84b15-153">For more information about the **Script** page of the **Script Transformation Editor**, see [Script Transformation Editor &#40;Script Page&#41;](../script-transformation-editor-script-page.md).</span></span>

## <a name="scripting-a-source-component-in-code-design-mode"></a><span data-ttu-id="84b15-154">在程式碼設計模式中編寫來源元件的指令碼</span><span class="sxs-lookup"><span data-stu-id="84b15-154">Scripting a Source Component in Code-Design Mode</span></span>
 <span data-ttu-id="84b15-155">在您已為元件設定中繼資料之後，請開啟 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE 以撰寫自訂指令碼。</span><span class="sxs-lookup"><span data-stu-id="84b15-155">After you have configured the metadata for your component, open the [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE to code your custom script.</span></span> <span data-ttu-id="84b15-156">若要開啟 VSTA，請在 [指令碼轉換編輯器]  的 [指令碼]  頁面上，按一下 [編輯指令碼]  。</span><span class="sxs-lookup"><span data-stu-id="84b15-156">To open VSTA, click **Edit Script** on the **Script** page of the **Script Transformation Editor**.</span></span> <span data-ttu-id="84b15-157">您可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 撰寫指令碼，視為 **ScriptLanguage** 屬性選取的指令碼語言而定。</span><span class="sxs-lookup"><span data-stu-id="84b15-157">You can write your script by using either [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic or [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#, depending on the script language selected for the **ScriptLanguage** property.</span></span>

 <span data-ttu-id="84b15-158">如需使用指令碼元件所建立之各種元件都適用的重要資訊，請參閱[編碼和偵錯指令碼元件](../extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。</span><span class="sxs-lookup"><span data-stu-id="84b15-158">For important information that applies to all kinds of components created by using the Script component, see [Coding and Debugging the Script Component](../extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).</span></span>

### <a name="understanding-the-auto-generated-code"></a><span data-ttu-id="84b15-159">了解自動產生的程式碼</span><span class="sxs-lookup"><span data-stu-id="84b15-159">Understanding the Auto-generated Code</span></span>
 <span data-ttu-id="84b15-160">當您在建立和設定來源元件之後開啟 VSTA IDE，可編輯的 `ScriptMain` 類別會出現在程式碼編輯器中。</span><span class="sxs-lookup"><span data-stu-id="84b15-160">When you open the VSTA IDE after creating and configuring a source component, the editable `ScriptMain` class appears in the code editor.</span></span> <span data-ttu-id="84b15-161">您在 `ScriptMain` 類別中撰寫自訂程式碼。</span><span class="sxs-lookup"><span data-stu-id="84b15-161">You write your custom code in the `ScriptMain` class.</span></span>

 <span data-ttu-id="84b15-162">`ScriptMain` 類別包括 `CreateNewOutputRows` 方法的 Stub。</span><span class="sxs-lookup"><span data-stu-id="84b15-162">The `ScriptMain` class includes a stub for the `CreateNewOutputRows` method.</span></span> <span data-ttu-id="84b15-163">`CreateNewOutputRows` 是來源元件中最重要的方法。</span><span class="sxs-lookup"><span data-stu-id="84b15-163">The `CreateNewOutputRows` is the most important method in a source component.</span></span>

 <span data-ttu-id="84b15-164">如果您在 VSTA 中開啟 [**專案管理器**] 視窗，您可以看到腳本元件也會產生唯讀 `BufferWrapper` 和 `ComponentWrapper` 專案專案。</span><span class="sxs-lookup"><span data-stu-id="84b15-164">If you open the **Project Explorer** window in VSTA, you can see that the Script component has also generated read-only `BufferWrapper` and `ComponentWrapper` project items.</span></span> <span data-ttu-id="84b15-165">`ScriptMain` 類別會繼承 `UserComponent` 專案項目中的 `ComponentWrapper` 類別。</span><span class="sxs-lookup"><span data-stu-id="84b15-165">The `ScriptMain` class inherits from `UserComponent` class in the `ComponentWrapper` project item.</span></span>

 <span data-ttu-id="84b15-166">在執行階段，資料流程引擎會叫用 `PrimeOutput` 類別中的 `UserComponent` 方法，它會覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost.PrimeOutput%2A> 父類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法。</span><span class="sxs-lookup"><span data-stu-id="84b15-166">At run time, the data flow engine invokes the `PrimeOutput` method in the `UserComponent` class, which overrides the <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost.PrimeOutput%2A> method of the <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> parent class.</span></span> <span data-ttu-id="84b15-167">`PrimeOutput` 方法會依序呼叫下列方法：</span><span class="sxs-lookup"><span data-stu-id="84b15-167">The `PrimeOutput` method in turn calls the following methods:</span></span>

1.  <span data-ttu-id="84b15-168">您在 `CreateNewOutputRows` 中覆寫以便從資料來源將資料列加入輸出緩衝區的 `ScriptMain` 方法，一開始會是空的。</span><span class="sxs-lookup"><span data-stu-id="84b15-168">The `CreateNewOutputRows` method, which you override in `ScriptMain` to add rows from the data source to the output buffers, which are empty at first.</span></span>

2.  <span data-ttu-id="84b15-169"> 方法預設是空的。</span><span class="sxs-lookup"><span data-stu-id="84b15-169">The `FinishOutputs` method, which is empty by default.</span></span> <span data-ttu-id="84b15-170">在 `ScriptMain` 中覆寫此方法以執行完成輸出所需的處理。</span><span class="sxs-lookup"><span data-stu-id="84b15-170">Override this method in `ScriptMain` to perform any processing that is required to complete the output.</span></span>

3.  <span data-ttu-id="84b15-171">私用 `MarkOutputsAsFinished` 方法 (呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.SetEndOfRowset%2A> 父類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 方法) 用以指出輸出已完成的資料流程引擎。</span><span class="sxs-lookup"><span data-stu-id="84b15-171">The private `MarkOutputsAsFinished` method, which calls the <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.SetEndOfRowset%2A> method of the <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> parent class to indicate to the data flow engine that the output is finished.</span></span> <span data-ttu-id="84b15-172">在自己的程式碼中不必明確地呼叫 `SetEndOfRowset`。</span><span class="sxs-lookup"><span data-stu-id="84b15-172">You do not have to call `SetEndOfRowset` explicitly in your own code.</span></span>

### <a name="writing-your-custom-code"></a><span data-ttu-id="84b15-173">撰寫您的自訂程式碼</span><span class="sxs-lookup"><span data-stu-id="84b15-173">Writing Your Custom Code</span></span>
 <span data-ttu-id="84b15-174">為了完成建立自訂來源元件，您可能會想要以 `ScriptMain` 類別中提供的下列方法來撰寫指令碼。</span><span class="sxs-lookup"><span data-stu-id="84b15-174">To finish creating a custom source component, you may want to write script in the following methods available in the `ScriptMain` class.</span></span>

1.  <span data-ttu-id="84b15-175">覆寫 `AcquireConnections` 方法以連接至外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="84b15-175">Override the `AcquireConnections` method to connect to the external data source.</span></span> <span data-ttu-id="84b15-176">從連接管理員擷取連接物件，或是必要的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="84b15-176">Extract the connection object, or the required connection information, from the connection manager.</span></span>

2.  <span data-ttu-id="84b15-177">如果您可以同時載入所有的來源資料，請覆寫 `PreExecute` 方法以載入資料。</span><span class="sxs-lookup"><span data-stu-id="84b15-177">Override the `PreExecute` method to load data, if you can load all the source data at the same time.</span></span> <span data-ttu-id="84b15-178">例如，您可以針對連至 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接，執行 `SqlCommand`，並同時將所有的來源資料載入 `SqlDataReader`。</span><span class="sxs-lookup"><span data-stu-id="84b15-178">For example, you can execute a `SqlCommand` against an [!INCLUDE[vstecado](../../includes/vstecado-md.md)] connection to a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database and load all the source data at the same time into a `SqlDataReader`.</span></span> <span data-ttu-id="84b15-179">如果您必須一次載入一個資料列的來源資料 (例如，在讀取文字檔時)，可以在 `CreateNewOutputRows` 中循環使用資料列時載入資料。</span><span class="sxs-lookup"><span data-stu-id="84b15-179">If you must load the source data one row at a time (for example, when reading a text file), you can load the data as you loop through rows in `CreateNewOutputRows`.</span></span>

3.  <span data-ttu-id="84b15-180">使用覆寫的 `CreateNewOutputRows` 方法將新資料列加入空的輸出緩衝區，並將新輸出資料列中的每個資料行填入值。</span><span class="sxs-lookup"><span data-stu-id="84b15-180">Use the overridden `CreateNewOutputRows` method to add new rows to the empty output buffers and to fill in the values of each column in the new output rows.</span></span> <span data-ttu-id="84b15-181">使用每個輸出緩衝區的 `AddRow` 方法，加入空的新資料列，然後設定每個資料行的值。</span><span class="sxs-lookup"><span data-stu-id="84b15-181">Use the `AddRow` method of each output buffer to add an empty new row, and then set the values of each column.</span></span> <span data-ttu-id="84b15-182">通常您會複製從外部來源載入的資料行值。</span><span class="sxs-lookup"><span data-stu-id="84b15-182">Typically you copy values from the columns loaded from the external source.</span></span>

4.  <span data-ttu-id="84b15-183">覆寫 `PostExecute` 方法以完成處理資料。</span><span class="sxs-lookup"><span data-stu-id="84b15-183">Override the `PostExecute` method to finish processing the data.</span></span> <span data-ttu-id="84b15-184">例如，您可以關閉用以載入資料的 `SqlDataReader`。</span><span class="sxs-lookup"><span data-stu-id="84b15-184">For example, you can close the `SqlDataReader` that you used to load data.</span></span>

5.  <span data-ttu-id="84b15-185">視需要，覆寫 `ReleaseConnections` 方法從外部資料來源中斷連接。</span><span class="sxs-lookup"><span data-stu-id="84b15-185">Override the `ReleaseConnections` method to disconnect from the external data source, if required.</span></span>

## <a name="examples"></a><span data-ttu-id="84b15-186">範例</span><span class="sxs-lookup"><span data-stu-id="84b15-186">Examples</span></span>
 <span data-ttu-id="84b15-187">下列範例示範建立來源元件時，`ScriptMain` 類別中所需的自訂程式碼。</span><span class="sxs-lookup"><span data-stu-id="84b15-187">The following examples demonstrate the custom code that is required in the `ScriptMain` class to create a source component.</span></span>

> [!NOTE]
>  <span data-ttu-id="84b15-188">這些範例會使用**Person.Address** `AdventureWorks` 範例資料庫中的**intAddressID**和第四個數據行，也就是透過資料流程來傳遞第一個和第四個數據行，也就是和**Nvarchar (30) City**資料行。</span><span class="sxs-lookup"><span data-stu-id="84b15-188">These examples use the **Person.Address** table in the `AdventureWorks` sample database and pass its first and fourth columns, the **intAddressID** and **nvarchar(30)City** columns, through the data flow.</span></span> <span data-ttu-id="84b15-189">在本章節中的來源、轉換和目的地範例使用相同的資料。</span><span class="sxs-lookup"><span data-stu-id="84b15-189">The same data is used in the source, transformation, and destination samples in this section.</span></span> <span data-ttu-id="84b15-190">每個範例都會記載其他必要條件與假設。</span><span class="sxs-lookup"><span data-stu-id="84b15-190">Additional prerequisites and assumptions are documented for each example.</span></span>

### <a name="adonet-source-example"></a><span data-ttu-id="84b15-191">ADO.NET 來源範例</span><span class="sxs-lookup"><span data-stu-id="84b15-191">ADO.NET Source Example</span></span>
 <span data-ttu-id="84b15-192">這個範例示範一個來源元件，它使用現有的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表將資料載入資料流程。</span><span class="sxs-lookup"><span data-stu-id="84b15-192">This example demonstrates a source component that uses an existing [!INCLUDE[vstecado](../../includes/vstecado-md.md)] connection manager to load data from a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] table into the data flow.</span></span>

 <span data-ttu-id="84b15-193">如果您要執行這個範例程式碼，必須依下列方式設定封裝與元件：</span><span class="sxs-lookup"><span data-stu-id="84b15-193">If you want to run this sample code, you must configure the package and the component as follows:</span></span>

1.  <span data-ttu-id="84b15-194">建立一個 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員，以使用 `SqlClient` 提供者連接到 `AdventureWorks` 資料庫。</span><span class="sxs-lookup"><span data-stu-id="84b15-194">Create an [!INCLUDE[vstecado](../../includes/vstecado-md.md)] connection manager that uses the `SqlClient` provider to connect to the `AdventureWorks` database.</span></span>

2.  <span data-ttu-id="84b15-195">將新指令碼元件加入資料流程設計師介面，並將它設定為來源。</span><span class="sxs-lookup"><span data-stu-id="84b15-195">Add a new Script component to the Data Flow designer surface and configure it as a source.</span></span>

3.  <span data-ttu-id="84b15-196">開啟**指令碼轉換編輯器**。</span><span class="sxs-lookup"><span data-stu-id="84b15-196">Open the **Script Transformation Editor**.</span></span> <span data-ttu-id="84b15-197">在 [輸入及輸出]  頁面上，以更具描述性的名稱重新命名預設輸出，例如 **MyAddressOutput**，以及新增和設定兩個輸出資料行：**AddressID** 和 **City**。</span><span class="sxs-lookup"><span data-stu-id="84b15-197">On the **Inputs and Outputs** page, rename the default output with a more descriptive name such as **MyAddressOutput**, and add and configure the two output columns, **AddressID** and **City**.</span></span>

    > [!NOTE]
    >  <span data-ttu-id="84b15-198">務必將 **City** 輸出資料行的資料類型變更為 DT_WSTR。</span><span class="sxs-lookup"><span data-stu-id="84b15-198">Be sure to change the data type of the **City** output column to DT_WSTR.</span></span>

4.  <span data-ttu-id="84b15-199">在 [連線管理員]  頁面上，新增或建立 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員，並指定一個名稱，例如 **MyADONETConnection**。</span><span class="sxs-lookup"><span data-stu-id="84b15-199">On the **Connection Managers** page, add or create the [!INCLUDE[vstecado](../../includes/vstecado-md.md)] connection manager and give it a name such as **MyADONETConnection**.</span></span>

5.  <span data-ttu-id="84b15-200">在 [指令碼]  頁面上，按一下 [編輯指令碼]  ，並輸入以下指令碼。</span><span class="sxs-lookup"><span data-stu-id="84b15-200">On the **Script** page, click **Edit Script** and enter the script that follows.</span></span> <span data-ttu-id="84b15-201">然後關閉指令碼開發環境以及 [指令碼轉換編輯器]  。</span><span class="sxs-lookup"><span data-stu-id="84b15-201">Then close the script development environment and the **Script Transformation Editor**.</span></span>

6.  <span data-ttu-id="84b15-202">建立和設定目的地元件，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地，或是在[使用指令碼元件建立目的地](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)中所示範的範例目的地元件，它需要 **AddressID** 和 **City** 資料行。</span><span class="sxs-lookup"><span data-stu-id="84b15-202">Create and configure a destination component, such as a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destination, or the sample destination component demonstrated in [Creating a Destination with the Script Component](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md), that expects the **AddressID** and **City** columns.</span></span> <span data-ttu-id="84b15-203">然後將來源元件連接到目的地</span><span class="sxs-lookup"><span data-stu-id="84b15-203">Then connect the source component to the destination.</span></span> <span data-ttu-id="84b15-204"> (您可以直接將來源連接到目的地，而不需要任何轉換。 ) 您可以 [!INCLUDE[tsql](../../includes/tsql-md.md)] 在資料庫中執行下列命令來建立目的地資料表 `AdventureWorks` ：</span><span class="sxs-lookup"><span data-stu-id="84b15-204">(You can connect a source directly to a destination without any transformations.) You can create a destination table by running the following [!INCLUDE[tsql](../../includes/tsql-md.md)] command in the `AdventureWorks` database:</span></span>

    ```
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,
        [City] [nvarchar](30) NOT NULL)
    ```

7.  <span data-ttu-id="84b15-205">執行範例。</span><span class="sxs-lookup"><span data-stu-id="84b15-205">Run the sample.</span></span>

    ```vb
    Imports System.Data.SqlClient
    ...
    Public Class ScriptMain
        Inherits UserComponent

        Dim connMgr As IDTSConnectionManager100
        Dim sqlConn As SqlConnection
        Dim sqlReader As SqlDataReader

        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)

            connMgr = Me.Connections.MyADONETConnection
            sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)

        End Sub

        Public Overrides Sub PreExecute()

            Dim cmd As New SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn)
            sqlReader = cmd.ExecuteReader

        End Sub

        Public Overrides Sub CreateNewOutputRows()

            Do While sqlReader.Read
                With MyAddressOutputBuffer
                    .AddRow()
                    .AddressID = sqlReader.GetInt32(0)
                    .City = sqlReader.GetString(1)
                End With
            Loop

        End Sub

        Public Overrides Sub PostExecute()

            sqlReader.Close()

        End Sub

        Public Overrides Sub ReleaseConnections()

            connMgr.ReleaseConnection(sqlConn)

        End Sub

    End Class
    ```

    ```csharp
    using System.Data.SqlClient;
    public class ScriptMain:
        UserComponent

    {
        IDTSConnectionManager100 connMgr;
        SqlConnection sqlConn;
        SqlDataReader sqlReader;

        public override void AcquireConnections(object Transaction)
        {
            connMgr = this.Connections.MyADONETConnection;
            sqlConn = (SqlConnection)connMgr.AcquireConnection(null);

        }

        public override void PreExecute()
        {

            SqlCommand cmd = new SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn);
            sqlReader = cmd.ExecuteReader();

        }

        public override void CreateNewOutputRows()
        {

            while (sqlReader.Read())
            {
                {
                    MyAddressOutputBuffer.AddRow();
                    MyAddressOutputBuffer.AddressID = sqlReader.GetInt32(0);
                    MyAddressOutputBuffer.City = sqlReader.GetString(1);
                }
            }

        }

        public override void PostExecute()
        {

            sqlReader.Close();

        }

        public override void ReleaseConnections()
        {

            connMgr.ReleaseConnection(sqlConn);

        }

    }
    ```

### <a name="flat-file-source-example"></a><span data-ttu-id="84b15-206">一般檔案來源範例</span><span class="sxs-lookup"><span data-stu-id="84b15-206">Flat File Source Example</span></span>
 <span data-ttu-id="84b15-207">這個範例示範一個來源元件，它使用現有的一般檔案連接管理員，從一般檔案將資料載入資料流程。</span><span class="sxs-lookup"><span data-stu-id="84b15-207">This example demonstrates a source component that uses an existing Flat File connection manager to load data from a flat file into the data flow.</span></span> <span data-ttu-id="84b15-208">透過從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將它匯出，就會建立一般檔案來源資料。</span><span class="sxs-lookup"><span data-stu-id="84b15-208">The flat file source data is created by exporting it from [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span>

 <span data-ttu-id="84b15-209">如果您要執行這個範例程式碼，必須依下列方式設定封裝與元件：</span><span class="sxs-lookup"><span data-stu-id="84b15-209">If you want to run this sample code, you must configure the package and the component as follows:</span></span>

1.  <span data-ttu-id="84b15-210">使用 [匯 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 入和匯出嚮導]，將 [ **Person. Address** ] 資料表從 `AdventureWorks` 範例資料庫匯出至逗號分隔的一般檔案。</span><span class="sxs-lookup"><span data-stu-id="84b15-210">Use the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard to export the **Person.Address** table from the `AdventureWorks` sample database to a comma-delimited flat file.</span></span> <span data-ttu-id="84b15-211">這個範例使用的檔案名稱為 ExportedAddresses.txt。</span><span class="sxs-lookup"><span data-stu-id="84b15-211">This sample uses the file name ExportedAddresses.txt.</span></span>

2.  <span data-ttu-id="84b15-212">建立一般檔案連接管理員以連接至匯出的資料檔案。</span><span class="sxs-lookup"><span data-stu-id="84b15-212">Create a Flat File connection manager that connects to the exported data file.</span></span>

3.  <span data-ttu-id="84b15-213">將新指令碼元件加入資料流程設計師介面，並將它設定為來源。</span><span class="sxs-lookup"><span data-stu-id="84b15-213">Add a new Script component to the Data Flow designer surface and configure it as a source.</span></span>

4.  <span data-ttu-id="84b15-214">開啟**指令碼轉換編輯器**。</span><span class="sxs-lookup"><span data-stu-id="84b15-214">Open the **Script Transformation Editor**.</span></span> <span data-ttu-id="84b15-215">在 [輸入及輸出]  頁面上，以更具描述性的名稱重新命名預設輸出，例如 **MyAddressOutput**。</span><span class="sxs-lookup"><span data-stu-id="84b15-215">On the **Inputs and Outputs** page, rename the default output with a more descriptive name such as **MyAddressOutput**.</span></span> <span data-ttu-id="84b15-216">新增和設定兩個輸出資料行：**AddressID** 和 **City**。</span><span class="sxs-lookup"><span data-stu-id="84b15-216">Add and configure the two output columns, **AddressID** and **City**.</span></span>

5.  <span data-ttu-id="84b15-217">在 [連線管理員]  頁面上，使用更具描述性的名稱 (例如 **MyFlatFileSrcConnectionManager**) 以新增或建立一般檔案連線管理員。</span><span class="sxs-lookup"><span data-stu-id="84b15-217">On the **Connection Managers** page, add or create the Flat File connection manager, using a descriptive name such as **MyFlatFileSrcConnectionManager**.</span></span>

6.  <span data-ttu-id="84b15-218">在 [指令碼]  頁面上，按一下 [編輯指令碼]  ，並輸入以下指令碼。</span><span class="sxs-lookup"><span data-stu-id="84b15-218">On the **Script** page, click **Edit Script** and enter the script that follows.</span></span> <span data-ttu-id="84b15-219">然後關閉指令碼開發環境以及 [指令碼轉換編輯器]  。</span><span class="sxs-lookup"><span data-stu-id="84b15-219">Then close the script development environment and the **Script Transformation Editor**.</span></span>

7.  <span data-ttu-id="84b15-220">建立和設定目的地元件，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地，或是在[使用指令碼元件建立目的地](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)中所示範的範例目的地元件。</span><span class="sxs-lookup"><span data-stu-id="84b15-220">Create and configure a destination component, such as a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destination, or the sample destination component demonstrated in [Creating a Destination with the Script Component](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md).</span></span> <span data-ttu-id="84b15-221">然後將來源元件連接到目的地</span><span class="sxs-lookup"><span data-stu-id="84b15-221">Then connect the source component to the destination.</span></span> <span data-ttu-id="84b15-222"> (您可以直接將來源連接到目的地，而不需要任何轉換。 ) 您可以 [!INCLUDE[tsql](../../includes/tsql-md.md)] 在資料庫中執行下列命令來建立目的地資料表 `AdventureWorks` ：</span><span class="sxs-lookup"><span data-stu-id="84b15-222">(You can connect a source directly to a destination without any transformations.) You can create a destination table by running the following [!INCLUDE[tsql](../../includes/tsql-md.md)] command in the `AdventureWorks` database:</span></span>

    ```
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,
        [City] [nvarchar](30) NOT NULL)
    ```

8.  <span data-ttu-id="84b15-223">執行範例。</span><span class="sxs-lookup"><span data-stu-id="84b15-223">Run the sample.</span></span>

    ```vb
    Imports System.IO
    ...
    Public Class ScriptMain
        Inherits UserComponent

        Private textReader As StreamReader
        Private exportedAddressFile As String

        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)

            Dim connMgr As IDTSConnectionManager100 = _
                Me.Connections.MyFlatFileSrcConnectionManager
            exportedAddressFile = _
                CType(connMgr.AcquireConnection(Nothing), String)

        End Sub

        Public Overrides Sub PreExecute()
            MyBase.PreExecute()
            textReader = New StreamReader(exportedAddressFile)
        End Sub

        Public Overrides Sub CreateNewOutputRows()

            Dim nextLine As String
            Dim columns As String()

            Dim delimiters As Char()
            delimiters = ",".ToCharArray

            nextLine = textReader.ReadLine
            Do While nextLine IsNot Nothing
                columns = nextLine.Split(delimiters)
                With MyAddressOutputBuffer
                    .AddRow()
                    .AddressID = columns(0)
                    .City = columns(3)
                End With
                nextLine = textReader.ReadLine
            Loop

        End Sub

        Public Overrides Sub PostExecute()
            MyBase.PostExecute()
            textReader.Close()

        End Sub

    End Class
    ```

    ```csharp
    using System.IO;
    public class ScriptMain:
        UserComponent

    {
        private StreamReader textReader;
        private string exportedAddressFile;

        public override void AcquireConnections(object Transaction)
        {

            IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileSrcConnectionManager;
            exportedAddressFile = (string)connMgr.AcquireConnection(null);

        }

        public override void PreExecute()
        {
            base.PreExecute();
            textReader = new StreamReader(exportedAddressFile);
        }

        public override void CreateNewOutputRows()
        {

            string nextLine;
            string[] columns;

            char[] delimiters;
            delimiters = ",".ToCharArray();

            nextLine = textReader.ReadLine();
            while (nextLine != null)
            {
                columns = nextLine.Split(delimiters);
                {
                    MyAddressOutputBuffer.AddRow();
                    MyAddressOutputBuffer.AddressID = columns[0];
                    MyAddressOutputBuffer.City = columns[3];
                }
                nextLine = textReader.ReadLine();
            }

        }

        public override void PostExecute()
        {

            base.PostExecute();
            textReader.Close();

        }

    }
    ```

<span data-ttu-id="84b15-224">![Integration Services 圖示 (小型) ](../media/dts-16.gif "Integration Services 圖示 (小)")會**保持最**新狀態 Integration Services  </span><span class="sxs-lookup"><span data-stu-id="84b15-224">![Integration Services icon (small)](../media/dts-16.gif "Integration Services icon (small)")  **Stay Up to Date with Integration Services**</span></span><br /> <span data-ttu-id="84b15-225">若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：</span><span class="sxs-lookup"><span data-stu-id="84b15-225">For the latest downloads, articles, samples, and videos from Microsoft, as well as selected solutions from the community, visit the [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] page on MSDN:</span></span><br /><br /> [<span data-ttu-id="84b15-226">瀏覽 MSDN 上的 Integration Services 頁面</span><span class="sxs-lookup"><span data-stu-id="84b15-226">Visit the Integration Services page on MSDN</span></span>](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> <span data-ttu-id="84b15-227">若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。</span><span class="sxs-lookup"><span data-stu-id="84b15-227">For automatic notification of these updates, subscribe to the RSS feeds available on the page.</span></span>

## <a name="see-also"></a><span data-ttu-id="84b15-228">另請參閱</span><span class="sxs-lookup"><span data-stu-id="84b15-228">See Also</span></span>
 <span data-ttu-id="84b15-229">[使用腳本元件建立目的地以](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)[開發自訂來源元件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)</span><span class="sxs-lookup"><span data-stu-id="84b15-229">[Creating a Destination with the Script Component](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md) [Developing a Custom Source Component](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)</span></span>


