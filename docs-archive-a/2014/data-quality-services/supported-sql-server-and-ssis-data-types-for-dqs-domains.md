---
title: DQS 定義域支援的 SQL Server 和 SSIS 資料類型 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 4931143a-b84d-478b-9b45-174128d36ed3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ad79983f570beb4c789379b2b48682b358c34e1b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709961"
---
# <a name="supported-sql-server-and-ssis-data-types-for-dqs-domains"></a><span data-ttu-id="43624-102">DQS 定義域支援的 SQL Server 和 SSIS 資料類型</span><span class="sxs-lookup"><span data-stu-id="43624-102">Supported SQL Server and SSIS Data Types for DQS Domains</span></span>
  <span data-ttu-id="43624-103">SQL Server 和 SQL Server Integration Services (SSIS) 中存在許多資料類型，但是只有四種資料類型適用於 DQS 定義域：Date、Decimal、Integer 和 String。</span><span class="sxs-lookup"><span data-stu-id="43624-103">There are many data types in SQL Server and SQL Server Integration Services (SSIS), but only four data types for DQS domains: Date, Decimal, Integer, and String.</span></span> <span data-ttu-id="43624-104">DQS 並不支援所有 SQL Server 和 SSIS 資料類型。</span><span class="sxs-lookup"><span data-stu-id="43624-104">Not all SQL Server and SSIS data types are supported in DQS.</span></span> <span data-ttu-id="43624-105">只有當 DQS 支援來源資料類型，而且該類型符合 DQS 定義域資料類型時，您才能將來源資料對應至 DQS 定義域，以便執行資料品質活動。</span><span class="sxs-lookup"><span data-stu-id="43624-105">You can map your source data to a DQS domain for performing data-quality activities only if the source data type is supported in DQS, and matches with the DQS domain data type.</span></span> <span data-ttu-id="43624-106">本主題將提供受支援而且可分別對應至 DQS 中四種定義域資料類型之 SQL Server 和 SSIS 資料類型的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="43624-106">This topic provides information about the SQL Server and SSIS data types that are supported, and available for mapping to each of the four domain data types in DQS.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="43624-107">在 .xlsx 和 .xls 檔案中，來源資料行的資料類型是由前八個資料列中最普遍的資料類型所決定。</span><span class="sxs-lookup"><span data-stu-id="43624-107">In .xlsx and .xls files, the data type of the source column is determined by the most prevalent data type in the first eight rows.</span></span> <span data-ttu-id="43624-108">如果資料格不符合該資料類型，將會為它提供 null 值。</span><span class="sxs-lookup"><span data-stu-id="43624-108">If a cell does not conform to that data type, it will be given a null value.</span></span> <span data-ttu-id="43624-109">同樣地，在 .csv 檔案中，來源資料行的資料類型是由前八個資料列中最普遍的資料類型所決定。</span><span class="sxs-lookup"><span data-stu-id="43624-109">Similarly, in .csv files, the data type of the source column is determined by the most prevalent data type in the first eight rows.</span></span>  
  
##  <a name="supported-sql-server-data-types"></a><a name="SQLServer"></a><span data-ttu-id="43624-110">支援的 SQL Server 資料類型</span><span class="sxs-lookup"><span data-stu-id="43624-110">Supported SQL Server Data Types</span></span>  
 <span data-ttu-id="43624-111">下表將提供每種 DQS 定義域資料類型所支援之 SQL Server 資料類型的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="43624-111">The following table provides information about the SQL Server data types supported for each DQS domain data type:</span></span>  
  
|<span data-ttu-id="43624-112">DQS 定義域資料類型</span><span class="sxs-lookup"><span data-stu-id="43624-112">DQS Domain Data Type</span></span>|<span data-ttu-id="43624-113">支援的 SQL Server 資料類型</span><span class="sxs-lookup"><span data-stu-id="43624-113">Supported SQL Server Data Type</span></span>|  
|--------------------------|------------------------------------|  
|<span data-ttu-id="43624-114">日期</span><span class="sxs-lookup"><span data-stu-id="43624-114">Date</span></span>|<span data-ttu-id="43624-115">date</span><span class="sxs-lookup"><span data-stu-id="43624-115">date</span></span>|  
|<span data-ttu-id="43624-116">Decimal</span><span class="sxs-lookup"><span data-stu-id="43624-116">Decimal</span></span>|<span data-ttu-id="43624-117">decimal</span><span class="sxs-lookup"><span data-stu-id="43624-117">decimal</span></span><br /><br /> <span data-ttu-id="43624-118">FLOAT</span><span class="sxs-lookup"><span data-stu-id="43624-118">float</span></span><br /><br /> <span data-ttu-id="43624-119">money</span><span class="sxs-lookup"><span data-stu-id="43624-119">money</span></span><br /><br /> <span data-ttu-id="43624-120">NUMERIC</span><span class="sxs-lookup"><span data-stu-id="43624-120">numeric</span></span><br /><br /> <span data-ttu-id="43624-121">real</span><span class="sxs-lookup"><span data-stu-id="43624-121">real</span></span><br /><br /> <span data-ttu-id="43624-122">SMALLMONEY</span><span class="sxs-lookup"><span data-stu-id="43624-122">smallmoney</span></span>|  
|<span data-ttu-id="43624-123">整數</span><span class="sxs-lookup"><span data-stu-id="43624-123">Integer</span></span>|<span data-ttu-id="43624-124">BIGINT</span><span class="sxs-lookup"><span data-stu-id="43624-124">bigint</span></span><br /><br /> <span data-ttu-id="43624-125">int</span><span class="sxs-lookup"><span data-stu-id="43624-125">int</span></span><br /><br /> <span data-ttu-id="43624-126">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="43624-126">smallint</span></span><br /><br /> <span data-ttu-id="43624-127">TINYINT</span><span class="sxs-lookup"><span data-stu-id="43624-127">tinyint</span></span>|  
|<span data-ttu-id="43624-128">String</span><span class="sxs-lookup"><span data-stu-id="43624-128">String</span></span>|<span data-ttu-id="43624-129">char</span><span class="sxs-lookup"><span data-stu-id="43624-129">char</span></span><br /><br /> <span data-ttu-id="43624-130">NCHAR</span><span class="sxs-lookup"><span data-stu-id="43624-130">nchar</span></span><br /><br /> <span data-ttu-id="43624-131">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="43624-131">nvarchar</span></span><br /><br /> <span data-ttu-id="43624-132">varchar</span><span class="sxs-lookup"><span data-stu-id="43624-132">varchar</span></span>|  
  
 <span data-ttu-id="43624-133">DQS 不支援其餘 SQL Server 資料類型。</span><span class="sxs-lookup"><span data-stu-id="43624-133">Rest of the SQL Server data types are not supported in DQS.</span></span> <span data-ttu-id="43624-134">如需所有 SQL Server 資料類型的資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="43624-134">For information about all the SQL Server data types, see [Data Types &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql).</span></span>  
  
##  <a name="supported-ssis-data-types"></a><a name="SSIS"></a> <span data-ttu-id="43624-135">支援的 SSIS 資料類型</span><span class="sxs-lookup"><span data-stu-id="43624-135">Supported SSIS Data Types</span></span>  
 <span data-ttu-id="43624-136">下表將提供每種 DQS 定義域資料類型所支援之 SSIS 資料類型的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="43624-136">The following table provides information about the SSIS data types supported for each DQS domain data type:</span></span>  
  
|<span data-ttu-id="43624-137">DQS 定義域資料類型</span><span class="sxs-lookup"><span data-stu-id="43624-137">DQS Domain Data Type</span></span>|<span data-ttu-id="43624-138">支援的 SSIS 資料類型</span><span class="sxs-lookup"><span data-stu-id="43624-138">Supported SSIS Data Type</span></span>|  
|--------------------------|------------------------------|  
|<span data-ttu-id="43624-139">Date</span><span class="sxs-lookup"><span data-stu-id="43624-139">Date</span></span>|<span data-ttu-id="43624-140">DT_DATE</span><span class="sxs-lookup"><span data-stu-id="43624-140">DT_DATE</span></span>|  
|<span data-ttu-id="43624-141">Decimal</span><span class="sxs-lookup"><span data-stu-id="43624-141">Decimal</span></span>|<span data-ttu-id="43624-142">DT_DECIMAL</span><span class="sxs-lookup"><span data-stu-id="43624-142">DT_DECIMAL</span></span><br /><br /> <span data-ttu-id="43624-143">DT_NUMERIC</span><span class="sxs-lookup"><span data-stu-id="43624-143">DT_NUMERIC</span></span><br /><br /> <span data-ttu-id="43624-144">DT_R4</span><span class="sxs-lookup"><span data-stu-id="43624-144">DT_R4</span></span><br /><br /> <span data-ttu-id="43624-145">DT_R8</span><span class="sxs-lookup"><span data-stu-id="43624-145">DT_R8</span></span>|  
|<span data-ttu-id="43624-146">整數</span><span class="sxs-lookup"><span data-stu-id="43624-146">Integer</span></span>|<span data-ttu-id="43624-147">DT_I1</span><span class="sxs-lookup"><span data-stu-id="43624-147">DT_I1</span></span><br /><br /> <span data-ttu-id="43624-148">DT_I2</span><span class="sxs-lookup"><span data-stu-id="43624-148">DT_I2</span></span><br /><br /> <span data-ttu-id="43624-149">DT_I4</span><span class="sxs-lookup"><span data-stu-id="43624-149">DT_I4</span></span><br /><br /> <span data-ttu-id="43624-150">DT_I8</span><span class="sxs-lookup"><span data-stu-id="43624-150">DT_I8</span></span><br /><br /> <span data-ttu-id="43624-151">DT_U1</span><span class="sxs-lookup"><span data-stu-id="43624-151">DT_U1</span></span><br /><br /> <span data-ttu-id="43624-152">DT_U2</span><span class="sxs-lookup"><span data-stu-id="43624-152">DT_U2</span></span><br /><br /> <span data-ttu-id="43624-153">DT_U4</span><span class="sxs-lookup"><span data-stu-id="43624-153">DT_U4</span></span><br /><br /> <span data-ttu-id="43624-154">DT_U8</span><span class="sxs-lookup"><span data-stu-id="43624-154">DT_U8</span></span>|  
|<span data-ttu-id="43624-155">String</span><span class="sxs-lookup"><span data-stu-id="43624-155">String</span></span>|<span data-ttu-id="43624-156">DT_STR</span><span class="sxs-lookup"><span data-stu-id="43624-156">DT_STR</span></span><br /><br /> <span data-ttu-id="43624-157">DT_WSTR</span><span class="sxs-lookup"><span data-stu-id="43624-157">DT_WSTR</span></span>|  
  
 <span data-ttu-id="43624-158">DQS 不支援其餘 SSIS 資料類型。</span><span class="sxs-lookup"><span data-stu-id="43624-158">Rest of the SSIS data types are not supported in DQS.</span></span> <span data-ttu-id="43624-159">如需有關所有 SSIS 資料類型的資訊，請參閱＜ [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md)＞。</span><span class="sxs-lookup"><span data-stu-id="43624-159">For information about all the SSIS data types, see [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="43624-160">另請參閱</span><span class="sxs-lookup"><span data-stu-id="43624-160">See Also</span></span>  
 [<span data-ttu-id="43624-161">管理定義域</span><span class="sxs-lookup"><span data-stu-id="43624-161">Managing a Domain</span></span>](../../2014/data-quality-services/managing-a-domain.md)  
  
  