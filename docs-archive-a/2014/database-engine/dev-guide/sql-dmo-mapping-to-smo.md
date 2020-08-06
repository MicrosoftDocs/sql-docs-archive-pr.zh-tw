---
title: SQL-DMO 與 SMO 的對應 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: 590f5396-98d5-485e-9b41-728c6ed7cb9d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: f597f64b87f72588af5e982d4e0b8de8a69c3140
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607062"
---
# <a name="sql-dmo-mapping-to-smo"></a>對 SMO 的 SQL-DMO 對應
  SQL Distributed Management Objects (SQL-DMO) 不再包含在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，SQL-DMO 應用程式應該轉換成使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件 (SMO)。 SMO 物件模型與 SQL-DMO 相似，因此大部分 SQL-DMO 物件都是以相同名稱對應到 SMO 中的物件。 不過，部分 SQL-DMO 物件已在轉移至 SMO 的過程中變更或是捨棄。 此表列出建議對未直接轉換成 SMO 的 SQL-DMO 物件採取的動作。  
  
|SQL-DMO 物件|SMO 中的動作|  
|---------------------|-------------------|  
|View2 物件|已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空間。|  
|AlertSystem 物件|已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空間。|  
|Application 物件|已移除。|  
|Backup 物件和 Backup2 物件|<xref:Microsoft.SqlServer.Management.Smo.Backup> 和 <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase> 物件。|  
|BackupDevice 物件|<xref:Microsoft.SqlServer.Management.Smo.BackupDevice> 物件|  
|BulkCopy 物件和 BulkCopy2 物件|已由 <xref:Microsoft.SqlServer.Management.Smo.Transfer> 物件移除並取代。|  
|Category 物件|已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空間。 已由 <xref:Microsoft.SqlServer.Management.Smo.Agent.AlertCategory>、<xref:Microsoft.SqlServer.Management.Smo.Agent.OperatorCategory>、<xref:Microsoft.SqlServer.Management.Smo.Agent.JobCategory> 物件取代。|  
|Check 物件|<xref:Microsoft.SqlServer.Management.Smo.Check> 物件|  
|Column 物件和 Column2 物件|<xref:Microsoft.SqlServer.Management.Smo.Column> 物件|  
|Configuration 物件|<xref:Microsoft.SqlServer.Management.Smo.Configuration> 和 <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase> 物件。|  
|ConfigValue 物件|<xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> 物件|  
|Database 物件和 Database2 物件|<xref:Microsoft.SqlServer.Management.Smo.Database> 物件|  
|DatabaseRole 物件和 DatabaseRole2 物件|<xref:Microsoft.SqlServer.Management.Smo.DatabaseRole> 物件|  
|DBFile 物件|<xref:Microsoft.SqlServer.Management.Smo.DataFile> 物件|  
|DBOption 物件和 DBOption2 物件|已移至 <xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions> 物件。|  
|Default 物件和 Default2 物件|<xref:Microsoft.SqlServer.Management.Smo.Default> 物件|  
|DistributionArticle 物件和 DistributionArticle2 物件|已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|DistributionDatabase 物件和 DistributionDatabase2 物件|已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|DistributionPublication 物件和 DistributionPublication2 物件|已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|DistributionSubscription 物件和 DistributionSubscription2 物件|已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|Distributor 物件和 Distributor2 物件|已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|DRIDefault 物件|已移至 <xref:Microsoft.SqlServer.Management.Smo.ScriptingOptions> 物件。|  
|FileGroup 物件和 FileGroup2 物件|<xref:Microsoft.SqlServer.Management.Smo.FileGroup> 物件|  
|FullTextCatalog 物件和 FullTextCatalog2 物件|<xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> 和 <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex> 物件。|  
|Index 物件和 Index2 物件|<xref:Microsoft.SqlServer.Management.Smo.Index> 物件|  
|IntegratedSecurity 物件|功能已移至 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 命名空間中的 <xref:Microsoft.SqlServer.Management.Common> 物件。|  
|Job 物件|<xref:Microsoft.SqlServer.Management.Smo.Agent.Job> 物件 已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空間。|  
|JobFilter 物件|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobFilter> 物件 已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空間。|  
|JobHistoryFilter 物件|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobHistoryFilter> 物件 已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空間。|  
|JobSchedule 物件|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobSchedule> 物件 已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空間。|  
|JobServer 物件和 JobServer2 物件|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobServer> 物件 已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空間。|  
|JobStep 物件|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobStep> 物件 已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空間。|  
|Key 物件|<xref:Microsoft.SqlServer.Management.Smo.ForeignKey> 和 <xref:Microsoft.SqlServer.Management.Smo.Index> 物件。|  
|LinkedServer 物件和 LinkedServer2 物件|<xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 物件|  
|LinkedServerLogin 物件|<xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> 物件|  
|LogFile 物件|<xref:Microsoft.SqlServer.Management.Smo.LogFile> 物件|  
|Login 物件和 Login2 物件|<xref:Microsoft.SqlServer.Management.Smo.Login> 物件|  
|MergeArticle 物件和 MergeArticle2 物件|<xref:Microsoft.SqlServer.Replication.MergeArticle> 物件 已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|MergeDynamicSnapshotJob 物件|已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|MergePublication 物件和 MergePublication2 物件|<xref:Microsoft.SqlServer.Replication.MergePublication> 物件 已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|MergePullSubscription 物件和 MergePullSubscription2 物件|<xref:Microsoft.SqlServer.Replication.MergePullSubscription> 物件 已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|MergeSubscription 物件|<xref:Microsoft.SqlServer.Replication.MergeSubscription> 物件 已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|MergeSubsetFilter 物件|已移至 `N:Microsoft.SqlServer.Replication` 命名空間。|  
|NameList 物件|已移除。 <xref:Microsoft.SqlServer.Management.Smo.Scripter> 物件中的替代功能。|  
|Operator 物件|已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空間。|  
|Permission 物件和 Permission2 物件|<xref:Microsoft.SqlServer.Management.Smo.ServerPermission>、<xref:Microsoft.SqlServer.Management.Smo.DatabasePermission>、<xref:Microsoft.SqlServer.Management.Smo.ApplicationRole> 和 <xref:Microsoft.SqlServer.Management.Smo.ObjectPermission> 物件。|  
|Property 物件|`Property` 物件|  
|Publisher 物件和 Publisher2 物件|<xref:Microsoft.SqlServer.Replication.ReplicationServer> 物件 已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|QueryResults 物件和 QueryResults2 物件|已由 <xref:System.Data.DataTable> 或 <xref:System.Data.DataSet> 系統物件取代。|  
|RegisteredServer 物件|已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|RegisteredSubscriber 物件|已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|Registry 物件和 Registry2 物件|已移除。|  
|RemoteLogin 物件|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件 已移至 Common 命名空間。|  
|RemoteServer 物件和 RemoteServer2 物件|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件 已移至 <xref:Microsoft.SqlServer.Management.Common> 命名空間。|  
|Replication 物件|已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|ReplicationDatabase 物件和 ReplicationDatabase2 物件|<xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 物件 已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|ReplicationSecurity 物件|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件 已移至 <xref:Microsoft.SqlServer.Management.Common> 命名空間。|  
|ReplicationStoredProcedure 物件和 ReplicationStoredProcedure2 物件|<xref:Microsoft.SqlServer.Replication.ReplicationStoredProcedure> 物件 已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|ReplicationTable 物件和 ReplicationTable2 物件|<xref:Microsoft.SqlServer.Replication.ReplicationTable> 物件 已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|Restore 物件和 Restore2 物件|<xref:Microsoft.SqlServer.Management.Smo.Restore> 和 <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase> 物件。|  
|Rule 物件和 Rule2 物件|<xref:Microsoft.SqlServer.Management.Smo.Rule> 物件|  
|Schedule 物件|已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|ServerGroup 物件|已移除。|  
|ServerRole 物件|<xref:Microsoft.SqlServer.Management.Smo.ServerRole> 物件|  
|SQLObjectList 物件|<xref:Microsoft.SqlServer.Management.Smo.SqlSmoObject> 陣列。|  
|SQLServer 物件和 SQLServer2 物件|<xref:Microsoft.SqlServer.Management.Smo.Server> 物件|  
|StoredProcedure 物件和 StoredProcedure2 物件|<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> 和 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> 物件。|  
|Subscriber 物件和 Subscriber2 物件|已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|SystemDatatype 物件和 SystemDataType2 物件|<xref:Microsoft.SqlServer.Management.Smo.DataType> 物件|  
|Table 物件和 Table2 物件|<xref:Microsoft.SqlServer.Management.Smo.Table> 物件|  
|TargetServer 物件|已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空間。|  
|TargetServerGroup 物件|已移至 <xref:Microsoft.SqlServer.Management.Smo.Agent> 命名空間。|  
|TransactionLog 物件|功能已移至 <xref:Microsoft.SqlServer.Management.Smo.Database> 物件中。|  
|TransArticle 物件和 TransArticle2 物件|<xref:Microsoft.SqlServer.Replication.TransArticle> 物件 已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|Transfer 物件和 Transfer2 物件|<xref:Microsoft.SqlServer.Management.Smo.Transfer> 物件|  
|TransPublication 物件和 TransPublication2 物件|<xref:Microsoft.SqlServer.Replication.TransPublication> 物件 已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|TransPullSubscription 物件和 TransPullSubscription2 物件|<xref:Microsoft.SqlServer.Replication.TransPullSubscription> 物件 已移至 <xref:Microsoft.SqlServer.Replication> 命名空間。|  
|Trigger 物件和 Trigger2 物件|<xref:Microsoft.SqlServer.Management.Smo.Trigger> 物件|  
|User 物件和 User2 物件|<xref:Microsoft.SqlServer.Management.Smo.User> 物件|  
|UserDefinedDatatype 物件和 UserDefinedDataType2 物件|<xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> 物件|  
|UserDefinedFunction 物件|<xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> 和 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter> 物件。|  
|View 物件和 View2 物件|<xref:Microsoft.SqlServer.Management.Smo.View> 物件|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 管理物件 &#40;SMO&#41; 程式設計指南](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
