---
title: 使用同義字 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- synonyms [SMO]
ms.assetid: db0a9022-9549-43e5-b6b3-deb236f05fb8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5e8416dc3daea3b173fae92e5454a8a65c399e53
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606712"
---
# <a name="using-synonyms"></a>使用同義字
  同義字是結構描述範圍物件的替代名稱。 在 SMO 中，同義字是由 <xref:Microsoft.SqlServer.Management.Smo.Synonym> 物件表示。 <xref:Microsoft.SqlServer.Management.Smo.Synonym> 物件是 <xref:Microsoft.SqlServer.Management.Smo.Database> 物件的子系。 這表示同義字只有在其定義所在的資料庫範圍內才有效。 不過，同義字可以參考另一個資料庫或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]遠端執行個體上的物件。  
  
 已具有給定替代名稱的物件也稱為基底物件。 <xref:Microsoft.SqlServer.Management.Smo.Synonym> 物件的名稱屬性是為基底物件所提供的替代名稱。  
  
## <a name="example"></a>範例  
 在下列的程式碼範例中，您必須選取用於建立應用程式的程式設計環境、程式設計範本和程式設計語言。 如需詳細資訊，請參閱[在 Visual Studio .net 中建立 VISUAL BASIC SMO 專案](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)和[在 Visual Studio .Net 中建立 VISUAL C&#35; SMO 專案](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-a-synonym-in-visual-basic"></a>在 Visual Basic 中建立同義字  
 此程式碼範例示範如何為結構描述範圍物件建立同義字或替代名稱。 用戶端應用程式可以透過同義字使用單一參考來參考基底物件，而不是使用多重部分名稱來參考基底物件。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBSynonyms1](SMO How to#SMO_VBSynonyms1)]  -->  
  
## <a name="creating-a-synonym-in-visual-c"></a>在 Visual C# 中建立同義字  
 此程式碼範例示範如何為結構描述範圍物件建立同義字或替代名稱。 用戶端應用程式可以透過同義字使用單一參考來參考基底物件，而不是使用多重部分名稱來參考基底物件。  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Synonym object variable by supplying the   
            //parent database, name, and schema arguments in the constructor.   
            //The name is also a synonym of the name of the base object.   
            Synonym syn = new Synonym(db, "Shop", "Sales");  
  
            //Specify the base object, which is the object on which   
            //the synonym is based.   
            syn.BaseDatabase = "AdventureWorks2012";  
            syn.BaseSchema = "Sales";  
            syn.BaseObject = "Store";  
            syn.BaseServer = srv.Name;  
  
            //Create the synonym on the instance of SQL Server.   
            syn.Create();  
        }  
```  
  
## <a name="creating-a-synonym-in-powershell"></a>在 PowerShell 中建立同義字  
 此程式碼範例示範如何為結構描述範圍物件建立同義字或替代名稱。 用戶端應用程式可以透過同義字使用單一參考來參考基底物件，而不是使用多重部分名稱來參考基底物件。  
  
```powershell
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#And the database object corresponding to Adventureworks  
$db = $srv.Databases["AdventureWorks2012"]  
  
$syn = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Synonym -ArgumentList $db, "Shop", "Sales"  
  
#Specify the base object, which is the object on which the synonym is based.  
$syn.BaseDatabase = "AdventureWorks2012"  
$syn.BaseSchema = "Sales"  
$syn.BaseObject = "Store"  
$syn.BaseServer = $srv.Name  
  
#Create the synonym on the instance of SQL Server.  
$syn.Create()  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-synonym-transact-sql)  
