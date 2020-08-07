---
title: MSSQLSERVER_137 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 137 (Database Engine error)
ms.assetid: 47fb4212-2165-4fec-bc41-6d548465d7be
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e0142cd53006609e9274972e4f5964132f5982c2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598967"
---
# <a name="mssqlserver_137"></a><span data-ttu-id="ddac6-102">MSSQLSERVER_137</span><span class="sxs-lookup"><span data-stu-id="ddac6-102">MSSQLSERVER_137</span></span>
    
## <a name="details"></a><span data-ttu-id="ddac6-103">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ddac6-103">Details</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="ddac6-104">產品名稱</span><span class="sxs-lookup"><span data-stu-id="ddac6-104">Product Name</span></span>|<span data-ttu-id="ddac6-105">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ddac6-105">SQL Server</span></span>|  
|<span data-ttu-id="ddac6-106">事件識別碼</span><span class="sxs-lookup"><span data-stu-id="ddac6-106">Event ID</span></span>|<span data-ttu-id="ddac6-107">137</span><span class="sxs-lookup"><span data-stu-id="ddac6-107">137</span></span>|  
|<span data-ttu-id="ddac6-108">事件來源</span><span class="sxs-lookup"><span data-stu-id="ddac6-108">Event Source</span></span>|<span data-ttu-id="ddac6-109">MSSQLSERVER</span><span class="sxs-lookup"><span data-stu-id="ddac6-109">MSSQLSERVER</span></span>|  
|<span data-ttu-id="ddac6-110">元件</span><span class="sxs-lookup"><span data-stu-id="ddac6-110">Component</span></span>|<span data-ttu-id="ddac6-111">SQLEngine</span><span class="sxs-lookup"><span data-stu-id="ddac6-111">SQLEngine</span></span>|  
|<span data-ttu-id="ddac6-112">符號名稱</span><span class="sxs-lookup"><span data-stu-id="ddac6-112">Symbolic Name</span></span>|<span data-ttu-id="ddac6-113">P_SCALAR_VAR_NOTFOUND</span><span class="sxs-lookup"><span data-stu-id="ddac6-113">P_SCALAR_VAR_NOTFOUND</span></span>|  
|<span data-ttu-id="ddac6-114">訊息文字</span><span class="sxs-lookup"><span data-stu-id="ddac6-114">Message Text</span></span>|<span data-ttu-id="ddac6-115">必須宣告純量變數 "%.\*ls"。</span><span class="sxs-lookup"><span data-stu-id="ddac6-115">Must declare the scalar variable "%.\*ls".</span></span>|  
  
## <a name="explanation"></a><span data-ttu-id="ddac6-116">說明</span><span class="sxs-lookup"><span data-stu-id="ddac6-116">Explanation</span></span>  
 <span data-ttu-id="ddac6-117">當您在 SQL 指令碼中使用某個變數，但卻沒有先宣告該變數時，就會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="ddac6-117">This error occurs when a variable is used in a SQL script without first declaring the variable.</span></span> <span data-ttu-id="ddac6-118">下列範例會針對 SET 和 SELECT 語句傳回錯誤137，因為 **@mycol** 未宣告。</span><span class="sxs-lookup"><span data-stu-id="ddac6-118">The following example returns error 137 for both the SET and SELECT statements because **@mycol** is not declared.</span></span>  
  
 <span data-ttu-id="ddac6-119">SET @mycol = 'ContactName';</span><span class="sxs-lookup"><span data-stu-id="ddac6-119">SET @mycol = 'ContactName';</span></span>  
  
 <span data-ttu-id="ddac6-120">SELECT @mycol;</span><span class="sxs-lookup"><span data-stu-id="ddac6-120">SELECT @mycol;</span></span>  
  
 <span data-ttu-id="ddac6-121">導致這個錯誤的其中一個更複雜原因包括使用了在 EXECUTE 陳述式外部宣告的變數。</span><span class="sxs-lookup"><span data-stu-id="ddac6-121">One of the more complicated causes of this error includes the use of a variable that is declared outside the EXECUTE statement.</span></span> <span data-ttu-id="ddac6-122">例如，select **@mycol** 語句中指定的變數是 select 語句的區域變數，因此它位於 EXECUTE 語句之外。</span><span class="sxs-lookup"><span data-stu-id="ddac6-122">For example, the variable **@mycol** specified in the SELECT statement is local to the SELECT statement; thus it is outside the EXECUTE statement.</span></span>  
  
 <span data-ttu-id="ddac6-123">USE AdventureWorks2012;</span><span class="sxs-lookup"><span data-stu-id="ddac6-123">USE AdventureWorks2012;</span></span>  
  
 <span data-ttu-id="ddac6-124">GO</span><span class="sxs-lookup"><span data-stu-id="ddac6-124">GO</span></span>  
  
 <span data-ttu-id="ddac6-125">DECLARE @mycol nvarchar(20);</span><span class="sxs-lookup"><span data-stu-id="ddac6-125">DECLARE @mycol nvarchar(20);</span></span>  
  
 <span data-ttu-id="ddac6-126">SET @mycol = 'Name';</span><span class="sxs-lookup"><span data-stu-id="ddac6-126">SET @mycol = 'Name';</span></span>  
  
 <span data-ttu-id="ddac6-127">EXECUTE ('SELECT @mycol FROM Production.Product;');</span><span class="sxs-lookup"><span data-stu-id="ddac6-127">EXECUTE ('SELECT @mycol FROM Production.Product;');</span></span>  
  
## <a name="user-action"></a><span data-ttu-id="ddac6-128">使用者動作</span><span class="sxs-lookup"><span data-stu-id="ddac6-128">User Action</span></span>  
 <span data-ttu-id="ddac6-129">請確認在 SQL 指令碼中使用的任何變數都已經過宣告，然後再用於指令碼的其他位置。</span><span class="sxs-lookup"><span data-stu-id="ddac6-129">Verify that any variables used in a SQL script are declared before being used elsewhere in the script.</span></span>  
  
 <span data-ttu-id="ddac6-130">重寫指令碼，讓它不會在 EXECUTE 陳述式中參考在該陳述式外部宣告的變數。</span><span class="sxs-lookup"><span data-stu-id="ddac6-130">Rewrite the script so that it does not reference variables in the EXECUTE statement that are declared outside of it.</span></span> <span data-ttu-id="ddac6-131">例如：</span><span class="sxs-lookup"><span data-stu-id="ddac6-131">For example:</span></span>  
  
 <span data-ttu-id="ddac6-132">USE AdventureWorks2012;</span><span class="sxs-lookup"><span data-stu-id="ddac6-132">USE AdventureWorks2012;</span></span>  
  
 <span data-ttu-id="ddac6-133">GO</span><span class="sxs-lookup"><span data-stu-id="ddac6-133">GO</span></span>  
  
 <span data-ttu-id="ddac6-134">DECLARE @mycol nvarchar(20) ;</span><span class="sxs-lookup"><span data-stu-id="ddac6-134">DECLARE @mycol nvarchar(20) ;</span></span>  
  
 <span data-ttu-id="ddac6-135">SET @mycol = 'Name';</span><span class="sxs-lookup"><span data-stu-id="ddac6-135">SET @mycol = 'Name';</span></span>  
  
 <span data-ttu-id="ddac6-136">EXECUTE ('SELECT ' + @mycol + ' FROM Production.Product';) ;</span><span class="sxs-lookup"><span data-stu-id="ddac6-136">EXECUTE ('SELECT ' + @mycol + ' FROM Production.Product';) ;</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ddac6-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ddac6-137">See Also</span></span>  
 <span data-ttu-id="ddac6-138">[EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="ddac6-138">[EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql) </span></span>  
 <span data-ttu-id="ddac6-139">[SET 陳述式 &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statements-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="ddac6-139">[SET Statements &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statements-transact-sql) </span></span>  
 [<span data-ttu-id="ddac6-140">DECLARE @local_variable &#40;Transact-SQL&#41;</span><span class="sxs-lookup"><span data-stu-id="ddac6-140">DECLARE @local_variable &#40;Transact-SQL&#41;</span></span>](/sql/t-sql/language-elements/declare-local-variable-transact-sql)  
  
  
