---
title: ErrorControl 屬性 (SqlService 類別) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ErrorControl Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ErrorControl property
ms.assetid: cbb1e0fa-5bfc-4b1b-a6ed-f7d5cfad4d73
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 73c726af514f2880484cf927282fc0e007f07e2c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706313"
---
# <a name="errorcontrol-property-sqlservice-class"></a>ErrorControl 屬性 (SqlService 類別)
  當服務在啟動期間無法啟動時，取得或設定錯誤的嚴重性。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.ErrorControl [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 字串值，可指定當服務在啟動期間失敗時所報告的錯誤嚴重性。 下表顯示可能的值。  
  
 忽略  
 不通知使用者。  
  
 正常  
 通知使用者。  
  
 Severe  
 使用上次的正確組態重新啟動系統。  
  
 重要  
 系統嘗試以正確的組態重新啟動。  
  
 Unknown  
 嚴重性未知。  
  
## <a name="remarks"></a>備註  
 此值表示在發生失敗時由啟動程式採取的動作。 電腦系統會記錄所有錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
