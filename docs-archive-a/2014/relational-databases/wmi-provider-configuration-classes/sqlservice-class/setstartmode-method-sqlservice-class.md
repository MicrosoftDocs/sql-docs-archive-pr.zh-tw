---
title: SetStartMode 方法 (SqlService 類別) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetStartMode Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetStartMode method
ms.assetid: f6f198b4-f9a4-468c-8977-76462ef06e61
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a9b7310623f526d7b106485ed9681df3aa100129
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585197"
---
# <a name="setstartmode-method-sqlservice-class"></a>SetStartMode 方法 (SqlService 類別)
  修改服務執行個體的啟動模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SetStartMode(  
StartMode  
)  
  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](sqlservice-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
 *StartMode*  
 指定服務執行個體之啟動模式的 `uint32` 值。  
  
 有效值如下：  
  
 值 = 0。 Boot - 由作業系統載入程式啟動的裝置驅動程式。 這個值只適用於驅動程式服務。  
  
 值 = 1。 System - 由 `IoInitSystem` 方法啟動的裝置驅動程式。 這個值只適用於驅動程式服務。  
  
 值 = 2。 Automatic - 要由服務控制管理員在系統啟動期間自動啟動的服務。  
  
 值 = 3。 Manual - 在處理序呼叫 `StartService` 方法時要由電腦管理員啟動的服務。  
  
 值 = 4。 Disabled - 無法再啟動服務。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 `uint32` 值，如果已成功修改此服務為 0，如果不支援要求則為 1。 任何其他數字表示發生錯誤。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
