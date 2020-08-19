---
title: " (資料採礦) 的預測查詢 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e5e6686c-1360-480e-8c0d-8a56204fbed9
author: minewiskan
ms.author: owend
ms.openlocfilehash: 543055aaed5d8991ed2c913a6ae46575c774e216
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87703453"
---
# <a name="prediction-queries-data-mining"></a><span data-ttu-id="f7190-102">預測查詢 (資料採礦)</span><span class="sxs-lookup"><span data-stu-id="f7190-102">Prediction Queries (Data Mining)</span></span>
  <span data-ttu-id="f7190-103">典型資料採礦專案的目標是要使用採礦模型來進行預測。</span><span class="sxs-lookup"><span data-stu-id="f7190-103">The goal of a typical data mining project is to use the mining model to make predictions.</span></span> <span data-ttu-id="f7190-104">例如，您可以預測特定伺服器叢集的預期停機時間，或產生分數以指出特定客戶是否可能回應廣告宣傳活動。</span><span class="sxs-lookup"><span data-stu-id="f7190-104">For example, you might want to predict the amount of expected downtime for a certain cluster of servers, or generate a score that indicates whether segments of customers are likely to respond to an advertising campaign.</span></span> <span data-ttu-id="f7190-105">若要執行所有這些作業，您需要建立預測查詢。</span><span class="sxs-lookup"><span data-stu-id="f7190-105">To do all these things, you would create a prediction query.</span></span>  
  
 <span data-ttu-id="f7190-106">就功能而言，SQL Server 中支援不同類型的預測查詢 (視查詢的輸入類型而定)：</span><span class="sxs-lookup"><span data-stu-id="f7190-106">Functionally, there are different types of prediction queries supported in SQL Server, depending on the type of inputs to the query:</span></span>  
  
|<span data-ttu-id="f7190-107">查詢類型</span><span class="sxs-lookup"><span data-stu-id="f7190-107">Query Type</span></span>|<span data-ttu-id="f7190-108">查詢選項</span><span class="sxs-lookup"><span data-stu-id="f7190-108">Query Options</span></span>|  
|----------------|-------------------|  
|<span data-ttu-id="f7190-109">單一預測查詢</span><span class="sxs-lookup"><span data-stu-id="f7190-109">Singleton prediction queries</span></span>|<span data-ttu-id="f7190-110">當您想要預測單一新案例或多個新案例的結果時，請使用單一查詢。</span><span class="sxs-lookup"><span data-stu-id="f7190-110">Use a singleton query when you want to predict outcomes for a single new case, or multiple new cases.</span></span> <span data-ttu-id="f7190-111">您可直接在查詢中提供輸入值，而查詢會當做單一工作階段執行。</span><span class="sxs-lookup"><span data-stu-id="f7190-111">You provide the input values directly in the query, and the query is executed as a single session.</span></span>|  
|<span data-ttu-id="f7190-112">批次預測</span><span class="sxs-lookup"><span data-stu-id="f7190-112">Batch predictions</span></span>|<span data-ttu-id="f7190-113">當您擁有想要送入模型中的外部資料時，請使用批次預測當做預測基礎。</span><span class="sxs-lookup"><span data-stu-id="f7190-113">Use batch predictions when you have external data that you want to feed into the model, to use as the basis for predictions.</span></span> <span data-ttu-id="f7190-114">若要對整組資料做出預測，您會將外部來源中的資料對應到模型中的資料行，然後指定您想要輸出的預測資料類型。</span><span class="sxs-lookup"><span data-stu-id="f7190-114">To make predictions for an entire set of data, you map the data in the external source to the columns in the model, and then specify the type of predictive data you want to output.</span></span><br /><br /> <span data-ttu-id="f7190-115">對整個資料集的查詢會在單一工作階段中執行，讓這個選項比傳送多個重複查詢更有效率。</span><span class="sxs-lookup"><span data-stu-id="f7190-115">The query for the entire dataset is executed in a single session, making this option much more efficient than sending multiple repeated queries.</span></span>|  
|<span data-ttu-id="f7190-116">時間序列預測</span><span class="sxs-lookup"><span data-stu-id="f7190-116">Time Series predictions</span></span>|<span data-ttu-id="f7190-117">當您想要預測某個未來步驟數的值時，請使用時間序列查詢。</span><span class="sxs-lookup"><span data-stu-id="f7190-117">Use a time series query when you want to predict a value over some number of future steps.</span></span> <span data-ttu-id="f7190-118">SQL Server 資料採礦會在時間序列查詢中提供以下功能：</span><span class="sxs-lookup"><span data-stu-id="f7190-118">SQL Server Data Mining also provides the following functionality in time series queries:</span></span><br /><br /> <span data-ttu-id="f7190-119">您可以加入新的資料當做查詢的一部分來擴充現有的模型，然後根據複合數列做出預測。</span><span class="sxs-lookup"><span data-stu-id="f7190-119">You can extend an existing model by adding new data as part of the query, and make predictions based on the composite series.</span></span><br /><br /> <span data-ttu-id="f7190-120">您可以使用 REPLACE_MODEL_CASES 選項將現有的模型套用至新的資料數列。</span><span class="sxs-lookup"><span data-stu-id="f7190-120">You can apply an existing model to a new data series by using the REPLACE_MODEL_CASES option.</span></span><br /><br /> <span data-ttu-id="f7190-121">您可以執行交叉預測。</span><span class="sxs-lookup"><span data-stu-id="f7190-121">You can perform cross-prediction.</span></span>|  
  
 <span data-ttu-id="f7190-122">下列各節描述預測查詢的一般語法、不同預測查詢類型，以及如何使用預測查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="f7190-122">The following sections describe the general syntax of prediction queries, the different types of prediction queries, and how to work with the results of prediction queries.</span></span>  
  
 [<span data-ttu-id="f7190-123">基本預測查詢設計</span><span class="sxs-lookup"><span data-stu-id="f7190-123">Basic Prediction Query Design</span></span>](#bkmk_PredQuery)  
  
-   [<span data-ttu-id="f7190-124">加入預測函數</span><span class="sxs-lookup"><span data-stu-id="f7190-124">Adding Prediction Functions</span></span>](#bkmk_PredFunc)  
  
-   [<span data-ttu-id="f7190-125">單一查詢</span><span class="sxs-lookup"><span data-stu-id="f7190-125">Singleton Queries</span></span>](#bkmk_SingletonQuery)  
  
-   [<span data-ttu-id="f7190-126">批次預測查詢</span><span class="sxs-lookup"><span data-stu-id="f7190-126">Batch Prediction Queries</span></span>](#bkmk_BatchQuery)  
  
 [<span data-ttu-id="f7190-127">使用查詢的結果</span><span class="sxs-lookup"><span data-stu-id="f7190-127">Working with the Results of Queries</span></span>](#bkmk_WorkResults)  
  
##  <a name="basic-prediction-query-design"></a><a name="bkmk_PredQuery"></a> <span data-ttu-id="f7190-128">基本預測查詢設計</span><span class="sxs-lookup"><span data-stu-id="f7190-128">Basic Prediction Query Design</span></span>  
 <span data-ttu-id="f7190-129">當您建立預測時，通常要提供一些新資料並要求模型根據新的資料產生預測。</span><span class="sxs-lookup"><span data-stu-id="f7190-129">When you create a prediction, you typically provide some piece of new data and ask the model to generate a prediction based on the new data.</span></span>  
  
-   <span data-ttu-id="f7190-130">在批次預測查詢中，您會使用 *「預測聯結」*(Prediction Join) 將模型對應至外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="f7190-130">In a batch prediction query, you map the model to an external source of data by using a *prediction join*.</span></span>  
  
-   <span data-ttu-id="f7190-131">在單一預測查詢中，您會輸入一個或多個值當做輸入。</span><span class="sxs-lookup"><span data-stu-id="f7190-131">In a singleton prediction query, you type one or more values to use as inputs.</span></span> <span data-ttu-id="f7190-132">您可以使用單一預測查詢來建立多個預測。</span><span class="sxs-lookup"><span data-stu-id="f7190-132">You can create multiple predictions using a singleton prediction query.</span></span> <span data-ttu-id="f7190-133">但是，如果您需要建立多個預測，當您使用批次查詢時的效能會更好。</span><span class="sxs-lookup"><span data-stu-id="f7190-133">However, if you need to create many predictions, performance is better when you use a batch query.</span></span>  
  
 <span data-ttu-id="f7190-134">單一查詢和批次預測查詢皆使用 PREDICTION JOIN 語法定義新資料。</span><span class="sxs-lookup"><span data-stu-id="f7190-134">Both singleton and batch prediction queries use the PREDICTION JOIN syntax to define the new data.</span></span> <span data-ttu-id="f7190-135">不同之處在於預測聯結之輸入端的指定方式。</span><span class="sxs-lookup"><span data-stu-id="f7190-135">The difference is in how the input side of the prediction join is specified.</span></span>  
  
-   <span data-ttu-id="f7190-136">在批次預測查詢中，資料來自使用 OPENQUERY 語法指定的外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="f7190-136">In a batch prediction query, the data comes from an external data source that is specified by using the OPENQUERY syntax.</span></span>  
  
-   <span data-ttu-id="f7190-137">在單一預測查詢中，資料會以內嵌方式當做查詢的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="f7190-137">In a singleton prediction query, the data is supplied inline as part of the query.</span></span>  
  
 <span data-ttu-id="f7190-138">對於時間序列模型而言，不一定需要輸入資料；您可以只使用模型中的現有資料做出預測。</span><span class="sxs-lookup"><span data-stu-id="f7190-138">For time series models, input data is not always required; it is possible to make predictions using just the data already in the model.</span></span> <span data-ttu-id="f7190-139">但是，如果您指定新的輸入資料，必須決定要使用新資料來更新及擴充模型，還是要取代原本在模型中使用的原始資料數列。</span><span class="sxs-lookup"><span data-stu-id="f7190-139">However, if you do specify new input data, you must decide whether you will use the new data to update and extend the model, or to replace the original series of data that was used in the model.</span></span>  <span data-ttu-id="f7190-140">如需這些選項的詳細資訊，請參閱 [Time Series Model Query Examples](time-series-model-query-examples.md)。</span><span class="sxs-lookup"><span data-stu-id="f7190-140">For more information about these options, see [Time Series Model Query Examples](time-series-model-query-examples.md).</span></span>  
  
###  <a name="adding-prediction-functions"></a><a name="bkmk_PredFunc"></a><span data-ttu-id="f7190-141">加入預測函數</span><span class="sxs-lookup"><span data-stu-id="f7190-141">Adding Prediction Functions</span></span>  
 <span data-ttu-id="f7190-142">除了預測值之外，您也可以自訂預測查詢以傳回與預測相關的各種資訊類型。</span><span class="sxs-lookup"><span data-stu-id="f7190-142">In addition to predicting a value, you can customize a prediction query to return various kinds of information that are related to the prediction.</span></span> <span data-ttu-id="f7190-143">例如，如果預測建立一份建議客戶購買的產品清單，您可能也想傳回每個預測的機率，以進行排名，並只向使用者呈現熱門建議。</span><span class="sxs-lookup"><span data-stu-id="f7190-143">For example, if the prediction creates a list of products to recommend to a customer, you might also want to return the probability for each prediction, so that you can rank them and present only the top recommendations to the user.</span></span>  
  
 <span data-ttu-id="f7190-144">若要這樣做，您需要將 *「預測函數」* (Prediction Function) 加入至查詢。</span><span class="sxs-lookup"><span data-stu-id="f7190-144">To do this, you add *prediction functions* to the query.</span></span> <span data-ttu-id="f7190-145">每個模型或查詢類型都支援特定的函數。</span><span class="sxs-lookup"><span data-stu-id="f7190-145">Each model or query type supports specific functions.</span></span> <span data-ttu-id="f7190-146">例如，叢集模型支援特殊的預測函數，可針對模型建立的叢集提供額外的詳細資料，而時間序列模型則含有可計算一段時間之差異的函數。</span><span class="sxs-lookup"><span data-stu-id="f7190-146">For example, clustering models support special prediction functions that provide extra detail about the clusters created by the model, whereas time series models have functions that calculate differences over time.</span></span> <span data-ttu-id="f7190-147">也有可用於幾乎所有模型類型的一般預測函數。</span><span class="sxs-lookup"><span data-stu-id="f7190-147">There are also general prediction functions that work with almost all model types.</span></span> <span data-ttu-id="f7190-148">如需不同查詢類型所支援的預測函數清單，請參閱本 DMX 參考主題：[一般預測函數 &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx)。</span><span class="sxs-lookup"><span data-stu-id="f7190-148">For a list of the prediction functions supported in different types of queries, see this topic the DMX reference:  [General Prediction Functions &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx).</span></span>  
  
###  <a name="creating-singleton-prediction-queries"></a><a name="bkmk_SingletonQuery"></a><span data-ttu-id="f7190-149">建立單一預測查詢</span><span class="sxs-lookup"><span data-stu-id="f7190-149">Creating Singleton Prediction Queries</span></span>  
 <span data-ttu-id="f7190-150">當您想要即時建立快速預測時，單一預測查詢便很有用。</span><span class="sxs-lookup"><span data-stu-id="f7190-150">A singleton prediction query is useful when you want to create quick predictions in real time.</span></span> <span data-ttu-id="f7190-151">常見的案例可能是您已經向客戶取得資訊 (或許是使用網站上的表單)，而且您想要以單一預測查詢的輸入形式提交該資料。</span><span class="sxs-lookup"><span data-stu-id="f7190-151">A common scenario might be that you have obtained information from a customer, perhaps by using a form on a Web site, and you want to submit that data as the input to a singleton prediction query.</span></span> <span data-ttu-id="f7190-152">例如，當客戶從清單中選擇產品時，您可以使用選取內容當做預測最佳建議產品的查詢輸入。</span><span class="sxs-lookup"><span data-stu-id="f7190-152">For example, when a customer chooses a product from a list, you could use that selection as the input to a query that predicts the best products to recommend.</span></span>  
  
 <span data-ttu-id="f7190-153">單一預測查詢不需要包含輸入的個別資料表。</span><span class="sxs-lookup"><span data-stu-id="f7190-153">Singleton prediction queries do not require a separate table that contains input.</span></span> <span data-ttu-id="f7190-154">相反地，您會提供一個或多個資料列值做為模型的輸入，然後再即時傳回一個或多個預測。</span><span class="sxs-lookup"><span data-stu-id="f7190-154">Instead, you provide one or multiple rows of values as input to the model, and the prediction or predictions are returned in real time.</span></span>  
  
> [!WARNING]  
>  <span data-ttu-id="f7190-155">儘管名稱，單一預測查詢不只會進行單一預測，您可以針對每一組輸入產生多個預測。</span><span class="sxs-lookup"><span data-stu-id="f7190-155">Despite the name, singleton prediction queries do not just make single predictions-you can generate multiple predictions for each set of inputs.</span></span> <span data-ttu-id="f7190-156">若要提供多個輸入案例，您會針對每一個輸入案例建立 SELECT 陳述式，並將其與 UNION 運算子結合。</span><span class="sxs-lookup"><span data-stu-id="f7190-156">You provide multiple input cases by creating a SELECT statement for each input case and combining them with the UNION operator.</span></span>  
  
 <span data-ttu-id="f7190-157">當您建立單一預測查詢時，必須以 PREDICTION JOIN 的形式為模型提供新資料。</span><span class="sxs-lookup"><span data-stu-id="f7190-157">When you create a singleton prediction query, you must provide the new data to the model in the form of a PREDICTION JOIN.</span></span> <span data-ttu-id="f7190-158">這表示即使不是對應至實際的資料表，也必須確定新資料符合採礦模型中現有的資料行。</span><span class="sxs-lookup"><span data-stu-id="f7190-158">This means that even though you are not mapping to an actual table, you must make sure that the new data matches the existing columns in the mining model.</span></span> <span data-ttu-id="f7190-159">如果新資料行和新資料完全相符，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會為您對應資料行。</span><span class="sxs-lookup"><span data-stu-id="f7190-159">If the new data columns and the new data match exactly, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] will map the columns for you.</span></span> <span data-ttu-id="f7190-160">這稱為 *NATURAL PREDICTION JOIN*。</span><span class="sxs-lookup"><span data-stu-id="f7190-160">This is called a *NATURAL PREDICTION JOIN*.</span></span> <span data-ttu-id="f7190-161">不過，如果資料行不相符，或者新資料所包含的資料類型和數量與模型中的不同，您必須指定模型中與新資料對應的資料行，或指定遺漏的值。</span><span class="sxs-lookup"><span data-stu-id="f7190-161">However, if the columns do not match, or if the new data does not contain the same kind and amount of data that is in the model, you must specify which columns in the model map to the new data, or specify the missing values.</span></span>  
  
###  <a name="batch-prediction-queries"></a><a name="bkmk_BatchQuery"></a> <span data-ttu-id="f7190-162">批次預測查詢</span><span class="sxs-lookup"><span data-stu-id="f7190-162">Batch Prediction Queries</span></span>  
 <span data-ttu-id="f7190-163">如果您有外部資料想要用來做預測，批次預測查詢便很有用。</span><span class="sxs-lookup"><span data-stu-id="f7190-163">A batch prediction query is useful when you have external data that you want to use in making predictions.</span></span> <span data-ttu-id="f7190-164">例如，您可能已經建立一個模型，此模型會根據客戶的線上活動和購買歷史記錄來為客戶分類。</span><span class="sxs-lookup"><span data-stu-id="f7190-164">For example, you might have built a model that categorizes customers by their online activity and purchasing history.</span></span> <span data-ttu-id="f7190-165">您可將該模型套用到最新取得的潛在客戶清單，以便建立銷售預測或是辨識建議促銷活動的目標客群。</span><span class="sxs-lookup"><span data-stu-id="f7190-165">You could apply that model to a list of newly acquired leads, to create projections for sales, or to identify targets for proposed campaigns.</span></span>  
  
 <span data-ttu-id="f7190-166">當您執行預測聯結時，必須將模型中的資料行對應到新資料來源中的資料行。</span><span class="sxs-lookup"><span data-stu-id="f7190-166">When you perform a prediction join, you must map the columns the model to the columns in the new data source.</span></span> <span data-ttu-id="f7190-167">因此，您選擇當做輸入的資料來源必須包含與模型中資料類似的內容。</span><span class="sxs-lookup"><span data-stu-id="f7190-167">Therefore, the data source that you choose for an input must data that is somewhat similar to the data in the model.</span></span> <span data-ttu-id="f7190-168">新資訊不必完全相符，也可以不完整。</span><span class="sxs-lookup"><span data-stu-id="f7190-168">The new information does not have to match exactly, and can be incomplete.</span></span> <span data-ttu-id="f7190-169">例如，假設使用收入和年齡資訊來定型模型，但是用於預測的客戶清單有年齡資訊，卻沒有與收入有關的任何資訊。</span><span class="sxs-lookup"><span data-stu-id="f7190-169">For example, suppose the model was trained using information about income and age, but the customer list you are using for predictions has age but nothing about income.</span></span> <span data-ttu-id="f7190-170">在此情況下，您仍可以將新資料對應至模型，並可為每個客戶建立預測。</span><span class="sxs-lookup"><span data-stu-id="f7190-170">In this scenario, you could still map the new data to the model and create a prediction for each customer.</span></span> <span data-ttu-id="f7190-171">但是，如果收入是模型的重要預測因數，則資訊不完整會影響預測的品質。</span><span class="sxs-lookup"><span data-stu-id="f7190-171">However, if income was an important predictor for the model, the lack of complete information would affect the quality of predictions.</span></span>  
  
 <span data-ttu-id="f7190-172">若要取得最佳結果，應該在新資料和模型之間盡可能聯結相符的資料行。</span><span class="sxs-lookup"><span data-stu-id="f7190-172">To get the best results, you should join as many of the matching columns as possible between the new data and the model.</span></span> <span data-ttu-id="f7190-173">不過，即使沒有相符的項目，查詢也會成功。</span><span class="sxs-lookup"><span data-stu-id="f7190-173">However, the query will succeed even if there are no matches.</span></span> <span data-ttu-id="f7190-174">如果沒有聯結任何資料行，則查詢會傳回臨界預測，該預測相當於不具有 PREDICTION JOIN 子句的陳述式 `SELECT <predictable-column> FROM <model>` 。</span><span class="sxs-lookup"><span data-stu-id="f7190-174">If no columns are joined, the query will return the marginal prediction, which is equivalent to the statement `SELECT <predictable-column> FROM <model>` without a PREDICTION JOIN clause.</span></span>  
  
 <span data-ttu-id="f7190-175">當您成功對應所有相關的資料行之後，您會執行查詢，而且 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會根據模型內的模式來針對新資料中的每一個資料列做出預測。</span><span class="sxs-lookup"><span data-stu-id="f7190-175">After you have successfully mapped all relevant columns, you run the query, and [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] makes predictions for each row in the new data based on patterns in the model.</span></span> <span data-ttu-id="f7190-176">您可以將結果儲存回資料來源檢視中包含外部資料的新資料表，或者可以複製和貼上資料 (如果您使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)])。</span><span class="sxs-lookup"><span data-stu-id="f7190-176">You can save the results back to a new table in the data source view that contains the external data, or you can copy and paste the data is you are using [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] or [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].</span></span>  
  
> [!WARNING]  
>  <span data-ttu-id="f7190-177">如果您使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的設計工具，則必須先將外部資料來源定義為資料來源檢視。</span><span class="sxs-lookup"><span data-stu-id="f7190-177">If you use the designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], the external data source must first be defined as a data source view.</span></span>  
  
 <span data-ttu-id="f7190-178">如果是使用 DMX 來建立預測聯結，則可使用 OPENQUERY、OPENROWSET 或 SHAPE 命令來指定外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="f7190-178">If you use DMX to create a prediction join, you can specify the external data source by using the OPENQUERY, OPENROWSET, or SHAPE commands.</span></span> <span data-ttu-id="f7190-179">DMX 範本中的預設資料存取方法是 OPENQUERY。</span><span class="sxs-lookup"><span data-stu-id="f7190-179">The default data access method in the DMX templates is OPENQUERY.</span></span> <span data-ttu-id="f7190-180">如需這些方法的相關資訊，請參閱 [&#60;來源資料查詢&#62;](/sql/dmx/source-data-query)。</span><span class="sxs-lookup"><span data-stu-id="f7190-180">For information about these methods, see [&#60;source data query&#62;](/sql/dmx/source-data-query).</span></span>  
  
###  <a name="predictions-in-time-series-mining-models"></a><a name="bkmk_TSQuery"></a> <span data-ttu-id="f7190-181">時間序列採礦模型中的預測</span><span class="sxs-lookup"><span data-stu-id="f7190-181">Predictions in Time Series Mining Models</span></span>  
 <span data-ttu-id="f7190-182">時間序列模型與其他模型類型不同；您可以使用此模型的原貌來建立預測，或者可以提供新資料給模型，根據最近的趨勢更新模型和建立預測。</span><span class="sxs-lookup"><span data-stu-id="f7190-182">Time series models are different from other models types; you can either use the model as it is to create predictions, or you can provide new data to the model to update the model and create predictions based on recent trends.</span></span> <span data-ttu-id="f7190-183">如果您加入新的資料，您可以指定應該使用新資料的方式。</span><span class="sxs-lookup"><span data-stu-id="f7190-183">If you add new data, you can specify the way the new data should be used.</span></span>  
  
-   <span data-ttu-id="f7190-184">*「擴充模型案例」* 表示您會將新的資料加入至時間序列模型內的現有資料數列。</span><span class="sxs-lookup"><span data-stu-id="f7190-184">*Extending the model cases* means that you add the new data onto the existing series of data in the time series model.</span></span> <span data-ttu-id="f7190-185">從此以後，預測會以新的結合數列為根據。</span><span class="sxs-lookup"><span data-stu-id="f7190-185">Henceforth, predictions are based on the new, combined series.</span></span> <span data-ttu-id="f7190-186">如果您只想要將幾個資料點加入至現有的模型，此選項是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="f7190-186">This option is good when you want to simply add a few data points to an existing model.</span></span>  
  
     <span data-ttu-id="f7190-187">例如，假設您擁有的現有時間序列模型已經過去年度銷售資料的定型。</span><span class="sxs-lookup"><span data-stu-id="f7190-187">For example, suppose that you have an existing time series model that has been trained on the sales data from the previous year.</span></span> <span data-ttu-id="f7190-188">在收集數個月的新銷售資料後，您決定更新今年度的銷售預測。</span><span class="sxs-lookup"><span data-stu-id="f7190-188">After you have collected several months of new sales data, you decide to update your sales forecasts for the current year.</span></span> <span data-ttu-id="f7190-189">您可以加入新資料並擴充模型來做出新預測，以建立更新模型的預測聯結。</span><span class="sxs-lookup"><span data-stu-id="f7190-189">You can create a prediction join that updates the model by adding new data and extends the model to make new predictions.</span></span>  
  
-   <span data-ttu-id="f7190-190">*「取代模型案例」* 表示您會保留定型的模型，但是會使用新的案例資料組來取代基礎案例。</span><span class="sxs-lookup"><span data-stu-id="f7190-190">*Replacing the model cases* means that you keep the trained model, but replace the underlying cases with a new set of case data.</span></span> <span data-ttu-id="f7190-191">當您想要將趨勢保留在模型中，但是將它套用到另一組資料時，這個選項會很有用。</span><span class="sxs-lookup"><span data-stu-id="f7190-191">This option is useful when you want to keep the trend in the model, but apply it to a different set of data.</span></span>  
  
     <span data-ttu-id="f7190-192">例如，您的原始模型可能已經過一組包含極高銷售數量之資料的定型，而當您使用新的數列取代基礎資料 (也許是來自較少銷售數量的存放區) 時，您會保留趨勢，但是預測會從取代數列中的值開始。</span><span class="sxs-lookup"><span data-stu-id="f7190-192">For example, your original model might have been trained on a set of data with very high sales volumes; when you replace the underlying data with a new series (perhaps from a store with lower sales volume), you preserve the trend, but the predictions begin from the values in the replacement series.</span></span>  
  
 <span data-ttu-id="f7190-193">不論使用的方法為何，預測一定是從原始數列的結尾開始。</span><span class="sxs-lookup"><span data-stu-id="f7190-193">Regardless of which approach you use, the starting point for predictions is always the end of the original series.</span></span>  
  
 <span data-ttu-id="f7190-194">如需如何在時間序列模型上建立預測聯結的詳細資訊，請參閱[時間序列模型查詢範例](time-series-model-query-examples.md)或 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)。</span><span class="sxs-lookup"><span data-stu-id="f7190-194">For more information about how to create prediction joins on time series models, see [Time Series Model Query Examples](time-series-model-query-examples.md) or [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).</span></span>  
  
##  <a name="working-with-the-results-of-a-prediction-query"></a><a name="bkmk_WorkResults"></a> <span data-ttu-id="f7190-195">使用預測查詢的結果</span><span class="sxs-lookup"><span data-stu-id="f7190-195">Working with the Results of a Prediction Query</span></span>  
 <span data-ttu-id="f7190-196">根據建立查詢的方式，用於儲存資料採礦預測查詢結果的選項也不相同。</span><span class="sxs-lookup"><span data-stu-id="f7190-196">Your options for saving the results of a data mining prediction query are different depending on how you create the query.</span></span>  
  
-   <span data-ttu-id="f7190-197">當您在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中使用預測查詢產生器建立查詢時，可以將預測查詢的結果儲存至現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源。</span><span class="sxs-lookup"><span data-stu-id="f7190-197">When you build a query using Prediction Query Builder in either [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] or [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], you can save the results of a prediction query to an existing [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] data source.</span></span> <span data-ttu-id="f7190-198">如需詳細資訊，請參閱 [檢視及儲存預測查詢的結果](view-and-save-the-results-of-a-prediction-query.md)。</span><span class="sxs-lookup"><span data-stu-id="f7190-198">For more information, see [View and Save the Results of a Prediction Query](view-and-save-the-results-of-a-prediction-query.md).</span></span>  
  
-   <span data-ttu-id="f7190-199">當您在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [查詢] 窗格中使用 DMX 建立預測查詢時，可以使用查詢輸出選項將結果儲存至檔案，或儲存至 [查詢結果] 窗格中做為文字或方格。</span><span class="sxs-lookup"><span data-stu-id="f7190-199">When you create prediction queries using DMX in the Query pane of [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], you can use the query output options to save the results to a file, or to the Query Results pane as text or in a grid.</span></span> <span data-ttu-id="f7190-200">如需詳細資訊，請參閱[查詢與文字編輯器 &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="f7190-200">For more information, see [Query and Text Editors &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md).</span></span>  
  
-   <span data-ttu-id="f7190-201">當您使用 Integration Services 元件執行預測查詢時，這些工作可讓您使用可用的 ADO.NET 連接管理員或 OLEDB 連接管理員將結果寫入資料庫中。</span><span class="sxs-lookup"><span data-stu-id="f7190-201">When you run a prediction query using the Integration Services components, the tasks provides the ability to write the results to a database by using an available ADO.NET connection manager or OLEDB connection manager.</span></span> <span data-ttu-id="f7190-202">如需詳細資訊，請參閱 [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)。</span><span class="sxs-lookup"><span data-stu-id="f7190-202">For more information, see [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md).</span></span>  
  
 <span data-ttu-id="f7190-203">預測查詢的結果與關聯式資料庫查詢的結果不同，後者永遠傳回單一資料列的相關值，了解這一點很重要。</span><span class="sxs-lookup"><span data-stu-id="f7190-203">It is important to understand that the results of a prediction query are not like the results of a query on a relational database, which always returns a single row of related values.</span></span> <span data-ttu-id="f7190-204">加入至查詢的每個 DMX 預測函數都會傳回本身的資料列集。</span><span class="sxs-lookup"><span data-stu-id="f7190-204">Each DMX prediction function that you add to a query returns its own rowset.</span></span> <span data-ttu-id="f7190-205">因此，當您對單一案例做出預測時，結果可能是一個預測值，以及數個包含其他詳細資料的巢狀資料表資料行。</span><span class="sxs-lookup"><span data-stu-id="f7190-205">Therefore, when you make a prediction on a single case, the result might be a predicted value together with several columns of nested tables containing additional detail.</span></span>  
  
 <span data-ttu-id="f7190-206">如果您在單一查詢中結合數個函數，傳回結果會結合為階層式資料列集。</span><span class="sxs-lookup"><span data-stu-id="f7190-206">If you combine multiple functions in one query, the return results are combined as a hierarchical rowset.</span></span> <span data-ttu-id="f7190-207">例如，假設您使用時間序列模型，以如下列 DMX 陳述式之類的查詢來預測銷售金額和銷售數量的未來值：</span><span class="sxs-lookup"><span data-stu-id="f7190-207">For example, say you use a time series model to predict future values for sales amount and sales quantity, using a query such as this DMX statement:</span></span>  
  
```  
SELECT  
  PredictTimeSeries([Forecasting].[Amount]) as [PredictedAmount]  
, PredictTimeSeries([Forecasting].[Quantity]) as [PredictedQty]  
FROM  
  [Forecasting]  
  
```  
  
 <span data-ttu-id="f7190-208">此查詢的結果有兩個資料行，每個預測數列各一個資料行，其中每一個資料列都包含有預測值的巢狀資料表：</span><span class="sxs-lookup"><span data-stu-id="f7190-208">The results of this query are two columns, one for each predicted series, where each row contains a nested table with the predicted values:</span></span>  
  
 <span data-ttu-id="f7190-209">**PredictedAmount**</span><span class="sxs-lookup"><span data-stu-id="f7190-209">**PredictedAmount**</span></span>  
  
|<span data-ttu-id="f7190-210">$TIME</span><span class="sxs-lookup"><span data-stu-id="f7190-210">$TIME</span></span>|<span data-ttu-id="f7190-211">金額</span><span class="sxs-lookup"><span data-stu-id="f7190-211">Amount</span></span>|  
|-----------|------------|  
|<span data-ttu-id="f7190-212">201101</span><span class="sxs-lookup"><span data-stu-id="f7190-212">201101</span></span>|<span data-ttu-id="f7190-213">172067.11</span><span class="sxs-lookup"><span data-stu-id="f7190-213">172067.11</span></span>|  
  
|<span data-ttu-id="f7190-214">$TIME</span><span class="sxs-lookup"><span data-stu-id="f7190-214">$TIME</span></span>|<span data-ttu-id="f7190-215">金額</span><span class="sxs-lookup"><span data-stu-id="f7190-215">Amount</span></span>|  
|-----------|------------|  
|<span data-ttu-id="f7190-216">201102</span><span class="sxs-lookup"><span data-stu-id="f7190-216">201102</span></span>|<span data-ttu-id="f7190-217">363390.68</span><span class="sxs-lookup"><span data-stu-id="f7190-217">363390.68</span></span>|  
  
 <span data-ttu-id="f7190-218">**PredictedQty**</span><span class="sxs-lookup"><span data-stu-id="f7190-218">**PredictedQty**</span></span>  
  
|<span data-ttu-id="f7190-219">$TIME</span><span class="sxs-lookup"><span data-stu-id="f7190-219">$TIME</span></span>|<span data-ttu-id="f7190-220">數量</span><span class="sxs-lookup"><span data-stu-id="f7190-220">Quantity</span></span>|  
|-----------|--------------|  
|<span data-ttu-id="f7190-221">201101</span><span class="sxs-lookup"><span data-stu-id="f7190-221">201101</span></span>|<span data-ttu-id="f7190-222">77</span><span class="sxs-lookup"><span data-stu-id="f7190-222">77</span></span>|  
  
|<span data-ttu-id="f7190-223">$TIME</span><span class="sxs-lookup"><span data-stu-id="f7190-223">$TIME</span></span>|<span data-ttu-id="f7190-224">數量</span><span class="sxs-lookup"><span data-stu-id="f7190-224">Quantity</span></span>|  
|-----------|--------------|  
|<span data-ttu-id="f7190-225">201102</span><span class="sxs-lookup"><span data-stu-id="f7190-225">201102</span></span>|<span data-ttu-id="f7190-226">260</span><span class="sxs-lookup"><span data-stu-id="f7190-226">260</span></span>|  
  
 <span data-ttu-id="f7190-227">如果提供者無法處理階層式資料列集，則您可以在預測查詢中使用 FLATTEN 關鍵字將結果扁平化。</span><span class="sxs-lookup"><span data-stu-id="f7190-227">If your provider cannot handle hierarchical rowsets, you can flatten the results by using the FLATTEN keyword in the prediction query.</span></span> <span data-ttu-id="f7190-228">如需包括扁平化資料列集範例的詳細資訊，請參閱 [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx)。</span><span class="sxs-lookup"><span data-stu-id="f7190-228">For more information, including examples of flattened rowsets, see [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f7190-229">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f7190-229">See Also</span></span>  
 <span data-ttu-id="f7190-230">[&#40;資料採礦&#41;的內容查詢](content-queries-data-mining.md) </span><span class="sxs-lookup"><span data-stu-id="f7190-230">[Content Queries &#40;Data Mining&#41;](content-queries-data-mining.md) </span></span>  
 [<span data-ttu-id="f7190-231">資料定義查詢 &#40;資料採礦&#41;</span><span class="sxs-lookup"><span data-stu-id="f7190-231">Data Definition Queries &#40;Data Mining&#41;</span></span>](data-definition-queries-data-mining.md)  
  
  