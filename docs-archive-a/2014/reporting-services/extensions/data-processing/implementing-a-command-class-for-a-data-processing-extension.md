---
title: 為資料處理延伸模組實作命令類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], commands
- Command class
- commands [Reporting Services]
ms.assetid: 465ef8d1-c503-407c-8afd-58d620e344ee
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f07b9beb798b1cd33ec2fee6af890a09a516b2f5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87708957"
---
# <a name="implementing-a-command-class-for-a-data-processing-extension"></a>為資料處理延伸模組實作命令類別
  **Command** 物件會構成要求，並將它傳遞到資料來源。 命令文字可採用許多不同的語法形式，包括文字與 XML。 如果傳回結果，**Command** 物件會傳回結果以作為 **DataReader** 物件。  
  
 若要建立 **Command** 類別，請實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand>。 實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 方法以傳回結果集作為 **DataReader** 物件。 **Command** 類別的 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 方法應該包括實作，它需要 <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior> 列舉作為引數。 如果您將資料處理延伸模組部署到報表設計師，請提供實作以處理 <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior.SchemaOnly> 方法中的 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 案例。 僅限結構描述實作是用以提供具有欄位清單的報表設計師。 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 方法傳回的 **DataReader** 物件，需要在結果集中包含欄位或是資料行中的類型與名稱資訊。  
  
 (選擇性) 您的 **Command** 類別可以實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>。 這個介面允許實作類別以分析查詢，並在查詢中傳回參數清單。 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> 介面的功能只能用於報表設計師中。 當您實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> 時，允許每當在預覽模式執行報表時，提示報表設計師的使用者所需的參數。 此外，您可以在 [資料集] 對話方塊的 [參數] 索引標籤中檢視參數。  
  
> [!NOTE]  
>  如果自訂資料處理延伸模組不支援參時，就不應該實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>。  
  
 如需範例 **Command** 類別實作，請參閱 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889) (SQL Server Reporting Services 產品範例)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../reporting-services-extensions.md)   
 [實作資料處理延伸模組](implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
