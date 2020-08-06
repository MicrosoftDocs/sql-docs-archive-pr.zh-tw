---
title: 診斷記錄和欄位 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- header records [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], diagnostic records
- ODBC error handling, diagnostic records
- SQLGetDiagField function
- diagnostic records [ODBC]
- errors [ODBC], diagnostic records
- fields [ODBC]
- status information [ODBC]
ms.assetid: 4949530c-62d1-4f1a-b592-144244444ce0
author: rothja
ms.author: jroth
ms.openlocfilehash: 4fe52b211eb6d5a0e4d875264609d036702b2b0b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706462"
---
# <a name="diagnostic-records-and-fields"></a><span data-ttu-id="2d9c9-102">診斷記錄和欄位</span><span class="sxs-lookup"><span data-stu-id="2d9c9-102">Diagnostic Records and Fields</span></span>
  <span data-ttu-id="2d9c9-103">診斷記錄與 ODBC 環境、連接、陳述式或描述項控制代碼相關聯。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-103">Diagnostic records are associated with ODBC environment, connection, statement, or descriptor handles.</span></span> <span data-ttu-id="2d9c9-104">當任何 ODBC 函數引發 SQL_SUCCESS 或 SQL_INVALID_HANDLE 以外的傳回碼時，該函數所呼叫的控制代碼會有包含參考用訊息或錯誤訊息的相關聯診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-104">When any ODBC function raises a return code other than SQL_SUCCESS or SQL_INVALID_HANDLE, the handle called by the function has associated diagnostic records that contain informational or error messages.</span></span> <span data-ttu-id="2d9c9-105">這些記錄會保留到系統使用該控制代碼呼叫另一個函數為止，屆時將捨棄這些記錄。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-105">These records are retained until another function is called using that handle, at which time they are discarded.</span></span> <span data-ttu-id="2d9c9-106">不論何時，可與控制代碼相關聯的診斷記錄數目沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-106">There is no limit to the number of diagnostic records that can be associated with a handle at any one time.</span></span>  
  
 <span data-ttu-id="2d9c9-107">共有兩種診斷記錄：標頭和狀態。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-107">There are two types of diagnostic records: header and status.</span></span> <span data-ttu-id="2d9c9-108">標頭記錄為記錄 0，而當有狀態記錄時，這兩種記錄分別為記錄 1 和具有更大編號的記錄。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-108">The header record is record 0; when there are status records, they are records 1 and later.</span></span> <span data-ttu-id="2d9c9-109">診斷記錄包含標頭記錄和狀態記錄的不同欄位。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-109">Diagnostic records contain different fields for the header record and the status records.</span></span> <span data-ttu-id="2d9c9-110">ODBC 元件也可以定義本身的診斷記錄欄位。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-110">ODBC components can also define their own diagnostic record fields.</span></span>  
  
 <span data-ttu-id="2d9c9-111">標頭記錄中的欄位包含有關函數執行的一般資訊，包括傳回碼、資料列計數、狀態記錄的數目和所執行的陳述式類型。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-111">Fields in the header record contain general information about a function's execution, including the return code, row count, number of status records, and type of statement executed.</span></span> <span data-ttu-id="2d9c9-112">除非 ODBC 函數傳回 SQL_INVALID_HANDLE，否則一定會建立標頭記錄。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-112">The header record is always created unless an ODBC function returns SQL_INVALID_HANDLE.</span></span> <span data-ttu-id="2d9c9-113">如需標頭記錄中的完整欄位清單，請參閱[SQLGetDiagField](../native-client-odbc-api/sqlgetdiagfield.md)。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-113">For a complete list of fields in the header record, see [SQLGetDiagField](../native-client-odbc-api/sqlgetdiagfield.md).</span></span>  
  
 <span data-ttu-id="2d9c9-114">狀態記錄中的欄位包含有關 ODBC 驅動程式管理員、驅動程式或資料來源所傳回的特定錯誤或警告的詳細資訊，包括 SQLSTATE、原生錯誤號碼、診斷訊息、資料行號碼和資料列號碼。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-114">Fields in the status records contain information about specific errors or warnings returned by the ODBC Driver Manager, driver, or data source, including the SQLSTATE, native error number, diagnostic message, column number, and row number.</span></span> <span data-ttu-id="2d9c9-115">只有在函數傳回 SQL_ERROR、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_NEED_DATA 或 SQL_STILL_EXECUTING 時，才會建立狀態記錄。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-115">Status records are created only if the function returns SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA, or SQL_STILL_EXECUTING.</span></span> <span data-ttu-id="2d9c9-116">如需狀態記錄中欄位的完整清單，請參閱**SQLGetDiagField**。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-116">For a complete list of fields in the status records, see **SQLGetDiagField**.</span></span>  
  
 <span data-ttu-id="2d9c9-117">**SQLGetDiagRec**會抓取單一診斷記錄及其 ODBC SQLSTATE、原生錯誤號碼和診斷訊息欄位。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-117">**SQLGetDiagRec** retrieves a single diagnostic record along with its ODBC SQLSTATE, native error number, and diagnostic-message fields.</span></span> <span data-ttu-id="2d9c9-118">這種功能類似于 ODBC 2。_x_**SQLError**函數。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-118">This functionality is similar to the ODBC 2._x_**SQLError** function.</span></span> <span data-ttu-id="2d9c9-119">ODBC 3 中最簡單的錯誤處理函式。*x*是要重複呼叫**SQLGetDiagRec** ，從*RecNumber*參數設為1，並將*RecNumber*遞增1，直到**SQLGetDiagRec**傳回 SQL_NO_DATA。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-119">The simplest error-handling function in ODBC 3.*x* is to repeatedly call **SQLGetDiagRec** starting with the *RecNumber* parameter set to 1 and incrementing *RecNumber* by 1 until **SQLGetDiagRec** returns SQL_NO_DATA.</span></span> <span data-ttu-id="2d9c9-120">這相當於 ODBC 2。*x*應用程式會呼叫**SQLError** ，直到它傳回 SQL_NO_DATA_FOUND 為止。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-120">This is equivalent to an ODBC 2.*x* application calling **SQLError** until it returns SQL_NO_DATA_FOUND.</span></span>  
  
 <span data-ttu-id="2d9c9-121">ODBC 3。*x*支援比 ODBC 2 更多的診斷資訊。*x*。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-121">ODBC 3.*x* supports much more diagnostic information than ODBC 2.*x*.</span></span> <span data-ttu-id="2d9c9-122">這項資訊會儲存在使用**SQLGetDiagField**所抓取之診斷記錄的其他欄位中。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-122">This information is stored in additional fields in diagnostic records retrieved by using **SQLGetDiagField**.</span></span>  
  
 <span data-ttu-id="2d9c9-123">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式具有驅動程式特定的診斷欄位，可以使用**SQLGetDiagField**來抓取。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-123">The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC driver has driver-specific diagnostic fields that can be retrieved with **SQLGetDiagField**.</span></span> <span data-ttu-id="2d9c9-124">這些驅動程式特定欄位的標籤會定義在 sqlncli.h 中。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-124">Labels for these driver-specific fields are defined in sqlncli.h.</span></span> <span data-ttu-id="2d9c9-125">請使用這些標籤來擷取與每個診斷記錄相關聯的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 狀態、嚴重性層級、伺服器名稱、程序名稱和行號。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-125">Use these labels to retrieve the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] state, severity level, server name, procedure name, and line number associated with each diagnostic record.</span></span> <span data-ttu-id="2d9c9-126">此外，如果應用程式呼叫**SQLGetDiagField**並將*以*設定為 SQL_DIAG_DYNAMIC_FUNCTION_CODE，則 sqlncli 會包含驅動程式用來識別 transact-sql 語句的程式碼定義。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-126">Also, sqlncli.h contains definitions of the codes the driver uses to identify Transact-SQL statements if an application calls **SQLGetDiagField** with *DiagIdentifier* set to SQL_DIAG_DYNAMIC_FUNCTION_CODE.</span></span>  
  
 <span data-ttu-id="2d9c9-127">ODBC 驅動程式管理員會使用從基礎驅動程式快取的錯誤資訊來處理**SQLGetDiagField** 。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-127">**SQLGetDiagField** is processed by the ODBC Driver Manager using error information it caches from the underlying driver.</span></span> <span data-ttu-id="2d9c9-128">在成功建立連接之前，ODBC 驅動程式管理員不會快取驅動程式專用的診斷欄位。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-128">The ODBC Driver Manager does not cache driver-specific diagnostic fields until after a successful connection has been made.</span></span> <span data-ttu-id="2d9c9-129">如果呼叫**SQLGetDiagField**以取得驅動程式特定的診斷欄位，然後才成功完成連接，則會傳回 SQL_ERROR。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-129">**SQLGetDiagField** returns SQL_ERROR if it is called to get driver-specific diagnostic fields before a successful connection has been completed.</span></span> <span data-ttu-id="2d9c9-130">如果 ODBC 連接函數傳回 SQL_SUCCESS_WITH_INFO，則連接函數的驅動程式特定的診斷欄位就還不能使用。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-130">If an ODBC connect function returns SQL_SUCCESS_WITH_INFO, the driver-specific diagnostic fields for the connect function are not yet available.</span></span> <span data-ttu-id="2d9c9-131">只有在您于 connect 函式之後進行另一個 ODBC 函數呼叫之後，才可以開始針對驅動程式特定的診斷欄位呼叫**SQLGetDiagField** 。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-131">You can start calling **SQLGetDiagField** for driver-specific diagnostic fields only after you have made another ODBC function call after the connect function.</span></span>  
  
 <span data-ttu-id="2d9c9-132">Native Client ODBC 驅動程式所報告的大部分錯誤， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都只能使用**SQLGetDiagRec**所傳回的資訊來有效診斷。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-132">Most errors reported by the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC driver can be effectively diagnosed using only the information returned by **SQLGetDiagRec**.</span></span> <span data-ttu-id="2d9c9-133">不過，在某些情況下，由驅動程式特定的診斷欄位所傳回的資訊對於診斷錯誤十分重要。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-133">In some cases, however, the information returned by the driver-specific diagnostic fields is important in diagnosing an error.</span></span> <span data-ttu-id="2d9c9-134">使用 Native Client ODBC 驅動程式為應用程式撰寫 ODBC 錯誤處理常式時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，最好也使用**SQLGetDiagField**來取出至少 SQL_DIAG_SS_MSGSTATE，並 SQL_DIAG_SS_SEVERITY 驅動程式特定的欄位。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-134">When coding an ODBC error handler for applications using the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC driver, it is a good idea to also use **SQLGetDiagField** to retrieve at least the SQL_DIAG_SS_MSGSTATE and SQL_DIAG_SS_SEVERITY driver-specific fields.</span></span> <span data-ttu-id="2d9c9-135">如果特定錯誤可能會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程式碼中的數個位置引發，SQL_DIAG_SS_MSGSTATE 會向 Microsoft 支援工程師明確地指出引發錯誤的位址，這項功能有時可以協助診斷問題。</span><span class="sxs-lookup"><span data-stu-id="2d9c9-135">If a particular error can be raised at several locations in the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] code, SQL_DIAG_SS_MSGSTATE indicates to a Microsoft support engineer specifically where an error was raised, which sometimes aids in diagnosing a problem.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2d9c9-136">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2d9c9-136">See Also</span></span>  
 [<span data-ttu-id="2d9c9-137">處理錯誤與訊息</span><span class="sxs-lookup"><span data-stu-id="2d9c9-137">Handling Errors and Messages</span></span>](handling-errors-and-messages.md)  
  
  