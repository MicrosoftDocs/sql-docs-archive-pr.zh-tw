---
title: 建立登入 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- creating a login
ms.assetid: a2512310-bdb6-41dc-858a-e866b2b58afc
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 400a57693fbea10270a51f5735a19b9639112ce9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705813"
---
# <a name="creating-a-login"></a><span data-ttu-id="92e65-102">建立登入</span><span class="sxs-lookup"><span data-stu-id="92e65-102">Creating a Login</span></span>
  <span data-ttu-id="92e65-103">若要存取 [!INCLUDE[ssDE](../includes/ssde-md.md)]，使用者需要登入。</span><span class="sxs-lookup"><span data-stu-id="92e65-103">To access the [!INCLUDE[ssDE](../includes/ssde-md.md)], users require a login.</span></span> <span data-ttu-id="92e65-104">登入可以用 Windows 帳戶或 Windows 群組的成員來代表使用者的身分識別，或者登入也可以是只存在於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]登入。</span><span class="sxs-lookup"><span data-stu-id="92e65-104">The login can represent the user's identity as a Windows account or as a member of a Windows group, or the login can be a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] login that exists only in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="92e65-105">請盡可能使用「Windows 驗證」。</span><span class="sxs-lookup"><span data-stu-id="92e65-105">Whenever possible you should use Windows Authentication.</span></span>  
  
 <span data-ttu-id="92e65-106">依預設，電腦的管理員具有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的完整存取權。</span><span class="sxs-lookup"><span data-stu-id="92e65-106">By default, administrators on your computer have full access to [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="92e65-107">在這一課中，我們希望有權限較低的使用者，因此您將會在電腦上建立新的本機「Windows 驗證」帳戶。</span><span class="sxs-lookup"><span data-stu-id="92e65-107">For this lesson, we want to have a less privileged user; therefore, you will create a new local Windows Authentication account on your computer.</span></span> <span data-ttu-id="92e65-108">若要執行此作業，您必須是電腦的管理員。</span><span class="sxs-lookup"><span data-stu-id="92e65-108">To do this, you must be an administrator on your computer.</span></span> <span data-ttu-id="92e65-109">接著，您將會為新使用者授與 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的存取權。</span><span class="sxs-lookup"><span data-stu-id="92e65-109">Then you will grant that new user access to [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].</span></span>  
  
### <a name="to-create-a-new-windows-account"></a><span data-ttu-id="92e65-110">若要建立新的 Windows 帳戶</span><span class="sxs-lookup"><span data-stu-id="92e65-110">To create a new Windows account</span></span>  
  
1.  <span data-ttu-id="92e65-111">按一下 [**開始**]，按一下 [**執行**]，在 [**開啟**] 方塊中輸入 `%SystemRoot%\system32\compmgmt.msc /s` ，然後按一下 **[確定]** 以開啟 [電腦管理] 程式。</span><span class="sxs-lookup"><span data-stu-id="92e65-111">Click **Start**, click **Run**, in the **Open** box, type `%SystemRoot%\system32\compmgmt.msc /s`, and then click **OK** to open the Computer Management program.</span></span>  
  
2.  <span data-ttu-id="92e65-112">在 [系統工具]\*\*\*\* 底下，展開 [本機使用者和群組]\*\*\*\*，以滑鼠右鍵按一下 [使用者]\*\*\*\*，然後按一下 [新增使用者]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="92e65-112">Under **System Tools**, expand **Local Users and Groups**, right-click **Users**, and then click **New User**.</span></span>  
  
3.  <span data-ttu-id="92e65-113">在 [使用者名稱]\*\*\*\* 方塊中輸入 **Mary**。</span><span class="sxs-lookup"><span data-stu-id="92e65-113">In the **User name** box type **Mary**.</span></span>  
  
4.  <span data-ttu-id="92e65-114">在 [密碼]\*\*\*\* 和 [確認密碼]\*\*\*\* 方塊中輸入強式密碼，然後按一下 [建立]\*\*\*\*，建立新的本機 Windows 使用者。</span><span class="sxs-lookup"><span data-stu-id="92e65-114">In the **Password** and **Confirm password** box, type a strong password, and then click **Create** to create a new local Windows user.</span></span>  
  
### <a name="to-create-a-login"></a><span data-ttu-id="92e65-115">若要建立登入</span><span class="sxs-lookup"><span data-stu-id="92e65-115">To create a login</span></span>  
  
1.  <span data-ttu-id="92e65-116">在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的 [查詢編輯器] 視窗中，輸入並執行下列程式碼，並以您的電腦名稱取代 `computer_name` 。</span><span class="sxs-lookup"><span data-stu-id="92e65-116">In a Query Editor window of [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], type and execute the following code replacing `computer_name` with the name of your computer.</span></span> <span data-ttu-id="92e65-117">`FROM WINDOWS` 表示 Windows 將會驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="92e65-117">`FROM WINDOWS` indicates that Windows will authenticate the user.</span></span> <span data-ttu-id="92e65-118">選擇性的 `DEFAULT_DATABASE` 引數會將 `Mary` 連接到 `TestData` 資料庫，除非她的連接字串指定要連接到其他資料庫。</span><span class="sxs-lookup"><span data-stu-id="92e65-118">The optional `DEFAULT_DATABASE` argument connects `Mary` to the `TestData` database, unless her connection string indicates another database.</span></span> <span data-ttu-id="92e65-119">這個陳述式採用分號作為 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式的選擇性結束符號。</span><span class="sxs-lookup"><span data-stu-id="92e65-119">This statement introduces the semicolon as an optional termination for a [!INCLUDE[tsql](../includes/tsql-md.md)] statement.</span></span>  
  
    ```  
    CREATE LOGIN [computer_name\Mary]  
        FROM WINDOWS  
        WITH DEFAULT_DATABASE = [TestData];  
    GO  
    ```  
  
     <span data-ttu-id="92e65-120">這個陳述式會授權使用者名稱 `Mary`在經過電腦驗證之後，可以存取這個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體。</span><span class="sxs-lookup"><span data-stu-id="92e65-120">This authorizes a user name `Mary`, authenticated by your computer, to access this instance of [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="92e65-121">如果電腦上有一個以上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，則您必須在 `Mary` 需要存取的每一個執行個體上分別建立登入。</span><span class="sxs-lookup"><span data-stu-id="92e65-121">If there is more than one instance of [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on the computer, you must create the login on each instance that `Mary` must access.</span></span>  
  
    > [!NOTE]  
    >  <span data-ttu-id="92e65-122">由於 `Mary` 不是網域帳戶，因此這個使用者名稱只能在這部電腦上進行驗證。</span><span class="sxs-lookup"><span data-stu-id="92e65-122">Because `Mary` is not a domain account, this user name can only be authenticated on this computer.</span></span>  
  
## <a name="next-task-in-lesson"></a><span data-ttu-id="92e65-123">本課程的下一項工作</span><span class="sxs-lookup"><span data-stu-id="92e65-123">Next Task in Lesson</span></span>  
 [<span data-ttu-id="92e65-124">授與資料庫的存取權</span><span class="sxs-lookup"><span data-stu-id="92e65-124">Granting Access to a Database</span></span>](lesson-2-2-granting-access-to-a-database.md)  
  
## <a name="see-also"></a><span data-ttu-id="92e65-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="92e65-125">See Also</span></span>  
 <span data-ttu-id="92e65-126">[CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="92e65-126">[CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql) </span></span>  
 [<span data-ttu-id="92e65-127">選擇驗證模式</span><span class="sxs-lookup"><span data-stu-id="92e65-127">Choose an Authentication Mode</span></span>](../relational-databases/security/choose-an-authentication-mode.md)  
  
  
