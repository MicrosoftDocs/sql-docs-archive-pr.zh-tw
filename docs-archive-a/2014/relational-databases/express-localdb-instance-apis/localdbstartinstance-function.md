---
title: LocalDBStartInstance 函式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBStartInstance
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: cb325f5d-10ee-4a56-ba28-db0074ab3926
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 748bc373e8b0dbad0a91247e068d21b67f2dbc1a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606327"
---
# <a name="localdbstartinstance-function"></a>LocalDBStartInstance 函數
  啟動指定的 SQL Server Express LocalDB 執行個體。  
  
 **標頭檔：** sqlncli。h  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT LocalDBStartInstance(  
           PCWSTR pInstanceName,  
           DWORD dwFlags,   
           LPWSTR wszSqlConnection,   
           LPDWORD lpcchSqlConnection   
);  
```  
  
## <a name="parameters"></a>參數  
 *pInstanceName*  
 [輸入] 要啟動的 LocalDB 執行個體名稱。  
  
 *dwFlags*  
 [輸入] 保留供日後使用。 目前應設為 0。  
  
 *wszSqlConnection*  
 [輸出] 儲存 LocalDB 執行個體連接字串的緩衝區。  
  
 *lpcchSqlConnection*  
 [輸入/輸出][輸入] 包含*wszSqlConnection*緩衝區的大小（以字元為單位），包括任何尾端的 null。 輸出時，如果指定的緩衝區大小太小，則會包含所需的緩衝區大小 (以字元為單位)，包括尾端的 Null。  
  
## <a name="returns"></a>傳回  
 S_OK  
 此函數已成功。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB 未安裝在電腦上。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 一個或多個指定的輸入參數無效。  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 指定的執行個體名稱無效。  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../express-localdb-error-messages/localdb-error-unknown-instance.md)  
 執行個體不存在。  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 指定的緩衝區*wszSqlConnection*太小。  
  
 [LOCALDB_ERROR_WAIT_TIMEOUT](../express-localdb-error-messages/localdb-error-wait-timeout.md)  
 嘗試取得同步處理鎖定時發生逾時。  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 應儲存執行個體的路徑長度超過 MAX_PATH。  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 無法擷取使用者設定檔資料夾。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 無法存取執行個體資料夾。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 無法存取執行個體登錄。  
  
 [LOCALDB_ERROR_CANNOT_MODIFY_INSTANCE_REGISTRY](../express-localdb-error-messages/localdb-error-cannot-modify-instance-registry.md)  
 無法修改執行個體登錄。  
  
 [LOCALDB_ERROR_CANNOT_CREATE_SQL_PROCESS](../express-localdb-error-messages/localdb-error-cannot-create-sql-process.md)  
 無法建立 SQL Server 處理序。  
  
 [LOCALDB_ERROR_SQL_SERVER_STARTUP_FAILED](../express-localdb-error-messages/localdb-error-sql-server-startup-failed.md)  
 已啟動 SQL Server 處理序，但是 SQL Server 啟動失敗。  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 執行個體組態已損毀。  
  
 [LOCALDB_ERROR_AUTO_INSTANCE_CREATE_FAILED](../express-localdb-error-messages/localdb-error-auto-instance-create-failed.md)  
 無法建立自動執行個體。 請參閱 Windows 應用程式事件記錄檔，以取得錯誤詳細資料。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 發生意外錯誤。 請參閱事件記錄檔，以取得詳細資料。  
  
## <a name="details"></a>詳細資料  
 連接緩衝區引數 (*wszSqlConnection*) 和連接緩衝區大小引數 (*lpcchSqlConnection*) 是選擇性的。 下表顯示使用這些引數的選項及其結果。  
  
|Buffer|緩衝區大小|基本原理|動作|  
|------------|-----------------|---------------|------------|  
|NULL|NULL|使用者想要啟動實例，而不需要管道名稱。|啟動執行個體 (不傳回管道且不傳回所需的緩衝區大小)。|  
|NULL|存在|使用者要求輸出緩衝區大小。 (在下一個呼叫中，使用者可能會要求實際啟動。)|傳回所需的緩衝區大小 (不啟動且不傳回管道)。 結果為 S_OK。|  
|存在|NULL|不允許；輸入不正確。|傳回的結果為 LOCALDB_ERROR_INVALID_PARAMETER。|  
|存在|存在|使用者想要啟動執行個體，且在啟動後，需要管道名稱以連接至此執行個體。|檢查緩衝區大小、啟動執行個體，然後傳回緩衝區中的管道名稱。 <br />緩衝區大小引數會傳回 "server =" 字串的長度，不包括終止的 null。|  
  
 如需使用 LocalDB API 的程式碼範例，請參閱[SQL Server Express Localdb 參考](../sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Express LocalDB 標頭和版本資訊](sql-server-express-localdb-header-and-version-information.md)  
  
  
