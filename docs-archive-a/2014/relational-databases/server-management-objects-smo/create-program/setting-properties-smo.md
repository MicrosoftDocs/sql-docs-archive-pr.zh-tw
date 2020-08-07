---
title: 設定屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SMO [SQL Server], properties
- SQL Server Management Objects, properties
- properties [SMO]
ms.assetid: 342569ba-d2f7-44d2-8f3f-ae9c701c7f0f
author: stevestein
ms.author: sstein
ms.openlocfilehash: de381f8e4e9dfe9f6590638742e988f866ccabdc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704009"
---
# <a name="setting-properties"></a>設定屬性
  屬性是儲存有關物件之描述性資訊的值。 例如，設定 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 選項會以 <xref:Microsoft.SqlServer.Management.Smo.Server.Configuration%2A> 物件的屬性來表示。 您可以使用屬性集合來直接或間接地存取屬性。 直接存取屬性會使用下列語法：  
  
 `objInstance.PropertyName`  
  
 您可以根據屬性是否具有讀/寫存取權或唯讀存取權來修改或擷取屬性值。 也必須先設定特定的屬性，才能建立物件。 如需詳細資訊，請參閱該特定物件的 SMO 參考。  
  
> [!NOTE]  
>  子物件的集合會顯示為物件的屬性。 例如，`Tables` 集合是 `Server` 物件的屬性。 如需詳細資訊，請參閱 [Using Collections](using-collections.md)。  
  
 物件的屬性是 Properties 集合的成員。 Properties 集合可用來反覆運算物件的每個屬性。  
  
 有時屬性會因為下列原因而無法使用：  
  
-   伺服器版本不支援該屬性，例如您在舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 上嘗試存取的屬性代表新增的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]功能。  
  
-   伺服器沒有提供該屬性的資料，例如您嘗試存取的屬性代表未安裝的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 元件。  
  
 您可以藉由捕捉 <xref:Microsoft.SqlServer.Management.Smo.UnknownPropertyException> 和 <xref:Microsoft.SqlServer.Management.Smo.PropertyCannotBeRetrievedException> SMO 例外狀況來處理這些情況。  
  
## <a name="setting-default-initialization-fields"></a>設定預設的初始化欄位  
 SMO 在擷取物件時會執行最佳化。 最佳化會藉由在下列狀況之間自動調整，而將載入的屬性數目最小化：  
  
1.  部分載入。 初次參考物件時，該物件會擁有最少的可用屬性 (例如「名稱」和「結構描述」)。  
  
2.  完整載入。 在參考任何屬性時，系統會初始化可快速載入的剩餘屬性並使這些屬性可供使用。  
  
3.  使用大量記憶體的屬性。 不可使用的剩餘屬性會使用許多記憶體，並具有 true 的 <xref:Microsoft.SqlServer.Management.Smo.Property.Expensive%2A> 屬性值 (例如，<xref:Microsoft.SqlServer.Management.Smo.Database.DataSpaceUsage%2A>)。 這些屬性只有在特別參考時才會載入。  
  
 如果您的應用程式真的會擷取額外的屬性，則除了以部分載入狀態提供的屬性外，該應用程式還會提交查詢以擷取這些額外的屬性，並擴充至完全載入的狀態。 這樣可能會造成用戶端和伺服器之間出現不必要的傳輸。 呼叫 <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A> 方法可以達到更高的最佳化。 <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A> 方法可用來指定在物件初始化時載入的屬性。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A> 方法會針對其餘的應用程式設定屬性載入行為，或等到應用程式重設為止。 您可以使用 <xref:Microsoft.SqlServer.Management.Smo.Server.GetDefaultInitFields%2A> 方法來儲存原始的行為，並依需求加以還原。  
  
## <a name="examples"></a>範例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="getting-and-setting-a-property-in-visual-basic"></a>在 Visual Basic 中取得和設定屬性  
 此程式碼範例示範如何取得 <xref:Microsoft.SqlServer.Management.Smo.Information.Edition%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.Information> 屬性，以及如何將 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.SqlExecutionModes%2A> 屬性的 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 屬性設定為 <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> 列舉型別的 `ExecuteSql` 成員。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBProperties1](SMO How to#SMO_VBProperties1)]  -->  
  
## <a name="getting-and-setting-a-property-in-visual-c"></a>在 Visual C# 中取得和設定屬性  
 此程式碼範例示範如何取得 <xref:Microsoft.SqlServer.Management.Smo.Information.Edition%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.Information> 屬性，以及如何將 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.SqlExecutionModes%2A> 屬性的 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 屬性設定為 <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> 列舉型別的 `ExecuteSql` 成員。  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Get a property.   
Console.WriteLine(srv.Information.Version);   
//Set a property.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql;   
}  
```  
  
## <a name="setting-various-properties-before-an-object-is-created-in-visual-basic"></a>在 Visual Basic 中建立物件之前先設定各種屬性  
 此程式碼範例示範如何直接設定 <xref:Microsoft.SqlServer.Management.Smo.Table.AnsiNullsStatus%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.Table> 屬性，以及如何在建立 <xref:Microsoft.SqlServer.Management.Smo.Table> 物件之前，先建立和加入資料行。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBProperties2](SMO How to#SMO_VBProperties2)]  -->  
  
## <a name="setting-various-properties-before-an-object-is-created-in-visual-c"></a>在 Visual C# 中建立物件之前先設定各種屬性  
 此程式碼範例示範如何直接設定 <xref:Microsoft.SqlServer.Management.Smo.Table.AnsiNullsStatus%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.Table> 屬性，以及如何在建立 <xref:Microsoft.SqlServer.Management.Smo.Table> 物件之前，先建立和加入資料行。  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Create a new table in the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
Table tb;   
//Specify the parent database, table schema, and the table name in the constructor.   
tb = new Table(db, "Test_Table", "HumanResources");   
//Add columns because the table requires columns before it can be created.   
Column c1;   
//Specify the parent table, the column name, and data type in the constructor.   
c1 = new Column(tb, "ID", DataType.Int);   
tb.Columns.Add(c1);   
c1.Nullable = false;   
c1.Identity = true;   
c1.IdentityIncrement = 1;   
c1.IdentitySeed = 0;   
Column c2;   
c2 = new Column(tb, "Name", DataType.NVarChar(100));   
c2.Nullable = false;   
tb.Columns.Add(c2);   
tb.AnsiNullsStatus = true;   
//Create the table on the instance of SQL Server.   
tb.Create();   
}  
```  
  
## <a name="iterating-through-all-properties-of-an-object-in-visual-basic"></a>在 Visual Basic 中反覆運算物件的所有屬性  
 此程式碼範例會反覆運算 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> 物件的 `Properties` 集合，並在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 輸出畫面上加以顯示。  
  
 在此範例中已將 <xref:Microsoft.SqlServer.Management.Smo.Property> 物件放入方括號中，因為它也是 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 關鍵字。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBProperties3](SMO How to#SMO_VBProperties3)]  -->  
  
## <a name="iterating-through-all-properties-of-an-object-in-visual-c"></a>在 Visual C# 中反覆運算物件的所有屬性  
 此程式碼範例會反覆運算 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> 物件的 `Properties` 集合，並在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 輸出畫面上加以顯示。  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Set properties on the uspGetEmployeedManagers stored procedure on the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
StoredProcedure sp;   
sp = db.StoredProcedures("uspGetEmployeeManagers");   
sp.AnsiNullsStatus = false;   
sp.QuotedIdentifierStatus = false;   
//Iterate through the properties of the stored procedure and display.   
  Property p;   
  foreach ( p in sp.Properties) {   
    Console.WriteLine(p.Name + p.Value);   
  }   
}  
```  
  
## <a name="setting-default-initialization-fields-in-visual-basic"></a>在 Visual Basic 中設定預設的初始化欄位  
 此程式碼範例示範如何將在 SMO 程式中初始化的物件屬性數目最小化。 您必須包含 `using System.Collections.Specialized`，即使用 <xref:System.Collections.Specialized.StringCollection> 物件的陳述式。  
  
 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 可用來將此最佳化與傳送至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的數字陳述式進行比較。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDefaultInitFields1](SMO How to#SMO_VBDefaultInitFields1)]  -->  
  
## <a name="setting-default-initialization-fields-in-visual-c"></a>在 Visual C# 中設定預設的初始化欄位  
 此程式碼範例示範如何將在 SMO 程式中初始化的物件屬性數目最小化。 您必須包含 `using System.Collections.Specialized`，即使用 <xref:System.Collections.Specialized.StringCollection> 物件的陳述式。  
  
 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 可用來將此最佳化與傳送至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的數字陳述式進行比較。  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Assign the Table object type to a System.Type object variable.   
Table tb;   
Type typ;   
tb = new Table();   
typ = tb.GetType;   
//Assign the current default initialization fields for the Table object type to a   
//StringCollection object variable.   
StringCollection sc;   
sc = srv.GetDefaultInitFields(typ);   
//Set the default initialization fields for the Table object type to the CreateDate property.   
srv.SetDefaultInitFields(typ, "CreateDate");   
//Retrieve the Schema, Name, and CreateDate properties for every table in AdventureWorks2012.   
   //Note that the improvement in performance can be viewed in SQL Server Profiler.   
foreach ( tb in db.Tables) {   
   Console.WriteLine(tb.Schema + "." + tb.Name + " " + tb.CreateDate);   
}   
//Set the default initialization fields for the Table object type back to the original settings.   
srv.SetDefaultInitFields(typ, sc);   
}  
```  
  
  
