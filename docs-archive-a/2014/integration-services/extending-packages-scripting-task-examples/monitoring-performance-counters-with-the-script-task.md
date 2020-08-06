---
title: 以指令碼工作監視效能計數器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- performance counters [Integration Services]
- SSIS Script task, performance counters
- custom performance counters [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], performance counters
- counters [Integration Services]
ms.assetid: 86609bf1-cae6-435e-a58d-41bdfc521e94
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 143e11ff966eb11961aa15073a503522c4b9c86b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705290"
---
# <a name="monitoring-performance-counters-with-the-script-task"></a>以指令碼工作監視效能計數器
  系統管理員可能需要監視 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝在大量資料執行複雜轉換時的效能。   的 [!INCLUDE[msCoName](../../includes/msconame-md.md)]System.Diagnostics[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 命名空間提供可讓您使用現有效能計數器或建立自訂效能計數器的類別。  
  
 效能計數器會儲存應用程式效能資訊，可用以分析某段時間的軟體效能。 透過使用 [效能監視器]  工具，就可以在本機或是遠端監視效能計數器。 您可以將效能計數器值儲存在變數中，以供之後在封裝中的控制流程分支使用。  
  
 若不使用效能計數器，您也可以透過 `Dts` 物件的 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> 屬性，引發 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> 事件。 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> 事件會將增加的進度與百分比完成資訊傳回 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行階段。  
  
> [!NOTE]  
>  如果您想要建立可更輕鬆地在多個封裝之間重複使用的工作，請考慮使用此指令碼工作範例中的程式碼做為自訂工作的起點。 如需詳細資訊，請參閱 [開發自訂工作](../extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>描述  
 下列範例會建立自訂效能計數器並遞增計數器。 首先，範例會判斷效能計數器是否已經存在。 如果尚未建立效能計數器，指令碼會呼叫 `Create` 物件的 `PerformanceCounterCategory` 方法。 在建立效能計數器之後，指令碼會遞增計數器。 最後，下面將提供範例說明當不再需要效能計數器時，呼叫效能計數器上的 `Close` 方法之最佳作法。  
  
> [!NOTE]  
>  建立新的效能計數器類別以及效能計數器需要系統管理權限。 另外，在建立新的類別與計數器之後，會保存在電腦上。  
  
#### <a name="to-configure-this-script-task-example"></a>設定此指令碼工作範例  
  
-   `Imports`在您的程式碼中使用語句來**System.Diagnostics**匯入 system.servicemodel 命名空間。  
  
### <a name="example-code"></a>範例程式碼  
  
```vb  
Public Sub Main()  
  
    Dim myCounter As PerformanceCounter  
  
    Try  
        'Create the performance counter if it does not already exist.  
        If Not _  
        PerformanceCounterCategory.Exists("TaskExample") Then  
            PerformanceCounterCategory.Create("TaskExample", _  
                "Task Performance Counter Example", "Iterations", _  
                "Number of times this task has been called.")  
        End If  
  
        'Initialize the performance counter.  
        myCounter = New PerformanceCounter("TaskExample", _  
            "Iterations", String.Empty, False)  
  
        'Increment the performance counter.  
        myCounter.Increment()  
  
         myCounter.Close()  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, _  
            "Task Performance Counter Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
  
public class ScriptMain  
{  
  
public void Main()  
        {  
  
            PerformanceCounter myCounter;  
  
            try  
            {  
                //Create the performance counter if it does not already exist.  
                if (!PerformanceCounterCategory.Exists("TaskExample"))  
                {  
                    PerformanceCounterCategory.Create("TaskExample", "Task Performance Counter Example", "Iterations", "Number of times this task has been called.");  
                }  
  
                //Initialize the performance counter.  
                myCounter = new PerformanceCounter("TaskExample", "Iterations", String.Empty, false);  
  
                //Increment the performance counter.  
                myCounter.Increment();  
  
                myCounter.Close();  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Task Performance Counter Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
```  
  
![Integration Services 圖示 (小型) ](../media/dts-16.gif "Integration Services 圖示 (小)")會**保持最**新狀態 Integration Services  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
  
