---
title: SetNumericalValue 方法 (ServerNetworkProtocolProperty 類別) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetNumericalValue Method (ServerNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetNumericalValue method
ms.assetid: b3b4bce8-9d9e-4ccb-a223-0454281353b0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f5a4b8d6819dae11abe4cc097f0e423c23d909e0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595856"
---
# <a name="setnumericalvalue-method-servernetworkprotocolproperty-class"></a>SetNumericalValue 方法 (ServerNetworkProtocolProperty 類別)
  設定參考之屬性的數值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SetNumericalValue(  
NumValue  
)  
  
```  
  
## <a name="parts"></a>組件  
 *object*  
 [ServerNetworkProtocolProperty 類別] ServerNetworkProtocolProperty-class.md) 物件，代表實例上網路通訊協定的屬性 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*Numvalue 個*|指定目前屬性之新值的 `uint32` 值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 `uint32` 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
