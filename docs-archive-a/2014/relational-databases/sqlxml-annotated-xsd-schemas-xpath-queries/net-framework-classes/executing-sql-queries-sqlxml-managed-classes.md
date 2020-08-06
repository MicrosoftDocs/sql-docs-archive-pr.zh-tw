---
title: " (SQLXML Managed 類別) 執行 SQL 查詢 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML], SQLXML Managed Classes
- SQLXML Managed Classes, executing SQL queries
- Managed Classes [SQLXML], executing SQL queries
- ExecuteToStream method
- SQL queries [SQLXML]
ms.assetid: a561ae83-a8b6-4b9b-a819-9b86839546b4
author: rothja
ms.author: jroth
ms.openlocfilehash: d869e45de359e602b2451b9f66fa3046f6823c1e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596573"
---
# <a name="executing-sql-queries-sqlxml-managed-classes"></a>執行 SQL 查詢 (SQLXML Managed 類別)
  此範例示範：  
  
-    (SqlXmlParameter 物件) 建立參數。  
  
-   將值指派給屬性 (SqlXmlParameter 物件的名稱和值) 。  
  
 在此範例中，系統會執行簡單 SQL 查詢來擷取其姓氏值當做參數傳遞之員工的名字、姓氏和生日。 在 (*LastName*) 中指定參數時，只會設定 Value 屬性。 未設定 Name 屬性，因為在此查詢中，參數是位置，而且不需要名稱。  
  
 SqlXmlCommand 物件的 CommandType 屬性預設為**Sql**。 因此，未明確地設定屬性。  
  
> [!NOTE]  
>  在程式碼中，您必須於連接字串內提供 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
 以下為 C# 程式碼：  
  
```  
using System;  
  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testParams()  
      {  
         Stream strm;  
         SqlXmlParameter p;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);        
         cmd.CommandText = "SELECT FirstName, LastName FROM Person.Contact WHERE LastName=? For XML Auto";  
         p = cmd.CreateParameter();  
         p.Value = "Achong";  
         string strResult;  
         try   
         {  
            strm = cmd.ExecuteStream();  
            strm.Position = 0;  
            using(StreamReader sr = new StreamReader(strm))  
            {  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         catch (SqlXmlException e)  
         {  
            //in case of an error, this prints error returned.  
            e.ErrorStream.Position=0;  
            strResult=new StreamReader(e.ErrorStream).ReadToEnd();  
            System.Console.WriteLine(strResult);  
         }  
  
         return 0;  
   }  
public static int Main(String[] args)  
{  
    testParams();  
    return 0;  
}  
}  
```  
  
### <a name="to-test-the-application"></a>若要測試應用程式  
  
1.  將此主題中提供的 C# 程式碼 (DocSample.cs) 儲存到資料夾中。  
  
2.  編譯程式碼。 若要在命令提示字元下編譯程式碼，請使用：  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     這樣會建立可執行檔 (DocSample.exe)。  
  
3.  在命令提示字元中，執行 DocSample.exe。  
  
 若要測試此範例，您必須先在電腦上安裝 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework。  
  
 您可以指定執行 Updategram (也是一個範本) 的範本 (如以下程式碼片段所示) 來插入客戶記錄，而不是指定 SQL 查詢當做命令文字。 您可以在檔案中指定範本和 Updategrams 並執行這些檔案。 如需詳細資訊，請參閱[使用 CommandText 屬性執行範本](executing-template-files-by-using-the-commandtext-property.md)檔案。  
  
```  
SqlXmlCommand cmd = new SqlXmlCommand("Provider=SQLOLEDB;Data Source=SqlServerName;Initial Catalog=Database; Integrated Security=SSPI;");  
Stream stm;  
cmd.CommandType = SqlXmlCommandType.UpdateGram;  
cmd.CommandText = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql' xmlns:updg='urn:schemas-microsoft-com:xml-updategram'>" +  
      "<updg:sync>" +  
       "<updg:before/>" +  
       "<updg:after>" +  
         "<Customer CustomerID='aaaaa' CustomerName='Some Name' CustomerTitle='SomeTitle' />" +  
       "</updg:after>" +  
       "</updg:sync>" +  
       "</ROOT>";  
  
stm = cmd.ExecuteStream();  
stm = null;  
cmd = null;  
```  
  
## <a name="using-executetostream"></a>使用 ExecuteToStream  
 如果您有現有的資料流程，您可以使用 ExecuteToStream 方法，而不是建立資料流程物件，並使用 Execute 方法。 上述範例中的程式碼會在這裡修訂，以使用 ExecuteToStream 方法：  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=SqlServerName;database=AdventureWorks;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      SqlXmlParameter p;  
      MemoryStream ms = new MemoryStream();  
      StreamReader sr = new StreamReader(ms);  
      ms.Position = 0;  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.CommandText = "select FirstName, LastName from Person.Contact where LastName = ? For XML Auto";  
      p = cmd.CreateParameter();  
      p.Value = "Achong";  
      cmd.ExecuteToStream(ms);  
      ms.Position = 0;  
      Console.WriteLine(sr.ReadToEnd());  
      return 0;        
   }  
   public static int Main(String[] args)  
   {  
      testParams();     
      return 0;  
   }  
}  
```  
  
> [!NOTE]  
>  您也可以使用傳回 XmlReader 物件的 ExecuteXMLReadermethod。 如需詳細資訊，請參閱[使用 ExecuteXMLReader 方法執行 SQL 查詢](executing-sql-queries-by-using-the-executexmlreader-method.md)。  
  
  
