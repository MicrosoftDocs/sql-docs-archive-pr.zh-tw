---
title: 日期和時間以及結構描述資料列集 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], schema rowsets
ms.assetid: 8c35e86f-0597-4ef4-b2b8-f643e53ed4c2
author: rothja
ms.author: jroth
ms.openlocfilehash: 71a54cd1d40101b48a0e02fc4b6a6343b04fe185
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707481"
---
# <a name="date-and-time-and-schema-rowsets"></a><span data-ttu-id="16781-102">日期和時間與架構資料列集</span><span class="sxs-lookup"><span data-stu-id="16781-102">Date and Time and Schema Rowsets</span></span>
  <span data-ttu-id="16781-103">本主題提供有關 COLUMNS 資料列集和 PROCEDURE_PARAMETERS 資料列集的資訊。</span><span class="sxs-lookup"><span data-stu-id="16781-103">This topic provides information about COLUMNS rowset and PROCEDURE_PARAMETERS rowset.</span></span> <span data-ttu-id="16781-104">這項資訊與 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中引進的 OLE DB 日期和時間增強功能相關。</span><span class="sxs-lookup"><span data-stu-id="16781-104">This information relates to the OLE DB date and time enhancements introduced in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].</span></span>  
  
## <a name="columns-rowset"></a><span data-ttu-id="16781-105">COLUMNS 資料列集</span><span class="sxs-lookup"><span data-stu-id="16781-105">COLUMNS Rowset</span></span>  
 <span data-ttu-id="16781-106">系統會傳回日期/時間類型的下列資料行值：</span><span class="sxs-lookup"><span data-stu-id="16781-106">The following column values are returned for date/time types:</span></span>  
  
|<span data-ttu-id="16781-107">資料行類型</span><span class="sxs-lookup"><span data-stu-id="16781-107">Column Type</span></span>|<span data-ttu-id="16781-108">DATA_TYPE</span><span class="sxs-lookup"><span data-stu-id="16781-108">DATA_TYPE</span></span>|<span data-ttu-id="16781-109">COLUMN_FLAGS、DBCOLUMFLAGS_SS_ISVARIABLESCALE</span><span class="sxs-lookup"><span data-stu-id="16781-109">COLUMN_FLAGS, DBCOLUMFLAGS_SS_ISVARIABLESCALE</span></span>|<span data-ttu-id="16781-110">DATETIME_PRECISION</span><span class="sxs-lookup"><span data-stu-id="16781-110">DATETIME_PRECISION</span></span>|  
|-----------------|----------------|------------------------------------------------------|-------------------------|  
|<span data-ttu-id="16781-111">date</span><span class="sxs-lookup"><span data-stu-id="16781-111">date</span></span>|<span data-ttu-id="16781-112">DBTYPE_DBDATE</span><span class="sxs-lookup"><span data-stu-id="16781-112">DBTYPE_DBDATE</span></span>|<span data-ttu-id="16781-113">清除</span><span class="sxs-lookup"><span data-stu-id="16781-113">Clear</span></span>|<span data-ttu-id="16781-114">0</span><span class="sxs-lookup"><span data-stu-id="16781-114">0</span></span>|  
|<span data-ttu-id="16781-115">time</span><span class="sxs-lookup"><span data-stu-id="16781-115">time</span></span>|<span data-ttu-id="16781-116">DBTYPE_DBTIME2</span><span class="sxs-lookup"><span data-stu-id="16781-116">DBTYPE_DBTIME2</span></span>|<span data-ttu-id="16781-117">設定</span><span class="sxs-lookup"><span data-stu-id="16781-117">Set</span></span>|<span data-ttu-id="16781-118">0..7</span><span class="sxs-lookup"><span data-stu-id="16781-118">0..7</span></span>|  
|<span data-ttu-id="16781-119">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="16781-119">smalldatetime</span></span>|<span data-ttu-id="16781-120">DBTYPE_DBTIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="16781-120">DBTYPE_DBTIMESTAMP</span></span>|<span data-ttu-id="16781-121">清除</span><span class="sxs-lookup"><span data-stu-id="16781-121">Clear</span></span>|<span data-ttu-id="16781-122">0</span><span class="sxs-lookup"><span data-stu-id="16781-122">0</span></span>|  
|<span data-ttu-id="16781-123">Datetime</span><span class="sxs-lookup"><span data-stu-id="16781-123">datetime</span></span>|<span data-ttu-id="16781-124">DBTYPE_DBTIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="16781-124">DBTYPE_DBTIMESTAMP</span></span>|<span data-ttu-id="16781-125">清除</span><span class="sxs-lookup"><span data-stu-id="16781-125">Clear</span></span>|<span data-ttu-id="16781-126">3</span><span class="sxs-lookup"><span data-stu-id="16781-126">3</span></span>|  
|<span data-ttu-id="16781-127">datetime2</span><span class="sxs-lookup"><span data-stu-id="16781-127">datetime2</span></span>|<span data-ttu-id="16781-128">DBTYPE_DBTIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="16781-128">DBTYPE_DBTIMESTAMP</span></span>|<span data-ttu-id="16781-129">設定</span><span class="sxs-lookup"><span data-stu-id="16781-129">Set</span></span>|<span data-ttu-id="16781-130">0..7</span><span class="sxs-lookup"><span data-stu-id="16781-130">0..7</span></span>|  
|<span data-ttu-id="16781-131">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="16781-131">datetimeoffset</span></span>|<span data-ttu-id="16781-132">DBTYPE_DBTIMESTAMPOFFSET</span><span class="sxs-lookup"><span data-stu-id="16781-132">DBTYPE_DBTIMESTAMPOFFSET</span></span>|<span data-ttu-id="16781-133">設定</span><span class="sxs-lookup"><span data-stu-id="16781-133">Set</span></span>|<span data-ttu-id="16781-134">0..7</span><span class="sxs-lookup"><span data-stu-id="16781-134">0..7</span></span>|  
  
 <span data-ttu-id="16781-135">在 COLUMN_FLAGS 中，DBCOLUMNFLAGS_ISFIXEDLENGTH 對 date/time 類型永遠為 true，而且下列旗標永遠為 false：</span><span class="sxs-lookup"><span data-stu-id="16781-135">In COLUMN_FLAGS, DBCOLUMNFLAGS_ISFIXEDLENGTH is always true for date/time types and the following flags are always false:</span></span>  
  
-   <span data-ttu-id="16781-136">DBCOLUMNFLAGS_CACHEDEFERRED</span><span class="sxs-lookup"><span data-stu-id="16781-136">DBCOLUMNFLAGS_CACHEDEFERRED</span></span>  
  
-   <span data-ttu-id="16781-137">DBCOLUMNFLAGS_ISBOOKMARK</span><span class="sxs-lookup"><span data-stu-id="16781-137">DBCOLUMNFLAGS_ISBOOKMARK</span></span>  
  
-   <span data-ttu-id="16781-138">DBCOLUMNFLAGS_ISCHAPTER</span><span class="sxs-lookup"><span data-stu-id="16781-138">DBCOLUMNFLAGS_ISCHAPTER</span></span>  
  
-   <span data-ttu-id="16781-139">DBCOLUMNFLAGS_ISLONG</span><span class="sxs-lookup"><span data-stu-id="16781-139">DBCOLUMNFLAGS_ISLONG</span></span>  
  
-   <span data-ttu-id="16781-140">DBCOLUMNFLAGS_ISROWID</span><span class="sxs-lookup"><span data-stu-id="16781-140">DBCOLUMNFLAGS_ISROWID</span></span>  
  
-   <span data-ttu-id="16781-141">DBCOLUMNFLAGS_ISROWVER</span><span class="sxs-lookup"><span data-stu-id="16781-141">DBCOLUMNFLAGS_ISROWVER</span></span>  
  
-   <span data-ttu-id="16781-142">DBCOLUMNFLAGS_MAYDEFER</span><span class="sxs-lookup"><span data-stu-id="16781-142">DBCOLUMNFLAGS_MAYDEFER</span></span>  
  
 <span data-ttu-id="16781-143">剩餘的旗標 (DBCOLUMNFLAGS_ISNULLABLE、DBCOLUMNFLAGS_MAYBENULL、DBCOLUMNFLAGS_WRITE 和 DBCOLUMNFLAGS_WRITEUNKNOWN) 可以根據資料行的定義方式來設定。</span><span class="sxs-lookup"><span data-stu-id="16781-143">The remaining flags (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE, and DBCOLUMNFLAGS_WRITEUNKNOWN) might be set, depending on how the column is defined.</span></span>  
  
 <span data-ttu-id="16781-144">在 COLUMN_FLAGS 中會提供新旗標 DBCOLUMNFLAGS_SS_ISVARIABLESCALE，以允許應用程式判斷資料行的伺服器類型，其中 DATA_TYPE 是 DBTYPE_DBTIMESTAMP。</span><span class="sxs-lookup"><span data-stu-id="16781-144">A new flag, DBCOLUMNFLAGS_SS_ISVARIABLESCALE, is provided in COLUMN_FLAGS to allow an application to determine the server type of columns where DATA_TYPE is DBTYPE_DBTIMESTAMP.</span></span> <span data-ttu-id="16781-145">DATETIME_PRECISION 也必須用來識別伺服器類型。</span><span class="sxs-lookup"><span data-stu-id="16781-145">DATETIME_PRECISION must also be used to identify the server type.</span></span>  
  
 <span data-ttu-id="16781-146">只有連接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本的伺服器時，DBCOLUMNFLAGS_SS_ISVARIABLESCALE 才有效。</span><span class="sxs-lookup"><span data-stu-id="16781-146">DBCOLUMNFLAGS_SS_ISVARIABLESCALE is only valid when connected to a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] or later server.</span></span> <span data-ttu-id="16781-147">連接到下層伺服器時，不會定義 DBCOLUMNFLAGS_SS_ISFIXEDSCALE。</span><span class="sxs-lookup"><span data-stu-id="16781-147">DBCOLUMNFLAGS_SS_ISFIXEDSCALE is undefined when connected to down-level servers.</span></span>  
  
## <a name="procedure_parameters-rowset"></a><span data-ttu-id="16781-148">PROCEDURE_PARAMETERS 資料列集</span><span class="sxs-lookup"><span data-stu-id="16781-148">PROCEDURE_PARAMETERS Rowset</span></span>  
 <span data-ttu-id="16781-149">DATA_TYPE 包含與 COLUMNS 結構描述資料列集相同的值，而 TYPE_NAME 包含伺服器類型。</span><span class="sxs-lookup"><span data-stu-id="16781-149">DATA_TYPE contains the same values as the COLUMNS schema rowset and TYPE_NAME contains the server type.</span></span>  
  
 <span data-ttu-id="16781-150">已經加入新的資料行 SS_DATETIME_PRECISION，以傳回與 DATETIME_PRECISION 資料行相同的類型，類似 COLUMNS 資料列集。</span><span class="sxs-lookup"><span data-stu-id="16781-150">A new column, SS_DATETIME_PRECISION, has been added to return the precision of the type as in the DATETIME_PRECISION column, similar to the COLUMNS rowset.</span></span>  
  
## <a name="provider_types-rowset"></a><span data-ttu-id="16781-151">PROVIDER_TYPES 資料列集</span><span class="sxs-lookup"><span data-stu-id="16781-151">PROVIDER_TYPES Rowset</span></span>  
 <span data-ttu-id="16781-152">系統會傳回日期/時間類型的下列資料列：</span><span class="sxs-lookup"><span data-stu-id="16781-152">The following rows are returned for date/time types:</span></span>  
  
|<span data-ttu-id="16781-153">類型 -></span><span class="sxs-lookup"><span data-stu-id="16781-153">Type -></span></span><br /><br /> <span data-ttu-id="16781-154">資料行</span><span class="sxs-lookup"><span data-stu-id="16781-154">Column</span></span>|<span data-ttu-id="16781-155">date</span><span class="sxs-lookup"><span data-stu-id="16781-155">date</span></span>|<span data-ttu-id="16781-156">time</span><span class="sxs-lookup"><span data-stu-id="16781-156">time</span></span>|<span data-ttu-id="16781-157">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="16781-157">smalldatetime</span></span>|<span data-ttu-id="16781-158">Datetime</span><span class="sxs-lookup"><span data-stu-id="16781-158">datetime</span></span>|<span data-ttu-id="16781-159">datetime2</span><span class="sxs-lookup"><span data-stu-id="16781-159">datetime2</span></span>|<span data-ttu-id="16781-160">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="16781-160">datetimeoffset</span></span>|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|<span data-ttu-id="16781-161">TYPE_NAME</span><span class="sxs-lookup"><span data-stu-id="16781-161">TYPE_NAME</span></span>|<span data-ttu-id="16781-162">date</span><span class="sxs-lookup"><span data-stu-id="16781-162">date</span></span>|<span data-ttu-id="16781-163">time</span><span class="sxs-lookup"><span data-stu-id="16781-163">time</span></span>|<span data-ttu-id="16781-164">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="16781-164">smalldatetime</span></span>|<span data-ttu-id="16781-165">Datetime</span><span class="sxs-lookup"><span data-stu-id="16781-165">datetime</span></span>|<span data-ttu-id="16781-166">datetime2</span><span class="sxs-lookup"><span data-stu-id="16781-166">datetime2</span></span>|<span data-ttu-id="16781-167">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="16781-167">datetimeoffset</span></span>|  
|<span data-ttu-id="16781-168">DATA_TYPE</span><span class="sxs-lookup"><span data-stu-id="16781-168">DATA_TYPE</span></span>|<span data-ttu-id="16781-169">DBTYPE_DBDATE</span><span class="sxs-lookup"><span data-stu-id="16781-169">DBTYPE_DBDATE</span></span>|<span data-ttu-id="16781-170">DBTYPE_DBTIME2</span><span class="sxs-lookup"><span data-stu-id="16781-170">DBTYPE_DBTIME2</span></span>|<span data-ttu-id="16781-171">DBTYPE_DBTIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="16781-171">DBTYPE_DBTIMESTAMP</span></span>|<span data-ttu-id="16781-172">DBTYPE_DBTIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="16781-172">DBTYPE_DBTIMESTAMP</span></span>|<span data-ttu-id="16781-173">DBTYPE_DBTIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="16781-173">DBTYPE_DBTIMESTAMP</span></span>|<span data-ttu-id="16781-174">DBTYPE_DBTIMESTAMPOFFSET</span><span class="sxs-lookup"><span data-stu-id="16781-174">DBTYPE_DBTIMESTAMPOFFSET</span></span>|  
|<span data-ttu-id="16781-175">COLUMN_SIZE</span><span class="sxs-lookup"><span data-stu-id="16781-175">COLUMN_SIZE</span></span>|<span data-ttu-id="16781-176">10</span><span class="sxs-lookup"><span data-stu-id="16781-176">10</span></span>|<span data-ttu-id="16781-177">16</span><span class="sxs-lookup"><span data-stu-id="16781-177">16</span></span>|<span data-ttu-id="16781-178">16</span><span class="sxs-lookup"><span data-stu-id="16781-178">16</span></span>|<span data-ttu-id="16781-179">23</span><span class="sxs-lookup"><span data-stu-id="16781-179">23</span></span>|<span data-ttu-id="16781-180">27</span><span class="sxs-lookup"><span data-stu-id="16781-180">27</span></span>|<span data-ttu-id="16781-181">34</span><span class="sxs-lookup"><span data-stu-id="16781-181">34</span></span>|  
|<span data-ttu-id="16781-182">LITERAL_PREFIX</span><span class="sxs-lookup"><span data-stu-id="16781-182">LITERAL_PREFIX</span></span>|<span data-ttu-id="16781-183">'</span><span class="sxs-lookup"><span data-stu-id="16781-183">'</span></span>|<span data-ttu-id="16781-184">'</span><span class="sxs-lookup"><span data-stu-id="16781-184">'</span></span>|<span data-ttu-id="16781-185">'</span><span class="sxs-lookup"><span data-stu-id="16781-185">'</span></span>|<span data-ttu-id="16781-186">'</span><span class="sxs-lookup"><span data-stu-id="16781-186">'</span></span>|<span data-ttu-id="16781-187">'</span><span class="sxs-lookup"><span data-stu-id="16781-187">'</span></span>|<span data-ttu-id="16781-188">'</span><span class="sxs-lookup"><span data-stu-id="16781-188">'</span></span>|  
|<span data-ttu-id="16781-189">LITERAL_SUFFIX</span><span class="sxs-lookup"><span data-stu-id="16781-189">LITERAL_SUFFIX</span></span>|<span data-ttu-id="16781-190">'</span><span class="sxs-lookup"><span data-stu-id="16781-190">'</span></span>|<span data-ttu-id="16781-191">'</span><span class="sxs-lookup"><span data-stu-id="16781-191">'</span></span>|<span data-ttu-id="16781-192">'</span><span class="sxs-lookup"><span data-stu-id="16781-192">'</span></span>|<span data-ttu-id="16781-193">'</span><span class="sxs-lookup"><span data-stu-id="16781-193">'</span></span>|<span data-ttu-id="16781-194">'</span><span class="sxs-lookup"><span data-stu-id="16781-194">'</span></span>|<span data-ttu-id="16781-195">'</span><span class="sxs-lookup"><span data-stu-id="16781-195">'</span></span>|  
|<span data-ttu-id="16781-196">CREATE_PARAMS</span><span class="sxs-lookup"><span data-stu-id="16781-196">CREATE_PARAMS</span></span>|<span data-ttu-id="16781-197">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-197">NULL</span></span>|<span data-ttu-id="16781-198">級別</span><span class="sxs-lookup"><span data-stu-id="16781-198">scale</span></span>|<span data-ttu-id="16781-199">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-199">NULL</span></span>|<span data-ttu-id="16781-200">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-200">NULL</span></span>|<span data-ttu-id="16781-201">級別</span><span class="sxs-lookup"><span data-stu-id="16781-201">scale</span></span>|<span data-ttu-id="16781-202">級別</span><span class="sxs-lookup"><span data-stu-id="16781-202">scale</span></span>|  
|<span data-ttu-id="16781-203">IS_NULLABLE</span><span class="sxs-lookup"><span data-stu-id="16781-203">IS_NULLABLE</span></span>|<span data-ttu-id="16781-204">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-204">VARIANT_TRUE</span></span>|<span data-ttu-id="16781-205">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-205">VARIANT_TRUE</span></span>|<span data-ttu-id="16781-206">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-206">VARIANT_TRUE</span></span>|<span data-ttu-id="16781-207">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-207">VARIANT_TRUE</span></span>|<span data-ttu-id="16781-208">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-208">VARIANT_TRUE</span></span>|<span data-ttu-id="16781-209">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-209">VARIANT_TRUE</span></span>|  
|<span data-ttu-id="16781-210">CASE_SENSITIVE</span><span class="sxs-lookup"><span data-stu-id="16781-210">CASE_SENSITIVE</span></span>|<span data-ttu-id="16781-211">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-211">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-212">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-212">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-213">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-213">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-214">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-214">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-215">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-215">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-216">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-216">VARIANT_FALSE</span></span>|  
|<span data-ttu-id="16781-217">可搜尋</span><span class="sxs-lookup"><span data-stu-id="16781-217">SEARCHABLE</span></span>|<span data-ttu-id="16781-218">DB_SEARCHABLE</span><span class="sxs-lookup"><span data-stu-id="16781-218">DB_SEARCHABLE</span></span>|<span data-ttu-id="16781-219">DB_SEARCHABLE</span><span class="sxs-lookup"><span data-stu-id="16781-219">DB_SEARCHABLE</span></span>|<span data-ttu-id="16781-220">DB_SEARCHABLE</span><span class="sxs-lookup"><span data-stu-id="16781-220">DB_SEARCHABLE</span></span>|<span data-ttu-id="16781-221">DB_SEARCHABLE</span><span class="sxs-lookup"><span data-stu-id="16781-221">DB_SEARCHABLE</span></span>|<span data-ttu-id="16781-222">DB_SEARCHABLE</span><span class="sxs-lookup"><span data-stu-id="16781-222">DB_SEARCHABLE</span></span>|<span data-ttu-id="16781-223">DB_SEARCHABLE</span><span class="sxs-lookup"><span data-stu-id="16781-223">DB_SEARCHABLE</span></span>|  
|<span data-ttu-id="16781-224">UNSIGNED_ATTRIBUTE</span><span class="sxs-lookup"><span data-stu-id="16781-224">UNSIGNED_ATTRIBUTE</span></span>|<span data-ttu-id="16781-225">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-225">NULL</span></span>|<span data-ttu-id="16781-226">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-226">NULL</span></span>|<span data-ttu-id="16781-227">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-227">NULL</span></span>|<span data-ttu-id="16781-228">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-228">NULL</span></span>|<span data-ttu-id="16781-229">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-229">NULL</span></span>|<span data-ttu-id="16781-230">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-230">NULL</span></span>|  
|<span data-ttu-id="16781-231">FIXED_PREC_SCALE</span><span class="sxs-lookup"><span data-stu-id="16781-231">FIXED_PREC_SCALE</span></span>|<span data-ttu-id="16781-232">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-232">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-233">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-233">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-234">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-234">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-235">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-235">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-236">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-236">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-237">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-237">VARIANT_FALSE</span></span>|  
|<span data-ttu-id="16781-238">AUTO_UNIQUE_VALUE</span><span class="sxs-lookup"><span data-stu-id="16781-238">AUTO_UNIQUE_VALUE</span></span>|<span data-ttu-id="16781-239">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-239">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-240">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-240">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-241">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-241">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-242">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-242">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-243">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-243">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-244">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-244">VARIANT_FALSE</span></span>|  
|<span data-ttu-id="16781-245">LOCAL_TYPE_NAME</span><span class="sxs-lookup"><span data-stu-id="16781-245">LOCAL_TYPE_NAME</span></span>|<span data-ttu-id="16781-246">date</span><span class="sxs-lookup"><span data-stu-id="16781-246">date</span></span>|<span data-ttu-id="16781-247">time</span><span class="sxs-lookup"><span data-stu-id="16781-247">time</span></span>|<span data-ttu-id="16781-248">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="16781-248">smalldatetime</span></span>|<span data-ttu-id="16781-249">Datetime</span><span class="sxs-lookup"><span data-stu-id="16781-249">datetime</span></span>|<span data-ttu-id="16781-250">datetime2</span><span class="sxs-lookup"><span data-stu-id="16781-250">datetime2</span></span>|<span data-ttu-id="16781-251">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="16781-251">datetimeoffset</span></span>|  
|<span data-ttu-id="16781-252">MINIMUM_SCALE</span><span class="sxs-lookup"><span data-stu-id="16781-252">MINIMUM_SCALE</span></span>|<span data-ttu-id="16781-253">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-253">NULL</span></span>|<span data-ttu-id="16781-254">0</span><span class="sxs-lookup"><span data-stu-id="16781-254">0</span></span>|<span data-ttu-id="16781-255">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-255">NULL</span></span>|<span data-ttu-id="16781-256">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-256">NULL</span></span>|<span data-ttu-id="16781-257">0</span><span class="sxs-lookup"><span data-stu-id="16781-257">0</span></span>|<span data-ttu-id="16781-258">0</span><span class="sxs-lookup"><span data-stu-id="16781-258">0</span></span>|  
|<span data-ttu-id="16781-259">MAXIMUM_SCALE</span><span class="sxs-lookup"><span data-stu-id="16781-259">MAXIMUM_SCALE</span></span>|<span data-ttu-id="16781-260">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-260">NULL</span></span>|<span data-ttu-id="16781-261">7</span><span class="sxs-lookup"><span data-stu-id="16781-261">7</span></span>|<span data-ttu-id="16781-262">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-262">NULL</span></span>|<span data-ttu-id="16781-263">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-263">NULL</span></span>|<span data-ttu-id="16781-264">7</span><span class="sxs-lookup"><span data-stu-id="16781-264">7</span></span>|<span data-ttu-id="16781-265">7</span><span class="sxs-lookup"><span data-stu-id="16781-265">7</span></span>|  
|<span data-ttu-id="16781-266">GUID</span><span class="sxs-lookup"><span data-stu-id="16781-266">GUID</span></span>|<span data-ttu-id="16781-267">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-267">NULL</span></span>|<span data-ttu-id="16781-268">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-268">NULL</span></span>|<span data-ttu-id="16781-269">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-269">NULL</span></span>|<span data-ttu-id="16781-270">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-270">NULL</span></span>|<span data-ttu-id="16781-271">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-271">NULL</span></span>|<span data-ttu-id="16781-272">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-272">NULL</span></span>|  
|<span data-ttu-id="16781-273">TYPELIB</span><span class="sxs-lookup"><span data-stu-id="16781-273">TYPELIB</span></span>|<span data-ttu-id="16781-274">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-274">NULL</span></span>|<span data-ttu-id="16781-275">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-275">NULL</span></span>|<span data-ttu-id="16781-276">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-276">NULL</span></span>|<span data-ttu-id="16781-277">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-277">NULL</span></span>|<span data-ttu-id="16781-278">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-278">NULL</span></span>|<span data-ttu-id="16781-279">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-279">NULL</span></span>|  
|<span data-ttu-id="16781-280">VERSION</span><span class="sxs-lookup"><span data-stu-id="16781-280">VERSION</span></span>|<span data-ttu-id="16781-281">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-281">NULL</span></span>|<span data-ttu-id="16781-282">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-282">NULL</span></span>|<span data-ttu-id="16781-283">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-283">NULL</span></span>|<span data-ttu-id="16781-284">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-284">NULL</span></span>|<span data-ttu-id="16781-285">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-285">NULL</span></span>|<span data-ttu-id="16781-286">NULL</span><span class="sxs-lookup"><span data-stu-id="16781-286">NULL</span></span>|  
|<span data-ttu-id="16781-287">IS_LONG</span><span class="sxs-lookup"><span data-stu-id="16781-287">IS_LONG</span></span>|<span data-ttu-id="16781-288">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-288">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-289">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-289">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-290">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-290">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-291">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-291">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-292">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-292">VARIANT_FALSE</span></span>|<span data-ttu-id="16781-293">VARIANT_FALSE</span><span class="sxs-lookup"><span data-stu-id="16781-293">VARIANT_FALSE</span></span>|  
|<span data-ttu-id="16781-294">BEST_MATCH</span><span class="sxs-lookup"><span data-stu-id="16781-294">BEST_MATCH</span></span>|<span data-ttu-id="16781-295">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-295">VARIANT_TRUE</span></span>|<span data-ttu-id="16781-296">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-296">VARIANT_TRUE</span></span>|<span data-ttu-id="16781-297">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-297">VARIANT_TRUE</span></span>|<span data-ttu-id="16781-298">除非下列其中之一是 true，否則為 VARIANT_TRUE：</span><span class="sxs-lookup"><span data-stu-id="16781-298">VARIANT_TRUE unless one of the following is true:</span></span><br /><br /> <span data-ttu-id="16781-299">-是連接到下層伺服器的用戶端。</span><span class="sxs-lookup"><span data-stu-id="16781-299">-   Is client connected to a down-level server.</span></span><br /><span data-ttu-id="16781-300">-資料類型相容性連接屬性會指定等於80的相容性層級。</span><span class="sxs-lookup"><span data-stu-id="16781-300">-   The data type compatibility connection property specifies a compatibility level that equals 80.</span></span>|<span data-ttu-id="16781-301">除非下列其中之一是 true，否則為 VARIANT_TRUE：</span><span class="sxs-lookup"><span data-stu-id="16781-301">VARIANT_TRUE unless one of the following is true:</span></span><br /><br /> <span data-ttu-id="16781-302">-是連接到下層伺服器的用戶端。</span><span class="sxs-lookup"><span data-stu-id="16781-302">-   Is client connected to a down-level server.</span></span><br /><span data-ttu-id="16781-303">-資料類型相容性連接屬性會指定等於80的相容性層級。</span><span class="sxs-lookup"><span data-stu-id="16781-303">-   The data type compatibility connection property specifies a compatibility level that equals 80.</span></span>|<span data-ttu-id="16781-304">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-304">VARIANT_TRUE</span></span>|  
|<span data-ttu-id="16781-305">IS_FIXEDLENGTH</span><span class="sxs-lookup"><span data-stu-id="16781-305">IS_FIXEDLENGTH</span></span>|<span data-ttu-id="16781-306">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-306">VARIANT_TRUE</span></span>|<span data-ttu-id="16781-307">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-307">VARIANT_TRUE</span></span>|<span data-ttu-id="16781-308">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-308">VARIANT_TRUE</span></span>|<span data-ttu-id="16781-309">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-309">VARIANT_TRUE</span></span>|<span data-ttu-id="16781-310">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-310">VARIANT_TRUE</span></span>|<span data-ttu-id="16781-311">VARIANT_TRUE</span><span class="sxs-lookup"><span data-stu-id="16781-311">VARIANT_TRUE</span></span>|  
  
 <span data-ttu-id="16781-312">OLE DB 只會定義數值和十進位類型的 MINIMUM_SCALE 和 MAXIMUM_SCALE，因此，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 對於 time、datetime2 和 datetimeoffset 這些資料行的用法不是標準的。</span><span class="sxs-lookup"><span data-stu-id="16781-312">OLE DB only defines MINIMUM_SCALE and MAXIMUM_SCALE for numeric and decimal types, so [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client's use of these columns for time, datetime2 and datetimeoffset is non-standard.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="16781-313">另請參閱</span><span class="sxs-lookup"><span data-stu-id="16781-313">See Also</span></span>  
 [<span data-ttu-id="16781-314">中繼資料 &#40;OLE DB&#41;</span><span class="sxs-lookup"><span data-stu-id="16781-314">Metadata &#40;OLE DB&#41;</span></span>](../../database-engine/dev-guide/metadata-ole-db.md)  
  
  