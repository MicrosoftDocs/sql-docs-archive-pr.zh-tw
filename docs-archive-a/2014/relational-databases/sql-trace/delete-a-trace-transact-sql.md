---
title: 刪除追蹤 (Transact-SQL) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], deleting
- removing traces
- deleting traces
ms.assetid: a5502814-b281-42dd-b885-5c9368025ae6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b3551cff36ef6e2c2e9cc6a4d9b7056ae44cb950
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596607"
---
# <a name="delete-a-trace-transact-sql"></a>刪除追蹤 (Transact-SQL)
  本主題說明如何使用預存程序來刪除追蹤。  
  
 如需使用追蹤預存程序的範例，請參閱[建立追蹤 &#40;Transact-SQL&#41;](create-a-trace-transact-sql.md)。  
  
### <a name="to-delete-a-trace"></a>若要刪除追蹤  
  
1.  指定 **@status = 0**，執行 **sp_trace_setstatus** 以停止追蹤。  
  
2.  指定 **@status = 2**，執行 **sp_trace_setstatus** 以關閉追蹤，並將其資訊從伺服器中刪除。  
  
> [!NOTE]  
>  您必須先關閉追蹤，才能將它刪除。  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [系統預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [SQL Server Profiler 預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
