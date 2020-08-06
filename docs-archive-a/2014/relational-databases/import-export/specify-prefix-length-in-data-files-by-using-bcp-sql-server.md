---
title: 使用 BCP 指定資料檔的前置長度 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server], prefix length
- prefix length [SQL Server]
- lengths [SQL Server], prefix characters
- data formats [SQL Server], prefix length
ms.assetid: ce32dd1a-26f1-4f61-b9fa-3f1feea9992e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ff16491ed9c021424d3d6371ccb7ba2941c61129
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687882"
---
# <a name="specify-prefix-length-in-data-files-by-using-bcp-sql-server"></a><span data-ttu-id="112ac-102">使用 bcp 指定資料檔的前置長度 (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="112ac-102">Specify Prefix Length in Data Files by Using bcp (SQL Server)</span></span>
  <span data-ttu-id="112ac-103">為了讓原生格式的資料大量匯出至資料檔時，能夠有最精簡的檔案儲存方式， **bcp** 命令會在每個欄位前面都加上一個或多個字元，指出欄位的長度。</span><span class="sxs-lookup"><span data-stu-id="112ac-103">To provide the most compact file storage for the bulk export of data in native format to a data file, the **bcp** command precedes each field with one or more characters that indicates the length of the field.</span></span> <span data-ttu-id="112ac-104">這些字元稱作 *「長度前置字元」* (Length prefix characters)。</span><span class="sxs-lookup"><span data-stu-id="112ac-104">These characters are called *length prefix characters*.</span></span>  
  
## <a name="the-bcp-prompt-for-prefix-length"></a><span data-ttu-id="112ac-105">前置長度的 bcp 提示字元</span><span class="sxs-lookup"><span data-stu-id="112ac-105">The bcp Prompt for Prefix Length</span></span>  
 <span data-ttu-id="112ac-106">如果互動式 **bcp** 命令包含 **in** 或 **out** 選項，但沒有格式檔案參數 ( **-f**) 或資料格式參數 ( **-n**、 **-c**、 **-w**或 **-N**)，此命令就會提示您輸入每個資料欄位的前置長度，如下所示：</span><span class="sxs-lookup"><span data-stu-id="112ac-106">If an interactive **bcp** command contains the **in** or **out** option without either the format file switch (**-f**) or a data-format switch (**-n**, **-c**, **-w**, or **-N**), the command prompts for the prefix length of each data field, as follows:</span></span>  
  
 `Enter prefix length of field <field_name> [<default>]:`  
  
 <span data-ttu-id="112ac-107">若您指定 0， **bcp** 會提示您輸入欄位的長度 (適用於字元資料類型) 或欄位結束字元 (適用於原生非字元類型)。</span><span class="sxs-lookup"><span data-stu-id="112ac-107">If you specify 0, **bcp** prompts you for either the length of the field (for a character data type) or a field terminator (for a native non-character type).</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="112ac-108">以互動方式在 **bcp** 命令中指定所有欄位之後，此命令會提示您將每個欄位的回應以非 XML 格式的檔案加以儲存。</span><span class="sxs-lookup"><span data-stu-id="112ac-108">After you interactively specify all of the fields in a **bcp** command, the command prompts you save your responses for each field in a non-XML format file.</span></span> <span data-ttu-id="112ac-109">如需非 XML 格式檔案的詳細資訊，請參閱[非 XML 格式檔案 &#40;SQL Server&#41;](xml-format-files-sql-server.md)。</span><span class="sxs-lookup"><span data-stu-id="112ac-109">For more information about non-XML format files, see [Non-XML Format Files &#40;SQL Server&#41;](xml-format-files-sql-server.md).</span></span>  
  
## <a name="overview-of-prefix-length"></a><span data-ttu-id="112ac-110">前置長度的概觀</span><span class="sxs-lookup"><span data-stu-id="112ac-110">Overview of Prefix Length</span></span>  
 <span data-ttu-id="112ac-111">若要儲存欄位的前置長度，您需要有足夠的位元組來表示欄位的最大長度。</span><span class="sxs-lookup"><span data-stu-id="112ac-111">To store the prefix length of a field, you need enough bytes to represent the maximum length of the field.</span></span> <span data-ttu-id="112ac-112">所需的位元組數目取決於檔案儲存類型、資料行的 Null 屬性，以及資料是以原生或字元格式儲存於資料檔中。</span><span class="sxs-lookup"><span data-stu-id="112ac-112">The number of bytes that are required also depends upon the file storage type, the nullability of a column, and whether the data is being stored in the data file in its native or character format.</span></span> <span data-ttu-id="112ac-113">例如，`text` 或 `image` 資料類型需要四個前置字元來儲存欄位長度，但是 `varchar` 資料類型則需要兩個字元。</span><span class="sxs-lookup"><span data-stu-id="112ac-113">For example, a `text` or `image` data type requires four prefix characters to store the field length, but a `varchar` data type requires two characters.</span></span> <span data-ttu-id="112ac-114">在資料檔中，這些長度前置字元會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的內部二進位資料格式儲存。</span><span class="sxs-lookup"><span data-stu-id="112ac-114">In the data file, these length-prefix characters are stored in the internal binary data format of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span>  
  
> [!IMPORTANT]  
>  <span data-ttu-id="112ac-115">在使用原生格式時，請使用長度前置詞，而不是欄位的結束字元。</span><span class="sxs-lookup"><span data-stu-id="112ac-115">When you use native format, use length prefixes rather than field terminators.</span></span> <span data-ttu-id="112ac-116">原生格式資料可能會和結束字元有衝突，因為原生格式的資料檔是以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部二進位資料格式儲存。</span><span class="sxs-lookup"><span data-stu-id="112ac-116">Native format data might conflict with terminators because a native-format data file is stored in the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] internal binary data format.</span></span>  
  
##  <a name="prefix-lengths-for-bulk-export"></a><a name="PrefixLengthsExport"></a> <span data-ttu-id="112ac-117">大量匯出的前置長度</span><span class="sxs-lookup"><span data-stu-id="112ac-117">Prefix Lengths for Bulk Export</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="112ac-118">您匯出欄位時，前置長度提示所提供的預設值，表示欄位最有效率的前置長度。</span><span class="sxs-lookup"><span data-stu-id="112ac-118">The default value that is provided at the prefix-length prompt when you export a field indicates the most efficient prefix length for the field.</span></span>  
  
 <span data-ttu-id="112ac-119">Null 值會以空白欄位表示。</span><span class="sxs-lookup"><span data-stu-id="112ac-119">Null values are represented as an empty field.</span></span> <span data-ttu-id="112ac-120">為了指出欄位為空白 (代表 NULL)，欄位前置包含了值 -1，也就是說，至少需要一個位元組。</span><span class="sxs-lookup"><span data-stu-id="112ac-120">To indicate that the field is empty (represents NULL), the field prefix contains the value -1; that is, it requires at least 1 byte.</span></span> <span data-ttu-id="112ac-121">請注意，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表資料行允許 Null 值，則資料行需要的前置長度為 1 或更多，取決於檔案儲存類型。</span><span class="sxs-lookup"><span data-stu-id="112ac-121">Note that if a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] table column allows null values, the column requires a prefix length of 1 or greater, depending on the file storage type.</span></span>  
  
 <span data-ttu-id="112ac-122">當您大量匯出資料並以原生資料類型或字元格式儲存時，請使用下表所示的前置詞長度。</span><span class="sxs-lookup"><span data-stu-id="112ac-122">When you bulk export data and store it in either native data types or character format, use the prefix lengths shown in the following table.</span></span>  
  
|<span data-ttu-id="112ac-123">SQL Server</span><span class="sxs-lookup"><span data-stu-id="112ac-123">SQL Server</span></span><br /><br /> <span data-ttu-id="112ac-124">資料類型</span><span class="sxs-lookup"><span data-stu-id="112ac-124">data type</span></span>|<span data-ttu-id="112ac-125">原生格式</span><span class="sxs-lookup"><span data-stu-id="112ac-125">Native format</span></span><br /><br /> <span data-ttu-id="112ac-126">NOT NULL</span><span class="sxs-lookup"><span data-stu-id="112ac-126">NOT NULL</span></span>|<span data-ttu-id="112ac-127">原生格式</span><span class="sxs-lookup"><span data-stu-id="112ac-127">Native format</span></span><br /><br /> <span data-ttu-id="112ac-128">NULL</span><span class="sxs-lookup"><span data-stu-id="112ac-128">NULL</span></span>|<span data-ttu-id="112ac-129">字元格式</span><span class="sxs-lookup"><span data-stu-id="112ac-129">Character format</span></span><br /><br /> <span data-ttu-id="112ac-130">NOT NULL</span><span class="sxs-lookup"><span data-stu-id="112ac-130">NOT NULL</span></span>|<span data-ttu-id="112ac-131">字元格式</span><span class="sxs-lookup"><span data-stu-id="112ac-131">Character format</span></span><br /><br /> <span data-ttu-id="112ac-132">NULL</span><span class="sxs-lookup"><span data-stu-id="112ac-132">NULL</span></span>|  
|------------------------------|--------------------------------|----------------------------|-----------------------------------|-------------------------------|  
|`char`|<span data-ttu-id="112ac-133">2</span><span class="sxs-lookup"><span data-stu-id="112ac-133">2</span></span>|<span data-ttu-id="112ac-134">2</span><span class="sxs-lookup"><span data-stu-id="112ac-134">2</span></span>|<span data-ttu-id="112ac-135">2</span><span class="sxs-lookup"><span data-stu-id="112ac-135">2</span></span>|<span data-ttu-id="112ac-136">2</span><span class="sxs-lookup"><span data-stu-id="112ac-136">2</span></span>|  
|`varchar`|<span data-ttu-id="112ac-137">2</span><span class="sxs-lookup"><span data-stu-id="112ac-137">2</span></span>|<span data-ttu-id="112ac-138">2</span><span class="sxs-lookup"><span data-stu-id="112ac-138">2</span></span>|<span data-ttu-id="112ac-139">2</span><span class="sxs-lookup"><span data-stu-id="112ac-139">2</span></span>|<span data-ttu-id="112ac-140">2</span><span class="sxs-lookup"><span data-stu-id="112ac-140">2</span></span>|  
|`nchar`|<span data-ttu-id="112ac-141">2</span><span class="sxs-lookup"><span data-stu-id="112ac-141">2</span></span>|<span data-ttu-id="112ac-142">2</span><span class="sxs-lookup"><span data-stu-id="112ac-142">2</span></span>|<span data-ttu-id="112ac-143">2</span><span class="sxs-lookup"><span data-stu-id="112ac-143">2</span></span>|<span data-ttu-id="112ac-144">2</span><span class="sxs-lookup"><span data-stu-id="112ac-144">2</span></span>|  
|`nvarchar`|<span data-ttu-id="112ac-145">2</span><span class="sxs-lookup"><span data-stu-id="112ac-145">2</span></span>|<span data-ttu-id="112ac-146">2</span><span class="sxs-lookup"><span data-stu-id="112ac-146">2</span></span>|<span data-ttu-id="112ac-147">2</span><span class="sxs-lookup"><span data-stu-id="112ac-147">2</span></span>|<span data-ttu-id="112ac-148">2</span><span class="sxs-lookup"><span data-stu-id="112ac-148">2</span></span>|  
|<span data-ttu-id="112ac-149">`text` <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="112ac-149">`text` <sup>1</sup></span></span>|<span data-ttu-id="112ac-150">4</span><span class="sxs-lookup"><span data-stu-id="112ac-150">4</span></span>|<span data-ttu-id="112ac-151">4</span><span class="sxs-lookup"><span data-stu-id="112ac-151">4</span></span>|<span data-ttu-id="112ac-152">4</span><span class="sxs-lookup"><span data-stu-id="112ac-152">4</span></span>|<span data-ttu-id="112ac-153">4</span><span class="sxs-lookup"><span data-stu-id="112ac-153">4</span></span>|  
|<span data-ttu-id="112ac-154">`ntext` <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="112ac-154">`ntext` <sup>1</sup></span></span>|<span data-ttu-id="112ac-155">4</span><span class="sxs-lookup"><span data-stu-id="112ac-155">4</span></span>|<span data-ttu-id="112ac-156">4</span><span class="sxs-lookup"><span data-stu-id="112ac-156">4</span></span>|<span data-ttu-id="112ac-157">4</span><span class="sxs-lookup"><span data-stu-id="112ac-157">4</span></span>|<span data-ttu-id="112ac-158">4</span><span class="sxs-lookup"><span data-stu-id="112ac-158">4</span></span>|  
|`binary`|<span data-ttu-id="112ac-159">2</span><span class="sxs-lookup"><span data-stu-id="112ac-159">2</span></span>|<span data-ttu-id="112ac-160">2</span><span class="sxs-lookup"><span data-stu-id="112ac-160">2</span></span>|<span data-ttu-id="112ac-161">2</span><span class="sxs-lookup"><span data-stu-id="112ac-161">2</span></span>|<span data-ttu-id="112ac-162">2</span><span class="sxs-lookup"><span data-stu-id="112ac-162">2</span></span>|  
|`varbinary`|<span data-ttu-id="112ac-163">2</span><span class="sxs-lookup"><span data-stu-id="112ac-163">2</span></span>|<span data-ttu-id="112ac-164">2</span><span class="sxs-lookup"><span data-stu-id="112ac-164">2</span></span>|<span data-ttu-id="112ac-165">2</span><span class="sxs-lookup"><span data-stu-id="112ac-165">2</span></span>|<span data-ttu-id="112ac-166">2</span><span class="sxs-lookup"><span data-stu-id="112ac-166">2</span></span>|  
|<span data-ttu-id="112ac-167">`image` <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="112ac-167">`image` <sup>1</sup></span></span>|<span data-ttu-id="112ac-168">4</span><span class="sxs-lookup"><span data-stu-id="112ac-168">4</span></span>|<span data-ttu-id="112ac-169">4</span><span class="sxs-lookup"><span data-stu-id="112ac-169">4</span></span>|<span data-ttu-id="112ac-170">4</span><span class="sxs-lookup"><span data-stu-id="112ac-170">4</span></span>|<span data-ttu-id="112ac-171">4</span><span class="sxs-lookup"><span data-stu-id="112ac-171">4</span></span>|  
|`datetime`|<span data-ttu-id="112ac-172">0</span><span class="sxs-lookup"><span data-stu-id="112ac-172">0</span></span>|<span data-ttu-id="112ac-173">1</span><span class="sxs-lookup"><span data-stu-id="112ac-173">1</span></span>|<span data-ttu-id="112ac-174">0</span><span class="sxs-lookup"><span data-stu-id="112ac-174">0</span></span>|<span data-ttu-id="112ac-175">1</span><span class="sxs-lookup"><span data-stu-id="112ac-175">1</span></span>|  
|`smalldatetime`|<span data-ttu-id="112ac-176">0</span><span class="sxs-lookup"><span data-stu-id="112ac-176">0</span></span>|<span data-ttu-id="112ac-177">1</span><span class="sxs-lookup"><span data-stu-id="112ac-177">1</span></span>|<span data-ttu-id="112ac-178">0</span><span class="sxs-lookup"><span data-stu-id="112ac-178">0</span></span>|<span data-ttu-id="112ac-179">1</span><span class="sxs-lookup"><span data-stu-id="112ac-179">1</span></span>|  
|`decimal`|<span data-ttu-id="112ac-180">1</span><span class="sxs-lookup"><span data-stu-id="112ac-180">1</span></span>|<span data-ttu-id="112ac-181">1</span><span class="sxs-lookup"><span data-stu-id="112ac-181">1</span></span>|<span data-ttu-id="112ac-182">1</span><span class="sxs-lookup"><span data-stu-id="112ac-182">1</span></span>|<span data-ttu-id="112ac-183">1</span><span class="sxs-lookup"><span data-stu-id="112ac-183">1</span></span>|  
|`numeric`|<span data-ttu-id="112ac-184">1</span><span class="sxs-lookup"><span data-stu-id="112ac-184">1</span></span>|<span data-ttu-id="112ac-185">1</span><span class="sxs-lookup"><span data-stu-id="112ac-185">1</span></span>|<span data-ttu-id="112ac-186">1</span><span class="sxs-lookup"><span data-stu-id="112ac-186">1</span></span>|<span data-ttu-id="112ac-187">1</span><span class="sxs-lookup"><span data-stu-id="112ac-187">1</span></span>|  
|`float`|<span data-ttu-id="112ac-188">0</span><span class="sxs-lookup"><span data-stu-id="112ac-188">0</span></span>|<span data-ttu-id="112ac-189">1</span><span class="sxs-lookup"><span data-stu-id="112ac-189">1</span></span>|<span data-ttu-id="112ac-190">0</span><span class="sxs-lookup"><span data-stu-id="112ac-190">0</span></span>|<span data-ttu-id="112ac-191">1</span><span class="sxs-lookup"><span data-stu-id="112ac-191">1</span></span>|  
|`real`|<span data-ttu-id="112ac-192">0</span><span class="sxs-lookup"><span data-stu-id="112ac-192">0</span></span>|<span data-ttu-id="112ac-193">1</span><span class="sxs-lookup"><span data-stu-id="112ac-193">1</span></span>|<span data-ttu-id="112ac-194">0</span><span class="sxs-lookup"><span data-stu-id="112ac-194">0</span></span>|<span data-ttu-id="112ac-195">1</span><span class="sxs-lookup"><span data-stu-id="112ac-195">1</span></span>|  
|`int`|<span data-ttu-id="112ac-196">0</span><span class="sxs-lookup"><span data-stu-id="112ac-196">0</span></span>|<span data-ttu-id="112ac-197">1</span><span class="sxs-lookup"><span data-stu-id="112ac-197">1</span></span>|<span data-ttu-id="112ac-198">0</span><span class="sxs-lookup"><span data-stu-id="112ac-198">0</span></span>|<span data-ttu-id="112ac-199">1</span><span class="sxs-lookup"><span data-stu-id="112ac-199">1</span></span>|  
|`bigint`|<span data-ttu-id="112ac-200">0</span><span class="sxs-lookup"><span data-stu-id="112ac-200">0</span></span>|<span data-ttu-id="112ac-201">1</span><span class="sxs-lookup"><span data-stu-id="112ac-201">1</span></span>|<span data-ttu-id="112ac-202">0</span><span class="sxs-lookup"><span data-stu-id="112ac-202">0</span></span>|<span data-ttu-id="112ac-203">1</span><span class="sxs-lookup"><span data-stu-id="112ac-203">1</span></span>|  
|`smallint`|<span data-ttu-id="112ac-204">0</span><span class="sxs-lookup"><span data-stu-id="112ac-204">0</span></span>|<span data-ttu-id="112ac-205">1</span><span class="sxs-lookup"><span data-stu-id="112ac-205">1</span></span>|<span data-ttu-id="112ac-206">0</span><span class="sxs-lookup"><span data-stu-id="112ac-206">0</span></span>|<span data-ttu-id="112ac-207">1</span><span class="sxs-lookup"><span data-stu-id="112ac-207">1</span></span>|  
|`tinyint`|<span data-ttu-id="112ac-208">0</span><span class="sxs-lookup"><span data-stu-id="112ac-208">0</span></span>|<span data-ttu-id="112ac-209">1</span><span class="sxs-lookup"><span data-stu-id="112ac-209">1</span></span>|<span data-ttu-id="112ac-210">0</span><span class="sxs-lookup"><span data-stu-id="112ac-210">0</span></span>|<span data-ttu-id="112ac-211">1</span><span class="sxs-lookup"><span data-stu-id="112ac-211">1</span></span>|  
|`money`|<span data-ttu-id="112ac-212">0</span><span class="sxs-lookup"><span data-stu-id="112ac-212">0</span></span>|<span data-ttu-id="112ac-213">1</span><span class="sxs-lookup"><span data-stu-id="112ac-213">1</span></span>|<span data-ttu-id="112ac-214">0</span><span class="sxs-lookup"><span data-stu-id="112ac-214">0</span></span>|<span data-ttu-id="112ac-215">1</span><span class="sxs-lookup"><span data-stu-id="112ac-215">1</span></span>|  
|`smallmoney`|<span data-ttu-id="112ac-216">0</span><span class="sxs-lookup"><span data-stu-id="112ac-216">0</span></span>|<span data-ttu-id="112ac-217">1</span><span class="sxs-lookup"><span data-stu-id="112ac-217">1</span></span>|<span data-ttu-id="112ac-218">0</span><span class="sxs-lookup"><span data-stu-id="112ac-218">0</span></span>|<span data-ttu-id="112ac-219">1</span><span class="sxs-lookup"><span data-stu-id="112ac-219">1</span></span>|  
|`bit`|<span data-ttu-id="112ac-220">0</span><span class="sxs-lookup"><span data-stu-id="112ac-220">0</span></span>|<span data-ttu-id="112ac-221">1</span><span class="sxs-lookup"><span data-stu-id="112ac-221">1</span></span>|<span data-ttu-id="112ac-222">0</span><span class="sxs-lookup"><span data-stu-id="112ac-222">0</span></span>|<span data-ttu-id="112ac-223">1</span><span class="sxs-lookup"><span data-stu-id="112ac-223">1</span></span>|  
|`uniqueidentifier`|<span data-ttu-id="112ac-224">1</span><span class="sxs-lookup"><span data-stu-id="112ac-224">1</span></span>|<span data-ttu-id="112ac-225">1</span><span class="sxs-lookup"><span data-stu-id="112ac-225">1</span></span>|<span data-ttu-id="112ac-226">0</span><span class="sxs-lookup"><span data-stu-id="112ac-226">0</span></span>|<span data-ttu-id="112ac-227">1</span><span class="sxs-lookup"><span data-stu-id="112ac-227">1</span></span>|  
|`timestamp`|<span data-ttu-id="112ac-228">1</span><span class="sxs-lookup"><span data-stu-id="112ac-228">1</span></span>|<span data-ttu-id="112ac-229">1</span><span class="sxs-lookup"><span data-stu-id="112ac-229">1</span></span>|<span data-ttu-id="112ac-230">1</span><span class="sxs-lookup"><span data-stu-id="112ac-230">1</span></span>|<span data-ttu-id="112ac-231">1</span><span class="sxs-lookup"><span data-stu-id="112ac-231">1</span></span>|  
|`varchar(max)`|<span data-ttu-id="112ac-232">8</span><span class="sxs-lookup"><span data-stu-id="112ac-232">8</span></span>|<span data-ttu-id="112ac-233">8</span><span class="sxs-lookup"><span data-stu-id="112ac-233">8</span></span>|<span data-ttu-id="112ac-234">8</span><span class="sxs-lookup"><span data-stu-id="112ac-234">8</span></span>|<span data-ttu-id="112ac-235">8</span><span class="sxs-lookup"><span data-stu-id="112ac-235">8</span></span>|  
|`varbinary(max)`|<span data-ttu-id="112ac-236">8</span><span class="sxs-lookup"><span data-stu-id="112ac-236">8</span></span>|<span data-ttu-id="112ac-237">8</span><span class="sxs-lookup"><span data-stu-id="112ac-237">8</span></span>|<span data-ttu-id="112ac-238">8</span><span class="sxs-lookup"><span data-stu-id="112ac-238">8</span></span>|<span data-ttu-id="112ac-239">8</span><span class="sxs-lookup"><span data-stu-id="112ac-239">8</span></span>|  
|<span data-ttu-id="112ac-240">UDT (使用者定義資料類型)</span><span class="sxs-lookup"><span data-stu-id="112ac-240">UDT (a user-defined data type)</span></span>|<span data-ttu-id="112ac-241">8</span><span class="sxs-lookup"><span data-stu-id="112ac-241">8</span></span>|<span data-ttu-id="112ac-242">8</span><span class="sxs-lookup"><span data-stu-id="112ac-242">8</span></span>|<span data-ttu-id="112ac-243">8</span><span class="sxs-lookup"><span data-stu-id="112ac-243">8</span></span>|<span data-ttu-id="112ac-244">8</span><span class="sxs-lookup"><span data-stu-id="112ac-244">8</span></span>|  
|<span data-ttu-id="112ac-245">XML</span><span class="sxs-lookup"><span data-stu-id="112ac-245">XML</span></span>|<span data-ttu-id="112ac-246">8</span><span class="sxs-lookup"><span data-stu-id="112ac-246">8</span></span>|<span data-ttu-id="112ac-247">8</span><span class="sxs-lookup"><span data-stu-id="112ac-247">8</span></span>|<span data-ttu-id="112ac-248">8</span><span class="sxs-lookup"><span data-stu-id="112ac-248">8</span></span>|<span data-ttu-id="112ac-249">8</span><span class="sxs-lookup"><span data-stu-id="112ac-249">8</span></span>|  
  
 <span data-ttu-id="112ac-250"><sup>1</sup>在 `ntext` 的 `text` `image` 未來版本中將會移除、和資料類型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="112ac-250"><sup>1</sup> The `ntext`, `text`, and `image` data types will be removed in a future version of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="112ac-251">請避免在新的開發工作中使用這些資料類型，並規劃修改目前在使用這些資料類型的應用程式。</span><span class="sxs-lookup"><span data-stu-id="112ac-251">Avoid using these data types in new development work, and plan to modify applications that currently use them.</span></span> <span data-ttu-id="112ac-252">請改用 `nvarchar(max)`、`varchar(max)` 和 `varbinary(max)`。</span><span class="sxs-lookup"><span data-stu-id="112ac-252">Use `nvarchar(max)`, `varchar(max)`, and `varbinary(max)` instead.</span></span>  
  
##  <a name="prefix-lengths-for-bulk-import"></a><a name="PrefixLengthsImport"></a> <span data-ttu-id="112ac-253">大量匯入的前置長度</span><span class="sxs-lookup"><span data-stu-id="112ac-253">Prefix Lengths for Bulk Import</span></span>  
 <span data-ttu-id="112ac-254">大量匯入資料時，前置長度就是原先建立資料檔時即指定的值。</span><span class="sxs-lookup"><span data-stu-id="112ac-254">When data is bulk imported, the prefix length is the value that was specified when the data file was created originally.</span></span> <span data-ttu-id="112ac-255">如果資料檔案不是由 **bcp** 命令所建立，則長度前置字元可能不存在。</span><span class="sxs-lookup"><span data-stu-id="112ac-255">If the data file was not created by a **bcp** command, length prefix characters probably do not exist.</span></span> <span data-ttu-id="112ac-256">在此狀況下，可指定 0 做為前置長度。</span><span class="sxs-lookup"><span data-stu-id="112ac-256">In this instance, specify 0 for the prefix length.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="112ac-257">若要在並非使用 **bcp**所建立的資料檔中指定前置長度，請使用本主題稍早在 [大量匯出的前置長度](#PrefixLengthsExport)中提供的長度。</span><span class="sxs-lookup"><span data-stu-id="112ac-257">To specify a prefix length in a data file that was not created by using **bcp**, use the lengths provided in [Prefix Lengths for Bulk Export](#PrefixLengthsExport), earlier in this topic.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="112ac-258">另請參閱</span><span class="sxs-lookup"><span data-stu-id="112ac-258">See Also</span></span>  
 <span data-ttu-id="112ac-259">[bcp 公用程式](../../tools/bcp-utility.md) </span><span class="sxs-lookup"><span data-stu-id="112ac-259">[bcp Utility](../../tools/bcp-utility.md) </span></span>  
 <span data-ttu-id="112ac-260">[資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="112ac-260">[Data Types &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) </span></span>  
 <span data-ttu-id="112ac-261">[使用 bcp 時指定欄位長度 &#40;SQL Server&#41;](specify-field-length-by-using-bcp-sql-server.md) </span><span class="sxs-lookup"><span data-stu-id="112ac-261">[Specify Field Length by Using bcp &#40;SQL Server&#41;](specify-field-length-by-using-bcp-sql-server.md) </span></span>  
 <span data-ttu-id="112ac-262">[指定欄位與資料列結束字元 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md) </span><span class="sxs-lookup"><span data-stu-id="112ac-262">[Specify Field and Row Terminators &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md) </span></span>  
 [<span data-ttu-id="112ac-263">使用 bcp 時指定檔案儲存類型 &#40;SQL Server&#41;</span><span class="sxs-lookup"><span data-stu-id="112ac-263">Specify File Storage Type by Using bcp &#40;SQL Server&#41;</span></span>](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
  