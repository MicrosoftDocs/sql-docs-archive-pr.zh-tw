---
title: srv_setutype (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_setutype
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_setutype
ms.assetid: 6160f15d-1b68-411e-ab6d-491ec288f264
author: rothja
ms.author: jroth
ms.openlocfilehash: e9e02605995e44f5869633d5e8778a955236005f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707565"
---
# <a name="srv_setutype-extended-stored-procedure-api"></a>srv_setutype (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 針對資料列中的資料行設定使用者定義資料類型。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_setutype (  
SRV_PROC *  
srvproc  
,  
int   
column  
,   
DBINT  
user_type   
);  
  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼。 擴充預存程序 API 程式庫會使用該結構所包含的資訊來管理應用程式與用戶端之間的通訊和資料。  
  
 *column*  
 指出要設定的資料行。 資料行的編號會從 1 開始。  
  
 *user_type*  
 指定使用者定義資料類型程式碼。  
  
## <a name="returns"></a>傳回  
 SUCCEED 或 FAIL。 如果此資料行不存在，則會傳回 FAIL。  
  
## <a name="remarks"></a>備註  
 一個資料行有兩個資料類型：其實際資料類型與其使用者定義資料類型。 使用者定義資料類型是由用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來儲存資料行的實際使用者定義資料類型（如果有的話）以及資料行描述資訊，例如資料行的 null 屬性和可更新性。  
  
 利用 **srv_describe** 定義 *column* 時，以及最後一個資料列送出之前，可以呼叫 **srv_setutype** 函式。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_describe &#40;擴充預存程序 API&#41;](srv-describe-extended-stored-procedure-api.md)  
  
  
