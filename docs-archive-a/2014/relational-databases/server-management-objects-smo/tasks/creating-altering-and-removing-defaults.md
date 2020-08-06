---
title: 建立、改變和移除預設值 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- defaults [SMO]
ms.assetid: c30ac3b9-8150-4264-ba4c-c549f44261ab
author: stevestein
ms.author: sstein
ms.openlocfilehash: 747f7ff60122c5265cd68060063946a3e22d0301
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707338"
---
# <a name="creating-altering-and-removing-defaults"></a>建立、改變和移除預設值
  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理物件 (SMO) 中，預設的條件約束是由 <xref:Microsoft.SqlServer.Management.Smo.Default> 物件表示。  
  
 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.Default> 屬性可用於設定要插入的值。 這可以是常數，或傳回常數值的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式，例如 GETDATE()。 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 屬性無法藉由 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法進行修改， 反而必須將 <xref:Microsoft.SqlServer.Management.Smo.Default> 物件卸除，然後重新建立。  
  
## <a name="example"></a>範例  
 如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱[在 Visual Studio .net 中建立 VISUAL BASIC SMO 專案](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)或[在 Visual Studio .Net 中建立 VISUAL C&#35; SMO 專案](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-altering-and-removing-a-default-in-visual-basic"></a>在 Visual Basic 中建立、改變和移除預設值  
 此程式碼範例示範如何建立一個純文字的預設值，以及另一個 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式的預設值。 預設值必須使用 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> 方法附加到資料行，並使用 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A> 方法卸離。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDefaults1](SMO How to#SMO_VBDefaults1)]  -->  
  
## <a name="creating-altering-and-removing-a-default-in-visual-c"></a>在 Visual C# 中建立、改變和移除預設值  
 此程式碼範例示範如何建立一個純文字的預設值，以及另一個 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式的預設值。 預設值必須使用 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> 方法附加到資料行，並使用 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A> 方法卸離。  
  
```csharp
{
          Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database  db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Default object variable by supplying the parent database and the default name   
            //in the constructor.   
            Default def = new Default(db, "Test_Default2");  
  
            //Set the TextHeader and TextBody properties that define the default.   
            def.TextHeader = "CREATE DEFAULT [Test_Default2] AS";  
            def.TextBody = "GetDate()";  
  
            //Create the default on the instance of SQL Server.   
            def.Create();  
  
            //Bind the default to a column in a table in AdventureWorks2012  
            def.BindToColumn("SpecialOffer", "StartDate", "Sales");  
  
            //Unbind the default from the column and remove it from the database.   
            def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales");  
            def.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-default-in-powershell"></a>在 PowerShell 中建立、改變和移除預設值  
 此程式碼範例示範如何建立一個純文字的預設值，以及另一個 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式的預設值。 預設值必須使用 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> 方法附加到資料行，並使用 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A> 方法卸離。  
  
```powershell
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = Get-Item Adventureworks2012  
  
#Define a Default object variable by supplying the parent database and the default name in the constructor.  
$def = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Default `  
-argumentlist $db, "Test_Default2"  
  
#Set the TextHeader and TextBody properties that define the default.   
$def.TextHeader = "CREATE DEFAULT [Test_Default2] AS"  
$def.TextBody = "GetDate()"  
  
#Create the default on the instance of SQL Server.   
$def.Create()  
  
#Bind the default to the column.   
$def.BindToColumn("SpecialOffer", "StartDate", "Sales")  
  
#Unbind the default from the column and remove it from the database.   
$def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales")  
$def.Drop()  
```  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.SqlServer.Management.Smo.Default>  
