---
title: 以程式設計方式使用變數 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- System namespace
- scope [Integration Services]
- variables [Integration Services], programmatically
- configuration files [Integration Services]
- Variables collection
- User namespace
- custom variables [Integration Services]
- variables [Integration Services], customizing
ms.assetid: c4b76a3d-94ca-4a8e-bb45-cb8bd0ea3ec1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2c903ee6adb8989eaeb93efbe943eca93c73eae4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706697"
---
# <a name="working-with-variables-programmatically"></a>以程式設計方式使用變數
  變數是在封裝、容器、工作及事件處理常式中動態設定值和控制處理序的方式。 優先順序條件約束也可以使用變數，以控制資料流向不同工作的方向。 變數有各種不同的用途：

-   在執行階段更新封裝的屬性。

-   在執行階段擴展 Transact-SQL 陳述式的參數值。

-   控制 Foreach 迴圈的流程。 如需詳細資訊，請參閱[將列舉新增至控制流程](../control-flow/control-flow.md)。

-   按照運算式中的用途控制優先順序條件約束。 優先順序條件約束可以包含條件約束定義中的變數。 如需詳細資訊，請參閱 [將運算式加入優先順序條件約束](../control-flow/precedence-constraints.md)。

-   控制 For 迴圈容器的條件式重複。 如需詳細資訊，請參閱[將反覆項目新增至控制流程](../add-iteration-to-a-control-flow.md)。

-   建立包含變數值的運算式。

-   您可以為下列所有容器類型建立自訂變數：套件、**Foreach 迴圈**容器、**For 迴圈**容器、**時序**容器、TaskHost 和事件處理常式。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)和[在封裝中使用變數](../use-variables-in-packages.md)。

## <a name="scope"></a>影響範圍
 每個容器有它自己的 <xref:Microsoft.SqlServer.Dts.Runtime.Variables> 集合。 在建立新變數時，它在其父容器的範圍內。 因為封裝容器位於容器階層的最上層，所以具有封裝範圍的變數在功能上與全域變數相同，而且在封裝中的所有容器都可以看到它們。 透過使用集合中的變數名稱或是變數的索引，容器的子系也可以透過 <xref:Microsoft.SqlServer.Dts.Runtime.Variables> 集合來存取容器的變數集合。

 因為變數的可見性範圍是從上向下，所以封裝中的所有容器都可以看到在封裝層級宣告的變數。 因此，在容器上的 <xref:Microsoft.SqlServer.Dts.Runtime.Variables> 集合除了自己的變數以外，還會包括屬於其父系的所有變數。

 相反的，包含在工作中的變數其範圍和可見性則有限，只有工作看得到它們。

 如果封裝執行其他封裝，則定義在呼叫封裝範圍中的變數可用於所呼叫的封裝。 只有在所呼叫的封裝中有相同名稱的變數時，才會發生例外狀況。 發生衝突時，在所呼叫的封裝中之變數值會覆寫來自呼叫封裝的值。 定義在所呼叫的封裝範圍中之變數絕對無法用於呼叫封裝中。

 下列程式碼範例以程式設計方式在封裝範圍建立變數 `myCustomVar`，然後在封裝可看見的所有變數中反覆運算，以列印其名稱、資料類型與值。

```csharp
using System;
using Microsoft.SqlServer.Dts.Runtime;

namespace Microsoft.SqlServer.Dts.Samples
{
  class Program
  {
    static void Main(string[] args)
    {
      Application app = new Application();
      // Load a sample package that contains a variable that sets the file name.
      Package pkg = app.LoadPackage(
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +
        @"\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx",
        null);
      Variables pkgVars = pkg.Variables;
      Variable myVar = pkg.Variables.Add("myCustomVar", false, "User", "3");
      foreach (Variable pkgVar in pkgVars)
      {
        Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name,
          pkgVar.DataType, pkgVar.Value.ToString());
      }
      Console.Read();
    }
  }
}
```

```vb
Imports Microsoft.SqlServer.Dts.Runtime

Module Module1

  Sub Main()

    Dim app As Application = New Application()
    ' Load a sample package that contains a variable that sets the file name.
    Dim pkg As Package = app.LoadPackage( _
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _
      "\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx", _
      Nothing)
    Dim pkgVars As Variables = pkg.Variables
    Dim myVar As Variable = pkg.Variables.Add("myCustomVar", False, "User", "3")
    Dim pkgVar As Variable
    For Each pkgVar In pkgVars
      Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name, _
        pkgVar.DataType, pkgVar.Value.ToString())
    Next
    Console.Read()

  End Sub

End Module
```

 **範例輸出：**

 `Variable: CancelEvent, Int32, 0`

 `Variable: CreationDate, DateTime, 4/18/2003 11:57:00 AM`

 `Variable: CreatorComputerName, String,`

 `Variable: CreatorName, String,`

 `Variable: ExecutionInstanceGUID, String, {237AB5A4-7E59-4FC9-8D61-E8F20363DF25}`

 `Variable: FileName, String, Junk`

 `Variable: InteractiveMode, Boolean, False`

 `Variable: LocaleID, Int32, 1033`

 `Variable: MachineName, String, MYCOMPUTERNAME`

 `Variable: myCustomVar, String, 3`

 `Variable: OfflineMode, Boolean, False`

 `Variable: PackageID, String, {F0D2E396-A6A5-42AE-9467-04CE946A810C}`

 `Variable: PackageName, String, DTSPackage1`

 `Variable: StartTime, DateTime, 1/28/2005 7:55:39 AM`

 `Variable: UserName, String, <domain>\<userid>`

 `Variable: VersionBuild, Int32, 198`

 `Variable: VersionComments, String,`

 `Variable: VersionGUID, String, {90E105B4-B4AF-4263-9CBD-C2050C2D6148}`

 `Variable: VersionMajor, Int32, 1`

 `Variable: VersionMinor, Int32, 0`

 請注意，在**系統**命名空間中限定範圍的所有變數，都可供套件使用。 如需詳細資訊，請參閱 [系統變數](../system-variables.md)。

## <a name="namespaces"></a>命名空間
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) 提供存在兩個變數的預設命名空間：**使用者**與**系統**命名空間。 根據預設，開發人員建立的任何自訂變數都會新增至**使用者**命名空間。 系統變數位於**系統**命名空間中。 您可以建立**使用者**命名空間之外的其他命名空間，以儲存自訂變數，而且可以變更**使用者**命名空間的名稱，但是無法在**系統**命名空間中新增或修改變數，也無法將系統變數指派給不同的命名空間。

 可使用的系統變數會因容器類型而異。 如需可用於套件、容器、工作和事件處理常式的系統變數清單，請參閱[系統變數](../system-variables.md)。

## <a name="value"></a>值
 自訂變數值可以是常值或是運算式：

-   如果您希望變數包含常值，請設定其 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> 屬性值。

-   如果您希望變數包含運算式，以便使用運算式的結果做為其值，請將變數的 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> 屬性設定為 `true`，並在 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Expression%2A> 屬性中提供運算式。 在執行階段會評估運算式，而且運算式的結果會做為變數值。 例如，如果變數的運算式屬性是 `"100 * 2""100 * 2"`，則變數會將值評估為 200。

 對於變數，您無法明確地設定其 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> 的值。 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> 值是從指派給變數的初始值來推斷，而且之後不能變更。 如需變數資料類型的詳細資訊，請參閱[整合服務資料類型](../data-flow/integration-services-data-types.md)。

 下列程式碼範例會建立新變數，將 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> 設定為 `true`、將運算式 `"100 * 2"` 指派給變數的運算式屬性，然後輸出變數值。

```csharp
using System;
using Microsoft.SqlServer.Dts.Runtime;

namespace Microsoft.SqlServer.Dts.Samples
{
  class Program
  {
    static void Main(string[] args)
    {
      Package pkg = new Package();
      Variable v100 = pkg.Variables.Add("myVar", false, "", 1);
      v100.EvaluateAsExpression = true;
      v100.Expression = "100 * 2";
      Console.WriteLine("Expression for myVar: {0}", 
        v100.Properties["Expression"].GetValue(v100));
      Console.WriteLine("Value of myVar: {0}", v100.Value.ToString());
      Console.Read();
    }
  }
}
```

```vb
Imports Microsoft.SqlServer.Dts.Runtime

Module Module1

  Sub Main()

    Dim pkg As Package = New Package
    Dim v100 As Variable = pkg.Variables.Add("myVar", False, "", 1)
    v100.EvaluateAsExpression = True
    v100.Expression = "100 * 2"
    Console.WriteLine("Expression for myVar: {0}", _
      v100.Properties("Expression").GetValue(v100))
    Console.WriteLine("Value of myVar: {0}", v100.Value.ToString)
    Console.Read()

  End Sub

End Module
```

 **範例輸出：**

 `Expression for myVar: 100 * 2`

 `Value of myVar: 200`

 運算式必須是使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 運算式語法的有效運算式。 除了運算式語法提供的運算子與函數之外，變數運算式中還允許常值，但是運算式無法參考其他變數或是資料行。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../expressions/integration-services-ssis-expressions.md)為止。

## <a name="configuration-files"></a>組態檔
 如果組態檔包含自訂變數，則可以在執行階段更新變數。 這表示當封裝執行時，會使用組態檔中的新值來取代原本在封裝中的變數值。 當將封裝部署到需要不同變數值的多部伺服器時，這個取代技術將特別有用。 例如，變數可以指定 **Foreach 迴圈**容器重複其工作流程的次數；或是列出事件處理常式在引發錯誤時，傳送電子郵件的收件者清單；或是變更套件失敗前，允許發生的錯誤次數。 這些變數是在每個環境的組態檔中動態提供的。 因此，在組態檔中只允許讀取/寫入的變數。 如需詳細資訊，請參閱 [建立封裝組態](../create-package-configurations.md)。

![Integration Services 圖示 (小型) ](../media/dts-16.gif "Integration Services 圖示 (小)")會**保持最**新狀態 Integration Services  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。

## <a name="see-also"></a>另請參閱
 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)[在封裝中使用變數](../use-variables-in-packages.md)


