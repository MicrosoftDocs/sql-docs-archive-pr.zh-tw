---
title: ADO 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], ADO
- connection managers [Integration Services], ADO
- ADO connection manager [Integration Services]
ms.assetid: 490418bc-5ef1-41b8-a9c8-de38aa96e0f6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fb4b667733f81eebbaf2b6a2ab9b205c09fe2c66
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599148"
---
# <a name="ado-connection-manager"></a>ADO 連接管理員
  ADO 連接管理員可讓封裝連接到 ActiveX Data Objects (ADO) 物件，例如資料錄集。 這個連接管理員一般用在以舊版語言 (例如 Microsoft Visual Basic 6.0) 所撰寫的自訂工作中，或用於做為使用 ADO 連接到資料來源之現有應用程式一部份的自訂工作中。  
  
 當您將 ADO 連線管理員加入封裝時， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立在執行時間解析為 ADO 連接的連線管理員、設定連線管理員屬性，並將連線管理員加入 `Connections` 封裝上的集合。 連接管理員的 `ConnectionManagerType` 屬性會設為 `ADO`。  
  
## <a name="troubleshooting-the-ado-connection-manager"></a>疑難排解 ADO 連接管理員  
 由 ADO 連接管理員讀取時，某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期資料類型會產生如下表所示結果。  
  
|SQL Server 資料類型|結果|  
|--------------------------|------------|  
|`time`, `datetimeoffset`|除非封裝使用參數化 SQL 命令，否則封裝會失敗。 若要使用參數化 SQL 命令，請在封裝中使用「執行 SQL 工作」。 如需詳細資訊，請參閱 [執行 SQL 工作](../control-flow/execute-sql-task.md) 和 [執行 SQL 工作中的參數和傳回碼](../parameters-and-return-codes-in-the-execute-sql-task.md)。|  
|`datetime2`|ADO 連接管理員會截斷毫秒值。|  
  
> [!NOTE]  
>  如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型以及如何將其對應到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型的詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) 和 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。  
  
## <a name="configuring-the-ado-connection-manager"></a>設定 ADO 連接管理員  
 您可以利用下列方式設定 ADO 連接管理員：  
  
-   提供設定的特定連接字串，以符合所選取提供者的需求。  
  
-   視提供者而定，包含要連接的資料來源名稱。  
  
-   為所選的提供者提供適當的安全性認證。  
  
-   指示是否在執行階段保留從連接管理員建立的連接。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列主題：  
  
-   [設定 OLE DB 連線管理員](ole-db-connection-manager.md)  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連接](integration-services-ssis-connections.md)  
  
  
