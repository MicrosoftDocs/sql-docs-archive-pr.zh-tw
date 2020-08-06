---
title: 使用檔案輸入輸出 API 存取 FileTable | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], accessing files with file APIs
ms.assetid: fa504c5a-f131-4781-9a90-46e6c2de27bb
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 56118ef2db319abd270ff51259e3537864fdd57e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705182"
---
# <a name="access-filetables-with-file-input-output-apis"></a><span data-ttu-id="adc95-102">使用檔案輸入輸出 API 存取 FileTable</span><span class="sxs-lookup"><span data-stu-id="adc95-102">Access FileTables with File Input-Output APIs</span></span>
  <span data-ttu-id="adc95-103">描述檔案系統 I/O 如何在 FileTable 上運作。</span><span class="sxs-lookup"><span data-stu-id="adc95-103">Describes how file system I/O works on a FileTable.</span></span>  
  
##  <a name="get-started-using-file-io-apis-with-filetables"></a><a name="accessing"></a> <span data-ttu-id="adc95-104">開始使用 FileTable 檔案的 I/O API</span><span class="sxs-lookup"><span data-stu-id="adc95-104">Get Started Using File I/O APIs with FileTables</span></span>  
 <span data-ttu-id="adc95-105">FileTable 的主要用法是透過 Windows 檔案系統和檔案 I/O API。</span><span class="sxs-lookup"><span data-stu-id="adc95-105">The primary usage of FileTables is expected to be through the Windows file system and file I/O APIs.</span></span> <span data-ttu-id="adc95-106">FileTable 支援透過一系列可用檔案 I/O API 的非交易式存取。</span><span class="sxs-lookup"><span data-stu-id="adc95-106">FileTables support non-transactional access through the rich set of available file I/O APIs.</span></span>  
  
1.  <span data-ttu-id="adc95-107">檔案 I/O API 存取通常一開始會先取得檔案或目錄的邏輯 UNC 路徑。</span><span class="sxs-lookup"><span data-stu-id="adc95-107">File I/O API access typically begins by acquiring a logical UNC path for the file or directory.</span></span> <span data-ttu-id="adc95-108">應用程式可以搭配 [GetFileNamespacePath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql) 函數使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，以取得檔案或目錄的邏輯路徑。</span><span class="sxs-lookup"><span data-stu-id="adc95-108">Applications can use a [!INCLUDE[tsql](../../includes/tsql-md.md)] statement with the [GetFileNamespacePath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql) function to obtain the logical path for the file or directory.</span></span> <span data-ttu-id="adc95-109">如需詳細資訊，請參閱 [Work with Directories and Paths in FileTables](work-with-directories-and-paths-in-filetables.md)。</span><span class="sxs-lookup"><span data-stu-id="adc95-109">For more information, see [Work with Directories and Paths in FileTables](work-with-directories-and-paths-in-filetables.md).</span></span>  
  
2.  <span data-ttu-id="adc95-110">然後應用程式會使用此邏輯路徑以取得檔案或目錄控制代碼，並對物件進行操作。</span><span class="sxs-lookup"><span data-stu-id="adc95-110">Then the application uses this logical path to obtain a handle to the file or directory and do something with the object.</span></span> <span data-ttu-id="adc95-111">該路徑可傳遞至任何支援的檔案系統 API 函數，例如 CreateFile() 或 CreateDirectory()，以建立或開啟檔案並取得控制代碼。</span><span class="sxs-lookup"><span data-stu-id="adc95-111">The path can be passed to any supported file system API function, such as CreateFile() or CreateDirectory(), to create or open a file and obtain a handle.</span></span> <span data-ttu-id="adc95-112">控制代碼隨後便可用於以資料流形式處理資料、列舉或組織目錄、取得或設定檔案屬性、刪除檔案或目錄等。</span><span class="sxs-lookup"><span data-stu-id="adc95-112">The handle can then be used to stream data, to enumerate or organize directories, to get or set file attributes, to delete files or directories, and so forth.</span></span>  
  
##  <a name="creating-files-and-directories-in-a-filetable"></a><a name="create"></a> <span data-ttu-id="adc95-113">在 FileTable 中建立檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="adc95-113">Creating Files and Directories in a FileTable</span></span>  
 <span data-ttu-id="adc95-114">透過呼叫檔案 I/O API (例如 CreateFile 或 CreateDirectory) 在 FileTable 中建立檔案或目錄。</span><span class="sxs-lookup"><span data-stu-id="adc95-114">A file or directory can be created in a FileTable by calling file I/O APIs such as CreateFile or CreateDirectory.</span></span>  
  
-   <span data-ttu-id="adc95-115">支援所有建立配置旗標、共用模式及存取模式。</span><span class="sxs-lookup"><span data-stu-id="adc95-115">All creation disposition flags, share modes, and access modes are supported.</span></span> <span data-ttu-id="adc95-116">其中包括檔案建立、刪除及就地修改。</span><span class="sxs-lookup"><span data-stu-id="adc95-116">This includes file creation, deletion and in-place modification.</span></span> <span data-ttu-id="adc95-117">另外也支援檔案命名空間更新，例如目錄建立/刪除、重新命名和移動作業。</span><span class="sxs-lookup"><span data-stu-id="adc95-117">Also supported are File Namespace updates i.e. directory creation/deletion, rename and move operations.</span></span>  
  
-   <span data-ttu-id="adc95-118">新檔案或目錄的建立會對應到基礎 FileTable 中新資料列的建立。</span><span class="sxs-lookup"><span data-stu-id="adc95-118">The creation of a new file or directory corresponds to the creation of a new row in the underlying FileTable.</span></span>  
  
-   <span data-ttu-id="adc95-119">若為檔案，資料流資料會儲存在 **file_stream** 資料行中；若為目錄，此資料行為 null。</span><span class="sxs-lookup"><span data-stu-id="adc95-119">For files, the stream data is stored in the **file_stream** column; for directories, this column is null.</span></span>  
  
-   <span data-ttu-id="adc95-120">若為檔案， **is_directory** 資料行內含 **false**。</span><span class="sxs-lookup"><span data-stu-id="adc95-120">For files, the **is_directory** column contains **false**.</span></span> <span data-ttu-id="adc95-121">若為目錄，此資料行內含 **true**。</span><span class="sxs-lookup"><span data-stu-id="adc95-121">For directories, this column contains **true**.</span></span>  
  
-   <span data-ttu-id="adc95-122">當多個並行的檔案 I/O 作業或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業在階層中影響同一個檔案或目錄時，會強制執行共用存取及並行存取。</span><span class="sxs-lookup"><span data-stu-id="adc95-122">Sharing and concurrency of access are enforced when multiple concurrent file I/O operations or [!INCLUDE[tsql](../../includes/tsql-md.md)] operations affect the same file or directory in the hierarchy.</span></span>  
  
##  <a name="reading-files-and-directories-in-a-filetable"></a><a name="read"></a> <span data-ttu-id="adc95-123">讀取 FileTable 中的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="adc95-123">Reading Files and Directories in a FileTable</span></span>  
 <span data-ttu-id="adc95-124">若為所有資料流及屬性資料的檔案 I/O 存取作業， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會強制執行讀取認可隔離語意。</span><span class="sxs-lookup"><span data-stu-id="adc95-124">Read Committed isolation semantics are enforced in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for all file I/O access operations on stream and attribute data.</span></span>  
  
##  <a name="writing-and-updating-files-and-directories-in-a-filetable"></a><a name="write"></a> <span data-ttu-id="adc95-125">寫入及更新 FileTable 中的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="adc95-125">Writing and Updating Files and Directories in a FileTable</span></span>  
  
-   <span data-ttu-id="adc95-126">所有 FileTable 上的檔案 I/O 寫入或更新作業都是非交易式的。</span><span class="sxs-lookup"><span data-stu-id="adc95-126">All file I/O write or update operations on a FileTable are non-transactional.</span></span> <span data-ttu-id="adc95-127">也就是說，不會有任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交易繫結至這些作業，而且不會提供任何 ACID 保證。</span><span class="sxs-lookup"><span data-stu-id="adc95-127">That is, no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transaction is bound to these operations, and no ACID guarantees are provided.</span></span>  
  
-   <span data-ttu-id="adc95-128">FileTable 支援所有檔案 I/O 資料流/就地更新。</span><span class="sxs-lookup"><span data-stu-id="adc95-128">All file I/O streaming/in-place updates are supported for the FileTable.</span></span>  
  
-   <span data-ttu-id="adc95-129">透過檔案 I/O API 進行的 FILESTREAM 資料或屬性更新都將更新 FileTable 中對應的 **file_stream** 及對應的檔案屬性資料行。</span><span class="sxs-lookup"><span data-stu-id="adc95-129">Updates to the FILESTREAM data or attributes through file I/O APIs result in updates of the corresponding **file_stream** and file attribute columns in the FileTable.</span></span>  
  
##  <a name="deleting-files-and-directories-in-a-filetable"></a><a name="delete"></a> <span data-ttu-id="adc95-130">刪除 FileTable 中的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="adc95-130">Deleting Files and Directories in a FileTable</span></span>  
 <span data-ttu-id="adc95-131">當您刪除檔案或目錄時會強制執行所有 Windows 檔案 I/O API 語意。</span><span class="sxs-lookup"><span data-stu-id="adc95-131">All Windows file I/O API semantics are enforced when you delete a file or directory.</span></span>  
  
-   <span data-ttu-id="adc95-132">如果目錄中包含任何檔案的子目錄，將無法刪除目錄。</span><span class="sxs-lookup"><span data-stu-id="adc95-132">Deleting a directory fails if the directory contains any files subdirectories.</span></span>  
  
-   <span data-ttu-id="adc95-133">刪除檔案或目錄將會從 FileTable 中移除對應的資料列。</span><span class="sxs-lookup"><span data-stu-id="adc95-133">Deleting a file or directory removes the corresponding row from the FileTable.</span></span> <span data-ttu-id="adc95-134">這相當於透過 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業刪除該資料列。</span><span class="sxs-lookup"><span data-stu-id="adc95-134">This is equivalent to deleting the row through a [!INCLUDE[tsql](../../includes/tsql-md.md)] operation.</span></span>  
  
##  <a name="supported-file-system-operations"></a><a name="supported"></a> <span data-ttu-id="adc95-135">支援的檔案系統作業</span><span class="sxs-lookup"><span data-stu-id="adc95-135">Supported File System Operations</span></span>  
 <span data-ttu-id="adc95-136">FileTable 支援與下列檔案系統作業相關的檔案系統 API：</span><span class="sxs-lookup"><span data-stu-id="adc95-136">FileTables support the file system APIs related to the following file system operations:</span></span>  
  
-   <span data-ttu-id="adc95-137">目錄管理</span><span class="sxs-lookup"><span data-stu-id="adc95-137">Directory Management</span></span>  
  
-   <span data-ttu-id="adc95-138">檔案管理</span><span class="sxs-lookup"><span data-stu-id="adc95-138">File Management</span></span>  
  
 <span data-ttu-id="adc95-139">FileTable 不支援下列作業：</span><span class="sxs-lookup"><span data-stu-id="adc95-139">FileTables do not support the following operations:</span></span>  
  
-   <span data-ttu-id="adc95-140">磁碟管理</span><span class="sxs-lookup"><span data-stu-id="adc95-140">Disk Management</span></span>  
  
-   <span data-ttu-id="adc95-141">磁碟區管理</span><span class="sxs-lookup"><span data-stu-id="adc95-141">Volume Management</span></span>  
  
-   <span data-ttu-id="adc95-142">交易式 NTFS</span><span class="sxs-lookup"><span data-stu-id="adc95-142">Transactional NTFS</span></span>  
  
##  <a name="additional-considerations-for-file-io-access-to-filetables"></a><a name="considerations"></a> <span data-ttu-id="adc95-143">FileTable 之檔案 I/O 存取的其他考量</span><span class="sxs-lookup"><span data-stu-id="adc95-143">Additional Considerations for File I/O Access to FileTables</span></span>  
  
###  <a name="using-virtual-network-names-vnns-with-alwayson-availability-groups"></a><a name="vnn"></a> <span data-ttu-id="adc95-144">使用虛擬網路名稱 (VNN) 搭配 AlwaysOn 可用性群組</span><span class="sxs-lookup"><span data-stu-id="adc95-144">Using Virtual Network Names (VNNs) with AlwaysOn Availability Groups</span></span>  
 <span data-ttu-id="adc95-145">當包含 FILESTREAM 或 FileTable 資料的資料庫屬於 AlwaysOn 可用性群組時，透過檔案系統 API 對 FILESTREAM 或 FileTable 資料進行的所有存取都應該使用 VNN 而非電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="adc95-145">When the database that contains FILESTREAM or FileTable data belongs to an AlwaysOn availability group, then all access to FILESTREAM or FileTable data through the file system APIs should use VNNs instead of computer names.</span></span> <span data-ttu-id="adc95-146">如需詳細資訊，請參閱 [FILESTREAM 和 FileTable 與 AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)。</span><span class="sxs-lookup"><span data-stu-id="adc95-146">For more information, see [FILESTREAM and FileTable with AlwaysOn Availability Groups &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md).</span></span>  
  
###  <a name="partial-updates"></a><a name="partial"></a> <span data-ttu-id="adc95-147">部分更新</span><span class="sxs-lookup"><span data-stu-id="adc95-147">Partial Updates</span></span>  
 <span data-ttu-id="adc95-148">使用 [GetFileNamespacePath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql) 函數在 FileTable 中取得的 FILESTREAM 資料可寫入控制代碼，可用於執行 FILESTREAM 內容的就地、部分更新。</span><span class="sxs-lookup"><span data-stu-id="adc95-148">A writable handle obtained for FILESTREAM data in a FileTable by using the [GetFileNamespacePath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql) function can be used to make in-place, partial updates to the FILESTREAM content.</span></span> <span data-ttu-id="adc95-149">此行為與交易 FILESTREAM 存取不同，它是透過呼叫 **OpenSQLFILESTREAM()** 及傳遞明確交易內容所取得的控制代碼來進行。</span><span class="sxs-lookup"><span data-stu-id="adc95-149">This behavior is different from the transacted FILESTREAM access through a handle obtained by calling **OpenSQLFILESTREAM()** and passing an explicit transaction context.</span></span>  
  
###  <a name="transactional-semantics"></a><a name="trans"></a> <span data-ttu-id="adc95-150">交易式語意</span><span class="sxs-lookup"><span data-stu-id="adc95-150">Transactional Semantics</span></span>  
 <span data-ttu-id="adc95-151">當您使用檔案 I/O API 於 FileTable 中存取檔案時，這些作業不會與任何使用者交易有關聯，並且具有下列其他特性：</span><span class="sxs-lookup"><span data-stu-id="adc95-151">When you access the files in a FileTable by using file I/O APIs, these operations are not associated with any user transactions, and have the following additional characteristics:</span></span>  
  
-   <span data-ttu-id="adc95-152">FileTable 中 FILESTREAM 資料的非交易式存取與任何交易無關，因此不會有任何特定的隔離語意。</span><span class="sxs-lookup"><span data-stu-id="adc95-152">Since non-transacted access to FILESTREAM data in a FileTable is not associated with any transaction, it does not have any specific isolation semantics.</span></span> <span data-ttu-id="adc95-153">但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會使用內部交易，針對 FileTable 資料強制執行鎖定或並行語意。</span><span class="sxs-lookup"><span data-stu-id="adc95-153">However [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] may use internal transactions to enforce locking or concurrency semantics on the FileTable data.</span></span> <span data-ttu-id="adc95-154">此類型的任何內部交易都已完成讀取認可隔離。</span><span class="sxs-lookup"><span data-stu-id="adc95-154">Any internal transactions of this type are done with read-committed isolation.</span></span>  
  
-   <span data-ttu-id="adc95-155">這些 FILESTREAM 資料上的非交易作業沒有任何 ACID 保證。</span><span class="sxs-lookup"><span data-stu-id="adc95-155">There are no ACID guarantees for these non-transacted operations on FILESTREAM data.</span></span> <span data-ttu-id="adc95-156">一致性保證類似於檔案系統上應用程式所建立的檔案更新。</span><span class="sxs-lookup"><span data-stu-id="adc95-156">The consistency guarantees are similar to those for file updates made by applications in the file system.</span></span>  
  
-   <span data-ttu-id="adc95-157">這些變更無法回復。</span><span class="sxs-lookup"><span data-stu-id="adc95-157">These changes cannot be rolled back.</span></span>  
  
 <span data-ttu-id="adc95-158">但是，FileTable 中的 FILESTREAM 資料行也可以透過呼叫 **OpenSqlFileStream()** ，與交易式 FILESTREAM 存取一同進行存取。</span><span class="sxs-lookup"><span data-stu-id="adc95-158">However, the FILESTREAM column in a FileTable can also be accessed with transactional FILESTREAM access by calling **OpenSqlFileStream()**.</span></span> <span data-ttu-id="adc95-159">這種存取可以完全為交易式，而且會接受目前一致支援的所有交易式層級。</span><span class="sxs-lookup"><span data-stu-id="adc95-159">This kind of access can be fully transactional and will honor all the levels of transactional consistently that are currently supported.</span></span>  
  
###  <a name="concurrency-control"></a><a name="concurrency"></a> <span data-ttu-id="adc95-160">並行存取控制</span><span class="sxs-lookup"><span data-stu-id="adc95-160">Concurrency Control</span></span>  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="adc95-161">會在檔案系統應用程式之間以及檔案系統應用程式和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 應用程式之間強制執行 FileTable 存取的並行存取控制。</span><span class="sxs-lookup"><span data-stu-id="adc95-161">enforces concurrency control for FileTable access among file system applications, and between file system applications and [!INCLUDE[tsql](../../includes/tsql-md.md)] applications.</span></span> <span data-ttu-id="adc95-162">達成此並行存取控制的方式是針對 FileTable 資料列採取適當的鎖定。</span><span class="sxs-lookup"><span data-stu-id="adc95-162">This concurrency control is achieved by taking appropriate locks on the FileTable rows.</span></span>  
  
###  <a name="triggers"></a><a name="triggers"></a> <span data-ttu-id="adc95-163">觸發程序</span><span class="sxs-lookup"><span data-stu-id="adc95-163">Triggers</span></span>  
 <span data-ttu-id="adc95-164">透過檔案系統建立、修改、或刪除檔案或目錄或其屬性，將會導致 FileTable 中對應的插入、更新或刪除作業。</span><span class="sxs-lookup"><span data-stu-id="adc95-164">Creating, modifying, or deleting files or directories or their attributes through the file system results in corresponding insert, update, or delete operations in the FileTable.</span></span> <span data-ttu-id="adc95-165">任何關聯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] DML 觸發程序都會當做這些作業的一部分引發。</span><span class="sxs-lookup"><span data-stu-id="adc95-165">Any associated [!INCLUDE[tsql](../../includes/tsql-md.md)] DML triggers are fired as part of these operations.</span></span>  
  
##  <a name="file-system-functionality-supported-in-filetables"></a><a name="funclist"></a> <span data-ttu-id="adc95-166">FileTable 中支援的檔案系統功能</span><span class="sxs-lookup"><span data-stu-id="adc95-166">File System Functionality Supported in FileTables</span></span>  
  
|<span data-ttu-id="adc95-167">功能</span><span class="sxs-lookup"><span data-stu-id="adc95-167">Capability</span></span>|<span data-ttu-id="adc95-168">支援</span><span class="sxs-lookup"><span data-stu-id="adc95-168">Supported</span></span>|<span data-ttu-id="adc95-169">註解</span><span class="sxs-lookup"><span data-stu-id="adc95-169">Comments</span></span>|  
|----------------|---------------|--------------|  
|<span data-ttu-id="adc95-170">**Oplock**</span><span class="sxs-lookup"><span data-stu-id="adc95-170">**Oplocks**</span></span>|<span data-ttu-id="adc95-171">是</span><span class="sxs-lookup"><span data-stu-id="adc95-171">Yes</span></span>|<span data-ttu-id="adc95-172">支援層級 2、層級 1、批次和篩選器 oplock。</span><span class="sxs-lookup"><span data-stu-id="adc95-172">There is support for Level 2, Level 1, Batch and Filter oplocks.</span></span>|  
|<span data-ttu-id="adc95-173">**擴充屬性**</span><span class="sxs-lookup"><span data-stu-id="adc95-173">**Extended Attributes**</span></span>|<span data-ttu-id="adc95-174">否</span><span class="sxs-lookup"><span data-stu-id="adc95-174">No</span></span>||  
|<span data-ttu-id="adc95-175">**重新剖析點**</span><span class="sxs-lookup"><span data-stu-id="adc95-175">**Reparse Points**</span></span>|<span data-ttu-id="adc95-176">否</span><span class="sxs-lookup"><span data-stu-id="adc95-176">No</span></span>||  
|<span data-ttu-id="adc95-177">**持續的 ACL**</span><span class="sxs-lookup"><span data-stu-id="adc95-177">**Persistent ACLs**</span></span>|<span data-ttu-id="adc95-178">否</span><span class="sxs-lookup"><span data-stu-id="adc95-178">No</span></span>||  
|<span data-ttu-id="adc95-179">**具名資料流**</span><span class="sxs-lookup"><span data-stu-id="adc95-179">**Named Streams**</span></span>|<span data-ttu-id="adc95-180">否</span><span class="sxs-lookup"><span data-stu-id="adc95-180">No</span></span>||  
|<span data-ttu-id="adc95-181">**疏鬆檔案**</span><span class="sxs-lookup"><span data-stu-id="adc95-181">**Sparse Files**</span></span>|<span data-ttu-id="adc95-182">是</span><span class="sxs-lookup"><span data-stu-id="adc95-182">Yes</span></span>|<span data-ttu-id="adc95-183">疏鬆性只能在檔案上設定，而且會影響資料流的儲存方式。</span><span class="sxs-lookup"><span data-stu-id="adc95-183">Sparseness can be set only on files, and affects the storage of the data stream.</span></span> <span data-ttu-id="adc95-184">FILESTREAM 資料儲存在 NTFS 磁碟區上，因此 FileTable 功能會將要求轉送至 NTFS 檔案系統以支援疏鬆檔案。</span><span class="sxs-lookup"><span data-stu-id="adc95-184">Since FILESTREAM data is stored on NTFS volumes, the FileTable feature supports sparse files by forwarding the requests to the NTFS file system.</span></span>|  
|<span data-ttu-id="adc95-185">**壓縮**</span><span class="sxs-lookup"><span data-stu-id="adc95-185">**Compression**</span></span>|<span data-ttu-id="adc95-186">是</span><span class="sxs-lookup"><span data-stu-id="adc95-186">Yes</span></span>||  
|<span data-ttu-id="adc95-187">**加密**</span><span class="sxs-lookup"><span data-stu-id="adc95-187">**Encryptiion**</span></span>|<span data-ttu-id="adc95-188">是</span><span class="sxs-lookup"><span data-stu-id="adc95-188">Yes</span></span>||  
|<span data-ttu-id="adc95-189">**TxF**</span><span class="sxs-lookup"><span data-stu-id="adc95-189">**TxF**</span></span>|<span data-ttu-id="adc95-190">否</span><span class="sxs-lookup"><span data-stu-id="adc95-190">No</span></span>||  
|<span data-ttu-id="adc95-191">**檔案識別碼**</span><span class="sxs-lookup"><span data-stu-id="adc95-191">**File Ids**</span></span>|<span data-ttu-id="adc95-192">否</span><span class="sxs-lookup"><span data-stu-id="adc95-192">No</span></span>||  
|<span data-ttu-id="adc95-193">**物件識別碼**</span><span class="sxs-lookup"><span data-stu-id="adc95-193">**Object Ids**</span></span>|<span data-ttu-id="adc95-194">否</span><span class="sxs-lookup"><span data-stu-id="adc95-194">No</span></span>||  
|<span data-ttu-id="adc95-195">**符號連結**</span><span class="sxs-lookup"><span data-stu-id="adc95-195">**Symbolic links**</span></span>|<span data-ttu-id="adc95-196">否</span><span class="sxs-lookup"><span data-stu-id="adc95-196">No</span></span>||  
|<span data-ttu-id="adc95-197">**永久連結**</span><span class="sxs-lookup"><span data-stu-id="adc95-197">**Hard links**</span></span>|<span data-ttu-id="adc95-198">否</span><span class="sxs-lookup"><span data-stu-id="adc95-198">No</span></span>||  
|<span data-ttu-id="adc95-199">**簡短名稱**</span><span class="sxs-lookup"><span data-stu-id="adc95-199">**Short names**</span></span>|<span data-ttu-id="adc95-200">否</span><span class="sxs-lookup"><span data-stu-id="adc95-200">No</span></span>||  
|<span data-ttu-id="adc95-201">**目錄變更通知**</span><span class="sxs-lookup"><span data-stu-id="adc95-201">**Directory change notifications**</span></span>|<span data-ttu-id="adc95-202">否</span><span class="sxs-lookup"><span data-stu-id="adc95-202">No</span></span>||  
|<span data-ttu-id="adc95-203">**位元組範圍鎖定**</span><span class="sxs-lookup"><span data-stu-id="adc95-203">**Byte range locking**</span></span>|<span data-ttu-id="adc95-204">是</span><span class="sxs-lookup"><span data-stu-id="adc95-204">Yes</span></span>|<span data-ttu-id="adc95-205">位元組範圍鎖定的要求會傳遞到 NTFS 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="adc95-205">Requests for byte range locking are passed to the NTFS file system.</span></span>|  
|<span data-ttu-id="adc95-206">**記憶體對應檔案**</span><span class="sxs-lookup"><span data-stu-id="adc95-206">**Memory mapped files**</span></span>|<span data-ttu-id="adc95-207">否</span><span class="sxs-lookup"><span data-stu-id="adc95-207">No</span></span>||  
|<span data-ttu-id="adc95-208">**取消 I/O**</span><span class="sxs-lookup"><span data-stu-id="adc95-208">**Cancel I/O**</span></span>|<span data-ttu-id="adc95-209">是</span><span class="sxs-lookup"><span data-stu-id="adc95-209">Yes</span></span>||  
|<span data-ttu-id="adc95-210">**安全性**</span><span class="sxs-lookup"><span data-stu-id="adc95-210">**Security**</span></span>|<span data-ttu-id="adc95-211">否</span><span class="sxs-lookup"><span data-stu-id="adc95-211">No</span></span>|<span data-ttu-id="adc95-212">系統會強制執行 Windows 共用層級安全性和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表與資料行層級安全性。</span><span class="sxs-lookup"><span data-stu-id="adc95-212">Windows share level security and [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] table and column level security are enforced.</span></span>|  
|<span data-ttu-id="adc95-213">**USN 日誌**</span><span class="sxs-lookup"><span data-stu-id="adc95-213">**USN journal**</span></span>|<span data-ttu-id="adc95-214">否</span><span class="sxs-lookup"><span data-stu-id="adc95-214">No</span></span>|<span data-ttu-id="adc95-215">FileTable 和 DML 作業中檔案和目錄的中繼資料變更為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫上的 DML 作業。</span><span class="sxs-lookup"><span data-stu-id="adc95-215">Metadata changes to files and directories in a FileTable are DML operations on a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.</span></span> <span data-ttu-id="adc95-216">因此，這些會記錄在對應的資料庫記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="adc95-216">Therefore they are logged in the corresponding database log file.</span></span> <span data-ttu-id="adc95-217">但是，並不會記錄在 NTFS USN 日誌中 (除非大小有變更)。</span><span class="sxs-lookup"><span data-stu-id="adc95-217">However they are not logged in the NTFS USN journal (except for changes in size).</span></span><br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="adc95-218">變更追蹤功能可用於取得類似的資訊。</span><span class="sxs-lookup"><span data-stu-id="adc95-218">change tracking capabilities can be used to capture similar information.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="adc95-219">另請參閱</span><span class="sxs-lookup"><span data-stu-id="adc95-219">See Also</span></span>  
 <span data-ttu-id="adc95-220">[載入檔案至 FileTable](load-files-into-filetables.md) </span><span class="sxs-lookup"><span data-stu-id="adc95-220">[Load Files into FileTables](load-files-into-filetables.md) </span></span>  
 <span data-ttu-id="adc95-221">[Work with Directories and Paths in FileTables](work-with-directories-and-paths-in-filetables.md) </span><span class="sxs-lookup"><span data-stu-id="adc95-221">[Work with Directories and Paths in FileTables](work-with-directories-and-paths-in-filetables.md) </span></span>  
 <span data-ttu-id="adc95-222">[利用 Transact-SQL 存取 FileTable](access-filetables-with-transact-sql.md) </span><span class="sxs-lookup"><span data-stu-id="adc95-222">[Access FileTables with Transact-SQL](access-filetables-with-transact-sql.md) </span></span>  
 [<span data-ttu-id="adc95-223">FileTable DDL、函數、預存程序及檢視</span><span class="sxs-lookup"><span data-stu-id="adc95-223">FileTable DDL, Functions, Stored Procedures, and Views</span></span>](../views/views.md)  
  
  