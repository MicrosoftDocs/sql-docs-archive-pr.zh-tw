---
title: " (表格式) 的關鍵效能指標標記法 |Microsoft Docs"
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 8d3d949e-5d43-4d2e-9dc8-48d182a7a935
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7cc9ec7e6ccae664a6f608c350483ae9744fb49d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706814"
---
# <a name="key-performance-indicator-representation-tabular"></a><span data-ttu-id="59f80-102">關鍵效能指標表示法 (表格式)</span><span class="sxs-lookup"><span data-stu-id="59f80-102">Key Performance Indicator Representation (Tabular)</span></span>
  <span data-ttu-id="59f80-103">KPI 是用來針對目標值，測量由基底量值定義之值的效能。</span><span class="sxs-lookup"><span data-stu-id="59f80-103">A KPI is used to gauge performance of a value, defined by a Base measure, against a Target value</span></span>  
  
## <a name="key-performance-indicator-representation"></a><span data-ttu-id="59f80-104">關鍵效能指標表示法</span><span class="sxs-lookup"><span data-stu-id="59f80-104">Key Performance Indicator Representation</span></span>  
 <span data-ttu-id="59f80-105">在表格式物件模型中，關鍵效能指標-kpi-是一個量值，其中包含用戶端應用程式以圖形方式顯示它的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="59f80-105">In tabular object models a key performance indicator -kpi- is a measure with additional information for the client application to display it graphically.</span></span> <span data-ttu-id="59f80-106">kpi 通常包含有關要取得之目標的資訊、要與目標相比較之量值的狀態，以及有關如何以圖形方式顯示狀態的用戶端工具資訊。</span><span class="sxs-lookup"><span data-stu-id="59f80-106">A kpi usually has information about a goal to be obtained, the status of the measure compared to a the goal, and information for the client tool on how to display graphically the status.</span></span>  
  
### <a name="key-performance-indicator-in-amo"></a><span data-ttu-id="59f80-107">AMO 中的關鍵效能指標</span><span class="sxs-lookup"><span data-stu-id="59f80-107">Key Performance Indicator in AMO</span></span>  
 <span data-ttu-id="59f80-108">當您使用 AMO 管理表格式模型 kpi 時，物件與 AMO 中的 kpi 之間有一對一的相符關係，AMO <xref:Microsoft.AnalysisServices.Kpi> 物件不會用於這個目的；在 AMO 中的表格式模型內，kpi 是由 <xref:Microsoft.AnalysisServices.MdxScript.Commands%2A> 集合和 <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A> 中其中一個元素內建立的一系列物件所表示。</span><span class="sxs-lookup"><span data-stu-id="59f80-108">When using AMO to manage a Tabular Model kpi there is no one-to-one object match for a kpi in AMO, the AMO <xref:Microsoft.AnalysisServices.Kpi>object is not used for this purpose; in AMO, for tabular models, a kpi is represented the by a series of objects created in one of the elements in the <xref:Microsoft.AnalysisServices.MdxScript.Commands%2A> collection and in the <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A>.</span></span>  
  
 <span data-ttu-id="59f80-109">下列程式碼片段示範如何建立多個可能的 kpi 定義的其中一個。</span><span class="sxs-lookup"><span data-stu-id="59f80-109">The following code snippet shows how to create one of many possible kpi definitions.</span></span>  
  
```  
  
private void addStaticKPI(object sender, EventArgs e)  
{  
    double KPIGoal = 0, status1ThresholdValue = 0, status2ThresholdValue = 0  
        , redAreaValue = 0, yellowAreaValue = 0, greenAreaValue = 0;  
    string clientStatusGraphicImageName = "Three Circles Colored";  
  
    //Verify input requirements  
    //Goal values  
    if (staticTargetKPI.Checked)  
    {//Static KPI Goal selected  
        if (string.IsNullOrEmpty(staticTargetKPIGoal.Text)  
            || string.IsNullOrWhiteSpace(staticTargetKPIGoal.Text)  
            || !double.TryParse(staticTargetKPIGoal.Text, out KPIGoal))  
        {  
            MessageBox.Show(String.Format("Static Goal is not defined or is not a valid number."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
            return;  
        }  
    }  
    else  
    {//Measure KPI Goal selected  
        if (!TargetMeasureForKPISelected)  
        {  
            MessageBox.Show(String.Format("Measure Goal is not selected."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
            return;  
        }  
    }  
  
    //Status  
    if (string.IsNullOrEmpty(firstStatusThresholdValue.Text)  
        || string.IsNullOrWhiteSpace(firstStatusThresholdValue.Text)  
        || !double.TryParse(firstStatusThresholdValue.Text, out status1ThresholdValue)  
        || string.IsNullOrEmpty(secondStatusThresholdValue.Text)  
        || string.IsNullOrWhiteSpace(secondStatusThresholdValue.Text)  
        || !double.TryParse(secondStatusThresholdValue.Text, out status2ThresholdValue))  
    {  
        MessageBox.Show(String.Format("Status Threshold are not defined or they are not a valid number."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    if (string.IsNullOrEmpty(statusValueRedArea.Text)  
        || string.IsNullOrWhiteSpace(statusValueRedArea.Text)  
        || !double.TryParse(statusValueRedArea.Text, out redAreaValue)  
        || string.IsNullOrEmpty(statusValueYellowArea.Text)  
        || string.IsNullOrWhiteSpace(statusValueYellowArea.Text)  
        || !double.TryParse(statusValueYellowArea.Text, out yellowAreaValue)  
        || string.IsNullOrEmpty(statusValueGreenArea.Text)  
        || string.IsNullOrWhiteSpace(statusValueGreenArea.Text)  
        || !double.TryParse(statusValueGreenArea.Text, out greenAreaValue))  
    {  
        MessageBox.Show(String.Format("Status Area values are not defined or they are not a valid number."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    //Set working variables  
    string kpiTableName = ((DataRowView)MeasuresInModelList.CheckedItems[0])[0].ToString();  
    string kpiMeasureName = ((DataRowView)MeasuresInModelList.CheckedItems[0])[1].ToString();  
  
    //Verify if KPI is already defined  
    if (modelCube.MdxScripts["MdxScript"].CalculationProperties.Contains(string.Format("KPIs.[{0}]", kpiMeasureName)))  
    {  
        //ToDo: Verify with the user if wants to update KPI or exit  
        //If user wants to update then remove KPI from mdxScripts and continue with the creating the KPI  
        //  
        // Until the code to remove KPI is finished we'll have to exit with a message of no duplicated KPIs are allowed  
        MessageBox.Show(String.Format("Another KPI exists for the same measeure."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    StringBuilder kpiCommand = new StringBuilder();  
  
    AMO.MdxScript mdxScript = modelCube.MdxScripts["MdxScript"];  
    kpiCommand.Append(mdxScript.Commands[1].Text);  
  
    string goalExpression;  
    if (staticTargetKPI.Checked)  
    {//Static KPI Goal selected  
        goalExpression = KPIGoal.ToString();  
    }  
    else  
    {//Measure KPI Goal selected  
        string measureGoalMeasureName = ((DataRowView)KpiTargetMeasures.CheckedItems[0])[1].ToString();  
        goalExpression = string.Format("[Measures].[{0}]", measureGoalMeasureName);  
    }  
  
    kpiCommand.AppendLine(string.Format("CREATE MEMBER CURRENTCUBE.Measures.[_{1} Goal] AS '{2}', ASSOCIATED_MEASURE_GROUP = '{0}';"  
            , kpiTableName, kpiMeasureName, goalExpression));  
  
    string statusExpression;  
    if (staticTargetKPI.Checked)  
    {//Static KPI Goal selected  
        statusExpression = string.Format("KpiValue(\"{0}\")", kpiMeasureName).Trim();  
    }  
    else  
    {//Measure KPI Goal selected  
        string measureGoalMeasureName = ((DataRowView)KpiTargetMeasures.CheckedItems[0])[1].ToString().Trim();  
  
        string M = string.Format("[Measures].[{0}]", kpiMeasureName);  
        string T = string.Format("[Measures].[{0}]", measureGoalMeasureName);  
  
        if (KpiRelationDifference.Checked)  
        {  
            statusExpression = string.Format("{1} - {0}", M, T);  
        }  
        else  
        {  
            if (KpiRelationRatioMT.Checked)  
            {  
                statusExpression = string.Format("{0} / {1}", M, T);  
            }  
            else  
            {  
                statusExpression = string.Format("{1} / {0}", M, T);  
            }  
        }  
    }  
    kpiCommand.AppendLine(string.Format("CREATE MEMBER CURRENTCUBE.Measures.[_{1} Status] "  
                                              + " AS 'Case When IsEmpty({9}) Then Null "  
                                                       + " When ({9}) {2} {3} Then {4} "  
                                                       + " When ({9}) {5} {6} Then {7} "  
                                                       + " Else {8} End'"  
                                              + ", ASSOCIATED_MEASURE_GROUP = '{0}';"  
        , kpiTableName, kpiMeasureName // 0, 1  
        , statusThreshold1ComparisonOperator.Text, status1ThresholdValue, redAreaValue // 2, 3, 4  
        , statusThreshold2ComparisonOperator.Text, status2ThresholdValue, yellowAreaValue, greenAreaValue // 5, 6, 7, 8  
        , statusExpression // 9  
        ));  
  
    kpiCommand.AppendLine(string.Format("CREATE MEMBER CURRENTCUBE.Measures.[_{1} Trend] AS '0', ASSOCIATED_MEASURE_GROUP = '{0}';"  
        , kpiTableName, kpiMeasureName));  
  
    kpiCommand.AppendLine(string.Format("CREATE KPI CURRENTCUBE.[{1}] AS Measures.[{1}]"  
                                               + ", ASSOCIATED_MEASURE_GROUP = '{0}'"  
                                               + ", GOAL = Measures.[_{1} Goal]"  
                                               + ", STATUS = Measures.[_{1} Status]"  
                                               + ", TREND = Measures.[_{1} Trend]"  
                                               + ", STATUS_GRAPHIC = '{2}'"  
                                               + ", TREND_GRAPHIC = '{2}';"  
        , kpiTableName, kpiMeasureName, clientStatusGraphicImageName));  
  
    {//Adding Calculation Reference for the Measure itself  
        if (!mdxScript.CalculationProperties.Contains(kpiMeasureName))  
        {  
            AMO.CalculationProperty cp = new AMO.CalculationProperty(kpiMeasureName, AMO.CalculationType.Member);  
            cp.FormatString = ""; // ToDo: Get formatting attributes for the member  
            cp.Visible = true;  
            mdxScript.CalculationProperties.Add(cp);  
        }  
    }  
    {//Adding Calculation Reference for the Goal measure  
        AMO.CalculationProperty cp = new AMO.CalculationProperty(string.Format("Measures.[_{0} Goal]", kpiMeasureName), AMO.CalculationType.Member);  
        cp.FormatString = ""; // ToDo: Get formatting attributes for the member  
        cp.Visible = false;  
        mdxScript.CalculationProperties.Add(cp);  
    }  
  
    {//Adding Calculation Reference for the Status measure  
        AMO.CalculationProperty cp = new AMO.CalculationProperty(string.Format("Measures.[_{0} Status]", kpiMeasureName), AMO.CalculationType.Member);  
        cp.FormatString = ""; // ToDo: Get formatting attributes for the member  
        cp.Visible = false;  
        mdxScript.CalculationProperties.Add(cp);  
    }  
  
    {//Adding Calculation Reference for the Status measure  
        AMO.CalculationProperty cp = new AMO.CalculationProperty(string.Format("Measures.[_{0} Trend]", kpiMeasureName), AMO.CalculationType.Member);  
        cp.FormatString = ""; // ToDo: Get formatting attributes for the member  
        cp.Visible = false;  
        mdxScript.CalculationProperties.Add(cp);  
    }  
  
    {//Adding Calculation Reference for the KPI  
        AMO.CalculationProperty cp = new AMO.CalculationProperty(string.Format("KPIs.[{0}]", kpiMeasureName), AMO.CalculationType.Member);  
        cp.FormatString = ""; // ToDo: Get formatting attributes for the member  
        cp.Visible = true;  
        mdxScript.CalculationProperties.Add(cp);  
    }  
    try  
    {                  
        newDatabase.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.UpdateOrCreate);  
        MessageBox.Show(String.Format("KPI successfully defined."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Information);  
    }  
    catch (AMO.OperationException amoOperationException)  
    {  
        //ToDo: remove anything left in mdxScript up to the point where the exception was thrown  
        MessageBox.Show(String.Format("Error creating KPI for Measure '{0}'[{1}]\nError message: {2}", kpiTableName, kpiMeasureName, amoOperationException.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Information);  
    }  
  
}  
  
```  
  
## <a name="amo2tabular-sample"></a><span data-ttu-id="59f80-110">AMO2Tabular 範例</span><span class="sxs-lookup"><span data-stu-id="59f80-110">AMO2Tabular sample</span></span>  
 <span data-ttu-id="59f80-111">若要了解如何使用 AMO 建立及操作關鍵效能指標表示法，請參閱 AMO 對表格式範例的原始程式碼，特別要檢查以下的原始程式檔：AddKPIs.cs。</span><span class="sxs-lookup"><span data-stu-id="59f80-111">To have an understanding on how to use AMO to create and manipulate Key Performance Indicator representations see the source code of the AMO to Tabular sample; specifically check in the following source file: AddKPIs.cs.</span></span> <span data-ttu-id="59f80-112">您可以在 Codeplex 上取得範例。</span><span class="sxs-lookup"><span data-stu-id="59f80-112">The sample is available at Codeplex.</span></span> <span data-ttu-id="59f80-113">有關此程式碼的重要注意事項：此程式碼的提供目的只是為了支援這裡所說明的邏輯概念，不應該用於實際執行環境，也不應該用於教學以外的其他用途。</span><span class="sxs-lookup"><span data-stu-id="59f80-113">An important note about the code: the code is provided only as a support to the logical concepts explained here and should not be used in a production environment; nor should it be used for other purpose other than the pedagogical one.</span></span>  
  
  
