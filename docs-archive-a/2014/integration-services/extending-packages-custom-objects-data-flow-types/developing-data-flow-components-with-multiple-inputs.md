---
title: 開發具有多個輸入的資料流程元件 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 3c7b50e8-2aa6-4f6a-8db4-e8293bc21027
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fb56878c1b1b68dfdc4de19cb2b811de494c761b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705313"
---
# <a name="developing-data-flow-components-with-multiple-inputs"></a><span data-ttu-id="40c99-102">開發具有多個輸入的資料流程元件</span><span class="sxs-lookup"><span data-stu-id="40c99-102">Developing Data Flow Components with Multiple Inputs</span></span>
  <span data-ttu-id="40c99-103">如果具有多個輸入的資料流程元件其多個輸入會以不平均的速率產生資料，可能會耗用過多的記憶體。</span><span class="sxs-lookup"><span data-stu-id="40c99-103">A data flow component with multiple inputs may consume excessive memory if its multiple inputs produce data at uneven rates.</span></span> <span data-ttu-id="40c99-104">當您開發支援兩個或多個輸入的自訂資料流程元件時，可以使用 Microsoft.SqlServer.Dts.Pipeline 命名空間中的下列成員來管理記憶體壓力：</span><span class="sxs-lookup"><span data-stu-id="40c99-104">When you develop a custom data flow component that supports two or more inputs, you can manage this memory pressure by using the following members in the Microsoft.SqlServer.Dts.Pipeline namespace:</span></span>  
  
-   <span data-ttu-id="40c99-105"><xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 屬性。</span><span class="sxs-lookup"><span data-stu-id="40c99-105">The <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> property of the <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> class.</span></span> <span data-ttu-id="40c99-106">如果您想要實作為了讓自訂資料流程元件管理速率不平均之資料所需的程式碼，請將這個屬性的值設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="40c99-106">Set the value of this property to `true` if you want to implement the code that is necessary for your custom data flow component to manage data flowing at uneven rates.</span></span>  
  
-   <span data-ttu-id="40c99-107"><xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法。</span><span class="sxs-lookup"><span data-stu-id="40c99-107">The <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> method of the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> class.</span></span> <span data-ttu-id="40c99-108">如果您將 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 屬性設定為 `true`，就必須提供這個方法的實作。</span><span class="sxs-lookup"><span data-stu-id="40c99-108">You must provide an implementation of this method if you set the <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> property to `true`.</span></span> <span data-ttu-id="40c99-109">如果您沒有提供實作，資料流程引擎會在執行階段引發例外狀況。</span><span class="sxs-lookup"><span data-stu-id="40c99-109">If you do not provide an implementation, the data flow engine raises an exception at run time.</span></span>  
  
-   <span data-ttu-id="40c99-110"><xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法。</span><span class="sxs-lookup"><span data-stu-id="40c99-110">The <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> method of the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> class.</span></span> <span data-ttu-id="40c99-111">如果您將 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 屬性設定為 `true`，而且自訂元件支援超過兩個的輸入，您也必須提供這個方法的實作。</span><span class="sxs-lookup"><span data-stu-id="40c99-111">You must also provide an implementation of this method if you set the <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> property to `true` and your custom component supports more than two inputs.</span></span> <span data-ttu-id="40c99-112">如果您沒有提供實作，而且使用者附加超過兩個輸入，資料流程引擎會在執行階段引發例外狀況。</span><span class="sxs-lookup"><span data-stu-id="40c99-112">If you do not provide an implementation, the data flow engine raises an exception at run time if the user attaches more than two inputs.</span></span>  
  
 <span data-ttu-id="40c99-113">結合這些成員，即可讓您開發與 Microsoft 所開發之「合併」和「合併聯結」轉換方案類似的記憶體壓力方案。</span><span class="sxs-lookup"><span data-stu-id="40c99-113">Together, these members enable you to develop a solution for memory pressure that is similar to the solution that Microsoft developed for the Merge and Merge Join transformations.</span></span>  
  
## <a name="setting-the-supportsbackpressure-property"></a><span data-ttu-id="40c99-114">設定 SupportsBackPressure 屬性</span><span class="sxs-lookup"><span data-stu-id="40c99-114">Setting the SupportsBackPressure Property</span></span>  
 <span data-ttu-id="40c99-115">針對自訂支援多個輸入之資料流程元件實作更好的記憶體管理中的第一個步驟，就是在 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 中將 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 屬性的值設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="40c99-115">The first step in implementing better memory management for a custom data flow component that supports multiple inputs is to set the value of the <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> property to `true` in the <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>.</span></span> <span data-ttu-id="40c99-116">當 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 的值為 `true` 時，資料流程引擎會呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法，具有超過兩個輸入時，也會在執行階段呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="40c99-116">When the value of <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> is `true`, the data flow engine calls the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> method and, when there are more than two inputs, also calls the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> method at run time.</span></span>  
  
### <a name="example"></a><span data-ttu-id="40c99-117">範例</span><span class="sxs-lookup"><span data-stu-id="40c99-117">Example</span></span>  
 <span data-ttu-id="40c99-118">在下列範例中，<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 的實作會將 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 的值設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="40c99-118">In the following example, the implementation of the <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> sets the value of <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> to `true`.</span></span>  
  
```csharp  
[DtsPipelineComponent(ComponentType = ComponentType.Transform,  
        DisplayName = "Shuffler",  
        Description = "Shuffle the rows from input.",  
        SupportsBackPressure = true,  
        LocalizationType = typeof(Localized),  
        IconResource = "Microsoft.Samples.SqlServer.Dts.MIBPComponent.ico")  
]  
public class Shuffler : Microsoft.SqlServer.Dts.Pipeline.PipelineComponent  
        {  
          ...  
        }  
```  
  
## <a name="implementing-the-isinputready-method"></a><span data-ttu-id="40c99-119">實作 IsInputReady 方法</span><span class="sxs-lookup"><span data-stu-id="40c99-119">Implementing the IsInputReady Method</span></span>  
 <span data-ttu-id="40c99-120">當您在 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 物件中將 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 屬性的值設定為 `true` 時，就必須提供 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 類別之 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法的實作。</span><span class="sxs-lookup"><span data-stu-id="40c99-120">When you set the value of the <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> property to `true` in the <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> object, you must also provide an implementation for the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> method of the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> class.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="40c99-121">您的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法實作不應該呼叫基底類別中實作。</span><span class="sxs-lookup"><span data-stu-id="40c99-121">Your implementation of the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> method should not call the implementations in the base class.</span></span> <span data-ttu-id="40c99-122">在基底類別中，這個方法的預設實作只會引發 `NotImplementedException`。</span><span class="sxs-lookup"><span data-stu-id="40c99-122">The default implementation of this method in the base class simply raises a `NotImplementedException`.</span></span>  
  
 <span data-ttu-id="40c99-123">實作這個方法時，您會針對每個元件的輸入設定布林值 *canProcess* 陣列中的元素狀態</span><span class="sxs-lookup"><span data-stu-id="40c99-123">When you implement this method, you set the status of an element in the Boolean *canProcess* array for each of the component's inputs.</span></span> <span data-ttu-id="40c99-124"> (輸入是由其在*i*陣列中的識別碼值所識別。 ) 當您將*canProcess*陣列中的元素值設定為時 `true` ，資料流程引擎會呼叫元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法，並為指定的輸入提供更多資料。</span><span class="sxs-lookup"><span data-stu-id="40c99-124">(The inputs are identified by their ID values in the *inputIDs* array.) When you set the value of an element in the *canProcess* array to `true` for an input, the data flow engine calls the component's <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> method and provides more data for the specified input.</span></span>  
  
 <span data-ttu-id="40c99-125">當有更多上游資料可用時，至少一個輸入的*canProcess*陣列元素值必須一律為 `true` ，否則處理就會停止。</span><span class="sxs-lookup"><span data-stu-id="40c99-125">While more upstream data is available, the value of the *canProcess* array element for at least one input must always be `true`, or processing stops.</span></span>  
  
 <span data-ttu-id="40c99-126">資料流程引擎會在傳送資料的每個緩衝區之前，呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法，以判斷哪一個輸入正在等候接收更多資料。</span><span class="sxs-lookup"><span data-stu-id="40c99-126">The data flow engine calls the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> method before sending each buffer of data to determine which inputs are waiting to receive more data.</span></span> <span data-ttu-id="40c99-127">當傳回值表示輸入遭到封鎖時，資料流程引擎就會為該輸入暫時快取資料的其他緩衝區，而不會將它們傳送到元件。</span><span class="sxs-lookup"><span data-stu-id="40c99-127">When the return value indicates that an input is blocked, the data flow engine temporarily caches additional buffers of data for that input instead of sending them to the component.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="40c99-128">您不用在自己的程式碼中呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 或 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="40c99-128">You do not call the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> or <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> methods in your own code.</span></span> <span data-ttu-id="40c99-129">資料流程引擎執行您的元件時，資料流程引擎會呼叫這些方法以及您所覆寫之 `PipelineComponent` 類別的其他方法。</span><span class="sxs-lookup"><span data-stu-id="40c99-129">The data flow engine calls these methods, and the other methods of the `PipelineComponent` class that you override, when the data flow engine runs your component.</span></span>  
  
### <a name="example"></a><span data-ttu-id="40c99-130">範例</span><span class="sxs-lookup"><span data-stu-id="40c99-130">Example</span></span>  
 <span data-ttu-id="40c99-131">在下列的範例中，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法的實作指出當下列條件成立時，輸入會等候接收更多資料：</span><span class="sxs-lookup"><span data-stu-id="40c99-131">In the following example, the implementation of the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> method indicates that an input is waiting to receive more data when the following conditions are true:</span></span>  
  
-   <span data-ttu-id="40c99-132">有更多的上游資料可供輸入使用 (`!inputEOR`)。</span><span class="sxs-lookup"><span data-stu-id="40c99-132">More upstream data is available for the input (`!inputEOR`).</span></span>  
  
-   <span data-ttu-id="40c99-133">元件目前沒有可用來處理元件已接收之緩衝區中的資料 (`inputBuffers[inputIndex].CurrentRow() == null`)。</span><span class="sxs-lookup"><span data-stu-id="40c99-133">The component does not currently have data available to process for the input in the buffers that the component has already received (`inputBuffers[inputIndex].CurrentRow() == null`).</span></span>  
  
 <span data-ttu-id="40c99-134">如果輸入正在等候接收更多資料，資料流程元件會將設定為 `true` 對應至該輸入之*canProcess*陣列中的專案值，以指出這種情況。</span><span class="sxs-lookup"><span data-stu-id="40c99-134">If an input is waiting to receive more data, the data flow component indicates this by setting to `true` the value of the element in the *canProcess* array that corresponds to that input.</span></span>  
  
 <span data-ttu-id="40c99-135">相反地，當元件仍有可用於處理輸入的資料時，這個範例會暫停處理輸入。</span><span class="sxs-lookup"><span data-stu-id="40c99-135">Conversely, when the component still has data available to process for the input, the example suspends the processing of the input.</span></span> <span data-ttu-id="40c99-136">這個範例會將設定為 `false` 對應至該輸入之*canProcess*陣列中的專案值，藉此執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="40c99-136">The example does this by setting to `false` the value of the element in the *canProcess* array that corresponds to that input.</span></span>  
  
```csharp  
public override void IsInputReady(int[] inputIDs, ref bool[] canProcess)  
{  
    for (int i = 0; i < inputIDs.Length; i++)  
    {  
        int inputIndex = ComponentMetaData.InputCollection.GetObjectIndexByID(inputIDs[i]);  
  
        canProcess[i] = (inputBuffers[inputIndex].CurrentRow() == null)  
            && !inputEOR[inputIndex];  
    }  
}  
```  
  
 <span data-ttu-id="40c99-137">前面的範例會使用布林 (Boolean) `inputEOR` 陣列來指出是否有更多的上游資料可供每個輸入使用。</span><span class="sxs-lookup"><span data-stu-id="40c99-137">The preceding example uses the Boolean `inputEOR` array to indicate whether more upstream data is available for each input.</span></span> <span data-ttu-id="40c99-138">陣列名稱中的 `EOR` 代表「資料列集結束」，也會參考資料流程緩衝區的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="40c99-138">`EOR` in the name of the array represents "end of rowset" and refers to the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> property of data flow buffers.</span></span> <span data-ttu-id="40c99-139">在這裡未包含的範例部分中，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法會檢查它所接收資料的每個緩衝區之 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 屬性值。</span><span class="sxs-lookup"><span data-stu-id="40c99-139">In a portion of the example that is not included here, the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> method checks the value of the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> property for each buffer of data that it receives.</span></span> <span data-ttu-id="40c99-140">當 `true` 的值表示沒有其他上游資料可供輸入使用時，範例會將該輸入的 `inputEOR` 陣列元素設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="40c99-140">When a value of `true` indicates that there is no more upstream data available for an input, the example sets the value of the `inputEOR` array element for that input to `true`.</span></span> <span data-ttu-id="40c99-141">此方法的範例 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> *canProcess* `false` `inputEOR` 會在 array 元素的值指出沒有其他上游資料可供輸入使用時，將 canProcess 陣列中對應元素的值設定為。</span><span class="sxs-lookup"><span data-stu-id="40c99-141">This example of the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> method sets the value of the corresponding element in the *canProcess* array to `false` for an input when the value of the `inputEOR` array element indicates that there is no more upstream data available for the input.</span></span>  
  
## <a name="implementing-the-getdependentinputs-method"></a><span data-ttu-id="40c99-142">實作 GetDependentInputs 方法</span><span class="sxs-lookup"><span data-stu-id="40c99-142">Implementing the GetDependentInputs Method</span></span>  
 <span data-ttu-id="40c99-143">當您的自訂資料元件支援超過兩個輸入時，您也必須針對 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法提供實作。</span><span class="sxs-lookup"><span data-stu-id="40c99-143">When your custom data flow component supports more than two inputs, you must also provide an implementation for the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> method of the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> class.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="40c99-144">您的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法實作不應該呼叫基底類別中實作。</span><span class="sxs-lookup"><span data-stu-id="40c99-144">Your implementation of the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> method should not call the implementations in the base class.</span></span> <span data-ttu-id="40c99-145">在基底類別中，這個方法的預設實作只會引發 `NotImplementedException`。</span><span class="sxs-lookup"><span data-stu-id="40c99-145">The default implementation of this method in the base class simply raises a `NotImplementedException`.</span></span>  
  
 <span data-ttu-id="40c99-146">資料流程引擎只會在使用者將超過兩個輸入附加至元件時呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="40c99-146">The data flow engine only calls the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> method when the user attaches more than two inputs to the component.</span></span> <span data-ttu-id="40c99-147">當元件只有兩個輸入，而且 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法指出其中一個輸入遭到封鎖 (*canProcess*  =  `false`) 時，資料流程引擎就會知道另一個輸入正在等候接收更多資料。</span><span class="sxs-lookup"><span data-stu-id="40c99-147">When a component has only two inputs, and the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> method indicates that one input is blocked (*canProcess* = `false`), the data flow engine knows that the other input is waiting to receive more data.</span></span> <span data-ttu-id="40c99-148">但是，具有超過兩個輸入，而且 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法指出其中一個輸入遭到封鎖時，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 中額外的程式碼就會識別哪一個輸入正在等候接收更多資料。</span><span class="sxs-lookup"><span data-stu-id="40c99-148">However, when there are more than two inputs, and the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> method indicates that one input is blocked, the additional code in the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> identifies which inputs are waiting to receive more data.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="40c99-149">您不用在自己的程式碼中呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 或 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="40c99-149">You do not call the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> or <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> methods in your own code.</span></span> <span data-ttu-id="40c99-150">資料流程引擎執行您的元件時，資料流程引擎會呼叫這些方法以及您所覆寫之 `PipelineComponent` 類別的其他方法。</span><span class="sxs-lookup"><span data-stu-id="40c99-150">The data flow engine calls these methods, and the other methods of the `PipelineComponent` class that you override, when the data flow engine runs your component.</span></span>  
  
### <a name="example"></a><span data-ttu-id="40c99-151">範例</span><span class="sxs-lookup"><span data-stu-id="40c99-151">Example</span></span>  
 <span data-ttu-id="40c99-152">針對遭到封鎖的特定輸入，下列 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法的實作會傳回正在等候接收更多資料之輸入的集合，進而封鎖指定的輸入。</span><span class="sxs-lookup"><span data-stu-id="40c99-152">For a specific input that is blocked, the following implementation of the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> method returns a collection of the inputs that are waiting to receive more data, and are therefore blocking the specified input.</span></span> <span data-ttu-id="40c99-153">元件會檢查除了已封鎖輸入之外，目前在元件已接收緩衝區中，哪些輸入沒有可供處理的資料，以識別正在封鎖的輸入 (`inputBuffers[i].CurrentRow() == null`)。</span><span class="sxs-lookup"><span data-stu-id="40c99-153">The component identifies the blocking inputs by checking for inputs other than the blocked input that do not currently have data available to process in the buffers that the component has already received (`inputBuffers[i].CurrentRow() == null`).</span></span> <span data-ttu-id="40c99-154">然後，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法會以輸入識別碼集合的方式傳回正在封鎖的輸入集合。</span><span class="sxs-lookup"><span data-stu-id="40c99-154">The <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> method then returns the collection of blocking inputs as a collection of input IDs.</span></span>  
  
```csharp  
public override Collection<int> GetDependentInputs(int blockedInputID)  
{  
    Collection<int> currentDependencies = new Collection<int>();  
    for (int i = 0; i < ComponentMetaData.InputCollection.Count; i++)  
    {  
        if (ComponentMetaData.InputCollection[i].ID != blockedInputID  
            && inputBuffers[i].CurrentRow() == null)  
        {  
            currentDependencies.Add(ComponentMetaData.InputCollection[i].ID);  
        }  
    }  
  
    return currentDependencies;  
}  
```  
  
  
