---
title: 建立記憶體最佳化資料表和原生編譯的預存程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 48a9a0a3-930f-477b-bd0f-e82e77999ecc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7de45ced2f4f39fff54c5beff6228c6f8a5c0476
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594569"
---
# <a name="creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure"></a><span data-ttu-id="abed0-102">建立記憶體最佳化資料表和原生編譯的預存程序</span><span class="sxs-lookup"><span data-stu-id="abed0-102">Creating a Memory-Optimized Table and a Natively Compiled Stored Procedure</span></span>
  <span data-ttu-id="abed0-103">本主題包含介紹記憶體中 OLTP 語法的範例。</span><span class="sxs-lookup"><span data-stu-id="abed0-103">This topic contains a sample that introduces you to the syntax for In-Memory OLTP.</span></span>  
  
 <span data-ttu-id="abed0-104">此範例示範如何讓應用程式使用記憶體中的 OLTP。</span><span class="sxs-lookup"><span data-stu-id="abed0-104">The sample demonstrates enabling an application to use In-Memory OLTP.</span></span> <span data-ttu-id="abed0-105">其會為記憶體中的 OLTP 設定資料庫、建立記憶體最佳化資料表 (其中顯示 DURABILITY 選項)，然後建立原生編譯預存程序，以存取記憶體最佳化資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="abed0-105">It sets up the database for In-Memory OLTP, creates memory-optimized tables showing DURABILITY options, and then creates natively compiled stored procedures to access the data in the memory-optimized tables.</span></span> <span data-ttu-id="abed0-106">下列步驟將於下方的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 詳述：</span><span class="sxs-lookup"><span data-stu-id="abed0-106">The following steps are detailed in the [!INCLUDE[tsql](../../includes/tsql-md.md)] below:</span></span>  
  
-   <span data-ttu-id="abed0-107">建立記憶體最佳化資料檔案群組並將容器加入至檔案群組。</span><span class="sxs-lookup"><span data-stu-id="abed0-107">Create a memory-optimized data filegroup and add a container to the filegroup.</span></span>  
  
-   <span data-ttu-id="abed0-108">建立記憶體最佳化資料表及索引</span><span class="sxs-lookup"><span data-stu-id="abed0-108">Create memory-optimized tables and indexes.</span></span> <span data-ttu-id="abed0-109">如需詳細資訊，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="abed0-109">For more information, see [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql).</span></span>  
  
-   <span data-ttu-id="abed0-110">使用解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)]，將資料載入記憶體最佳化資料表，並於更新統計資料後再建立原生編譯預存程序。</span><span class="sxs-lookup"><span data-stu-id="abed0-110">Using interpreted [!INCLUDE[tsql](../../includes/tsql-md.md)], load data into the memory-optimized table and update statistics before creating natively compiled stored procedures.</span></span> <span data-ttu-id="abed0-111">如需詳細資訊，請參閱 [記憶體最佳化資料表的統計資料](memory-optimized-tables.md)。</span><span class="sxs-lookup"><span data-stu-id="abed0-111">For more information, see [Statistics for Memory-Optimized Tables](memory-optimized-tables.md).</span></span>  
  
-   <span data-ttu-id="abed0-112">建立原生編譯的預存程序來存取記憶體最佳化資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="abed0-112">Create natively compiled stored procedures to access data in memory-optimized tables.</span></span> <span data-ttu-id="abed0-113">如需詳細資訊，請參閱 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="abed0-113">For more information, see [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql).</span></span>  
  
-   <span data-ttu-id="abed0-114">視需要將現有資料表中的資料移轉至記憶體最佳化資料表。</span><span class="sxs-lookup"><span data-stu-id="abed0-114">As needed, migrate data from existing tables to memory-optimized tables.</span></span>  
  
 <span data-ttu-id="abed0-115">如需如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 建立記憶體最佳化資料表的資訊，請參閱 [SQL Server Management Studio 對記憶體內部 OLTP 的支援](sql-server-management-studio-support-for-in-memory-oltp.md)。</span><span class="sxs-lookup"><span data-stu-id="abed0-115">For information on how to use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] to create memory-optimized tables, see [SQL Server Management Studio Support for In-Memory OLTP](sql-server-management-studio-support-for-in-memory-oltp.md).</span></span>  
  
 <span data-ttu-id="abed0-116">下列程式碼範例需要名為 c:\Data 的目錄。</span><span class="sxs-lookup"><span data-stu-id="abed0-116">The following code sample requires a directory called c:\Data.</span></span>  
  
```sql  
-- create a database with a memory-optimized filegroup and a container.  
CREATE DATABASE imoltp   
GO  
  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA   
ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod   
ALTER DATABASE imoltp SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON  
GO  
  
USE imoltp  
GO  
  
-- create a durable (data will be persisted) memory-optimized table  
-- two of the columns are indexed  
CREATE TABLE dbo.ShoppingCart (   
  ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,  
  UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),   
  CreatedDate DATETIME2 NOT NULL,   
  TotalPrice MONEY  
  ) WITH (MEMORY_OPTIMIZED=ON)   
GO  
  
 -- create a non-durable table. Data will not be persisted, data loss if the server turns off unexpectedly  
CREATE TABLE dbo.UserSession (   
  SessionId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=400000),   
  UserId int NOT NULL,   
  CreatedDate DATETIME2 NOT NULL,  
  ShoppingCartId INT,  
  INDEX ix_UserId NONCLUSTERED HASH (UserId) WITH (BUCKET_COUNT=400000)   
  ) WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_ONLY)   
GO  
  
-- insert data into the tables  
INSERT dbo.UserSession (UserId, CreatedDate, ShoppingCartId) VALUES (342, SYSDATETIME(), 4)   
INSERT dbo.UserSession (UserId, CreatedDate, ShoppingCartId) VALUES (65, SYSDATETIME(), NULL)   
INSERT dbo.UserSession (UserId, CreatedDate, ShoppingCartId) VALUES (8798, SYSDATETIME(), 1)   
INSERT dbo.UserSession (UserId, CreatedDate, ShoppingCartId) VALUES (80, SYSDATETIME(), NULL)   
INSERT dbo.UserSession (UserId, CreatedDate, ShoppingCartId) VALUES (4321, SYSDATETIME(), NULL)   
INSERT dbo.UserSession (UserId, CreatedDate, ShoppingCartId) VALUES (8578, SYSDATETIME(), NULL)   
  
INSERT dbo.ShoppingCart VALUES (UserId, CreatedDate, TotalPrice) (8798, SYSDATETIME(), NULL)   
INSERT dbo.ShoppingCart VALUES (UserId, CreatedDate, TotalPrice) (23, SYSDATETIME(), 45.4)   
INSERT dbo.ShoppingCart VALUES (UserId, CreatedDate, TotalPrice) (80, SYSDATETIME(), NULL)   
INSERT dbo.ShoppingCart VALUES (UserId, CreatedDate, TotalPrice) (342, SYSDATETIME(), 65.4)   
GO  
  
-- verify table contents   
SELECT * FROM dbo.UserSession   
SELECT * FROM dbo.ShoppingCart   
GO  
  
--  update statistics on memory-optimized tables   
UPDATE STATISTICS dbo.UserSession WITH FULLSCAN, NORECOMPUTE   
UPDATE STATISTICS dbo.ShoppingCart WITH FULLSCAN, NORECOMPUTE   
GO  
  
-- in an explicit transaction, assign a cart to a session and update the total price.   
-- SELECT/UPDATE/DELETE statements in explicit transactions   
BEGIN TRAN   
  UPDATE dbo.UserSession SET ShoppingCartId=3 WHERE SessionId=4   
  UPDATE dbo.ShoppingCart SET TotalPrice=65.84 WHERE ShoppingCartId=3   
COMMIT   
GO   
  
 -- verify table contents   
SELECT *   
FROM dbo.UserSession u   
   JOIN dbo.ShoppingCart s on u.ShoppingCartId=s.ShoppingCartId   
WHERE u.SessionId=4   
GO  
  
-- natively compiled stored procedure for assigning a shopping cart to a session   
CREATE PROCEDURE dbo.usp_AssignCart @SessionId int   
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER   
AS   
BEGIN ATOMIC   
 WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  
  DECLARE @UserId INT,  
          @ShoppingCartId INT  
  
  SELECT @UserId=UserId, @ShoppingCartId=ShoppingCartId   
  FROM dbo.UserSession WHERE SessionId=@SessionId  
  
  IF @UserId IS NULL   
  THROW 51000, N'The session or shopping cart does not exist.', 1  
  
  UPDATE dbo.UserSession SET ShoppingCartId=@ShoppingCartId WHERE SessionId=@SessionId   
END   
GO  
  
EXEC usp_AssignCart 1   
GO  
  
-- natively compiled stored procedure for inserting a large number of rows   
-- this demonstrates the performance of native procs   
CREATE PROCEDURE dbo.usp_InsertSampleCarts @InsertCount int   
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER   
AS   
BEGIN ATOMIC   
WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  
DECLARE @i int = 0  
  
WHILE @i < @InsertCount   
  BEGIN   
    INSERT INTO dbo.ShoppingCart (UserId, CreatedDate, TotalPrice) VALUES (1, SYSDATETIME() , NULL)   
    SET @i += 1   
  END  
  
END   
GO  
  
-- insert 1,000,000 rows   
EXEC usp_InsertSampleCarts 1000000   
GO  
  
---- verify the rows have been inserted   
SELECT COUNT(*) FROM dbo.ShoppingCart   
GO  
  
-- sample memory-optimized tables for sales orders and sales order details  
CREATE TABLE dbo.SalesOrders   
(  
   so_id INT NOT NULL PRIMARY KEY NONCLUSTERED,  
   cust_id INT NOT NULL,  
   so_date DATE NOT NULL INDEX ix_date NONCLUSTERED,  
   so_total MONEY NOT NULL,  
   INDEX ix_date_total NONCLUSTERED (so_date DESC, so_total DESC)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
CREATE TABLE dbo.SalesOrderDetails  
(  
   so_id INT NOT NULL,  
   lineitem_id INT NOT NULL,  
   product_id INT NOT NULL,  
   unitprice MONEY NOT NULL,  
  
   CONSTRAINT PK_SOD PRIMARY KEY NONCLUSTERED (so_id,lineitem_id)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- memory-optimized table type for collecting sales order details  
CREATE TYPE dbo.SalesOrderDetailsType AS TABLE  
(  
   so_id INT NOT NULL,  
   lineitem_id INT NOT NULL,  
   product_id INT NOT NULL,  
   unitprice MONEY NOT NULL,  
  
   PRIMARY KEY NONCLUSTERED (so_id,lineitem_id)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- stored procedure that inserts a sales order, along with its details  
CREATE PROCEDURE dbo.InsertSalesOrder @so_id INT, @cust_id INT, @items dbo.SalesOrderDetailsType READONLY  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  
   TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
   LANGUAGE = N'us_english'  
)  
   DECLARE @total MONEY  
   SELECT @total = SUM(unitprice) FROM @items  
   INSERT dbo.SalesOrders VALUES (so_id, cust_id, so_date, so_total) (@so_id, @cust_id, getdate(), @total)  
   INSERT dbo.SalesOrderDetails SELECT so_id, lineitem_id, product_id, unitprice FROM @items  
END  
GO  
  
-- insert a sample sales order  
DECLARE @so_id INT = 18,  
       @cust_id INT = 8,  
       @items dbo.SalesOrderDetailsType  
INSERT @items  VALUES   
       (@so_id, 1, 4, 43),   
       (@so_id, 2, 3, 3),   
       (@so_id, 3, 8, 453),   
       (@so_id, 4, 5, 76),   
       (@so_id, 5, 4, 43)  
EXEC dbo.InsertSalesOrder @so_id, @cust_id, @items  
GO  
  
-- verify the content of the tables  
SELECT   
       so.so_id,  
       so.so_date,  
       sod.lineitem_id,  
       sod.product_id,  
       sod.unitprice  
FROM dbo.SalesOrders so JOIN dbo.SalesOrderDetails sod on so.so_id=sod.so_id  
ORDER BY so.so_id, sod.lineitem_id  
  
```  
  
## <a name="see-also"></a><span data-ttu-id="abed0-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="abed0-117">See Also</span></span>  
 <span data-ttu-id="abed0-118">[記憶體內部 OLTP 程式碼範例](in-memory-oltp-code-samples.md) </span><span class="sxs-lookup"><span data-stu-id="abed0-118">[In-Memory OLTP Code Samples](in-memory-oltp-code-samples.md) </span></span>  
 <span data-ttu-id="abed0-119">[遷移計算資料行](migrating-computed-columns.md) </span><span class="sxs-lookup"><span data-stu-id="abed0-119">[Migrating Computed Columns](migrating-computed-columns.md) </span></span>  
 [<span data-ttu-id="abed0-120">在記憶體最佳化資料表中實作 IDENTITY</span><span class="sxs-lookup"><span data-stu-id="abed0-120">Implementing IDENTITY in a Memory-Optimized Table</span></span>](implementing-identity-in-a-memory-optimized-table.md)  
  
  
