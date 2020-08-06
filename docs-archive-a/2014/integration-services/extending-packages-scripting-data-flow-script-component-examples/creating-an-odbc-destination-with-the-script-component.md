---
title: 使用指令碼元件建立 ODBC 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], destination components
- ODBC destination [Integration Services]
- destinations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: d198c866-78f4-4a50-ae15-333160645815
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 10adff11a7e1db24d9a244c3e83949a010b606c7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597221"
---
# <a name="creating-an-odbc-destination-with-the-script-component"></a>使用指令碼元件建立 ODBC 目的地
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，您通常會使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 目的地與 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for ODB 來將資料儲存到 ODBC 目的地。 不過，您也可以建立在單一封裝中要使用的特定 ODBC 目的地。 若要建立這個特定的 ODBC 目的地，可以使用如下列範例所示的指令碼元件。  
  
> [!NOTE]  
>  如果您要建立可以更輕鬆地在多個資料流程工作與多個封裝之間重複使用的元件，請考慮使用這個指令碼元件範例中的程式碼，做為自訂資料流程元件的起點。 如需詳細資訊，請參閱 [開發自訂資料流程元件](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="example"></a>範例  
 下列範例示範如何建立一個目的地元件，以使用現有的 ODBC 連線管理員來將資料從資料流程儲存到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
 此範例是[使用指令碼元件建立目的地](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)主題中所示範的自訂 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 目的地之修改版本。 不過，在這個範例中，已修改自訂 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 目的地以搭配 ODBC 連接管理員使用，並將資料儲存到 ODBC 目的地。 這些修改也包括下列變更：  
  
-   您無法從 Managed 程式碼呼叫 ODBC 連接管理員的 `AcquireConnection` 方法，因為它會傳回原生物件。 因此，這個範例使用連接管理員的連接字串以 Managed ODBC [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者直接連到資料來源。  
  
-   `OdbcCommand` 需要位置參數。 參數的位置由命令文字中的問號 (?) 指出 (相較之下，`SqlCommand` 需要具名的參數)。  
  
 此範例使用 **AdventureWorks** 範例資料庫中的 **Person.Address** 資料表。 此範例會透過資料流程傳遞第一個和第四個數據行，也就是這個資料表的**int * AddressID*** 和**Nvarchar (30) City**資料行。 在[開發特定類型的指令碼元件](../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)主題中，這個相同的資料用於來源、轉換和目的地範例中。  
  
#### <a name="to-configure-this-script-component-example"></a>設定此指令碼元件範例  
  
1.  建立 ODBC 連線管理員，以連線至 **AdventureWorks** 資料庫。  
  
2.  在 **AdventureWorks** 資料庫中執行下列 Transact-SQL 命令，以建立目的地資料表：  
  
    ```  
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  將新的指令碼元件加入至資料流程設計師介面，並將它設定為目的地。  
  
4.  將上游來源或轉換的輸出連接到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的目的地元件 (您不需要進行任何轉換，就可以直接將來源連線到目的地。)為了確保這個範例可運作，上游元件的輸出必須至少包含 **AdventureWorks** 範例資料庫中 **Person.Address** 資料表的 **AddressID** 和 **City** 資料行。  
  
5.  開啟**指令碼轉換編輯器**。 在 [輸入資料行]  頁面上，選取 [AddressID]  與 [City]  資料行。  
  
6.  在 [輸入及輸出]  頁面上，以更具描述性的名稱重新命名輸入，例如 **MyAddressInput**。  
  
7.  在 [連線管理員]  頁面上，使用 **MyODBCConnectionManager** 之類的描述性名稱，新增或建立 ODBC 連線管理員。  
  
8.  在 [**腳本**] 頁面上，按一下 [**編輯腳本**]，然後在類別中輸入如下所示的腳本 `ScriptMain` 。  
  
9. 依序關閉指令碼開發環境和**指令碼轉換編輯器**，然後執行此範例。  
  
    ```vb  
    Imports System.Data.Odbc  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Dim odbcConn As OdbcConnection  
        Dim odbcCmd As OdbcCommand  
        Dim odbcParam As OdbcParameter  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            Dim connectionString As String  
            connectionString = Me.Connections.MyODBCConnectionManager.ConnectionString  
            odbcConn = New OdbcConnection(connectionString)  
            odbcConn.Open()  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            odbcCmd = New OdbcCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
                "VALUES(?, ?)", odbcConn)  
            odbcParam = New OdbcParameter("@addressid", OdbcType.Int)  
            odbcCmd.Parameters.Add(odbcParam)  
            odbcParam = New OdbcParameter("@city", OdbcType.NVarChar, 30)  
            odbcCmd.Parameters.Add(odbcParam)  
  
        End Sub  
  
        Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
            With odbcCmd  
                .Parameters("@addressid").Value = Row.AddressID  
                .Parameters("@city").Value = Row.City  
                .ExecuteNonQuery()  
            End With  
  
        End Sub  
  
        Public Overrides Sub ReleaseConnections()  
  
            odbcConn.Close()  
  
        End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System.Data.Odbc;  
    ...  
    public class ScriptMain :  
        UserComponent  
    {  
        OdbcConnection odbcConn;  
        OdbcCommand odbcCmd;  
        OdbcParameter odbcParam;  
  
        public override void AcquireConnections(object Transaction)  
        {  
  
            string connectionString;  
            connectionString = this.Connections.MyODBCConnectionManager.ConnectionString;  
            odbcConn = new OdbcConnection(connectionString);  
            odbcConn.Open();  
  
        }  
  
        public override void PreExecute()  
        {  
  
            odbcCmd = new OdbcCommand("INSERT INTO Person.Address2(AddressID, City) " +  
                "VALUES(?, ?)", odbcConn);  
            odbcParam = new OdbcParameter("@addressid", OdbcType.Int);  
            odbcCmd.Parameters.Add(odbcParam);  
            odbcParam = new OdbcParameter("@city", OdbcType.NVarChar, 30);  
            odbcCmd.Parameters.Add(odbcParam);  
  
        }  
  
        public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
        {  
  
            {  
                odbcCmd.Parameters["@addressid"].Value = Row.AddressID;  
                odbcCmd.Parameters["@city"].Value = Row.City;  
                odbcCmd.ExecuteNonQuery();  
            }  
  
        }  
  
        public override void ReleaseConnections()  
        {  
  
            odbcConn.Close();  
  
        }  
    }  
    ```  
  
![Integration Services 圖示 (小型) ](../media/dts-16.gif "Integration Services 圖示 (小)")會**保持最**新狀態 Integration Services  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [使用指令碼元件建立目的地](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
  
  
