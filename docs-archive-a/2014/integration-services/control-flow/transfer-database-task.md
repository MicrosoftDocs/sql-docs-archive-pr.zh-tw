---
title: 傳送資料庫工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 85123eaff3e274bb4a96908ea99aef02c328ba23
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584666"
---
# <a name="transfer-database-task"></a><span data-ttu-id="0859e-102">傳送資料庫工作</span><span class="sxs-lookup"><span data-stu-id="0859e-102">Transfer Database Task</span></span>
  <span data-ttu-id="0859e-103">「傳送資料庫」工作會在兩個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體之間傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。</span><span class="sxs-lookup"><span data-stu-id="0859e-103">The Transfer Database task transfers a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database between two instances of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="0859e-104">與其他只能透過複製 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件來傳送它們的工作不同，「傳送資料庫」工作可以複製或移動資料庫。</span><span class="sxs-lookup"><span data-stu-id="0859e-104">In contrast to the other tasks that only transfer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objects by copying them, the Transfer Database task can either copy or move a database.</span></span> <span data-ttu-id="0859e-105">這項工作也可用來在同一部伺服器內複製資料庫。</span><span class="sxs-lookup"><span data-stu-id="0859e-105">This task can also be used to copy a database within the same server.</span></span>  
  
## <a name="offline-and-online-modes"></a><span data-ttu-id="0859e-106">離線和線上模式</span><span class="sxs-lookup"><span data-stu-id="0859e-106">Offline and Online Modes</span></span>  
 <span data-ttu-id="0859e-107">資料庫可以使用線上或離線模式傳送。</span><span class="sxs-lookup"><span data-stu-id="0859e-107">The database can be transferred by using online or offline mode.</span></span> <span data-ttu-id="0859e-108">當您使用線上模式時，資料庫會保持附加狀態，並使用 SQL Management Object (SMO) 複製資料庫物件來進行傳送。</span><span class="sxs-lookup"><span data-stu-id="0859e-108">When you use online mode, the database remains attached and it is transferred by using SQL Management Object (SMO) to copy the database objects.</span></span> <span data-ttu-id="0859e-109">當您使用離線模式時，會卸離資料庫，複製或移動資料庫檔案，並在傳送成功完成後將資料庫附加至目的地。</span><span class="sxs-lookup"><span data-stu-id="0859e-109">When you use offline mode, the database is detached, the database files are copied or moved, and the database is attached at the destination after the transfer finishes successfully.</span></span> <span data-ttu-id="0859e-110">如果複製資料庫，則會在成功複製後將資料庫自動重新附加至來源。</span><span class="sxs-lookup"><span data-stu-id="0859e-110">If the database is copied, it is automatically reattached at the source if the copy is successful.</span></span> <span data-ttu-id="0859e-111">在離線模式中，資料庫的複製速度會更快，但使用者在傳送期間無法使用資料庫。</span><span class="sxs-lookup"><span data-stu-id="0859e-111">In offline mode, the database is copied more quickly, but the database is unavailable to users during the transfer.</span></span>  
  
 <span data-ttu-id="0859e-112">離線模式需要您在包含資料庫檔案的來源和目的地伺服器上，指定網路檔案共用。</span><span class="sxs-lookup"><span data-stu-id="0859e-112">Offline mode requires that you specify the network file shares on the source and destination servers that contain the database files.</span></span> <span data-ttu-id="0859e-113">如果資料夾已共用，且可由使用者存取，則您可以使用語法 \\\computername\Program Files\myfolder\\參考網路共用。</span><span class="sxs-lookup"><span data-stu-id="0859e-113">If the folder is shared and can be accessed by the user, you can reference the network share using the syntax \\\computername\Program Files\myfolder\\.</span></span> <span data-ttu-id="0859e-114">否則，您必須使用語法 \\\computername\c$\Program Files\myfolder\\。</span><span class="sxs-lookup"><span data-stu-id="0859e-114">Otherwise, you must use the syntax \\\computername\c$\Program Files\myfolder\\.</span></span> <span data-ttu-id="0859e-115">若要使用後面的語法，使用者必須具有來源和目的地網路共用的寫入權限。</span><span class="sxs-lookup"><span data-stu-id="0859e-115">To use the latter syntax, the user must have write access to the source and destination network shares.</span></span>  
  
## <a name="transfer-of-databases-between-versions-of-sql-server"></a><span data-ttu-id="0859e-116">在 SQL Server 的版本之間傳送資料庫</span><span class="sxs-lookup"><span data-stu-id="0859e-116">Transfer of Databases Between Versions of SQL Server</span></span>  
 <span data-ttu-id="0859e-117">「傳送資料庫」工作可以在不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的執行個體之間，傳送資料庫。</span><span class="sxs-lookup"><span data-stu-id="0859e-117">The Transfer Database task can transfer a database between instances of different [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versions.</span></span>  
  
## <a name="events"></a><span data-ttu-id="0859e-118">事件</span><span class="sxs-lookup"><span data-stu-id="0859e-118">Events</span></span>  
 <span data-ttu-id="0859e-119">「傳送資料庫」工作並不報告錯誤訊息傳送的累加進度，它只報告 0% 和 100 % 完成。</span><span class="sxs-lookup"><span data-stu-id="0859e-119">The Transfer Database task does not report incremental progress of the error message transfer; it reports only 0% and 100 % completion.</span></span>  
  
## <a name="execution-value"></a><span data-ttu-id="0859e-120">執行值</span><span class="sxs-lookup"><span data-stu-id="0859e-120">Execution Value</span></span>  
 <span data-ttu-id="0859e-121">執行值 (在工作的 `ExecutionValue` 屬性中定義) 會傳回值 1，因為與其他傳送工作不同，「傳送資料庫」工作只能傳送一個資料庫。</span><span class="sxs-lookup"><span data-stu-id="0859e-121">The execution value, defined in the `ExecutionValue` property of the task, returns the value 1, because in contrast to other transfer tasks, the Transfer Database task can transfer only one database.</span></span>  
  
 <span data-ttu-id="0859e-122">透過將使用者自訂變數指派給「傳送資料庫」工作的 `ExecValueVariable` 屬性，可將與錯誤訊息傳送相關的資訊用於封裝中的其他物件。</span><span class="sxs-lookup"><span data-stu-id="0859e-122">By assigning a user-defined variable to the `ExecValueVariable` property of the Transfer Database task, information about the error message transfer can be made available to other objects in the package.</span></span> <span data-ttu-id="0859e-123">如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)和[在封裝中使用變數](../use-variables-in-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="0859e-123">For more information, see [Integration Services &#40;SSIS&#41; Variables](../integration-services-ssis-variables.md) and [Use Variables in Packages](../use-variables-in-packages.md).</span></span>  
  
## <a name="log-entries"></a><span data-ttu-id="0859e-124">記錄項目</span><span class="sxs-lookup"><span data-stu-id="0859e-124">Log Entries</span></span>  
 <span data-ttu-id="0859e-125">「傳送資料庫」工作包含下列自訂記錄項目：</span><span class="sxs-lookup"><span data-stu-id="0859e-125">The Transfer Database task includes the following custom log entries:</span></span>  
  
-   <span data-ttu-id="0859e-126">SourceSQLServer    此記錄項目列出來源伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="0859e-126">SourceSQLServer    This log entry lists the name of the source server.</span></span>  
  
-   <span data-ttu-id="0859e-127">DestSQLServer    此記錄項目列出目的地伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="0859e-127">DestSQLServer    This log entry lists the name of the destination server.</span></span>  
  
-   <span data-ttu-id="0859e-128">SourceDB    此記錄項目列出傳送之資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="0859e-128">SourceDB    This log entry lists the name of the database that is transferred.</span></span>  
  
 <span data-ttu-id="0859e-129">另外，在覆寫目的地資料庫時，會寫入 `OnInformation` 事件的記錄項目。</span><span class="sxs-lookup"><span data-stu-id="0859e-129">In addition, a log entry for the `OnInformation` event is written when the destination database is overwritten.</span></span>  
  
## <a name="security-and-permissions"></a><span data-ttu-id="0859e-130">安全性和權限</span><span class="sxs-lookup"><span data-stu-id="0859e-130">Security and Permissions</span></span>  
 <span data-ttu-id="0859e-131">若要使用離線模式傳送資料庫，執行封裝的使用者必須是 sysadmin 伺服器角色的成員。</span><span class="sxs-lookup"><span data-stu-id="0859e-131">To transfer a database using offline mode, the user who runs the package must be a member of the sysadmin server role.</span></span>  
  
 <span data-ttu-id="0859e-132">若要使用線上模式傳送資料庫，執行封裝的使用者必須是 sysadmin 伺服器角色的成員，或是選取之資料庫的資料庫擁有者 (dbo)。</span><span class="sxs-lookup"><span data-stu-id="0859e-132">To transfer a database using online mode, the user who runs the package must be a member of the sysadmin server role or the database owner (dbo) of the selected database.</span></span>  
  
## <a name="configuration-of-the-transfer-database-task"></a><span data-ttu-id="0859e-133">傳送資料庫工作的組態</span><span class="sxs-lookup"><span data-stu-id="0859e-133">Configuration of the Transfer Database Task</span></span>  
 <span data-ttu-id="0859e-134">您可以指定如果資料庫傳送失敗，工作是否嘗試重新附加來源資料庫。</span><span class="sxs-lookup"><span data-stu-id="0859e-134">You can specify whether the task tries to reattach the source database if the database transfer fails.</span></span>  
  
 <span data-ttu-id="0859e-135">「傳送資料庫」工作還可設為允許覆寫具有相同名稱的目的地資料庫，以取代目的地資料庫。</span><span class="sxs-lookup"><span data-stu-id="0859e-135">The Transfer Database task can also be configured to permit overwriting a destination database that has the same name, replacing the destination database.</span></span>  
  
 <span data-ttu-id="0859e-136">來源資料庫還可以重新命名為傳送處理序的一部分。</span><span class="sxs-lookup"><span data-stu-id="0859e-136">The source database can also be renamed as part of the transfer process.</span></span> <span data-ttu-id="0859e-137">如果您想要將資料庫傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目的地執行個體，而該執行個體已包含相同名稱的資料庫，則重新命名來源資料庫便可允許傳送資料庫。</span><span class="sxs-lookup"><span data-stu-id="0859e-137">If you want to transfer a database to a destination instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] that already contains a database that has the same name, renaming the source database allows the database to be transferred.</span></span> <span data-ttu-id="0859e-138">不過，資料庫檔案名稱也必須不同，如果目的地上已存在具有相同名稱的資料庫檔案，則工作會失敗。</span><span class="sxs-lookup"><span data-stu-id="0859e-138">However, the database file names must also be different; if database files that have the same names already exist at the destination, the task fails.</span></span>  
  
 <span data-ttu-id="0859e-139">當您複製資料庫時，資料庫不能小於目的地伺服器上的 **model** 資料庫大小。</span><span class="sxs-lookup"><span data-stu-id="0859e-139">When you copy a database, the database cannot be smaller than the size of the **model** database on the destination server.</span></span> <span data-ttu-id="0859e-140">您可以增加要複製的資料庫大小，或減少 **model**的大小。</span><span class="sxs-lookup"><span data-stu-id="0859e-140">You can either increase the size of the database to copy, or reduce the size of **model**.</span></span>  
  
 <span data-ttu-id="0859e-141">在執行階段，「傳送資料庫」工作會使用一或兩個 SMO 連接管理員，連接到來源和目的地伺服器。</span><span class="sxs-lookup"><span data-stu-id="0859e-141">At run time, the Transfer Database task connects to the source and destination servers by using one or two SMO connection managers.</span></span> <span data-ttu-id="0859e-142">當您在同一伺服器上建立資料庫的副本時，只需要一個 SMO 連接管理員。</span><span class="sxs-lookup"><span data-stu-id="0859e-142">When you create a copy of a database on the same server, only one SMO connection manager is required.</span></span> <span data-ttu-id="0859e-143">SMO 連接管理員會在「傳送資料庫」工作以外另行設定，然後在「傳送資料庫」工作中參考。</span><span class="sxs-lookup"><span data-stu-id="0859e-143">The SMO connection managers are configured separately from the Transfer Database task, and then are referenced in the Transfer Database task.</span></span> <span data-ttu-id="0859e-144">當工作存取伺服器時，SMO 連接管理員會指定要使用的伺服器和驗證模式。</span><span class="sxs-lookup"><span data-stu-id="0859e-144">The SMO connection managers specify the server and the authentication mode to use when the task accesses the server.</span></span> <span data-ttu-id="0859e-145">如需詳細資訊，請參閱 [SMO Connection Manager](../connection-manager/smo-connection-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="0859e-145">For more information, see [SMO Connection Manager](../connection-manager/smo-connection-manager.md).</span></span>  
  
 <span data-ttu-id="0859e-146">您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。</span><span class="sxs-lookup"><span data-stu-id="0859e-146">You can set properties through [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer or programmatically.</span></span>  
  
 <span data-ttu-id="0859e-147">如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：</span><span class="sxs-lookup"><span data-stu-id="0859e-147">For more information about the properties that you can set in [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, click one of the following topics:</span></span>  
  
-   [<span data-ttu-id="0859e-148">傳送資料庫工作編輯器 &#40;一般頁面&#41;</span><span class="sxs-lookup"><span data-stu-id="0859e-148">Transfer Database Task Editor &#40;General Page&#41;</span></span>](../general-page-of-integration-services-designers-options.md)  
  
-   [<span data-ttu-id="0859e-149">傳送資料庫工作編輯器 &#40;資料庫頁面&#41;</span><span class="sxs-lookup"><span data-stu-id="0859e-149">Transfer Database Task Editor &#40;Databases Page&#41;</span></span>](../transfer-database-task-editor-databases-page.md)  
  
-   [<span data-ttu-id="0859e-150">運算式頁面</span><span class="sxs-lookup"><span data-stu-id="0859e-150">Expressions Page</span></span>](../expressions/expressions-page.md)  
  
 <span data-ttu-id="0859e-151">如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：</span><span class="sxs-lookup"><span data-stu-id="0859e-151">For more information about how to set these properties in [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, click the following topic:</span></span>  
  
-   [<span data-ttu-id="0859e-152">設定工作或容器的屬性</span><span class="sxs-lookup"><span data-stu-id="0859e-152">Set the Properties of a Task or Container</span></span>](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a><span data-ttu-id="0859e-153">傳送資料庫工作的程式設計組態</span><span class="sxs-lookup"><span data-stu-id="0859e-153">Programmatic Configuration of the Transfer Database Task</span></span>  
 <span data-ttu-id="0859e-154">如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：</span><span class="sxs-lookup"><span data-stu-id="0859e-154">For more information about programmatically setting these properties, click the following topic:</span></span>  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
  
