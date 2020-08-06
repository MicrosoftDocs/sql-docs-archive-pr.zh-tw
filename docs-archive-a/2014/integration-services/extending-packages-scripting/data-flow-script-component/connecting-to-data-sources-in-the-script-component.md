---
title: 連接到指令碼元件中的資料來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], connecting to data sources
ms.assetid: 96de63ab-ff48-4e7e-89e0-ffd6a89c63b6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9272f946abb68a1c54cd6f4851806ec6a1b15de7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597215"
---
# <a name="connecting-to-data-sources-in-the-script-component"></a>連接到指令碼元件中的資料來源
  連接管理員只是一種便利的單位，用以封裝和儲存連接至特定類型的資料來源所需的資訊。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 連接](../../connection-manager/integration-services-ssis-connections.md)。  
  
 您可以在 [指令碼轉換編輯器] 的 [連線管理員] 頁面上，按一下 [加入] 與 [移除] 按鈕，讓來源或目的地元件中的自訂指令碼可以存取現有的連線管理員。 不過，您必須撰寫自己的自訂程式碼，以載入或是儲存資料，以及 (可能的話) 開啟和關閉連至資料來源的連接。 如需 [指令碼轉換編輯器] 之 [連線管理員] 頁面的詳細資訊，請參閱[在指令碼元件編輯器中設定指令碼元件](configuring-the-script-component-in-the-script-component-editor.md)和[指令碼轉換編輯器 &#40;連線管理員頁面&#41;](../../script-transformation-editor-connection-managers-page.md)。  
  
 指令碼元件會建立 `Connections` 專案項目中的 `ComponentWrapper` 集合類別，它含有每個連接管理員之強式類型存取子，具有與連接管理員本身相同的名稱。 此集合是透過 `Connections` 類別的 `ScriptMain` 屬性來公開。 存取子屬性會傳回連接管理員的參考，以做為 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100> 的執行個體。 例如，如果您已在對話方塊的 [連接管理員] 頁面中加入名為 `MyADONETConnection` 的連接管理員，就可以加入下列程式碼，取得指令碼中該連接管理員的參考：  
  
 `Dim myADONETConnectionManager As IDTSConnectionManager100 = _`  
  
 `Me.Connections.MyADONETConnection`  
  
> [!NOTE]  
>  您必須知道連接管理員傳回的連接類型，才能呼叫 `AcquireConnection`。 因為指令碼工作已啟用 `Option Strict`，所以您必須將以 `Object` 類型傳回的連接，轉換為適當的連接類型，才能使用它。  
  
 接下來，您呼叫特定連接管理員的 `AcquireConnection` 方法，以取得基礎連接或是連接至資料來源所需的資訊。 例如，您透過使用下列程式碼取得 ADO.NET 連線管理員所包裝的 **System.Data.SqlConnection** 之參考：  
  
 `Dim myADOConnection As SqlConnection = _`  
  
 `CType(MyADONETConnectionManager.AcquireConnection(Nothing), SqlConnection)`  
  
 相反的，對於一般檔案連接管理員的相同呼叫，只會傳回檔案資料來源的路徑與檔案名稱。  
  
 `Dim myFlatFile As String = _`  
  
 `CType(MyFlatFileConnectionManager.AcquireConnection(Nothing), String)`  
  
 然後您必須將此路徑和檔案名稱提供給 `System.IO.StreamReader` 或 `Streamwriter`，才可在一般檔案中讀取或寫入資料。  
  
> [!IMPORTANT]  
>  當您在指令碼元件中撰寫 Managed 程式碼時，無法呼叫傳回 Unmanaged 物件之連線管理員的 AcquireConnection 方法，例如 OLE DB 連線管理員與 Excel 連線管理員。 不過，您可以讀取這些連線管理員的 ConnectionString 屬性，而且可以透過使用來自 **System.Data.OleDb** 命名空間的 OLEDB **連接**之連接字串，直接在程式碼中連接至資料來源。  
>   
>  如果您需要呼叫會傳回 Unmanaged 物件之連線管理員的 AcquireConnection 方法，請使用 ADO.NET 連線管理員。 當您設定 ADO.NET 連接管理員以使用 OLE DB 提供者時，它會透過使用 .NET Framework Data Provider for OLE DB 來連接。 在此情況下，AcquireConnection 方法會傳回， `System.Data.OleDb.OleDbConnection` 而不是非受控物件。 若要將 ADO.NET 連線管理員設定成與 Excel 資料來源搭配使用，請選取 Microsoft OLE DB Provider for Jet，指定 Excel 活頁簿，然後在 [連線管理員] 對話方塊的 [全部] 頁面上輸入 `Excel 8.0` (針對 Excel 97 和更新的版本)，作為 [擴充屬性] 的值。  
  
 如需如何透過指令碼元件使用連線管理員的詳細資訊，請參閱[以指令碼元件建立來源](../../extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)和[以指令碼元件建立目的地](../../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)。  
  
![Integration Services 圖示 (小型) ](../../media/dts-16.gif "Integration Services 圖示 (小)")會**保持最**新狀態 Integration Services  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連接](../../connection-manager/integration-services-ssis-connections.md)   
 [建立連接管理員](../../create-connection-managers.md)  
  
  
