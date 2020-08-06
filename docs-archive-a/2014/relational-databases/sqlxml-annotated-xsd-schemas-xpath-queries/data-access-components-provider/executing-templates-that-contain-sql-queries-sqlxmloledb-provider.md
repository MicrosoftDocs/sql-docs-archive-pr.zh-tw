---
title: 執行包含 SQL 查詢 (SQLXMLOLEDB 提供者) 的範本 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- templates [SQLXML]
- SQLXMLOLEDB Provider, executing template files
- templates [SQLXML], SQL queries
- XML templates [SQLXML]
- SQL queries [SQLXML]
ms.assetid: ff2bc36f-e3fb-4d8f-8e3a-2680a39eda11
author: rothja
ms.author: jroth
ms.openlocfilehash: c3d3bc340612286e211d85f52a3d914d1d1b6b9f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597037"
---
# <a name="executing-templates-that-contain-sql-queries-sqlxmloledb-provider"></a>執行包含 SQL 查詢的範本 (SQLXMLOLEDB 提供者)
  這個範例說明如何使用 SQLXMLOLEDB 提供者特定的屬性 ClientSideXML。 在此用戶端 ADO 範例應用程式中，由 SQL 查詢所組成的 XML 範本會在伺服器上執行。  
  
 因為 ClientSideXML 屬性設定為 True，所以不含 FOR XML 子句的 SELECT 語句會傳送至伺服器。 伺服器會執行查詢，並將資料列集傳回給用戶端。 用戶端接著會將 FOR XML 轉換套用至資料列集，並產生 XML 文件。  
  
 XML 範本會針對所產生的 XML 檔提供單一最上層根項目 (\<ROOT>) ，因此不會提供 xml 根屬性。  
  
 若要執行 XML 範本，必須指定 Dialect {5d531cb2-e6ed-11d2-b252-00c04f681b71}。  
  
> [!NOTE]  
>  在程式碼中，您必須於連接字串內提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。 此外，這個範例會指定針對資料提供者使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) (需要安裝其他網路用戶端軟體)。 如需詳細資訊，請參閱[SQL Server Native Client 的系統需求](../../native-client/system-requirements-for-sql-server-native-client.md)。  
  
```  
Option Explicit  
  
Sub Main()  
  Dim oTestStream As New ADODB.Stream  
  Dim oTestConnection As New ADODB.Connection  
  Dim oTestCommand As New ADODB.Command  
  oTestConnection.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Data Source=SqlServerName;Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
  
  Set oTestCommand.ActiveConnection = oTestConnection  
  oTestCommand.Properties("ClientSideXML") = True  
  oTestCommand.CommandText = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'> " & _  
        " <sql:query> " & _  
        "   SELECT TOP 10 FirstName, LastName FROM Person.Contact FOR XML AUTO " & _  
        "   </sql:query> " & _  
        " </ROOT> "  
  oTestStream.Open  
  ' You need the dialect if you are executing   
  ' XML templates (not for SQL queries).  
  oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  oTestCommand.Properties("Output Stream").Value = oTestStream  
  oTestCommand.Execute , , adExecuteStream  
  
  oTestStream.Position = 0  
  oTestStream.Charset = "utf-8"  
  Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
  
Sub Form_Load()  
  Main  
End Sub  
```  
  
  
