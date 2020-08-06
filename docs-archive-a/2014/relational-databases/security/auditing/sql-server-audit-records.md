---
title: SQL Server 稽核記錄 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- audit records [SQL Server]
ms.assetid: 7a291015-df15-44fe-8d53-c6d90a157118
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 19e9ba9013d592d752189adadfb761f1741fd91a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592573"
---
# <a name="sql-server-audit-records"></a>SQL Server Audit 記錄
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit 功能可讓您稽核伺服器層級和資料庫層級的事件群組和事件。 如需詳細資訊，請參閱 [SQL Server Audit &#40;Database Engine&#41;](sql-server-audit-database-engine.md)。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 稽核是由零或多個稽核動作項目所組成，這些項目會記錄到稽核 *「目標」* (Target)。 稽核目標可以是二進位檔案、Windows 應用程式事件記錄檔或 Windows 安全性事件記錄檔。 傳送給目標的記錄包含下表所述的元素。  
  
|資料行名稱|描述|類型|永遠可使用|  
|-----------------|-----------------|----------|----------------------|  
|**event_time**|可稽核的動作引發時的日期/時間。|`datetime2`|是|  
|**sequence_no**|追蹤單一稽核記錄中太長而無法納入稽核寫入緩衝區內的記錄順序。|`int`|是|  
|**action_id**|動作的識別碼<br /><br /> 提示：若要使用 **action_id** 作為述詞，您必須將它從字元字串轉換為數值。 如需詳細資訊，請參閱 [針對 action_id/class_type 述詞篩選 SQL Server Audit](https://docs.microsoft.com/archive/blogs/sqlsecurity/filter-sql-server-audit-on-action_id-class_type-predicate)。|`varchar(4)`|是|  
|**succeeded**|指示觸發此事件的動作是否成功|`bit`-1 = 成功，0 = 失敗|是|  
|**permission_bitmask**|當適用時，顯示已授與、拒絕或撤銷的權限|`bigint`|否|  
|**is_column_permission**|指出資料行層級權限的旗標|`bit`-1 = True，0 = False|否|  
|**session_id**|事件發生所在之工作階段的識別碼。|`int`|是|  
|**server_principal_id**|動作執行所在之登入環境的識別碼。|`int`|是|  
|**database_principal_id**|動作執行所在之資料庫使用者環境的識別碼。|`int`|否|  
|**object_ 識別碼**|稽核發生所在之實體的主要識別碼。 這包括：<br /><br /> 伺服器物件<br /><br /> 資料庫<br /><br /> 資料庫物件<br /><br /> 結構描述物件|`int`|否|  
|**target_server_principal_id**|套用可稽核之動作的伺服器主體。|`int`|是|  
|**target_database_principal_id**|套用可稽核之動作的資料庫主體。|`int`|否|  
|**class_type**|稽核發生所在之可稽核的實體類型。|`varchar(2)`|是|  
|**session_server_principal_name**|工作階段的伺服器主體。|`sysname`|是|  
|**server_principal_name**|目前的登入。|`sysname`|是|  
|**server_principal_sid**|目前的登入 SID。|`varbinary`|是|  
|**database_principal_name**|目前的使用者。|`sysname`|否|  
|**target_server_principal_name**|動作的目標登入。|`sysname`|否|  
|**target_server_principal_sid**|目標登入的 SID。|`varbinary`|否|  
|**target_database_principal_name**|動作的目標使用者。|`sysname`|否|  
|**server_instance_name**|稽核發生所在的伺服器執行個體名稱。 使用標準的 machine\instance 格式。|`nvarchar(120)`|是|  
|**database_name**|動作發生所在的資料庫環境。|`sysname`|否|  
|**schema_name**|動作發生所在的結構描述環境。|`sysname`|否|  
|**object_name**|稽核發生所在之實體的名稱。 這包括：<br /><br /> 伺服器物件<br /><br /> 資料庫<br /><br /> 資料庫物件<br /><br /> 結構描述物件<br /><br /> TSQL 陳述式 (如果有的話)|`sysname`|否|  
|**陳述式**|TSQL 陳述式 (如果有的話)|`nvarchar(4000)`|否|  
|**additional_information**|有關儲存為 XML 之事件的任何其他資訊。|`nvarchar(4000)`|否|  
  
## <a name="remarks"></a>備註  
 某些動作不會填入資料行的值，因為它可能不適用於此動作。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit 會將字元欄位的 4000 個字元資料儲存在稽核記錄中。 當從可稽核的動作傳回的 **additional_information** 和 **statement** 值傳回 4000 個以上的字元時， **sequence_no** 資料行會用來將多筆記錄寫入單一稽核動作的稽核報表中，以記錄這些資料。 此程序如下：  
  
-   **statement** 資料行分成 4000 個字元。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit 會寫成具有部分資料之稽核記錄的第一個資料列。 所有其他欄位會在每一個資料列中重複。  
  
-   **sequence_no** 值會遞增。  
  
-   重複執行此程序，直到記錄所有資料為止。  
  
 您可以使用 **sequence_no** 值、 **event_Time**、 **action_id** 和 **session_id** 資料行按順序讀取資料列來識別此動作，以便連接資料。  
  
## <a name="related-content"></a>相關內容  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-transact-sql)  
  
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-audit-specification-transact-sql)  
  
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-audit-transact-sql)  
  
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-specification-transact-sql)  
  
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-audit-transact-sql)  
  
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-audit-specification-transact-sql)  
  
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-audit-specification-transact-sql)  
  
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-audit-specification-transact-sql)  
  
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-encryption-key-transact-sql)  
  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-authorization-transact-sql)  
  
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)  
  
 [sys.server_audits &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audits-transact-sql)  
  
 [sys.server_file_audits &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-file-audits-transact-sql)  
  
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql)  
  
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql)  
  
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql)  
  
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql)  
  
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql)  
  
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql)  
  
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql)  
  
  
