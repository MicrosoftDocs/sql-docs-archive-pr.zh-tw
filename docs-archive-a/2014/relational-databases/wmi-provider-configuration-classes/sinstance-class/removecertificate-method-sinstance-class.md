---
title: RemoveCertificate 方法 (SInstance 類別) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- RemoveCertificate Method (SInstance Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- RemoveCertificate method
ms.assetid: 7e5dbafa-a634-4617-9622-510514fce0ce
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4b876cd75778d1da9c9a46f65f39b915ebee0552
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687634"
---
# <a name="removecertificate-method-sinstance-class"></a>RemoveCertificate 方法 (SInstance 類別)
  從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體中移除目前的安全性憑證。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.RemoveCertificate()  
  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表 [執行個體上之伺服器設定的](sinstance-class.md) SInstance 類別 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 uint32 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
