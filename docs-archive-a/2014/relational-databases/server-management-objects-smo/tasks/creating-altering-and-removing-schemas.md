---
title: 建立、改變和移除架構 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- schemas [SMO]
ms.assetid: 3e3619de-c6a2-4280-b2be-4ec9924608fb
author: stevestein
ms.author: sstein
ms.openlocfilehash: 390a70c48d442b52a6aa29185880de67467c0cdd
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598259"
---
# <a name="creating-altering-and-removing-schemas"></a>建立、改變和移除結構描述
  <xref:Microsoft.SqlServer.Management.Smo.Schema> 物件表示資料庫物件的擁有權內容。 <xref:Microsoft.SqlServer.Management.Smo.Database.Schemas%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.Database> 屬性表示 <xref:Microsoft.SqlServer.Management.Smo.Schema> 物件的集合。  
  
## <a name="example"></a>範例  
 如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱[在 Visual Studio .net 中建立 VISUAL BASIC SMO 專案](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)或[在 Visual Studio .Net 中建立 VISUAL C&#35; SMO 專案](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-altering-and-removing-a-schema-in-visual-basic"></a>在 Visual Basic 中建立、改變和移除結構描述  
 此程式碼範例示範如何建立結構描述，並將其指派給資料庫物件。 程式接著會授與權限給使用者，然後再於結構描述中建立新的資料表。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBSchemas1](SMO How to#SMO_VBSchemas1)]  -->  
  
## <a name="creating-altering-and-removing-a-schema-in-visual-c"></a>在 Visual C# 中建立、改變和移除結構描述  
 此程式碼範例示範如何建立結構描述，並將其指派給資料庫物件。 程式接著會授與權限給使用者，然後再於結構描述中建立新的資料表。  
  
```csharp
{  
         //Connect to the local, default instance of SQL Server.   
         Server srv = new Server();   
        //Reference the AdventureWorks2012 database.   
        Database db = srv.Databases["AdventureWorks2012"];   
        //Define a Schema object variable by supplying the parent database and name arguments in the constructor.   
        Schema sch = new Schema(db, "MySchema1");   
        sch.Owner = "dbo";   
  
        //Create the schema on the instance of SQL Server.   
        sch.Create();   
  
        //Define an ObjectPermissionSet that contains the Update and Select object permissions.   
        ObjectPermissionSet obperset = new ObjectPermissionSet();   
        obperset.Add(ObjectPermission.Select);   
        obperset.Add(ObjectPermission.Update);   
  
        //Grant the set of permissions on the schema to the guest account.   
        sch.Grant(obperset, "guest");   
  
        //Define a Table object variable by supplying the parent database, name and schema arguments in the constructor.   
        Table tb = new Table(db, "MyTable", "MySchema1");   
       Column mycol = new Column(tb, "Date", DataType.DateTime);   
        tb.Columns.Add(mycol);   
        tb.Create();   
  
        //Modify the owner of the schema and run the Alter method to make the change on the instance of SQL Server.   
        sch.Owner = "guest";   
        sch.Alter();   
  
        //Run the Drop method for the table and the schema to remove them.   
        tb.Drop();   
        sch.Drop();   
}  
```  
  
## <a name="creating-altering-and-removing-a-schema-in-powershell"></a>在 PowerShell 中建立、改變和移除結構描述  
 此程式碼範例示範如何建立結構描述，並將其指派給資料庫物件。 程式接著會授與權限給使用者，然後再於結構描述中建立新的資料表。  
  
```powershell
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = Get-Item Adventureworks2012  
  
# Define a schema object variable by supplying the parent database and name arguments in the constructor.
$sch  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Schema -argumentlist $db, "MySchema1"  
  
# Set schema owner  
$sch.Owner = "dbo"
  
# Create the schema on the instance of SQL Server.
$sch.Create()  
  
# Define an ObjectPermissionSet that contains the Update and Select object permissions.
$obperset  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.ObjectPermissionSet  
$obperset.Add([Microsoft.SqlServer.Management.SMO.ObjectPermission]::Select)  
$obperset.Add([Microsoft.SqlServer.Management.SMO.ObjectPermission]::Update)  
  
# Grant the set of permissions on the schema to the guest account.
$sch.Grant($obperset, "guest")  
  
#Create a SMO Table with one column and add it to the database  
$tb = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Table -argumentlist $db, "MyTable", "MySchema1"  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$mycol =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Date", $Type  
$tb.Columns.Add($mycol)  
$tb.Create()
  
# Modify the owner of the schema and run the Alter method to make the change on the instance of SQL Server.
$sch.Owner = "guest"  
$sch.Alter()  
  
# Run the Drop method for the table and the schema to remove them.
$tb.Drop()  
$sch.Drop()  
```
