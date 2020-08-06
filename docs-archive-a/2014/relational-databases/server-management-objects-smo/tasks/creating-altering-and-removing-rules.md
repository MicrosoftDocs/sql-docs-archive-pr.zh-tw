---
title: 建立、改變和移除規則 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- rules [SMO]
ms.assetid: 16981459-524e-4b39-a899-4370eaf763cc
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7742a9cb718bdde4f268d5226c45eba475f44ddd
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598258"
---
# <a name="creating-altering-and-removing-rules"></a>建立、改變和移除規則
  在 SMO 中，規則會以 <xref:Microsoft.SqlServer.Management.Smo.Rule> 物件表示， 並由 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 屬性定義，該屬性是文字字串，包含使用運算子或述詞 (例如 IN、LIKE 或 BETWEEN) 的條件運算式。 規則不能參考資料行或其他資料庫物件。 未參考資料庫物件的內建函數可以包括在內。  
  
 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 屬性中的定義必須包含參考所輸入之資料值的變數。 建立規則時，可以使用任何名稱或符號來代表值，但第一個字元必須是 \@ 符號。  
  
## <a name="example"></a>範例  
 如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱[在 Visual Studio .net 中建立 VISUAL BASIC SMO 專案](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)或[在 Visual Studio .Net 中建立 VISUAL C&#35; SMO 專案](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-basic"></a>在 Visual Basic 中建立、改變和移除規則  
 此程式碼範例示範如何建立規則、將規則附加至資料行、修改 <xref:Microsoft.SqlServer.Management.Smo.Rule> 物件的屬性、將規則從資料行卸離，然後再加以卸除。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Rule> 物件的 `Dim` 陳述式會以完整的組件路徑指定，以避免與 System.Data 組件中的 <xref:Microsoft.SqlServer.Management.Smo.Rule> 物件混淆。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBRules1](SMO How to#SMO_VBRules1)]  -->  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-c"></a>在 Visual C# 中建立、改變和移除規則  
 此程式碼範例示範如何建立規則、將規則附加至資料行、修改 <xref:Microsoft.SqlServer.Management.Smo.Rule> 物件的屬性、將規則從資料行卸離，然後再加以卸除。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Rule> 物件的 `Dim` 陳述式會以完整的組件路徑指定，以避免與 System.Data 組件中的 <xref:Microsoft.SqlServer.Management.Smo.Rule> 物件混淆。  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
            //Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.   
            Microsoft.SqlServer.Management.Smo.Rule ru;  
            ru = new Rule(db, "TestRule", "Production");  
            //Set the TextHeader and TextBody properties to define the rule.   
            ru.TextHeader = "CREATE RULE [Production].[TestRule] AS";  
            ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())";  
            //Create the rule on the instance of SQL Server.   
            ru.Create();  
            //Bind the rule to a column in the Product table by supplying the table, schema, and   
            //column as arguments in the BindToColumn method.   
            ru.BindToColumn("Product", "SellEndDate", "Production");  
            //Unbind from the column before removing the rule from the database.   
            ru.UnbindFromColumn("Product", "SellEndDate", "Production");  
            ru.Drop();  
  
        }  
```  
  
## <a name="creating-altering-and-removing-a-rule-in-powershell"></a>在 PowerShell 中建立、改變和移除規則  
 此程式碼範例示範如何建立規則、將規則附加至資料行、修改 <xref:Microsoft.SqlServer.Management.Smo.Rule> 物件的屬性、將規則從資料行卸離，然後再加以卸除。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Rule> 物件的 `Dim` 陳述式會以完整的組件路徑指定，以避免與 System.Data 組件中的 <xref:Microsoft.SqlServer.Management.Smo.Rule> 物件混淆。  
  
```powershell
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = Get-Item Adventureworks2012  
  
# Define a Rule object variable by supplying the parent database, name and schema in the constructor.
$ru = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Rule -argumentlist $db, "TestRule", "Production"  
  
#Set the TextHeader and TextBody properties to define the rule.
$ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"  
$ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"  
  
#Create the rule on the instance of SQL Server.
$ru.Create()  
  
# Bind the rule to a column in the Product table by supplying the table, schema, and column as arguments in the BindToColumn method.
$ru.BindToColumn("Product", "SellEndDate", "Production")  
  
#Unbind from the column before removing the rule from the database.
$ru.UnbindFromColumn("Product", "SellEndDate", "Production")  
$ru.Drop()  
```  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.SqlServer.Management.Smo.Rule>  
