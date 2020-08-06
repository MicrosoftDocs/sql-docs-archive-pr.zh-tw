---
title: 使用 ADO 執行 SQLXML 4.0 查詢
ms.custom: ''
ms.date: 12/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- query testers [SQLXML]
- test scripts
- ADO [SQLXML]
- queries [SQLXML], ADO
- SQLXML, ADO
ms.assetid: 3d54e3bb-7c5f-427e-82f8-1403a54c4f53
author: rothja
ms.author: jroth
ms.openlocfilehash: 169d20b4192e4a5b8e7b32839f2da255fc58d89c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687749"
---
# <a name="using-ado-to-execute-sqlxml-40-queries"></a>使用 ADO 執行 SQLXML 4.0 查詢
  在舊版的 SQLXML 中，可使用 SQLXML IIS 虛擬目錄和 SQLXML ISAPI 篩選來支援以 HTTP 為基礎的查詢執行。 在 SQLXML 4.0 中已經移除這些元件，因為自 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始引進的原生 XML Web 服務提供了類似且重疊的功能。  
  
 另一種選擇是利用在 Microsoft Data Access Components (MDAC) 2.6 和更新版本中初次引進的 ActiveX Data Objects (ADO) 的 SQL XML 延伸模組來執行查詢，並使用 SQLXML 4.0 來搭配以 COM 為基礎的應用程式。  
  
 本主題示範如何使用 SQLXML 和 ADO 以當做 Visual Basic Scripting Edition (VBScript) 應用程式的一部分 (具有 .vbs 副檔名的指令碼)。 本主題提供初始的安裝程序，以協助您重建和測試 SQLXML 4.0 文件集中的查詢範例。  
  
## <a name="creating-the-sqlxml-40-test-script"></a>建立 SQLXML 4.0 測試指令碼  
 在此程序中，您會建立 VBScript (.vbs) 檔案 Sqlxml4test.vbs，這個檔案可利用 ADO 2.6 和更新版本的 SQLXML ADO 延伸模組來執行 SQLXML 查詢。  
  
#### <a name="to-create-the-sqlxml-40-query-tester-using-ado-vbscript"></a>使用 ADO (VBScript) 建立 SQLXML 4.0 查詢測試者  
  
1.  複製下列 VBScript 程式碼，並將它貼到文字檔中。 將檔案儲存為 Sqlxml4test.vbs。  
  
    ```vb
    WScript.Echo "Query process may take a few seconds to complete. Please be patient."  
  
    ' Note that for SQL Server Native Client to be used as the data provider,  
    ' it needs to be installed on the client computer first. Also, SQLXML extensions   
    ' for ADO are used and available in MDAC 2.6 or later.  
  
    'Set script variables.  
    inputFile = "@@FILE_NAME@@"  
    strServer = "@@SERVER_NAME@@"  
    strDatabase = "@@DATABASE_NAME@@"  
    dbGuid = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  
    ' Establish ADO connection to SQL Server and   
    ' create an instance of the ADO Command object.  
    Set conn = CreateObject("ADODB.Connection")  
    Set cmd = CreateObject("ADODB.Command")  
    conn.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Server=" & strServer & _  
              ";Database=" & strDatabase & ";Integrated Security=SSPI"  
    Set cmd.ActiveConnection = conn  
  
    ' Create the input stream as an instance of the ADO Stream object.  
    Set inStream = CreateObject("ADODB.Stream")  
    inStream.Open  
    inStream.Charset = "utf-8"  
    inStream.LoadFromFile inputFile  
  
    ' Set ADO Command instance to use input stream.  
    Set cmd.CommandStream = inStream  
  
    ' Set the command dialect.  
    cmd.Dialect = dbGuid  
  
    ' Set a second ADO Stream instance for use as a results stream.   
    Set outStream = CreateObject("ADODB.Stream")  
    outStream.Open  
  
    ' Set dynamic properties used by the SQLXML ADO command instance.   
    cmd.Properties("XML Root").Value = "ROOT"  
    cmd.Properties("Output Encoding").Value = "UTF-8"  
  
    ' Connect the results stream to the command instance and execute the command.  
    cmd.Properties("Output Stream").Value = outStream  
    cmd.Execute , , 1024  
  
    ' Echo cropped/partial results to console.  
    WScript.Echo Left(outStream.ReadText, 1023)  
  
    inStream.Close  
    outStream.Close  
    ```  
  
2.  針對您正嘗試測試的範例及您的測試環境更新下列的指令碼值。  
  
    -   尋找 "`@@FILE_NAME@@`"，並以您的範例檔名稱加以取代。  
  
    -   尋找 "`@@SERVER_NAME@@`"，並以您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱加以取代 (例如，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在本機執行，則為 "`(local)`")。  
  
    -   尋找 "`@@DATABASE_NAME@@`"，並以資料庫的名稱加以取代 (例如，"`AdventureWorks2012`" 或 "`tempdb`")。  
  
     更新任何的其他值 (若您嘗試在電腦本機上重新建立之範例的特定指示中有提及)。  
  
3.  儲存並關閉檔案。  
  
4.  確認您已建立了任何其他的檔案，例如屬於您嘗試在電腦本機上重新建立之範例的 XML 範本或結構描述。 這些檔案應該位於與您儲存測試指令碼檔案 (Sqlxml4test.vbs) 相同的目錄中。  
  
5.  請遵照下一節中的指示來使用 SQLXML 4.0 測試指令碼。  
  
## <a name="using-the-sqlxml-40-test-script"></a>使用 SQLXML 4.0 測試指令碼  
 下列程序描述如何使用 Sqlxml4test.vbs 檔案來測試本文件集所提供的範例查詢。  
  
#### <a name="to-use-the-sqlxml-40-query-tester"></a>使用 SQLXML 4.0 查詢測試者  
  
1.  確認已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client，如下所示：  
  
    1.  在 [**開始**] 功能表中，指向 [**設定**]，然後按一下 [**控制台**]。  
  
    2.  在 [控制台] 中，開啟 [**新增或移除程式**]  
  
    3.  在目前已安裝的程式清單中，確認 [ **Microsoft SQL Server Native Client** ] 出現在清單中。  
  
        > [!NOTE]  
        >  如果您需要安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client，請參閱[安裝 SQL Server Native Client](../native-client/applications/installing-sql-server-native-client.md)。  
  
2.  確認用戶端電腦所安裝的 MDAC 版本為 2.6 或更新版本。 如果您需要驗證 MDAC 版本資訊，您可以使用 MDAC Component 檢查工具，這是從 Microsoft 網站免費下載提供 [https://www.microsoft.com/](https://www.microsoft.com/) 。 如需詳細資訊，請在 Microsoft 網站上搜尋「MDAC 元件檢查程式」。  
  
3.  執行指令碼。  
  
     您可以在命令列使用 Cscript.exe 來執行 VBScript 檔案，或者按兩下 Sqlxml4test.vbs 檔案來叫用 Windows Script Host (WScript.exe)。  
  
     此指令碼在執行時會顯示訊息，警示您指令碼可能需要一些時間執行，才能將查詢結果傳回並顯示為指令碼輸出。 當輸出出現時，請將其內容與範例的預期結果比較。  
  
  
