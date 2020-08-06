---
title: 指定標記為日期資料表以搭配時間智慧使用 (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 30841d1f-0c3b-4575-8f4a-27a1492e248c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 81038369b8cb8636a2aa216f1c26783a96d5f7ca
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686486"
---
# <a name="specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular"></a><span data-ttu-id="91a51-102">指定標記為日期資料表以搭配時間智慧使用 (SSAS 表格式)</span><span class="sxs-lookup"><span data-stu-id="91a51-102">Specify Mark as Date Table for use with Time Intelligence (SSAS Tabular)</span></span>
  <span data-ttu-id="91a51-103">若要在 DAX 公式中使用時間智慧函數，您必須指定日期資料表以及 Date 資料類型的唯一識別碼 (日期時間) 資料行。</span><span class="sxs-lookup"><span data-stu-id="91a51-103">In order to use time intelligence functions in DAX formulas, you must specify a date table and a unique identifier (datetime) column of the Date data type.</span></span> <span data-ttu-id="91a51-104">您將日期資料表中的某個資料行指定為唯一識別碼之後，就可以在日期資料表與任何事實資料表的資料行之間建立關聯性。</span><span class="sxs-lookup"><span data-stu-id="91a51-104">Once a column in the date table is specified as a unique identifier, you can create relationships between columns in the date table and any fact tables.</span></span>  
  
 <span data-ttu-id="91a51-105">使用時間智慧函數時，適用下列規則：</span><span class="sxs-lookup"><span data-stu-id="91a51-105">When using time intelligence functions, the following rules apply:</span></span>  
  
-   <span data-ttu-id="91a51-106">使用 DAX 時間智慧函數時，請勿指定事實資料表中的日期時間資料行。</span><span class="sxs-lookup"><span data-stu-id="91a51-106">When using DAX time intelligence functions, never specify a datetime column from a fact table.</span></span> <span data-ttu-id="91a51-107">請務必在您的模型中建立個別的日期資料表，其中至少包含一個 Date 資料類型的日期時間資料行且包含唯一值。</span><span class="sxs-lookup"><span data-stu-id="91a51-107">Always create a separate date table in your model with at least one datetime column of Date data type and with unique values.</span></span>  
  
-   <span data-ttu-id="91a51-108">請確定您的日期資料表具有連續的日期範圍。</span><span class="sxs-lookup"><span data-stu-id="91a51-108">Make sure your date table has a continuous date range.</span></span>  
  
-   <span data-ttu-id="91a51-109">日期資料表中的日期時間資料行應該具有日資料粒度 (不含日的分數部分)。</span><span class="sxs-lookup"><span data-stu-id="91a51-109">The datetime column in the date table should be at day granularity (without fractions of a day).</span></span>  
  
-   <span data-ttu-id="91a51-110">您必須使用 **[標記為日期資料表]** 對話方塊來指定日期資料表和唯一識別碼資料行。</span><span class="sxs-lookup"><span data-stu-id="91a51-110">You must specify a date table and a unique identifier column by using the **Mark the Date Table** dialog box.</span></span>  
  
-   <span data-ttu-id="91a51-111">在事實資料表與日期資料表中 Date 資料類型的資料行之間建立關聯性。</span><span class="sxs-lookup"><span data-stu-id="91a51-111">Create relationships between fact tables and columns of Date data type in the date table.</span></span>  
  
#### <a name="to-specify-a-date-table-and-unique-identifier"></a><span data-ttu-id="91a51-112">若要指定日期資料表和唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="91a51-112">To specify a date table and unique identifier</span></span>  
  
1.  <span data-ttu-id="91a51-113">在模型設計師中，按一下日期資料表。</span><span class="sxs-lookup"><span data-stu-id="91a51-113">In the model designer, click the date table.</span></span>  
  
2.  <span data-ttu-id="91a51-114">依序按一下 **[資料表]** 功能表、 **[日期]** 和 **Mark as [日期] [資料表]**。</span><span class="sxs-lookup"><span data-stu-id="91a51-114">Click the **Table** menu, then click **Date**, and then click **Mark as Date Table**</span></span>  
  
3.  <span data-ttu-id="91a51-115">在 **[標記為日期資料表]** 對話方塊的 **[日期]** 清單方塊中，選取要當做唯一識別碼使用的資料行。</span><span class="sxs-lookup"><span data-stu-id="91a51-115">In the **Mark as Date Table** dialog box, in the **Date** listbox, select a column to be used as a unique identifier.</span></span> <span data-ttu-id="91a51-116">這個資料行必須包含唯一值而且應該屬於 Date 資料類型。</span><span class="sxs-lookup"><span data-stu-id="91a51-116">This column must contain unique values and should be of Date data type.</span></span> <span data-ttu-id="91a51-117">例如：</span><span class="sxs-lookup"><span data-stu-id="91a51-117">For example:</span></span>  
  
    |<span data-ttu-id="91a51-118">Date</span><span class="sxs-lookup"><span data-stu-id="91a51-118">Date</span></span>|  
    |----------|  
    |<span data-ttu-id="91a51-119">7/1/2010 12:00:00 AM</span><span class="sxs-lookup"><span data-stu-id="91a51-119">7/1/2010 12:00:00 AM</span></span>|  
    |<span data-ttu-id="91a51-120">7/2/2010 12:00:00 AM</span><span class="sxs-lookup"><span data-stu-id="91a51-120">7/2/2010 12:00:00 AM</span></span>|  
    |<span data-ttu-id="91a51-121">7/3/2010 12:00:00 AM</span><span class="sxs-lookup"><span data-stu-id="91a51-121">7/3/2010 12:00:00 AM</span></span>|  
    |<span data-ttu-id="91a51-122">7/4/2010 12:00:00 AM</span><span class="sxs-lookup"><span data-stu-id="91a51-122">7/4/2010 12:00:00 AM</span></span>|  
    |<span data-ttu-id="91a51-123">7/5/2010 12:00:00 AM</span><span class="sxs-lookup"><span data-stu-id="91a51-123">7/5/2010 12:00:00 AM</span></span>|  
  
4.  <span data-ttu-id="91a51-124">必要時，請在事實資料表與日期資料表之間建立任何關聯性。</span><span class="sxs-lookup"><span data-stu-id="91a51-124">If necessary, create any relationships between fact tables and the date table.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="91a51-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="91a51-125">See Also</span></span>  
 <span data-ttu-id="91a51-126">[&#40;SSAS 表格式&#41;的計算](calculations-ssas-tabular.md) </span><span class="sxs-lookup"><span data-stu-id="91a51-126">[Calculations &#40;SSAS Tabular&#41;](calculations-ssas-tabular.md) </span></span>  
 [<span data-ttu-id="91a51-127">&#40;DAX&#41;的時間智慧函數</span><span class="sxs-lookup"><span data-stu-id="91a51-127">Time Intelligence Functions &#40;DAX&#41;</span></span>](/dax/time-intelligence-functions-dax)  
  
  