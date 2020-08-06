---
title: 文字方塊 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10134"
- sql12.rtp.rptdesigner.textproperties.general.f1
- "10120"
- sql12.rtp.rptdesigner.textboxproperties.general.f1
ms.assetid: df49e4e3-f279-4c63-a03b-b70c095f4ba2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f3bc9d9d645fe2a966197af9059eb90c64ce3954
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595647"
---
# <a name="text-boxes-report-builder-and-ssrs"></a><span data-ttu-id="49951-102">文字方塊 (報表產生器及 SSRS)</span><span class="sxs-lookup"><span data-stu-id="49951-102">Text Boxes (Report Builder and SSRS)</span></span>
  <span data-ttu-id="49951-103">當您考慮文字方塊時，可能會考慮包含介面 (如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office PowerPoint) 文字的獨立方塊。</span><span class="sxs-lookup"><span data-stu-id="49951-103">When you think of a text box, you probably think of a stand-alone box containing text on a surface like [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office PowerPoint.</span></span> <span data-ttu-id="49951-104">在報表產生器中，有些文字方塊就像那樣，而且這些文字方塊可以根據運算式，顯示標題、描述與標籤或動態文字的常值文字。</span><span class="sxs-lookup"><span data-stu-id="49951-104">In Report Builder, some text boxes are like that, and they can display literal text for titles, descriptions, and labels, or dynamic text based on expressions.</span></span> <span data-ttu-id="49951-105">但是，資料表或矩陣 (Tablix 資料區) 中的每個資料格也都包含一個文字方塊，這個文字方塊可以使用報表中之獨立文字方塊的相同方式進行格式化。</span><span class="sxs-lookup"><span data-stu-id="49951-105">But every cell in a table or matrix (a tablix data region) also contains a text box, which can be formatted in the same way as stand-alone text boxes in your report.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="49951-106">如果將報表資料集欄位值直接拖曳到報表設計介面，或報表設計介面上的文字方塊，則您在執行報表時，只能看到結果集中的第一個值。</span><span class="sxs-lookup"><span data-stu-id="49951-106">If you drag a report dataset field value directly to the report design surface, or to a text box on the report design surface, you only see the first value in the result set when you run the report.</span></span> <span data-ttu-id="49951-107">若要查看欄位的所有值，則必須將欄位拖曳到資料表或矩陣中的資料格。</span><span class="sxs-lookup"><span data-stu-id="49951-107">To see all the values for a field, you must drag the field to a cell in a table or matrix.</span></span> <span data-ttu-id="49951-108">如此一來，當您執行報表時，將會看到該欄位中的所有值。</span><span class="sxs-lookup"><span data-stu-id="49951-108">That way, when you run the report, you will see all the values in that field.</span></span>  
  
 <span data-ttu-id="49951-109">若要以自由形式配置顯示重複的文字，請在清單資料區中放置一個文字方塊。</span><span class="sxs-lookup"><span data-stu-id="49951-109">To show repeating text in a free-form layout, place a text box in a list data region.</span></span> <span data-ttu-id="49951-110">當您想要重複多個值的形式時，請使用清單，例如，客戶發票表單會針對每個客戶重複一次。</span><span class="sxs-lookup"><span data-stu-id="49951-110">Use a list when you want to repeat a form for multiple values, for example, a customer invoice form repeated once for each customer.</span></span> <span data-ttu-id="49951-111">如需詳細資訊，請參閱[&#40;報表產生器和 SSRS&#41;清單](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="49951-111">For more information, see [Lists &#40;Report Builder and SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).</span></span>  
  
 <span data-ttu-id="49951-112">當您想要控制文字方塊配置和最後一個文字方塊下的空白字元時，使用矩形容器。</span><span class="sxs-lookup"><span data-stu-id="49951-112">Use a rectangle container when you want to control the text box layout and white space below the last text box.</span></span> <span data-ttu-id="49951-113">如需詳細資訊，請參閱[矩形和線條 &#40;報表產生器及 SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="49951-113">For more information, see [Rectangles and Lines &#40;Report Builder and SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md).</span></span>  
  
 <span data-ttu-id="49951-114">文字方塊中的運算式可以包含指向資料庫欄位的常值文字，也可以計算資料。</span><span class="sxs-lookup"><span data-stu-id="49951-114">The expressions in a text box can contain literal text, point to a field in the database, or calculate data.</span></span> <span data-ttu-id="49951-115">所有運算式都會顯示為預留位置文字，讓您可以格式化數字、色彩和其他外觀屬性。</span><span class="sxs-lookup"><span data-stu-id="49951-115">All expressions are shown as placeholder text so that you can format numbers, colors, and other appearance properties.</span></span> <span data-ttu-id="49951-116">您也可以在相同的文字方塊中結合預留位置與常值文字。</span><span class="sxs-lookup"><span data-stu-id="49951-116">You can also combine placeholders with literal text in the same text box.</span></span>  
  
 <span data-ttu-id="49951-117">您可以在任何單一文字方塊中，使用多個字型、色彩、樣式和動作格式化文字。</span><span class="sxs-lookup"><span data-stu-id="49951-117">You can format text in any single text box with multiple fonts, colors, styles, and actions.</span></span> <span data-ttu-id="49951-118">如需詳細資訊，請參閱 [格式化文字和預留位置 &#40;報表產生器及 SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)(建立發票和表單的清單)。</span><span class="sxs-lookup"><span data-stu-id="49951-118">For more information, see [Formatting Text and Placeholders &#40;Report Builder and SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md).</span></span>  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="growing-and-shrinking-a-text-box"></a><a name="GrowShrinkTextBox"></a> <span data-ttu-id="49951-119">文字方塊的擴張和縮小</span><span class="sxs-lookup"><span data-stu-id="49951-119">Growing and Shrinking a Text Box</span></span>  
 <span data-ttu-id="49951-120">根據預設，文字方塊是固定的大小。</span><span class="sxs-lookup"><span data-stu-id="49951-120">By default, text boxes are a fixed size.</span></span> <span data-ttu-id="49951-121">您可以讓文字方塊根據其內容垂直縮小或擴張。</span><span class="sxs-lookup"><span data-stu-id="49951-121">You can allow a text box to shrink or expand vertically based on its contents.</span></span> <span data-ttu-id="49951-122">如需詳細資訊，請參閱 [允許文字方塊擴張或縮小 &#40;報表產生器及 SSRS&#41;](allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md)(建立發票和表單的清單)。</span><span class="sxs-lookup"><span data-stu-id="49951-122">For more information, see [Allow a Text Box to Grow or Shrink &#40;Report Builder and SSRS&#41;](allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md).</span></span>  
  
## <a name="orienting-a-text-box"></a><span data-ttu-id="49951-123">指定文字方塊的方向</span><span class="sxs-lookup"><span data-stu-id="49951-123">Orienting a Text Box</span></span>  
 <span data-ttu-id="49951-124">指定文字方塊方向可協助您建立更容易閱讀的報表、支援特定地區設定的文字方向、在固定頁面大小的列印報表中容納更多資料行，並以更受觀迎的圖形方式建立報表。</span><span class="sxs-lookup"><span data-stu-id="49951-124">Orienting text boxes can help you create more readable reports, support locale-specific text orientation, fit more columns on a printed report that has fixed page size, and create reports with more graphical appeal.</span></span> <span data-ttu-id="49951-125">文字方塊可以朝向不同的方向：水平、垂直，或旋轉 270 度。</span><span class="sxs-lookup"><span data-stu-id="49951-125">A text box can be oriented in different directions: horizontal, vertical, or rotated by 270 degrees.</span></span> <span data-ttu-id="49951-126">垂直選項最常用於由上往下書寫的東亞洲語言。</span><span class="sxs-lookup"><span data-stu-id="49951-126">The vertical option is most commonly used for East Asian languages that are written top to bottom.</span></span> <span data-ttu-id="49951-127">在大部分轉譯器中，垂直選項會處理字符旋轉屬性，以便讓文字由上而下的方向書寫，但字元並不會側躺。</span><span class="sxs-lookup"><span data-stu-id="49951-127">In most renderers the vertical option handles the glyph rotation property so that the text is written top to bottom, but the characters are not on their sides.</span></span> <span data-ttu-id="49951-128">針對其他語言，在垂直和 270 度選項中，文字是側躺的。</span><span class="sxs-lookup"><span data-stu-id="49951-128">For other languages, in the vertical and 270-degree options the text is written sideways.</span></span>  
  
 <span data-ttu-id="49951-129">您可以將方向套用至包含常值，來自報表資料集的欄位，或計算的資料等項目的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="49951-129">You can apply orientation to text boxes that contain literal text, fields from a report dataset, or calculated data.</span></span> <span data-ttu-id="49951-130">文字方塊可以在報表主體、資料表或矩陣，或報表首及尾上獨立呈現。</span><span class="sxs-lookup"><span data-stu-id="49951-130">The text box can be stand-alone in the report body, in a table or matrix, or in a report header and footer.</span></span>  
  
 <span data-ttu-id="49951-131">下圖顯示依月份群組的三種版本資料表報表。</span><span class="sxs-lookup"><span data-stu-id="49951-131">The following picture shows three versions of a table report that groups data by month.</span></span> <span data-ttu-id="49951-132">包含月份值的文字方塊使用不同的文字方塊方向。</span><span class="sxs-lookup"><span data-stu-id="49951-132">The text box that contains the month value uses a different text box orientation.</span></span>  
  
 <span data-ttu-id="49951-133">![rs_TextBoxOrientation](../media/rs-textboxorientation.gif "rs_TextBoxOrientation")</span><span class="sxs-lookup"><span data-stu-id="49951-133">![rs_TextBoxOrientation](../media/rs-textboxorientation.gif "rs_TextBoxOrientation")</span></span>  
  
 <span data-ttu-id="49951-134">方向是在文字方塊上設定，並套用至方塊中的所有文字。</span><span class="sxs-lookup"><span data-stu-id="49951-134">Orientation is set on the text box and applies to all the text in the box.</span></span> <span data-ttu-id="49951-135">您無法針對文字方塊的各個部分指定不同的方向。</span><span class="sxs-lookup"><span data-stu-id="49951-135">You cannot specify a different orientation for parts of the text box.</span></span>  
  
 <span data-ttu-id="49951-136">若要快速地開始變更文字方向，請參閱[教學課程：將文字格式化 &#40;報表產生器&#41;](../tutorial-format-text-report-builder.md)中的旋轉文字一節。</span><span class="sxs-lookup"><span data-stu-id="49951-136">To quickly get started with changing text orientation, see the section on rotating text in the [Tutorial: Format Text &#40;Report Builder&#41;](../tutorial-format-text-report-builder.md).</span></span> <span data-ttu-id="49951-137">如需詳細資訊，請參閱[&#40;報表產生器和 SSRS&#41;設定文字方塊方向](set-text-box-orientation-report-builder-and-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="49951-137">For more information, see [Set Text Box Orientation &#40;Report Builder and SSRS&#41;](set-text-box-orientation-report-builder-and-ssrs.md).</span></span>  
  
##  <a name="how-to-topics"></a><a name="HowTo"></a><span data-ttu-id="49951-138">How To 主題</span><span class="sxs-lookup"><span data-stu-id="49951-138">How-To Topics</span></span>  
 [<span data-ttu-id="49951-139">加入、移動或刪除文字方塊 &#40;報表產生器及 SSRS&#41;</span><span class="sxs-lookup"><span data-stu-id="49951-139">Add, Move, or Delete a Text Box &#40;Report Builder and SSRS&#41;</span></span>](add-move-or-delete-a-text-box-report-builder-and-ssrs.md)  
  
 [<span data-ttu-id="49951-140">格式化文字方塊中的文字 &#40;報表產生器及 SSRS&#41;</span><span class="sxs-lookup"><span data-stu-id="49951-140">Format Text in a Text Box &#40;Report Builder and SSRS&#41;</span></span>](format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
 [<span data-ttu-id="49951-141">設定文字方塊方向 &#40;報表產生器及 SSRS&#41;</span><span class="sxs-lookup"><span data-stu-id="49951-141">Set Text Box Orientation &#40;Report Builder and SSRS&#41;</span></span>](set-text-box-orientation-report-builder-and-ssrs.md)  
  
 [<span data-ttu-id="49951-142">允許文字方塊擴張或縮小 &#40;報表產生器及 SSRS&#41;</span><span class="sxs-lookup"><span data-stu-id="49951-142">Allow a Text Box to Grow or Shrink &#40;Report Builder and SSRS&#41;</span></span>](allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a><span data-ttu-id="49951-143">另請參閱</span><span class="sxs-lookup"><span data-stu-id="49951-143">See Also</span></span>  
 <span data-ttu-id="49951-144">[&#40;報表產生器和 SSRS 設定文字和預留位置的格式&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md) </span><span class="sxs-lookup"><span data-stu-id="49951-144">[Formatting Text and Placeholders &#40;Report Builder and SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md) </span></span>  
 [<span data-ttu-id="49951-145">格式化數字和日期 &#40;報表產生器及 SSRS&#41;</span><span class="sxs-lookup"><span data-stu-id="49951-145">Formatting Numbers and Dates &#40;Report Builder and SSRS&#41;</span></span>](formatting-numbers-and-dates-report-builder-and-ssrs.md)  
  
  
