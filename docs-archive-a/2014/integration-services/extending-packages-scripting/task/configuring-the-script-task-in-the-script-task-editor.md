---
title: 在指令碼工作編輯器設定指令碼工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], configuring
- Script Task Editor
- SSIS Script task, configuring
ms.assetid: 232de0c9-b24d-4c38-861d-6c1f4a75bdf3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b75b4a030e6c5baa2e26c610b0e8216843c8cca7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593450"
---
# <a name="configuring-the-script-task-in-the-script-task-editor"></a>在指令碼工作編輯器設定指令碼工作
  在指令碼工作內撰寫自訂程式碼之前，必須先在 [指令碼工作編輯器]  的三個頁面中設定其主要屬性。 您可以使用 [屬性] 視窗，設定其他非指令碼工作專用的工作屬性。

> [!NOTE]
>  不同於在舊版中可以指出是否已編譯了指令碼，所有指令碼在 [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 中皆會先進行編譯。

## <a name="general-page-of-the-script-task-editor"></a>指令碼工作編輯器的一般頁面
 在 [指令碼工作編輯器] 的 [一般] 頁面上，為指令碼工作指派唯一的名稱與描述。

## <a name="script-page-of-the-script-task-editor"></a>指令碼工作編輯器的指令碼頁面
 [指令碼工作編輯器] 的 [指令碼] 頁面會顯示指令碼工作的自訂屬性。

### <a name="scriptlanguage-property"></a>ScriptLanguage 屬性
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 支援 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 程式設計語言。 當您在指令碼工作內建立指令碼之後，就無法變更 **ScriptLanguage** 屬性的值。

 若要為指令碼工作和指令碼元件設定預設指令碼語言，請使用 [選項] 對話方塊之 [一般] 頁面上的 **ScriptLanguage** 屬性。 如需相關資訊，請參閱 [General Page](../../general-page-of-integration-services-designers-options.md)。

### <a name="entrypoint-property"></a>EntryPoint 屬性
 `EntryPoint` 屬性會將 VSTA 專案中 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 執行階段所呼叫的 `ScriptMain` 類別方法指定為指令碼工作程式碼的進入點。 `ScriptMain`類別是腳本範本所產生的預設類別。

 如果您在 VSTA 專案內變更此方法的名稱，您就必須變更 `EntryPoint` 屬性的值。

### <a name="readonlyvariables-and-readwritevariables-properties"></a>ReadOnlyVariables 與 ReadWriteVariables 屬性
 您可以輸入現有變數的逗號分隔清單做為這些屬性的值，使得變數可在指令碼工作程式碼中以唯讀或讀取/寫入的方式來存取。 您可以透過 `Dts` 物件的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 屬性在程式碼中存取這兩種類型的變數。 如需詳細資訊，請參閱 [在指令碼工作中使用變數](../../extending-packages-scripting/task/using-variables-in-the-script-task.md)。

> [!NOTE]
>  變數名稱會區分大小寫。

 若要選取變數，請按一下屬性欄位旁邊的省略符號 ([...]  ) 按鈕。 如需詳細資訊，請參閱[選取變數頁面](../../control-flow/select-variables-page.md)。

### <a name="edit-script-button"></a>編輯指令碼按鈕
 [編輯指令碼]  按鈕會啟動您用來撰寫自訂指令碼的 VSTA 開發環境。 如需詳細資訊，請參閱[指令碼工作的程式碼撰寫和偵錯](coding-and-debugging-the-script-task.md)。

## <a name="expressions-page-of-the-script-task-editor"></a>指令碼工作編輯器的運算式頁面
 在 [指令碼工作編輯器] 的 [運算式] 頁面上，您可以使用運算式，針對上面列出之指令碼工作的屬性及許多其他工作屬性來提供值。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../expressions/integration-services-ssis-expressions.md)為止。

![Integration Services 圖示 (小型) ](../../media/dts-16.gif "Integration Services 圖示 (小)")會**保持最**新狀態 Integration Services  <br /> 若要取得 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 的最新下載、文件、範例和影片以及社群中的選定方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。

## <a name="see-also"></a>另請參閱
 [指令碼工作的程式碼撰寫和偵錯](coding-and-debugging-the-script-task.md)


