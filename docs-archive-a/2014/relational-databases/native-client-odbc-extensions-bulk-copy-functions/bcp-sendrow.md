---
title: bcp_sendrow |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_sendrow
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
author: rothja
ms.author: jroth
ms.openlocfilehash: 3d2f55486ba57101ffc7b1903de5d19ac8eaaca2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594048"
---
# <a name="bcp_sendrow"></a>bcp_sendrow
  將程式變數中的資料列傳送給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
## <a name="returns"></a>傳回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 **Bcp_sendrow**函式會從程式變數建立資料列，並將它傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 呼叫**bcp_sendrow**之前，您必須先呼叫[bcp_bind](bcp-bind.md) ，以指定包含資料列資料的程式變數。  
  
 如果呼叫**bcp_bind**指定長的可變長度資料類型（例如，SQLTEXT 的*eDataType*參數和非 null *pData*參數），則**bcp_sendrow**會傳送 entiredata 值，就如同任何其他資料類型一樣。 不過，如果**bcp_bind**具有 Null *pData*參數， **bcp_sendrow**將控制權傳回給應用程式，並在所有具有指定資料的資料行都傳送至之後立即傳回控制項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 然後，應用程式就可以重複呼叫[bcp_moretext](bcp-moretext.md) ，將長的可變長度資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一次傳送給一個區塊。 如需詳細資訊，請參閱[bcp_moretext](bcp-moretext.md)。  
  
 當**bcp_sendrow**用來將程式變數中的資料列大量複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表時，只有當使用者呼叫[bcp_batch](bcp-batch.md)或[bcp_done](bcp-done.md)時，才會認可資料列。 使用者可以選擇在每個*n*個數據列或在傳入資料的期間牢靠時，呼叫**bcp_batch**一次。 如果永遠不會呼叫**bcp_batch** ，則會在呼叫**bcp_done**時認可資料列。  
  
 如需從開始大量複製的重大變更相關資訊 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ，請參閱[&#40;ODBC&#41;執行大量複製作業](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
