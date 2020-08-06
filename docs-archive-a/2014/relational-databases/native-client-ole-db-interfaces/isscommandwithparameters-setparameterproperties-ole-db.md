---
title: ISSCommandWithParameters::SetParameterProperties (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- SetParameterProperties method
ms.assetid: 4cd0281a-a2a0-43df-8e46-eb478b64cb4b
author: rothja
ms.author: jroth
ms.openlocfilehash: 4bf8e5cde9885a5d9b55d84c6384b76aecf50b8a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687837"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
  依照序數根據每個參數來設定參數的屬性，或指定 SSPARAMPROPS 結構的陣列來設定大量參數屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT SetParameterProperties(  
DB_UPARAMS cParams,   
SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>引數  
 *cParams*[in]  
 *rgParamProperties* 陣列中 SSPARAMPROPS 結構的數目。 如果此數位為零， `ISSCommandWithParameters::SetParameterProperties` 將會刪除命令中所有參數可能已指定的所有屬性。  
  
 *rgParamProperties*[in]  
 要設定的 SSPARAMPROPS 結構的陣列。  
  
## <a name="return-code-values"></a>傳回碼值  
 方法會傳回與 `ISSCommandWithParameters::SetParameterProperties` core OLE DB **ICommandProperties：： SetProperties**方法相同的錯誤碼。  
  
## <a name="remarks"></a>備註  
 使用此方法來設定參數屬性時，會依序數，或在 `ISSCommandWithParameters::SetParameterProperties` 從屬性陣列建立 SSPARAMPROPS 之後，以單一呼叫的方式來進行。  
  
 呼叫方法之前，必須先呼叫**SetParameterInfo**方法 `ISSCommandWithParameters::SetParameterProperties` 。 呼叫 `SetParameterProperties(0, NULL)` 會清除所有指定的參數屬性，呼叫 `SetParameterInfo(0,NULL,NULL)` 則會清除所有的參數資訊，包括任何可能與參數相關聯的屬性。  
  
 呼叫 `ISSCommandWithParameters::SetParameterProperties` 以指定不屬於類型 DBTYPE_XML 或 DBTYPE_UDT 的參數屬性會傳回 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED，並將該參數包含在 SSPARAMPROPS 中所有標示出 dbprop 的*dwStatus*欄位標記為 DBPROPSTATUS_NOTSET。 系統會周遊 SSPARAMPROPS 中包含的每個 DBPROPSET 的 DBPROP 陣列，以偵測 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED 所參考的是哪一個參數。  
  
 如果 `ISSCommandWithParameters::SetParameterProperties` 呼叫以指定尚未使用**SetParameterInfo**設定參數資訊的參數屬性，則提供者會傳回 E_UNEXPECTED，並顯示下列錯誤訊息：  
  
 必須先針對指定的參數呼叫 SetParameterInfo 方法，然後才能呼叫 SetParameterProperties 方法。 而在設定參數屬性之前，也必須先設定參數資訊。  
  
 如果呼叫 `ISSCommandWithParameters::SetParameterProperties` 包含已設定參數資訊的某些參數，而且尚未設定參數資訊的某些參數，則 SSPARAMPROPS 屬性集之 DBPROPSET 中的 dwStatus 屬性將會傳回 DBSTATUS_NOTSET。  
  
 SSPARAMPROPS 結構定義如下：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始，資料庫引擎的改進功能就允許 ISSCommandWithParameters::SetParameterProperties 針對預期的結果取得更精確的描述。 這些更精確的結果可能會與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中 ISSCommandWithParameters::SetParameterProperties 所傳回的值不同。 如需詳細資訊，請參閱[中繼資料探索](../native-client/features/metadata-discovery.md)。  
  
|成員|描述|  
|------------|-----------------|  
|*iOrdinal*|所傳遞參數的序數。|  
|*cPropertySets*|*rgPropertySets* 中的 DBPROPSET 結構數目。|  
|*rgPropertySets*|藉其傳回 DBPROPSET 結構陣列的記憶體指標。|  
  
## <a name="see-also"></a>另請參閱  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
