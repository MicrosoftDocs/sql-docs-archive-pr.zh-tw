---
title: SQL Server Express LocalDB 標頭和版本資訊 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_location:
- sqluserinstance.dll
ms.assetid: 506b5161-b902-4894-b87b-9192d7b1664a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 138081852cf505b03265fd9c5f39eae6ed2af39b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606326"
---
# <a name="sql-server-express-localdb-header-and-version-information"></a>SQL Server Express LocalDB 標頭和版本資訊
  SQL Server Express LocalDB 執行個體 API 沒有個別的標頭檔；LocalDB 函數簽章和錯誤碼會定義在 SQL Server Native Client 標頭檔 (sqlncli.h) 中。 若要使用 LocalDB 執行個體 API，您必須在專案中包含 sqlncli.h 標頭檔。  
  
## <a name="localdb-versioning"></a>LocalDB 版本設定  
 LocalDB 安裝針對每個主要 SQL Server 版本使用一組二進位檔。 這些 LocalDB 版本會個別進行維護及修補。 這表示使用者必須指定所要使用的 LocalDB 基準版本 (亦即主要 SQL Server 版本)。 版本是以 .NET Framework **system.web**類別所定義的標準版本格式來指定：  
  
 *major.minor[.build[.revision]]*  
  
 版本字串中的前兩個數字 (*主要*和*次要*) 是強制性的。 版本字串中的最後兩個數字 (*組建*和*修訂*) 是選擇性的，而且如果使用者離開，則預設為零。這表示如果使用者僅指定 "12.2" 做為 LocalDB 版本號碼，則會將其視為使用者指定 "12.2.0.0"。  
  
 例如，LocalDB 安裝的版本定義於 MSSQLServer\CurrentVersion 登錄機碼中的 SQL Server 執行個體登錄機碼底下，例如：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL12E.LOCALDB\ MSSQLServer\CurrentVersion: "CurrentVersion"="12.0.2531.0"  
```  
  
 支援在相同的工作站上並存多個 LocalDB 版本。 不過，使用者程式碼一律會使用本機電腦上最新可用的**Sqluserinstance.dll** DLL 來連接到 LocalDB 實例。  
  
## <a name="locating-the-sqluserinstance-dll"></a>尋找 SQLUserInstance DLL  
 為了找出**Sqluserinstance.dll** DLL，用戶端提供者會使用下列登錄機碼：  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions]  
```  
  
 在此機碼下會列出機碼清單，其中每個機碼各代表電腦上已安裝的每個 LocalDB 版本。 這些索引鍵的每一個都是以格式的 LocalDB 版本號碼來命名 *\<major-version>* 。*\<minor-version>* 例如， (的索引鍵 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 名稱為 12.0) 。 在每個版本機碼下會列出 `InstanceAPIPath` 名稱/值組，定義隨該版本安裝之 SQLUserInstance.dll 檔案的完整路徑。 下列範例顯示安裝 LocalDB 11.0 和 12.0 版之電腦的登錄項目：  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"]  
```  
  
 用戶端提供者必須在所有已安裝的版本之間尋找最新版本，並從相關聯的值載入**Sqluserinstance.dll** DLL 檔案 `InstanceAPIPath` 。  
  
### <a name="wow64-mode-on-64-bit-windows"></a>64 位元 Windows 上的 WOW64 模式  
 LocalDB 的 64 位元安裝包含一組額外的登錄機碼，可讓在 Windows-32-on-Windows-64 (WOW64) 模式下執行的 32 位元應用程式使用 LocalDB。 具體而言，在 64 位元 Windows 上，LocalDB MSI 會建立下列登錄機碼：  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"]  
  
```  
  
 64-讀取金鑰的程式 `Installed Versions` 會看到指向64位版本的**sqluserinstance.dll** DLL 的值，而32位程式 (在 WOW64 模式的64位 Windows 上執行) 會自動重新導向至位於 hive 底下的機 `Installed Versions` 碼 `Wow6432Node` 。 此機碼包含指向32位版本之**Sqluserinstance.dll** DLL 的值。  
  
## <a name="using-localdb_define_proxy_functions"></a>使用 LOCALDB_DEFINE_PROXY_FUNCTIONS  
 LocalDB 實例 API 會定義名為 LOCALDB_DEFINE_PROXY_FUNCTIONS 的常數，以自動探索和載入**Sqluserinstance.dll** DLL。  
  
 此常數啟用的程式碼區段可實作每個 LocalDB API 的 Proxy。 Proxy 執行會使用通用函式系結至最新安裝的**Sqluserinstance.dll** DLL 中的進入點，然後轉送要求。  
  
 只有在包含 sqlncli.h 檔案之前，使用者程式碼中已定義常數 LOCALDB_DEFINE_PROXY_FUNCTIONS，才會啟用 Proxy 函數。 此常數應該僅定義於一個來源模組 (.cpp 檔) 中，因為該模組會為所有 API 進入點定義外部函數名稱。 此常數可以實作每個 LocalDB API 的 Proxy。  
  
 下列程式碼範例顯示如何透過原生 C++ 程式碼使用巨集：  
  
```  
// Define the LOCALDB_DEFINE_PROXY_FUNCTIONS constant to enable the LocalDB proxy functions   
// The #define has to take place BEFORE the API header file (sqlncli.h) is included  
#define LOCALDB_DEFINE_PROXY_FUNCTIONS  
#include <sqlncli.h>  
...  
HRESULT hr = S_OK;  
  
// Create LocalDB instance by calling the create API proxy function included by macro  
if (FAILED(hr = LocalDBCreateInstance( L"12.0", L"name", 0)))  
{  
...  
}  
...  
  
```  
  
  
