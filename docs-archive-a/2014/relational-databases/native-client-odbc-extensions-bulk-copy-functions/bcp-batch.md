---
title: bcp_batch |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_batch
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_batch function
ms.assetid: 0bda489e-86bc-4a7e-80f6-96047e03f281
author: rothja
ms.author: jroth
ms.openlocfilehash: 24cdf6e2934c2b80a55d8fa1fcc572a976b636ee
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595939"
---
# <a name="bcp_batch"></a>bcp_batch
  認可先前從程式變數大量複製並由 bcp_sendrow 傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的[bcp_sendrow](bcp-sendrow.md)所有資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
DBINT bcp_batch (HDBC  
hdbc  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
## <a name="returns"></a>傳回  
 最後一次呼叫**bcp_batch**之後所儲存的資料列數，如果發生錯誤，則為-1。  
  
## <a name="remarks"></a>備註  
 大量複製批次會定義交易。 當應用程式使用[bcp_bind](bcp-bind.md)和**bcp_sendrow**將程式變數中的資料列大量複製到 SQL Server 資料表時，只有在程式呼叫**bcp_batch**或[bcp_done](bcp-done.md)時，才會認可這些資料列。  
  
 您可以**bcp_batch**每*n*個數據列，或在傳入資料中有牢靠時， (與遙測應用程式) 。 如果應用程式不會呼叫**bcp_batch**只有在呼叫**bcp_done**時，才會認可大量複製的資料列。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
