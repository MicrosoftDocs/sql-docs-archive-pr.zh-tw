---
title: 資料表和預存程序的原生編譯 | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5880fbd9-a23e-464a-8b44-09750eeb2dad
author: rothja
ms.author: jroth
ms.openlocfilehash: 32c5b04610d894e06278fbeecdaf3bbebe850d60
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597121"
---
# <a name="native-compilation-of-tables-and-stored-procedures"></a>資料表和預存程序的原生編譯
  記憶體中 OLTP 導入了原生編譯的概念。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可原生編譯用來存取記憶體最佳化資料表的預存程序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也可以透過原生方式編譯記憶體最佳化資料表。 與解譯的 (傳統) [!INCLUDE[tsql](../../includes/tsql-md.md)]相較之下，原生編譯可提供更快速的資料存取並且更有效率地執行查詢。 資料表和預存程序的原生編譯會產生 DLL。  
  
 另外也支援記憶體最佳化資料表類型的原生編譯。 如需詳細資訊，請參閱 [Memory-Optimized Table Variables](../../database-engine/memory-optimized-table-variables.md)。  
  
 原生編譯是指將程式設計結構轉換成原生程式碼的程序，包含處理器指令，而不需再進一步編譯或解譯。  
  
 記憶體內 OLTP 會在建立記憶體最佳化資料表時，以及原生編譯預存程序載入原生 DLL 時，對兩者編譯記憶體最佳化資料表。 此外，DLL 會在資料庫或伺服器重新啟動之後重新編譯。 重新建立 DLL 所需的資訊儲存在資料庫中繼資料內。 DLL 不是資料庫的一部分，不過它們與資料庫相關聯。 例如，DLL 不包含在資料庫備份中。  
  
> [!NOTE]  
>  記憶體最佳化資料表會在重新啟動伺服器期間重新編譯。 為了加速資料庫的復原，不會在啟動伺服器期間重新編譯原生編譯預存程序，而是會在第一次執行時進行編譯。 因為此延遲編譯，原生編譯預存程序只會在第一次執行後，呼叫 [sys.dm_os_loaded_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-loaded-modules-transact-sql) 時出現。  
  
## <a name="maintenance-of-in-memory-oltp-dlls"></a>維護記憶體中 OLTP DLL  
 下列查詢顯示目前載入伺服器記憶體中的所有資料表和預存程序 DLL：  
  
```sql  
SELECT name, description FROM sys.dm_os_loaded_modules  
where description = 'XTP Native DLL'  
```  
  
 資料庫管理員不需要維護原生編譯所產生的檔案。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在不再需要時自動移除產生的檔案。 例如，產生的檔案會在資料表和預存程序已刪除，或資料庫卸載時移除。  
  
> [!NOTE]  
>  編譯失敗或中斷時，某些產生的檔案並不會刪除。 刻意留下這些檔案是為了提供支援，而這些檔案會在資料庫卸除時移除。  
  
> [!NOTE]  
>  資料庫在啟動期間，SQL Server 會為資料庫復原所需的所有資料表編譯 Dll。 如果資料表在資料庫重新啟動之前已卸除，則檢查點檔案或交易記錄檔中可能仍有剩餘的資料表，讓資料表 DLL 可能會在資料庫啟動期間重新編譯。 重新啟動之後 DLL 將會被卸載，一般的清理程序就會移除檔案。  
  
## <a name="native-compilation-of-tables"></a>資料表的原生編譯  
 使用 `CREATE TABLE` 陳述式建立記憶體最佳化資料表會導致將資料表資訊寫入資料庫中繼資料，並且在記憶體中建立資料表和索引結構。 資料表也會編譯為 DLL。  
  
 請考慮下列範例指令碼，該指令碼會建立資料庫和記憶體最佳化資料表：  
  
```sql  
use master  
go  
create database db1  
go  
alter database db1 add filegroup db1_mod contains memory_optimized_data  
go  
-- adapt filename as needed  
alter database db1 add file (name='db1_mod', filename='c:\data\db1_mod') to filegroup db1_mod  
go  
use db1  
go  
create table dbo.t1  
   (c1 int not null primary key nonclustered,  
    c2 INT)  
with (memory_optimized=on)  
go  
-- retrieve the path of the DLL for table t1  
select name, description FROM sys.dm_os_loaded_modules  
where name like '%xtp_t_' + cast(db_id() as varchar(10)) + '_' + cast(object_id('dbo.t1') as varchar(10)) + '.dll'  
go  
```  
  
 建立資料表也會建立資料表 DLL 並將 DLL 載入記憶體中。 CREATE TABLE 陳述式後面緊接著的 DMV 查詢會擷取資料表 DLL 的路徑。  
  
 資料表 DLL 可理解資料表的索引結構和資料列格式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 DLL 周遊索引、擷取資料列，以及儲存資料列內容。  
  
## <a name="native-compilation-of-stored-procedures"></a>預存程序的原生編譯  
 標示為 NATIVE_COMPILATION 的預存程序為原生編譯。 這表示，程序中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式全都編譯為原生程式碼，能夠有效率地執行效能具有決定性的商務邏輯。  
  
 如需原生編譯的預存程序的詳細資訊，請參閱 [原生編譯的預存程序](natively-compiled-stored-procedures.md)。  
  
 請考慮下列範例預存程序，它會在上一個範例的資料表 t1 中插入資料列：  
  
```sql  
create procedure dbo.native_sp  
with native_compilation, schemabinding, execute as owner  
as  
begin atomic  
with (transaction isolation level=snapshot, language=N'us_english')  
  
  declare @i int = 1000000  
  while @i > 0  
  begin  
    insert dbo.t1 values (@i, @i+1)  
    set @i -= 1  
  end  
  
end  
go  
exec dbo.native_sp  
go  
-- reset  
delete from dbo.t1  
go  
```  
  
 native_sp 的 DLL 可直接與 t1 的 DLL 以及記憶體中 OLTP 儲存引擎互動，以盡快將資料列插入。  
  
 記憶體中 OLTP 編譯器會利用查詢最佳化工具，為預存程序中的每個查詢建立有效率的執行計畫。 請注意，原生編譯的預存程序不會在資料表中的資料變更時自動重新編譯。 如需維護記憶體內部 OLTP 中的統計資料和預存程序的詳細資訊，請參閱 [記憶體最佳化資料表的統計資料](memory-optimized-tables.md)。  
  
## <a name="security-considerations-for-native-compilation"></a>原生編譯的安全性考量  
 資料表和預存程序的原生編譯使用記憶體中 OLTP 編譯器。 此編譯器會產生寫入磁碟並載入記憶體中的檔案。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用下列機制限制這些檔案的存取權。  
  
### <a name="native-compiler"></a>原生編譯器  
 原生編譯所需的編譯器可執行檔以及二進位和標頭檔案已在 MSSQL\Binn\Xtp 資料夾之下，安裝為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的一部分。 因此，如果預設實例安裝在 C:\Program files 底下，編譯器檔案就會安裝在 C:\Program Files \\ [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12。MSSQLSERVER\MSSQL\Binn\Xtp.  
  
 若要限制編譯器的存取權， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用存取控制清單 (ACL) 限制二進位檔案的存取。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 二進位皆受到保護，以防止其遭到修改或透過 ACL 竄改。 原生編譯器的 ACL 也限制編譯器的使用權，僅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶和系統管理員擁有原生編譯器檔案的讀取和執行權限。  
  
### <a name="files-generated-by-a-native-compilation"></a>原生編譯產生的檔案  
 當資料表或預存程序進行編譯時，所產生的檔案會包含 DLL 以及中繼檔案，而中繼檔案含有下列附檔名：.c、.obj、.xml 和 .pdb。 產生的檔案會儲存在預設資料夾的子資料夾中。 這個子資料夾名為 Xtp。 使用預設資料夾安裝預設實例時，產生的檔案會放在 C:\Program files \\ [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12。MSSQLSERVER\MSSQL\DATA\Xtp.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用三種方式防止產生的 DLL 遭竄改：  
  
-   當資料表或預存程序編譯為 DLL 時，此 DLL 會立即載入記憶體並連結到 sqlserver.exe 處理序。 DLL 連結到處理序時無法修改。  
  
-   當資料庫重新啟動時，所有資料表和預存程序將會依據資料庫中繼資料重新編譯 (移除並重新建立)。 這將會移除惡意代理程式對產生之檔案所做的任何變更。  
  
-   產生的資料會視為使用者資料的一部分，並和資料庫檔案擁有相同的安全性限制 (透過 ACL)：僅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶和系統管理員能夠存取這些檔案。  
  
 管理這些檔案不需要使用者互動。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在必要時建立和移除檔案。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體優化資料表](memory-optimized-tables.md)   
 [原生編譯的預存程序](natively-compiled-stored-procedures.md)  
  
  
