---
title: MSSQLSERVER_3271 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3271 (Database Engine error)
ms.assetid: 21b8de4b-6624-4163-9561-1a6cc8fe3d51
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 56bdb5875dbba3fbe5037a308d713170a9b6f9ea
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595064"
---
# <a name="mssqlserver_3271"></a>MSSQLSERVER_3271
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|3271|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DMPIO_IO_ERROR|  
|訊息文字|檔案 "%ls:" %ls 上發生無法復原的 I/O 錯誤。|  
  
## <a name="explanation"></a>說明  
 這是作業系統在備份或還原作業期間執行 I/O 時引發錯誤時所發生的一般錯誤。 大部分情況下，造成這項錯誤的原因純粹因為備份媒體已滿。  
  
 此錯誤可能包括作業系統指出磁碟已滿的其他文字。 以協力廠商軟體執行備份或還原作業時，可能會出現另一則訊息，指出備份已經失敗。 這則訊息看起來可能與下列文字類似：  
  
```  
"2005-08-02 16:05:16.04 spid55 Error: 18210, Severity: 16, State: 1.  
 2005-08-02 16:05:16.04 spid55 BackupVirtualDeviceFile  
::RequestDurableMedia: Flush failure on backup device 'VDINULL'.   
Operating system error 995(The I/O operation has been aborted because   
of either a thread exit or an application request.)."  
```  
  
 這則訊息代表備份軟體要求您結束備份或還原作業。  
  
## <a name="user-action"></a>使用者動作  
 依照需要執行下列工作：  
  
-   檢閱這則訊息之前的基本系統錯誤訊息和 SQL Server 錯誤訊息，找出失敗的原因。  
  
-   確定備份和還原媒體具有足夠的空間。  
  
-   更正協力廠商備份和還原軟體引發的任何錯誤。  
  
  
