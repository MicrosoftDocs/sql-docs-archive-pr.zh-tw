---
title: 使用 ADO 執行 DiffGram (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], SQLOLEDB Provider
- ADO [SQLXML]
- SQLXMLOLEDB Provider, DiffGrams
- data providers [SQLXML], SQLOLEDB Provider
- DiffGrams [SQLXML], ADO
ms.assetid: 741fce82-de83-4923-86eb-30acb5b9a5e6
author: rothja
ms.author: jroth
ms.openlocfilehash: b96db25fd46b1ecbbc15c8acd912743e5560f178
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596597"
---
# <a name="executing-a-diffgram-by-using-ado-sqlxml-40"></a>使用 ADO 執行 DiffGram (SQLXML 4.0)
  這個 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 應用程式會使用 ADO 來建立 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的連接，然後執行 DiffGram。 在此應用程式中，DiffGram 和 XSD 結構描述會儲存在一個檔案中。 應用程式會從指定的檔案載入 DiffGram。 您可以使用任何 Diffgram (和相關聯的 XSD 架構) ，如[DiffGram 範例](diffgram-examples-sqlxml-4-0.md)中所述。  
  
 這是範例應用程式的程序：  
  
-    (ADODB 的**conn**物件 **。連接**) 會建立與特定伺服器上 SQL Server 之執行中實例的連接。  
  
-   **Cmd**物件 (**ADODB** ，) 會在已建立的連接上執行。  
  
-   命令用語會設定為 DBGUID_MSSQLXML。  
  
-   DiffGram 會從檔案複製到命令資料流程 (**字串分 text.append**) 。  
  
-   命令的輸出資料流程會設定為**StrmOut**物件 (**ADODB。串流**) 以接收任何傳回的資料。  
  
-   當您使用 SQLOLEDB 提供者時，根據預設，您會取得 Sqlxmlx.dll 提供的 Microsoft SQLXML 功能。 若要使用 Sqlxml4.dll 搭配 SQLOLEDB 提供者，必須在 SQLOLEDB 提供者**連接**物件上，將**sqlxml Version**屬性設定為**sqlxml. 4.0。**  
  
-   執行命令 (DiffGram)。  
  
 下列程式碼是範例應用程式。  
  
> [!NOTE]  
>  在程式碼中，您必須於連接字串內提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
```  
Private Sub Command1_Click()  
  Dim cmd As New ADODB.Command  
  Dim conn As New ADODB.Connection  
  Dim strmOut As New ADODB.Stream  
  Dim strmIn As New ADODB.Stream  
  
  'Open a connection to SQL Server.  
  conn.Provider = "SQLOLEDB"  
  conn.Open "server=SqlServerName; database=tempdb; Integrated Security=SSPI; "  
  conn.Properties("SQLXML Version") = "SQLXML.4.0"  
  Set cmd.ActiveConnection = conn  
  strmIn.Open  
  strmIn.Charset = "UTF-8"  
  strmIn.LoadFromFile "C:\SomeFilePath\SampleDiffGram.xml"  
  strmIn.Position = 0  
  Set cmd.CommandStream = strmIn  
  
  strmOut.Open  
  cmd.Properties("Output Stream").Value = strmOut  
  cmd.Properties("Output Encoding").Value = "UTF-8"  
  
  cmd.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  cmd.Properties("Mapping Schema") = "C:\SomeFilePath\SampleDiffGram.xml"  
  cmd.Execute , , adExecuteStream  
  strmOut.Position = 0  
  Set cmd = Nothing  
  strmOut.Charset = "UTF-8"  
  strmOut.SaveToFile "C:\DropIt.txt", adSaveCreateOverWrite  
  strmOut.Close  
  Set strmOut = Nothing  
  
End Sub  
```  
  
### <a name="to-test-the-diffgram"></a>若要測試 DiffGram  
  
1.  如果您是電腦上的資料夾，請從[DiffGram 範例](diffgram-examples-sqlxml-4-0.md)中的其中一個範例複製其中一個 diffgram 和對應的 XSD 架構。  
  
2.  開啟 Visual Basic，然後建立一個標準的 EXE 專案。  
  
3.  將這些參考加入到專案中：  
  
    ```  
    Microsoft ActiveX Data Objects 2.8 Library  
    ```  
  
4.  在 [工具箱] 中，按一下 [**命令**]，然後在表單上繪製一個按鈕。  
  
5.  按兩下該按鈕來編輯程式碼，然後加入主題中提供之應用程式的程式碼。  
  
6.  編輯程式碼以指定 DiffGram 和 XSD 檔案名稱。 同時在適當時，編輯連接字串。  
  
7.  執行應用程式。 執行的結果取決於您所執行的 DiffGram。  
  
  
