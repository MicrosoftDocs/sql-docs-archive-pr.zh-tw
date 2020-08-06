---
title: SQL Server 2014 Express LocalDB |Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- user instances
- LocalDB, described
- local database runtime
- file database
- LocalDB
ms.assetid: 5a641a46-7cfb-4d7b-a90d-6e4625719d74
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: af60935af0d183ab7ed6d1c10f84229b7ead3730
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607081"
---
# <a name="sql-server-2014-express-localdb"></a>SQL Server 2014 Express LocalDB
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` 是 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 以程式開發人員為目標的執行模式。 `LocalDB`安裝會複製啟動所需的最小檔案集合 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 。 `LocalDB`安裝之後，開發人員會使用特殊的連接字串來起始連接。 連接時，就會自動建立及啟動必要的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基礎結構，應用程式不需複雜或耗時的組態工作即可開始使用資料庫。 Developer Tools 為開發人員提供 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，讓他們撰寫和測試 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，而不需要管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的完整伺服器執行個體。 的實例 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] `LocalDB` 是使用公用程式來管理 `SqlLocalDB.exe` 。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB`應該用來取代 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 已被取代的使用者實例功能。  
  
## <a name="installing-localdb"></a>安裝 LocalDB  
 安裝的主要方法 `LocalDB` 是使用 SqlLocalDB.msi 程式。 `LocalDB`是安裝的任何 SKU 時的選項 [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] 。 在 `LocalDB` 安裝期間，于 [**特徵選取**] 頁面上選取 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 。 `LocalDB`每個主要版本只能有一個二進位檔案安裝 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 。 多個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 處理序可以啟動，而且全部都會使用相同的二進位檔案。 當做啟動的實例與 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] `LocalDB` 具有相同的限制[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]  
  
## <a name="description"></a>描述  
 `LocalDB`安裝程式會使用 SqlLocalDB.msi 程式，在電腦上安裝必要的檔案。 安裝之後， `LocalDB` 就是 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 可建立及開啟資料庫的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 資料庫的系統資料庫檔案儲存在使用者本機上通常處於隱藏狀態的 AppData 路徑。 例如 **C:\Users\\<使用者\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**。 使用者資料庫檔案儲存在使用者指定的位置，通常是在 **C:\Users\\<使用者\>\Documents\\** 資料夾中的某個位置。  
  
 如需 `LocalDB` 在應用程式中包含的詳細資訊，請參閱 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 檔[本機資料總覽](https://msdn.microsoft.com/library/ms233817\(VS.110\).aspx)、[逐步解說：建立 SQL Server LocalDB 資料庫](https://msdn.microsoft.com/library/ms233763\(VS.110\).aspx)和[逐步解說：連接至 SQL Server LocalDB 資料庫中的資料 (Windows Forms) ](https://msdn.microsoft.com/library/ms171890\(VS.110\).aspx)。  
  
 如需有關 API 的詳細資訊 `LocalDB` ，請參閱[SQL Server Express LOCALDB 實例 API 參考](https://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx)和[LocalDBStartInstance](https://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx)函式。  
  
 SqlLocalDb 公用程式可以建立的新實例 `LocalDB` 、啟動和停止的實例 `LocalDB` ，並包含可協助您管理的選項 `LocalDB` 。  如需 SqlLocalDb 公用程式的詳細資訊，請參閱 [SqlLocalDB 公用程式](../../tools/sqllocaldb-utility.md)。  
  
 的實例定序 `LocalDB` 設定為 SQL_Latin1_General_CP1_CI_AS，而且無法變更。 通常支援資料庫層級、資料行層級和運算式層級定序。 自主資料庫遵循 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)所定義的中繼資料和 tempdb 定序規則。  
  
### <a name="restrictions"></a>限制  
 `LocalDB`不可以是合併式複寫訂閱者。  
  
 `LocalDB`不支援 FILESTREAM。  
  
 `LocalDB`僅允許 Service Broker 的本機佇列。  
  
 `LocalDB`內建帳戶（例如 NT AUTHORITY\SYSTEM）所擁有的實例，可能因為 windows 檔案系統重新導向而有管理性問題。改為使用一般 windows 帳戶作為擁有者。  
  
### <a name="automatic-and-named-instances"></a>自動和具名執行個體  
 `LocalDB`支援兩種類型的實例：自動實例和已命名的實例。  
  
-   的自動實例 `LocalDB` 是公用的。 這些執行個體會自動為使用者建立及管理，並且可供任何應用程式使用。 在 `LocalDB` `LocalDB` 使用者電腦上安裝的每個版本都有一個自動實例。 自動實例可 `LocalDB` 提供無縫的實例管理。 無需建立執行個體，它就會運作。 這允許應用程式輕鬆安裝和移轉到另一部電腦。 如果目標電腦已安裝指定的 `LocalDB` 版本，該目標電腦可以使用此版本的 `LocalDB` 自動執行個體。 的自動實例 `LocalDB` 具有屬於保留命名空間之實例名稱的特殊模式。 這可避免與的已命名實例發生名稱衝突 `LocalDB` 。 自動執行個體的名稱是 **MSSQLLocalDB**。  
  
-   的命名實例 `LocalDB` 是私用的。 這些執行個體是由負責建立及管理該執行個體的單一應用程式所擁有。 具名執行個體與其他執行個體隔離，並透過減少與其他資料庫使用者的資源競爭來提高效能。 已命名的實例必須由使用者透過管理 API 明確建立， `LocalDB` 或在受控應用程式的 app.config 檔中以隱含的方式建立 (雖然受控應用程式也可以使用 API （如有) 需要）。 的每一個實例 `LocalDB` 都有相關聯的 `LocalDB` 版本，指向各自的一組 `LocalDB` 二進位檔。 的實例名稱 `LocalDB` 是 `sysname` 資料類型，最多可以有128個字元。  (這不同于的一般命名實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，這會將名稱限制為16個 ASCII 字元的一般 NetBIOS 名稱。 ) 實例的名稱 `LocalDB` 可以包含檔案名中任何合法的 Unicode 字元。  使用自動執行個體名稱的具名執行個體會成為自動執行個體。  
  
 電腦的不同使用者可有同名的執行個體。 每個執行個體都是以不同使用者身分執行的不同處理序。  
  
## <a name="shared-instances-of-localdb"></a>LocalDB 的共用執行個體  
 為了支援電腦的多個使用者需要連接到單一實例的案例 `LocalDB` ， `LocalDB` 支援實例共用。 執行個體擁有者可以選擇允許電腦上的其他使用者連接到他的執行個體。 可以共用的自動和已命名的實例 `LocalDB` 。 若要共用 `LocalDB` 執行個體，使用者必須為它選取共用名稱 (別名)。 因為電腦上的所有使用者都可以看到共用名稱，此共用名稱在電腦上必須是唯一的。 實例的共用名稱與的 `LocalDB` 命名實例具有相同的格式 `LocalDB` 。  
  
 只有電腦上的系統管理員可以建立的共用實例 `LocalDB` 。 的共用實例 `LocalDB` 可由系統管理員或共用實例的擁有者取消共用 `LocalDB` 。 若要共用和取消共用的實例 `LocalDB` ，請使用 `LocalDBShareInstance` API 的和 `LocalDBUnShareInstance` 方法 `LocalDB` ，或 SqlLocalDb 公用程式的共用和取消共用選項。  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>啟動 LocalDB 以及連接到 LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>連接到自動執行個體  
 最簡單的方法 `LocalDB` 是使用連接字串 **"Server = (localdb) \Mssqllocaldb; 整合式安全性 = true"**，連接到目前使用者所擁有的自動實例。 若要使用檔案名稱來連接到特定的資料庫，請使用類似於 **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"** 的連接字串進行連接。  
  
> [!NOTE]  
>  第一次在電腦上的使用者嘗試連接到時 `LocalDB` ，必須同時建立和啟動自動實例。 建立執行個體所需的額外時間可能會導致連接嘗試失敗並顯示逾時訊息。 發生這種情況時，請等候幾秒鐘，讓建立程序完成，然後再重新連接。  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>建立及連接到具名執行個體  
 除了自動實例之外， `LocalDB` 也支援已命名的實例。 使用 SqlLocalDB.exe 程式來建立、啟動和停止的已命名實例 `LocalDB` 。 如需 SqlLocalDB.exe 的詳細資訊，請參閱 [SqlLocalDB 公用程式](../../tools/sqllocaldb-utility.md)。  
  
```ms-dos  
REM Create an instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" create LocalDBApp1  
REM Start the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" start LocalDBApp1  
REM Gather information about the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" info LocalDBApp1  
```  
  
 以上最後一行傳回的資訊如下所示。  
  
|||  
|-|-|  
|名稱|"LocalDBApp1"|  
|版本|\<Current Version>|  
|共用名稱|""|  
|擁有者|"\<Your Windows User>"|  
|自動建立|否|  
|State|執行中|  
|上次啟動時間|\<Date and Time>|  
|執行個體管道名稱|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  如果您的應用程式在4.0.2 之前使用 .NET 版本，您必須直接連接到的具名管道 `LocalDB` 。 實例管道名稱值是實例正在接聽的具名管道 `LocalDB` 。 在 LOCALDB # 之後，實例管道名稱的部分將會在每次啟動實例時變更 `LocalDB` 。 若要使用連接到的實例 `LocalDB` [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，請在 [**連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ** ] 對話方塊的 [**伺服器名稱**] 方塊中，輸入實例管道名稱。 從您的自訂程式，您可以 `LocalDB` 使用類似于的連接字串，建立與實例的連接。`SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>連接到 LocalDB 的共用執行個體  
 若要連接到的共用實例 `LocalDB` ** \\ ** ，請在連接字串)  (點 + 反斜線），以參考保留給共用實例的命名空間。 例如，若要連接到名為的共用實例，請 `LocalDB` `AppData` 使用連接字串，例如， `(localdb)\.\AppData` 做為連接字串的一部分。 連接到 `LocalDB` 不在其擁有之共用實例的使用者，必須具有 Windows 驗證或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入。  
  
## <a name="troubleshooting"></a>疑難排解  
 如需疑難排解的相關資訊 `LocalDB` ，請參閱[疑難排解 SQL Server 2012 Express LocalDB](https://social.technet.microsoft.com/wiki/contents/articles/4609.aspx)。  
  
## <a name="permissions"></a>權限  
 的實例 [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` 是由使用者建立的實例，供其使用。 電腦上的任何使用者都可以使用的實例建立資料庫 `LocalDB` 、在其使用者設定檔下儲存檔案，並在其認證之下執行進程。 根據預設，對實例的存取權 `LocalDB` 僅限於其擁有者。 包含在中的資料受到資料庫檔案之 `LocalDB` 檔案系統存取的保護。 如果使用者資料庫檔案儲存在共用位置中，任何人都可以使用其擁有的實例，來開啟該位置的檔案系統存取權 `LocalDB` 。 如果資料庫檔案位於受保護的位置，例如使用者資料夾，則只有該使用者和擁有該資料夾存取權的任何系統管理員才可以開啟資料庫。 檔案 `LocalDB` 一次只能由一個實例開啟 `LocalDB` 。  
  
> [!NOTE]  
>  `LocalDB`一律在使用者安全性內容下執行;也就是， `LocalDB` 絕對不會使用本機系統管理員群組的認證來執行。 這表示實例所使用的所有資料庫檔案都 `LocalDB` 必須可使用擁有使用者的 Windows 帳戶來存取，而不需要考慮本機 Administrators 群組的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [SqlLocalDB 公用程式](../../tools/sqllocaldb-utility.md)  
  
  
