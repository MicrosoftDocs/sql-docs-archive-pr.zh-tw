---
title: 存取 ADO.NET 中的使用者定義類型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
author: rothja
ms.author: jroth
ms.openlocfilehash: a94e333ad743ed07dff6b973ebfe227312a1cab2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598447"
---
# <a name="accessing-user-defined-types-in-adonet"></a>存取 ADO.NET 中的使用者定義型別
   (Udt) 的使用者定義型別是使用 .NET Framework common language runtime 所支援的任何語言所撰寫， [!INCLUDE[msCoName](../../includes/msconame-md.md)] (CLR) 會產生可驗證的程式碼。 這包含 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic。 UDT 允許在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中儲存物件及自訂資料結構。 資料會做為 .NET Framework 類別或結構的公用成員而公開，行為可使用類別或結構的方法來定義。 UDT 可用作資料表的資料行定義、[!INCLUDE[tsql](../../includes/tsql-md.md)] 批次中的變數，或是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函式或預存程序的引數。  
  
 在 ADO.NET 中，`System.Data.SqlClient` 提供者以下列方式公開 UDT：  
  
-   做為物件透過 `System.Data.SqlClient.SqlDataReader`。  
  
-   做為未經處理位元組透過 `SqlDataReader`。  
  
-   做為 `System.Data.SqlClient.SqlParameter` 物件的參數。  
  
## <a name="in-this-section"></a>本節內容  
 [擷取 UDT 資料](accessing-user-defined-types-retrieving-udt-data.md)  
 說明如何擷取 UDT 資料及如何指定參數。  
  
 [以 DataAdapter 更新 UDT 資料行](accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 說明如何在 `DataSets` 中使用 UDT，以及如何使用 `DataAdapters` 更新 UDT 資料。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 使用者定義類型](clr-user-defined-types.md)  
  
  
