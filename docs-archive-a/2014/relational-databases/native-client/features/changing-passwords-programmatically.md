---
title: 以程式設計方式變更密碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], password expiration
- SQL Server Native Client ODBC driver, passwords
- SQL Server Native Client OLE DB provider, passwords
- passwords [SQL Server], expiration
- SQLNCLI, password expiration
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- expired passwords [SQL Server Native Client]
- SQL Server Native Client, password expiration
- modifying passwords
ms.assetid: 624ad949-5fed-4ce5-b319-878549f9487b
author: rothja
ms.author: jroth
ms.openlocfilehash: 86085f8ba7c54cfcab1a3c7f6e8ade30ecf9d0da
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87698104"
---
# <a name="changing-passwords-programmatically"></a>以程式設計方式變更密碼
  在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 之前，當使用者密碼到期時，只有系統管理員可以重設密碼。 從開始 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client 支援透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client OLE DB 提供者和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client ODBC 驅動程式，以及透過變更**SQL Server 登**入對話方塊，以程式設計方式處理密碼到期。  
  
> [!NOTE]  
>  如果可能的話，請在執行階段提示使用者輸入其認證，並避免以保存的格式儲存其認證。 如果您必須保存其認證，則應該用 [Win32 crypto API](https://go.microsoft.com/fwlink/?LinkId=64532) 加密這些認證。 如需使用密碼的詳細資訊，請參閱[強式密碼](../../security/strong-passwords.md)。  
  
## <a name="sql-server-login-error-codes"></a>SQL Server 登入錯誤碼  
 當連接因為驗證問題而無法建立時，將會提供下列其中一個 SQL Server 錯誤碼給應用程式來協助診斷和復原。  
  
|SQL Server 錯誤碼|錯誤訊息|  
|---------------------------|-------------------|  
|15113|使用者 '%.*ls' 登入失敗。原因: 密碼驗證失敗。 帳戶已經鎖定。|  
|18463|使用者 '%.*ls' 的登入失敗。 原因: 密碼變更失敗。 密碼此時不適用。|  
|18464|使用者 '%.*ls' 的登入失敗。 原因: 密碼變更失敗。 因為密碼太短而不符合原則需求。|  
|18465|使用者 '%.*ls' 的登入失敗。 原因: 密碼變更失敗。 因為密碼太長而不符合原則需求。|  
|18466|使用者 '%.*ls' 的登入失敗。 原因: 密碼變更失敗。 因為密碼不夠複雜而不符合原則需求。|  
|18467|使用者 '%.*ls' 的登入失敗。 原因: 密碼變更失敗。 密碼不符合密碼篩選 DLL 的需求。|  
|18468|使用者 '%.*ls' 的登入失敗。 原因: 密碼變更失敗。 密碼驗證期間發生意外的錯誤。|  
|18487|使用者 '%.*ls' 的登入失敗。 原因: 帳戶的密碼已過期。|  
|18488|使用者 '%.*ls' 的登入失敗。 原因: 必須變更帳戶的密碼。|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 提供者  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者透過使用者介面和以程式設計方式支援密碼到期。  
  
### <a name="ole-db-user-interface-password-expiration"></a>OLE DB 使用者介面密碼逾期  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者透過對**SQL Server 登**入對話方塊所做的變更，支援密碼到期。 如果 DBPROP_INIT_PROMPT 的值設定為 DBPROMPT_NOPROMPT，則密碼到期時，初始連接嘗試將會失敗。  
  
 如果 DBPROP_INIT_PROMPT 已設定為其他任何值，不管密碼是否到期，使用者都會看到 [SQL Server 登入]**** 對話方塊。 使用者可以按一下 [選項]**** 按鈕，然後核取 [變更密碼]**** 來變更密碼。  
  
 如果使用者按一下 [確定]，而且密碼已到期，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 就會使用 [變更 SQL Server 密碼]**** 對話方塊提示使用者輸入並確認新密碼。  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>OLE DB 提示行為與鎖定帳戶  
 連接嘗試可能會因為帳戶遭到鎖定而失敗。 如果在顯示 [SQL Server 登入]**** 對話方塊後發生這個狀況，就會向使用者顯示伺服器錯誤訊息，並中止連接嘗試。 如果使用者輸入錯誤的舊密碼值，也可能在顯示 [變更 SQL Server 密碼]**** 對話方塊後發生這個狀況。 在此情況下，會顯示相同的錯誤訊息，並中止連接嘗試。  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>OLE DB 連接共用、密碼逾期與鎖定帳戶  
 當連接在連接共用中仍處於作用中狀態時，帳戶可能會遭到鎖定，或者其密碼可能會過期。 伺服器會在兩種時機下檢查過期的密碼與鎖定的帳戶。 第一個時機是首次建立連接時。 第二個時機則是在連接取自集區而重設連接時。  
  
 當重設嘗試失敗後，連接便會從集區移除並傳回錯誤。  
  
### <a name="ole-db-programmatic-password-expiration"></a>OLE DB 程式設計密碼逾期  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者透過新增 SSPROP_AUTH_OLD_PASSWORD (類型 VT_BSTR) 屬性（已加入 DBPROPSET_SQLSERVERDBINIT 屬性集）來支援密碼到期。  
  
 現有的 "Password" 屬性會參考 DBPROP_AUTH_PASSWORD，並用於儲存新的密碼。  
  
> [!NOTE]  
>  在此連接字串中，"Old Password" 屬性會設定 SSPROP_AUTH_OLD_PASSWORD，這是無法透過提供者字串屬性取得的目前密碼 (可能已過期)。  
  
 提供者不會保存此屬性的值。 設定此屬性時，提供者不會將連接共用用於第一個連接，因為將會產生新的連接。 如果密碼變更成功，則無法重複使用目前的連接，因為該連接仍然包含舊密碼，而這個密碼將在密碼變更後變成無效。 同時，如果登入成功，提供者會清除這個屬性。 後續嘗試擷取舊密碼時，便會傳回 VT_EMPTY。  
  
> [!NOTE]  
>  系統絕不會保存 SSPROP_AUTH_OLD_PASSWORD，因為只有在密碼到期時才會使用它。  
  
 請注意，每當設定 "Old Password" 屬性時，除非同時指定優先順序永遠最高的 Windows 驗證，否則提供者會假設有嘗試變更密碼。  
  
 如果使用 Windows 驗證，指定舊密碼會導致 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED，這取決於舊密碼是否分別指定為 REQUIRED 或 OPTIONAL，以及 *dwStatus* 中是否傳回 DBPROPSTATUS_CONFLICTINGBADVALUE 的狀態值而定。 在呼叫 **IDBInitialize::Initialize** 時，會偵測到這個狀況。  
  
 如果嘗試變更密碼時意外失敗，伺服器會傳回錯誤碼 18468。 標準 OLEDB 錯誤會從連線嘗試傳回。  
  
 如需 DBPROPSET_SQLSERVERDBINIT 屬性集的詳細資訊，請參閱[初始化和授權屬性](../../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驅動程式  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者透過使用者介面和以程式設計方式支援密碼到期。  
  
### <a name="odbc-user-interface-password-expiration"></a>ODBC 使用者介面密碼逾期  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式可透過對**SQL Server 登**入對話方塊所做的變更，來支援密碼到期。  
  
 如果呼叫[SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md) ，且**DriverCompletion**的值設定為 SQL_DRIVER_NOPROMPT，則如果密碼已過期，則初始連接嘗試會失敗。 後續呼叫**SQLError**或**SQLGetDiagRec**時，會傳回 SQLSTATE 值28000和原生錯誤碼值18487。  
  
 如果**DriverCompletion**已設定為任何其他值，不論密碼是否已過期，使用者都會看到 [ **SQL Server 登**入] 對話方塊。 使用者可以按一下 [選項]**** 按鈕，然後核取 [變更密碼]**** 來變更密碼。  
  
 如果使用者按一下 [確定]，而且密碼已過期，則 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會使用 [**變更 SQL Server 密碼**] 對話方塊提示輸入並確認新密碼。  
  
#### <a name="odbc-prompt-behavior-and-locked-accounts"></a>ODBC 提示行為與鎖定帳戶  
 連接嘗試可能會因為帳戶遭到鎖定而失敗。 如果在顯示 [SQL Server 登入]**** 對話方塊後發生這個狀況，就會向使用者顯示伺服器錯誤訊息，並中止連接嘗試。 如果使用者輸入錯誤的舊密碼值，也可能在顯示 [變更 SQL Server 密碼]**** 對話方塊後發生這個狀況。 在此情況下，會顯示相同的錯誤訊息，並中止連接嘗試。  
  
#### <a name="odbc-connection-pooling-password-expiry-and-locked-accounts"></a>ODBC 連接共用、密碼逾期與鎖定帳戶  
 當連接在連接共用中仍處於作用中狀態時，帳戶可能會遭到鎖定，或者其密碼可能會過期。 伺服器會在兩種時機下檢查過期的密碼與鎖定的帳戶。 第一個時機是首次建立連接時。 第二個時機則是在連接取自集區而重設連接時。  
  
 當重設嘗試失敗後，連接便會從集區移除並傳回錯誤。  
  
### <a name="odbc-programmatic-password-expiration"></a>ODBC 程式設計密碼逾期  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式透過加入 SQL_COPT_SS_OLDPWD 屬性（在使用[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)函數連接到伺服器之前設定）來支援密碼到期。  
  
 連接控制代碼的 SQL_COPT_SS_OLDPWD 屬性指的是過期的密碼。 此屬性沒有任何連接字串屬性，因為這會干擾連接共用。 如果登入成功，驅動程式會清除這個屬性。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式會在這項功能的四個案例中傳回 SQL_ERROR：密碼到期、密碼原則衝突、帳戶鎖定，以及使用 Windows 驗證時設定舊密碼屬性的時間。 叫用[SQLGetDiagField](../../native-client-odbc-api/sqlgetdiagfield.md)時，驅動程式會將適當的錯誤訊息傳回給使用者。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
