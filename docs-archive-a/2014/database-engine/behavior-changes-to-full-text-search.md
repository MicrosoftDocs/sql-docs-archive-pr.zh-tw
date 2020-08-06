---
title: 全文檢索搜尋的行為變更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], breaking changes
- behavior changes [full-text search]
- full-text indexes [SQL Server], breaking changes
ms.assetid: 573444e8-51bc-4f3d-9813-0037d2e13b8f
author: rothja
ms.author: jroth
ms.openlocfilehash: cbe807237651bd8bb81fa1c9f028847654b97889
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87700231"
---
# <a name="behavior-changes-to-full-text-search"></a><span data-ttu-id="7cb6b-102">全文檢索搜尋的行為變更</span><span class="sxs-lookup"><span data-stu-id="7cb6b-102">Behavior Changes to Full-Text Search</span></span>
  <span data-ttu-id="7cb6b-103">本主題描述全文檢索搜尋的行為變更。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-103">This topic describes behavior changes in full-text search.</span></span> <span data-ttu-id="7cb6b-104">行為變更會影響 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 功能的運作或互動方式 (相較於舊版的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)])。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-104">Behavior changes affect how features work or interact in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] as compared to earlier versions of [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].</span></span>  
  
## <a name="behavior-changes-in-full-text-search-in-sssql14"></a><span data-ttu-id="7cb6b-105">[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 全文檢索搜尋的行為變更</span><span class="sxs-lookup"><span data-stu-id="7cb6b-105">Behavior Changes in Full-Text Search in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]</span></span>  
 <span data-ttu-id="7cb6b-106">將於日後提供資訊。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-106">Information to come later.</span></span>  
  
## <a name="behavior-changes-in-full-text-search-in-sssql11"></a><span data-ttu-id="7cb6b-107">[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 全文檢索搜尋的行為變更</span><span class="sxs-lookup"><span data-stu-id="7cb6b-107">Behavior Changes in Full-Text Search in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]</span></span>  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] <span data-ttu-id="7cb6b-108">會安裝美式英文 (LCID 1033) 和英式英文 (LCID 2057) 的新版斷詞工具和字幹分析器。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-108">installs a new version of the word breakers and stemmers for US English (LCID 1033) and UK English (LCID 2057).</span></span> <span data-ttu-id="7cb6b-109">不過，如果您要保留舊版的行為，可以切換到這些元件的舊版。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-109">However you can switch to the previous version of these components if you want to retain the previous behavior.</span></span> <span data-ttu-id="7cb6b-110">如需詳細資訊，請參閱 [變更用於美式英文與英式英文的斷詞工具](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-110">For more information, see [Change the Word Breaker Used for US English and UK English](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md).</span></span>  
  
### <a name="new-word-breakers-and-stemmers-installed"></a><span data-ttu-id="7cb6b-111">已安裝新的斷詞工具和字幹分析器</span><span class="sxs-lookup"><span data-stu-id="7cb6b-111">New Word Breakers and Stemmers Installed</span></span>  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] <span data-ttu-id="7cb6b-112">更新全文檢索搜尋和語意搜尋使用的所有斷詞工具和字幹分析器。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-112">updates all the word breakers and stemmers used by Full-Text Search and Semantic Search.</span></span> <span data-ttu-id="7cb6b-113">建議您重新擴展現有的全文檢索索引，以取得索引內容和查詢結果的一致性。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-113">For consistency between the contents of indexes and the results of queries, we recommend that you repopulate existing full-text indexes.</span></span>  
  
1.  <span data-ttu-id="7cb6b-114">目前有英文的新斷詞工具。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-114">There are new word breakers for English.</span></span> <span data-ttu-id="7cb6b-115">如果您必須保留舊版的行為，請參閱 [變更用於美式英文與英式英文的斷詞工具](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-115">If you have to retain the previous behavior, see [Change the Word Breaker Used for US English and UK English](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md).</span></span>  
  
2.  <span data-ttu-id="7cb6b-116">舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 隨附之丹麥文、波蘭文及土耳其文的協力廠商斷詞工具已取代為 [!INCLUDE[msCoName](../includes/msconame-md.md)] 元件。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-116">The third-party word breakers for Danish, Polish, and Turkish that were included with previous releases of [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] have been replaced with [!INCLUDE[msCoName](../includes/msconame-md.md)] components.</span></span> <span data-ttu-id="7cb6b-117">預設會啟用新元件。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-117">The new components are enabled by default.</span></span>  
  
3.  <span data-ttu-id="7cb6b-118">目前有捷克文和希臘文的新斷詞工具。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-118">There are new word breakers for Czech and Greek.</span></span> <span data-ttu-id="7cb6b-119">舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 全文檢索搜尋不支援這兩種語言。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-119">Previous releases of [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Full-Text Search did not include support for these two languages.</span></span>  
  
### <a name="behavior-changes-of-new-word-breakers-and-stemmers"></a><span data-ttu-id="7cb6b-120">新斷詞工具和字幹分析器的行為變更</span><span class="sxs-lookup"><span data-stu-id="7cb6b-120">Behavior Changes of New Word Breakers and Stemmers</span></span>  
 <span data-ttu-id="7cb6b-121">當您擴展及查詢全文檢索索引時，新元件可能會傳回與舊元件不同的結果。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-121">The new components might return different results than the older components when you populate and query full-text indexes.</span></span> <span data-ttu-id="7cb6b-122">下表示範英文結果中一些可預期的差異。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-122">The following tables demonstrate some of the differences that can be expected in English results.</span></span>  
  
 <span data-ttu-id="7cb6b-123">如果您必須保留舊版斷詞工具和字幹分析器的行為，請參閱以下主題：</span><span class="sxs-lookup"><span data-stu-id="7cb6b-123">If you have to retain the previous behavior of the word breakers and stemmers, see the following topics:</span></span>  
  
-   [<span data-ttu-id="7cb6b-124">變更用於美式英文與英式英文的斷詞工具</span><span class="sxs-lookup"><span data-stu-id="7cb6b-124">Change the Word Breaker Used for US English and UK English</span></span>](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
-   [<span data-ttu-id="7cb6b-125">將搜索所使用的斷詞工具還原為舊版</span><span class="sxs-lookup"><span data-stu-id="7cb6b-125">Revert the Word Breakers Used by Search to the Previous Version</span></span>](../relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
 <span data-ttu-id="7cb6b-126">在某些情況下，新元件會傳回「更多」\*\* 結果：</span><span class="sxs-lookup"><span data-stu-id="7cb6b-126">In some cases, the new components return *more* results:</span></span>  
  
|<span data-ttu-id="7cb6b-127">**字詞**</span><span class="sxs-lookup"><span data-stu-id="7cb6b-127">**Term**</span></span>|<span data-ttu-id="7cb6b-128">**舊版斷詞工具和字幹分析器的結果**</span><span class="sxs-lookup"><span data-stu-id="7cb6b-128">**Results with previous word breaker and stemmer**</span></span>|<span data-ttu-id="7cb6b-129">**新版斷詞工具和字幹分析器的結果**</span><span class="sxs-lookup"><span data-stu-id="7cb6b-129">**Results with new word breaker and stemmer**</span></span>|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|<span data-ttu-id="7cb6b-130">cat-dog</span><span class="sxs-lookup"><span data-stu-id="7cb6b-130">cat-dog</span></span>|<span data-ttu-id="7cb6b-131">cat</span><span class="sxs-lookup"><span data-stu-id="7cb6b-131">cat</span></span><br /><br /> <span data-ttu-id="7cb6b-132">dog</span><span class="sxs-lookup"><span data-stu-id="7cb6b-132">dog</span></span>|<span data-ttu-id="7cb6b-133">cat</span><span class="sxs-lookup"><span data-stu-id="7cb6b-133">cat</span></span><br /><br /> <span data-ttu-id="7cb6b-134">cat-dog</span><span class="sxs-lookup"><span data-stu-id="7cb6b-134">cat-dog</span></span><br /><br /> <span data-ttu-id="7cb6b-135">dog</span><span class="sxs-lookup"><span data-stu-id="7cb6b-135">dog</span></span>|  
|cat@dog.com|<span data-ttu-id="7cb6b-136">cat</span><span class="sxs-lookup"><span data-stu-id="7cb6b-136">cat</span></span><br /><br /> <span data-ttu-id="7cb6b-137">com</span><span class="sxs-lookup"><span data-stu-id="7cb6b-137">com</span></span><br /><br /> <span data-ttu-id="7cb6b-138">dog</span><span class="sxs-lookup"><span data-stu-id="7cb6b-138">dog</span></span>|<span data-ttu-id="7cb6b-139">cat</span><span class="sxs-lookup"><span data-stu-id="7cb6b-139">cat</span></span><br /><br /> cat@dog.com<br /><br /> <span data-ttu-id="7cb6b-140">com</span><span class="sxs-lookup"><span data-stu-id="7cb6b-140">com</span></span><br /><br /> <span data-ttu-id="7cb6b-141">dog</span><span class="sxs-lookup"><span data-stu-id="7cb6b-141">dog</span></span>|  
|<span data-ttu-id="7cb6b-142">12/11/2011</span><span class="sxs-lookup"><span data-stu-id="7cb6b-142">12/11/2011</span></span><br /><br /> <span data-ttu-id="7cb6b-143">*(其中詞彙是日期)*</span><span class="sxs-lookup"><span data-stu-id="7cb6b-143">*(where the term is a date)*</span></span>|<span data-ttu-id="7cb6b-144">12/11/2011</span><span class="sxs-lookup"><span data-stu-id="7cb6b-144">12/11/2011</span></span><br /><br /> <span data-ttu-id="7cb6b-145">dd20111211</span><span class="sxs-lookup"><span data-stu-id="7cb6b-145">dd20111211</span></span>|<span data-ttu-id="7cb6b-146">11</span><span class="sxs-lookup"><span data-stu-id="7cb6b-146">11</span></span><br /><br /> <span data-ttu-id="7cb6b-147">12</span><span class="sxs-lookup"><span data-stu-id="7cb6b-147">12</span></span><br /><br /> <span data-ttu-id="7cb6b-148">12/11/2011</span><span class="sxs-lookup"><span data-stu-id="7cb6b-148">12/11/2011</span></span><br /><br /> <span data-ttu-id="7cb6b-149">2011</span><span class="sxs-lookup"><span data-stu-id="7cb6b-149">2011</span></span><br /><br /> <span data-ttu-id="7cb6b-150">dd20111211</span><span class="sxs-lookup"><span data-stu-id="7cb6b-150">dd20111211</span></span>|  
  
 <span data-ttu-id="7cb6b-151">在某些情況下，新元件會傳回「類似」\*\* 的結果：</span><span class="sxs-lookup"><span data-stu-id="7cb6b-151">In some cases, the new components return *similar* results:</span></span>  
  
|<span data-ttu-id="7cb6b-152">**字詞**</span><span class="sxs-lookup"><span data-stu-id="7cb6b-152">**Term**</span></span>|<span data-ttu-id="7cb6b-153">**舊版斷詞工具和字幹分析器的結果**</span><span class="sxs-lookup"><span data-stu-id="7cb6b-153">**Results with previous word breaker and stemmer**</span></span>|<span data-ttu-id="7cb6b-154">**新版斷詞工具和字幹分析器的結果**</span><span class="sxs-lookup"><span data-stu-id="7cb6b-154">**Results with new word breaker and stemmer**</span></span>|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|<span data-ttu-id="7cb6b-155">100$</span><span class="sxs-lookup"><span data-stu-id="7cb6b-155">100$</span></span>|<span data-ttu-id="7cb6b-156">100$</span><span class="sxs-lookup"><span data-stu-id="7cb6b-156">100$</span></span><br /><br /> <span data-ttu-id="7cb6b-157">nn100$</span><span class="sxs-lookup"><span data-stu-id="7cb6b-157">nn100$</span></span>|<span data-ttu-id="7cb6b-158">100$</span><span class="sxs-lookup"><span data-stu-id="7cb6b-158">100$</span></span><br /><br /> <span data-ttu-id="7cb6b-159">nn100usd</span><span class="sxs-lookup"><span data-stu-id="7cb6b-159">nn100usd</span></span>|  
|<span data-ttu-id="7cb6b-160">022</span><span class="sxs-lookup"><span data-stu-id="7cb6b-160">022</span></span>|<span data-ttu-id="7cb6b-161">022</span><span class="sxs-lookup"><span data-stu-id="7cb6b-161">022</span></span><br /><br /> <span data-ttu-id="7cb6b-162">nn022</span><span class="sxs-lookup"><span data-stu-id="7cb6b-162">nn022</span></span>|<span data-ttu-id="7cb6b-163">022</span><span class="sxs-lookup"><span data-stu-id="7cb6b-163">022</span></span><br /><br /> <span data-ttu-id="7cb6b-164">nn22</span><span class="sxs-lookup"><span data-stu-id="7cb6b-164">nn22</span></span>|  
|<span data-ttu-id="7cb6b-165">10:49AM</span><span class="sxs-lookup"><span data-stu-id="7cb6b-165">10:49AM</span></span><br /><br /> <span data-ttu-id="7cb6b-166">*(其中詞彙是時間)*</span><span class="sxs-lookup"><span data-stu-id="7cb6b-166">*(where the term is a time)*</span></span>|<span data-ttu-id="7cb6b-167">10:49AM</span><span class="sxs-lookup"><span data-stu-id="7cb6b-167">10:49am</span></span><br /><br /> <span data-ttu-id="7cb6b-168">tt1049</span><span class="sxs-lookup"><span data-stu-id="7cb6b-168">tt1049</span></span>|<span data-ttu-id="7cb6b-169">10:49AM</span><span class="sxs-lookup"><span data-stu-id="7cb6b-169">10:49am</span></span><br /><br /> <span data-ttu-id="7cb6b-170">tt24104900</span><span class="sxs-lookup"><span data-stu-id="7cb6b-170">tt24104900</span></span>|  
  
 <span data-ttu-id="7cb6b-171">在某些情況下，新元件會傳回「較少」\*\* 結果或應用程式可能未預期的結果：</span><span class="sxs-lookup"><span data-stu-id="7cb6b-171">In some cases the new components return *fewer* results or results that may be unexpected by applications:</span></span>  
  
|<span data-ttu-id="7cb6b-172">**字詞**</span><span class="sxs-lookup"><span data-stu-id="7cb6b-172">**Term**</span></span>|<span data-ttu-id="7cb6b-173">**舊版斷詞工具和字幹分析器的結果**</span><span class="sxs-lookup"><span data-stu-id="7cb6b-173">**Results with previous word breaker and stemmer**</span></span>|<span data-ttu-id="7cb6b-174">**新版斷詞工具和字幹分析器的結果**</span><span class="sxs-lookup"><span data-stu-id="7cb6b-174">**Results with new word breaker and stemmer**</span></span>|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|<span data-ttu-id="7cb6b-175">jěˊÿｑℭžl</span><span class="sxs-lookup"><span data-stu-id="7cb6b-175">jěˊÿｑℭžl</span></span><br /><br /> <span data-ttu-id="7cb6b-176">*(其中詞彙不是有效的英文字元)*</span><span class="sxs-lookup"><span data-stu-id="7cb6b-176">*(where the terms are not valid English characters)*</span></span>|<span data-ttu-id="7cb6b-177">'jěˊÿｑℭžl'</span><span class="sxs-lookup"><span data-stu-id="7cb6b-177">'jěˊÿｑℭžl'</span></span>|<span data-ttu-id="7cb6b-178">je yq zl</span><span class="sxs-lookup"><span data-stu-id="7cb6b-178">je yq zl</span></span>|  
|<span data-ttu-id="7cb6b-179">table's</span><span class="sxs-lookup"><span data-stu-id="7cb6b-179">table's</span></span>|<span data-ttu-id="7cb6b-180">table's</span><span class="sxs-lookup"><span data-stu-id="7cb6b-180">table's</span></span><br /><br /> <span data-ttu-id="7cb6b-181">資料表</span><span class="sxs-lookup"><span data-stu-id="7cb6b-181">table</span></span>|<span data-ttu-id="7cb6b-182">table's</span><span class="sxs-lookup"><span data-stu-id="7cb6b-182">table's</span></span>|  
|<span data-ttu-id="7cb6b-183">cat-</span><span class="sxs-lookup"><span data-stu-id="7cb6b-183">cat-</span></span>|<span data-ttu-id="7cb6b-184">cat</span><span class="sxs-lookup"><span data-stu-id="7cb6b-184">cat</span></span><br /><br /> <span data-ttu-id="7cb6b-185">cat-</span><span class="sxs-lookup"><span data-stu-id="7cb6b-185">cat-</span></span>|<span data-ttu-id="7cb6b-186">cat</span><span class="sxs-lookup"><span data-stu-id="7cb6b-186">cat</span></span>|  
|<span data-ttu-id="7cb6b-187">v-z (其中 v 和 z 是非搜尋字)\*\*</span><span class="sxs-lookup"><span data-stu-id="7cb6b-187">v-z *(where v and z are noise words)*</span></span>|<span data-ttu-id="7cb6b-188">\*不 (任何結果) \*</span><span class="sxs-lookup"><span data-stu-id="7cb6b-188">*(no results)*</span></span>|<span data-ttu-id="7cb6b-189">v-z</span><span class="sxs-lookup"><span data-stu-id="7cb6b-189">v-z</span></span>|  
|<span data-ttu-id="7cb6b-190">$100 000 USD</span><span class="sxs-lookup"><span data-stu-id="7cb6b-190">$100 000 USD</span></span>|<span data-ttu-id="7cb6b-191">$100</span><span class="sxs-lookup"><span data-stu-id="7cb6b-191">$100</span></span><br /><br /> <span data-ttu-id="7cb6b-192">000</span><span class="sxs-lookup"><span data-stu-id="7cb6b-192">000</span></span><br /><br /> <span data-ttu-id="7cb6b-193">nn000</span><span class="sxs-lookup"><span data-stu-id="7cb6b-193">nn000</span></span><br /><br /> <span data-ttu-id="7cb6b-194">nn100$</span><span class="sxs-lookup"><span data-stu-id="7cb6b-194">nn100$</span></span><br /><br /> <span data-ttu-id="7cb6b-195">usd</span><span class="sxs-lookup"><span data-stu-id="7cb6b-195">usd</span></span>|<span data-ttu-id="7cb6b-196">$100 000 USD</span><span class="sxs-lookup"><span data-stu-id="7cb6b-196">$100 000 usd</span></span><br /><br /> <span data-ttu-id="7cb6b-197">nn100000usd</span><span class="sxs-lookup"><span data-stu-id="7cb6b-197">nn100000usd</span></span>|  
|<span data-ttu-id="7cb6b-198">beautiful U.S land</span><span class="sxs-lookup"><span data-stu-id="7cb6b-198">beautiful U.S land</span></span>|<span data-ttu-id="7cb6b-199">beautiful</span><span class="sxs-lookup"><span data-stu-id="7cb6b-199">beautiful</span></span><br /><br /> <span data-ttu-id="7cb6b-200">land</span><span class="sxs-lookup"><span data-stu-id="7cb6b-200">land</span></span><br /><br /> <span data-ttu-id="7cb6b-201">u.s</span><span class="sxs-lookup"><span data-stu-id="7cb6b-201">u.s</span></span><br /><br /> <span data-ttu-id="7cb6b-202">us</span><span class="sxs-lookup"><span data-stu-id="7cb6b-202">us</span></span>|<span data-ttu-id="7cb6b-203">beautiful</span><span class="sxs-lookup"><span data-stu-id="7cb6b-203">beautiful</span></span><br /><br /> <span data-ttu-id="7cb6b-204">land</span><span class="sxs-lookup"><span data-stu-id="7cb6b-204">land</span></span>|  
|<span data-ttu-id="7cb6b-205">Mt.</span><span class="sxs-lookup"><span data-stu-id="7cb6b-205">Mt.</span></span> <span data-ttu-id="7cb6b-206">Kent and Mt Challenger</span><span class="sxs-lookup"><span data-stu-id="7cb6b-206">Kent and Mt Challenger</span></span>|<span data-ttu-id="7cb6b-207">challenger</span><span class="sxs-lookup"><span data-stu-id="7cb6b-207">challenger</span></span><br /><br /> <span data-ttu-id="7cb6b-208">kent</span><span class="sxs-lookup"><span data-stu-id="7cb6b-208">kent</span></span><br /><br /> <span data-ttu-id="7cb6b-209">mt</span><span class="sxs-lookup"><span data-stu-id="7cb6b-209">mt</span></span><br /><br /> <span data-ttu-id="7cb6b-210">Mt.</span><span class="sxs-lookup"><span data-stu-id="7cb6b-210">mt.</span></span>|<span data-ttu-id="7cb6b-211">mt</span><span class="sxs-lookup"><span data-stu-id="7cb6b-211">mt</span></span><br /><br /> <span data-ttu-id="7cb6b-212">kent</span><span class="sxs-lookup"><span data-stu-id="7cb6b-212">kent</span></span><br /><br /> <span data-ttu-id="7cb6b-213">challenger</span><span class="sxs-lookup"><span data-stu-id="7cb6b-213">challenger</span></span>|  
  
## <a name="behavior-changes-in-full-text-search-in-sql-server-2008"></a><span data-ttu-id="7cb6b-214">SQL Server 2008 中全文檢索搜尋的行為變更</span><span class="sxs-lookup"><span data-stu-id="7cb6b-214">Behavior Changes in Full-Text Search in SQL Server 2008</span></span>  
 <span data-ttu-id="7cb6b-215">在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 和更新的版本中，全文檢索引擎會以資料庫服務的形式整合至關係資料庫中，成為伺服器查詢和儲存引擎基礎結構的一部分。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-215">In [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] and later versions, the Full-Text Engine is integrated as a database service into the relational database as part of the server query and storage engine infrastructure.</span></span> <span data-ttu-id="7cb6b-216">新的全文檢索搜尋架構可達成下列目標：</span><span class="sxs-lookup"><span data-stu-id="7cb6b-216">The new full-text search architecture achieves the following goals:</span></span>  
  
-   <span data-ttu-id="7cb6b-217">整合式儲存與管理-全文檢索搜尋現在直接與的固有儲存體和管理功能整合 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，而 MSFTESQL 服務已不存在。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-217">Integrated storage and management-Full-text search is now integrated directly with the inherent storage and management features of [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], and the MSFTESQL service no longer exists.</span></span>  
  
    -   <span data-ttu-id="7cb6b-218">全文檢索索引會儲存在資料庫檔案群組內部，而非儲存在檔案系統中。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-218">Full-text indexes are stored inside the database filegroups, rather than in the file system.</span></span> <span data-ttu-id="7cb6b-219">資料庫的管理作業 (例如建立備份) 會自動影響其全文檢索索引。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-219">Administrative operations on a database, such as creating a backup, automatically affect its full-text indexes.</span></span>  
  
    -   <span data-ttu-id="7cb6b-220">全文檢索目錄現在是不屬於任何檔案群組的虛擬物件。它是參考一組全文檢索索引的邏輯概念。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-220">A full-text catalog is now a virtual object that does not belong to any filegroup; it is a logical concept that refers to a group of full-text indexes.</span></span> <span data-ttu-id="7cb6b-221">因此，許多目錄管理功能都已經被取代，而且這項取代已經針對某些功能建立重大變更。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-221">Therefore, many catalog-management features have been deprecated, and deprecation has created breaking changes for some features.</span></span> <span data-ttu-id="7cb6b-222">如需詳細資訊，請參閱[SQL Server 2014 中的已淘汰資料庫引擎功能](deprecated-database-engine-features-in-sql-server-2016.md)和[全文檢索搜尋的重大變更](breaking-changes-to-full-text-search.md)。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-222">For more information, see [Deprecated Database Engine Features in SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md) and [Breaking Changes to Full-Text Search](breaking-changes-to-full-text-search.md).</span></span>  
  
        > [!NOTE]  
        >  [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]<span data-ttu-id="7cb6b-223">[!INCLUDE[tsql](../includes/tsql-md.md)]指定全文檢索目錄正常運作的 DDL 語句。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-223">[!INCLUDE[tsql](../includes/tsql-md.md)] DDL statements that specify full-text catalogs work correctly.</span></span>  
  
-   <span data-ttu-id="7cb6b-224">整合式查詢處理-新的全文檢索搜尋查詢處理器是資料庫引擎的一部分，而且已與 SQL Server 查詢處理器完全整合。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-224">Integrated query processing-The new full-text search query processor is part of the Database Engine and is fully integrated with the SQL Server Query processor.</span></span> <span data-ttu-id="7cb6b-225">這表示，查詢最佳化工具會辨識全文檢索查詢述詞並且盡可能有效率地自動執行它們。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-225">This means that, the query optimizer recognizes full-text query predicates and automatically executes them as efficiently as possible.</span></span>  
  
-   <span data-ttu-id="7cb6b-226">增強式管理和疑難排解-整合的全文檢索搜尋提供的工具可協助您分析搜尋結構，例如全文檢索索引、給定斷詞工具的輸出、停用字詞設定等等。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-226">Enhanced administration and troubleshooting-Integrated full-text search provides tools to help you analyze search structures such as the full-text index, the output of a given word breaker, stopword configuration, and so forth.</span></span>  
  
-   <span data-ttu-id="7cb6b-227">停用字詞和停用字詞表已經取代了非搜尋字和非搜尋字檔案。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-227">Stopwords and stoplists have replaced noise words and noise-word files.</span></span> <span data-ttu-id="7cb6b-228">停用字詞表是一個資料庫物件，可加快停用字詞管理工作的速度並且改善不同伺服器執行個體與環境之間的完整性。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-228">A stoplist is a database object that facilitates manageability tasks for stopwords and improves the integrity between different server instances and environments.</span></span> <span data-ttu-id="7cb6b-229">如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-229">For more information, see [Configure and Manage Stopwords and Stoplists for Full-Text Search](../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).</span></span>  
  
-   [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] <span data-ttu-id="7cb6b-230">和更新的版本包含 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 中許多語言的新斷詞工具。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-230">and later versions include new word breakers for many of the languages that exist in [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)].</span></span> <span data-ttu-id="7cb6b-231">只有英文、韓文、泰文和中文 (所有形式) 的斷詞工具維持原狀。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-231">Only the word breakers for English, Korean, Thai, and Chinese (all forms) remain the same.</span></span> <span data-ttu-id="7cb6b-232">對於其他語言，如果全文檢索目錄是在 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 資料庫升級為 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 或更新版本時匯入，則全文檢索目錄中的全文檢索索引所使用的一或多個語言現在可能會與新的斷詞工具相關聯，其行為可能與匯入的斷詞工具有些許不同。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-232">For other languages, if a full-text catalog was imported when a [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] database was upgraded to [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] or a later version, one or more languages used by the full-text indexes in full-text catalog might now be associated with new word breakers that might behave slightly differently from the imported word breakers.</span></span> <span data-ttu-id="7cb6b-233">如需有關如何確保查詢與全文檢索索引內容之間一致性的詳細資訊，請參閱[升級全文檢索搜尋](../relational-databases/search/upgrade-full-text-search.md)。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-233">For more information about how to ensure consistency between queries and the full-text index content, see [Upgrade Full-Text Search](../relational-databases/search/upgrade-full-text-search.md).</span></span>  
  
-   <span data-ttu-id="7cb6b-234">加入了新的 FDHOST Launcher (MSSQLFDLauncher) 服務。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-234">A new FDHOST Launcher (MSSQLFDLauncher) service has been added.</span></span> <span data-ttu-id="7cb6b-235">如需詳細資訊，請參閱[開始使用全文檢索搜尋](../relational-databases/search/get-started-with-full-text-search.md)。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-235">For more information, see [Get Started with Full-Text Search](../relational-databases/search/get-started-with-full-text-search.md).</span></span>  
  
-   <span data-ttu-id="7cb6b-236">全文檢索索引的運作方式與[FILESTREAM](../relational-databases/blob/filestream-sql-server.md)資料行相同，方法與資料 `varbinary(max)` 行相同。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-236">Full-text indexing works with a [FILESTREAM](../relational-databases/blob/filestream-sql-server.md) column in the same way that it does with a `varbinary(max)` column.</span></span> <span data-ttu-id="7cb6b-237">FILESTREAM 資料表必須有一個資料行包含每一個 FILESTREAM BLOB 的副檔名。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-237">The FILESTREAM table must have a column that contains the file name extension for each FILESTREAM BLOB.</span></span> <span data-ttu-id="7cb6b-238">如需詳細資訊，請參閱[使用全文檢索搜尋進行查詢](../relational-databases/search/query-with-full-text-search.md)、[設定及管理搜尋的篩選](../relational-databases/search/configure-and-manage-filters-for-search.md)，以及[fulltext_document_types &#40;transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-238">For more information, see [Query with Full-Text Search](../relational-databases/search/query-with-full-text-search.md),[Configure and Manage Filters for Search](../relational-databases/search/configure-and-manage-filters-for-search.md), and [sys.fulltext_document_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql).</span></span>  
  
     <span data-ttu-id="7cb6b-239">全文檢索引擎會針對 FILESTREAM BLOB 的內容建立索引。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-239">The full-text engine indexes the contents of the FILESTREAM BLOBs.</span></span> <span data-ttu-id="7cb6b-240">為檔案 (如影像) 建立索引可能不會很實用。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-240">Indexing files such as images might not be useful.</span></span> <span data-ttu-id="7cb6b-241">當更新 FILESTREAM BLOB 時，會為它重新建立索引。</span><span class="sxs-lookup"><span data-stu-id="7cb6b-241">When a FILESTREAM BLOB is updated it is reindexed.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7cb6b-242">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7cb6b-242">See Also</span></span>  
 <span data-ttu-id="7cb6b-243">[全文檢索搜尋](../relational-databases/search/full-text-search.md) </span><span class="sxs-lookup"><span data-stu-id="7cb6b-243">[Full-Text Search](../relational-databases/search/full-text-search.md) </span></span>  
 <span data-ttu-id="7cb6b-244">[全文檢索搜尋回溯相容性](../../2014/database-engine/full-text-search-backward-compatibility.md) </span><span class="sxs-lookup"><span data-stu-id="7cb6b-244">[Full-Text Search Backward Compatibility](../../2014/database-engine/full-text-search-backward-compatibility.md) </span></span>  
 <span data-ttu-id="7cb6b-245">[升級全文檢索搜尋](../relational-databases/search/upgrade-full-text-search.md) </span><span class="sxs-lookup"><span data-stu-id="7cb6b-245">[Upgrade Full-Text Search](../relational-databases/search/upgrade-full-text-search.md) </span></span>  
 [<span data-ttu-id="7cb6b-246">全文檢索搜尋使用者入門</span><span class="sxs-lookup"><span data-stu-id="7cb6b-246">Get Started with Full-Text Search</span></span>](../relational-databases/search/get-started-with-full-text-search.md)  
  
  