---
title: SMO에 대 한 SQL-DMO 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 590f5396-98d5-485e-9b41-728c6ed7cb9d
caps.latest.revision: 36
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 54c66973a1cc0ca7f024a696902f694b45778a9a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37182820"
---
# <a name="sql-dmo-mapping-to-smo"></a>SMO에 대한 SQL-DMO 매핑
  SQL-DMO(SQL Distributed Management Objects)는 더 이상 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 포함되지 않습니다. SMO([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects)를 사용하도록 SQL-DMO 응용 프로그램을 변환해야 합니다. SMO 개체 모델은 SQL-DMO와 비슷하므로 대부분의 SQL-DMO 개체는 SMO에서 이름이 같은 개체에 매핑됩니다. 그러나 일부 SQL-DMO 개체는 SMO로 전환되는 과정에서 변경되거나 삭제되었습니다. 다음 표에는 SMO로 직접 변환되지 않은 SQL-DMO 개체에 대해 수행할 수 있는 권장 작업이 나와 있습니다.  
  
|SQL-DMO 개체|SMO에서의 동작|  
|---------------------|-------------------|  
|View2 개체|<xref:Microsoft.SqlServer.Management.Smo.Agent> 네임스페이스로 이동되었습니다.|  
|AlertSystem 개체|<xref:Microsoft.SqlServer.Management.Smo.Agent> 네임스페이스로 이동되었습니다.|  
|Application 개체|제거되었습니다.|  
|Backup 개체 및 Backup2 개체|<xref:Microsoft.SqlServer.Management.Smo.Backup> 및 <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase> 개체입니다.|  
|BackupDevice 개체|<xref:Microsoft.SqlServer.Management.Smo.BackupDevice> 개체입니다.|  
|BulkCopy 개체 및 BulkCopy2 개체|제거되고 <xref:Microsoft.SqlServer.Management.Smo.Transfer> 개체로 대체되었습니다.|  
|Category 개체|<xref:Microsoft.SqlServer.Management.Smo.Agent> 네임스페이스로 이동되었습니다. <xref:Microsoft.SqlServer.Management.Smo.Agent.AlertCategory>, <xref:Microsoft.SqlServer.Management.Smo.Agent.OperatorCategory>, <xref:Microsoft.SqlServer.Management.Smo.Agent.JobCategory> 개체로 대체되었습니다.|  
|Check 개체|<xref:Microsoft.SqlServer.Management.Smo.Check> 개체|  
|Column 개체 및 Column2 개체|<xref:Microsoft.SqlServer.Management.Smo.Column> 개체입니다.|  
|Configuration 개체|<xref:Microsoft.SqlServer.Management.Smo.Configuration> 및 <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase> 개체입니다.|  
|ConfigValue 개체|<xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> 개체입니다.|  
|Database 개체 및 Database2 개체|<xref:Microsoft.SqlServer.Management.Smo.Database> 개체입니다.|  
|DatabaseRole 개체 및 DatabaseRole2 개체|<xref:Microsoft.SqlServer.Management.Smo.DatabaseRole> 개체입니다.|  
|DBFile 개체|<xref:Microsoft.SqlServer.Management.Smo.DataFile> 개체입니다.|  
|DBOption 개체 및 DBOption2 개체|<xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions> 개체로 이동되었습니다.|  
|Default 개체 및 Default2 개체|<xref:Microsoft.SqlServer.Management.Smo.Default> 개체입니다.|  
|DistributionArticle 개체 및 DistributionArticle2 개체|<xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|DistributionDatabase 개체 및 DistributionDatabase2 개체|<xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|DistributionPublication 개체 및 DistributionPublication2 개체|<xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|DistributionSubscription 개체 및 DistributionSubscription2 개체|<xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|Distributor 개체 및 Distributor2 개체|<xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|DRIDefault 개체|<xref:Microsoft.SqlServer.Management.Smo.ScriptingOptions> 개체로 이동되었습니다.|  
|FileGroup 개체 및 FileGroup2 개체|<xref:Microsoft.SqlServer.Management.Smo.FileGroup> 개체입니다.|  
|FullTextCatalog 개체 및 FullTextCatalog2 개체|<xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> 및 <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex> 개체입니다.|  
|Index 개체 및 Index2 개체|<xref:Microsoft.SqlServer.Management.Smo.Index> 개체|  
|IntegratedSecurity 개체|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> 네임스페이스의 <xref:Microsoft.SqlServer.Management.Common> 개체로 기능이 이동되었습니다.|  
|Job 개체|<xref:Microsoft.SqlServer.Management.Smo.Agent.Job> 개체입니다. <xref:Microsoft.SqlServer.Management.Smo.Agent> 네임스페이스로 이동되었습니다.|  
|JobFilter 개체|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobFilter> 개체입니다. <xref:Microsoft.SqlServer.Management.Smo.Agent> 네임스페이스로 이동되었습니다.|  
|JobHistoryFilter 개체|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobHistoryFilter> 개체입니다. <xref:Microsoft.SqlServer.Management.Smo.Agent> 네임스페이스로 이동되었습니다.|  
|JobSchedule 개체|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobSchedule> 개체입니다. <xref:Microsoft.SqlServer.Management.Smo.Agent> 네임스페이스로 이동되었습니다.|  
|JobServer 개체 및 JobServer2 개체|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobServer> 개체입니다. <xref:Microsoft.SqlServer.Management.Smo.Agent> 네임스페이스로 이동되었습니다.|  
|JobStep 개체|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobStep> 개체입니다. <xref:Microsoft.SqlServer.Management.Smo.Agent> 네임스페이스로 이동되었습니다.|  
|Key 개체|<xref:Microsoft.SqlServer.Management.Smo.ForeignKey> 및 <xref:Microsoft.SqlServer.Management.Smo.Index> 개체입니다.|  
|LinkedServer 개체 및 LinkedServer2 개체|<xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 개체입니다.|  
|LinkedServerLogin 개체|<xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> 개체입니다.|  
|LogFile 개체|<xref:Microsoft.SqlServer.Management.Smo.LogFile> 개체입니다.|  
|Login 개체 및 Login2 개체|<xref:Microsoft.SqlServer.Management.Smo.Login> 개체입니다.|  
|MergeArticle 개체 및 MergeArticle2 개체|<xref:Microsoft.SqlServer.Replication.MergeArticle> 개체입니다. <xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|MergeDynamicSnapshotJob 개체|<xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|MergePublication 개체 및 MergePublication2 개체|<xref:Microsoft.SqlServer.Replication.MergePublication> 개체입니다. <xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|MergePullSubscription 개체 및 MergePullSubscription2 개체|<xref:Microsoft.SqlServer.Replication.MergePullSubscription> 개체입니다. <xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|MergeSubscription 개체|<xref:Microsoft.SqlServer.Replication.MergeSubscription> 개체입니다. <xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|MergeSubsetFilter 개체|`N:Microsoft.SqlServer.Replication` 네임스페이스로 이동되었습니다.|  
|NameList 개체|제거되었습니다. <xref:Microsoft.SqlServer.Management.Smo.Scripter> 개체의 대체 기능입니다.|  
|Operator 개체|<xref:Microsoft.SqlServer.Management.Smo.Agent> 네임스페이스로 이동되었습니다.|  
|Permission 개체 및 Permission2 개체|<xref:Microsoft.SqlServer.Management.Smo.ServerPermission>, <xref:Microsoft.SqlServer.Management.Smo.DatabasePermission>, <xref:Microsoft.SqlServer.Management.Smo.ApplicationRole> 및 <xref:Microsoft.SqlServer.Management.Smo.ObjectPermission> 개체입니다.|  
|Property 개체|`Property` 개체입니다.|  
|Publisher 개체 및 Publisher2 개체|<xref:Microsoft.SqlServer.Replication.ReplicationServer> 개체입니다. <xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|QueryResults 개체 및 QueryResults2 개체|<xref:System.Data.DataTable> 또는 <xref:System.Data.DataSet> 시스템 개체로 대체되었습니다.|  
|RegisteredServer 개체|<xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|RegisteredSubscriber 개체|<xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|Registry 개체 및 Registry2 개체|제거되었습니다.|  
|RemoteLogin 개체|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체입니다. Common 네임스페이스로 이동되었습니다.|  
|RemoteServer 개체 및 RemoteServer2 개체|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체입니다. <xref:Microsoft.SqlServer.Management.Common> 네임스페이스로 이동되었습니다.|  
|Replication 개체|<xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|ReplicationDatabase 개체 및 ReplicationDatabase2 개체|<xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 개체입니다. <xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|ReplicationSecurity 개체|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체입니다. <xref:Microsoft.SqlServer.Management.Common> 네임스페이스로 이동되었습니다.|  
|ReplicationStoredProcedure 개체 및 ReplicationStoredProcedure2 개체|<xref:Microsoft.SqlServer.Replication.ReplicationStoredProcedure> 개체입니다. <xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|ReplicationTable 개체 및 ReplicationTable2 개체|<xref:Microsoft.SqlServer.Replication.ReplicationTable> 개체입니다. <xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|Restore 개체 및 Restore2 개체|<xref:Microsoft.SqlServer.Management.Smo.Restore> 및 <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase> 개체입니다.|  
|Rule 개체 및 Rule2 개체|<xref:Microsoft.SqlServer.Management.Smo.Rule> 개체|  
|Schedule 개체|<xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|ServerGroup 개체|제거되었습니다.|  
|ServerRole 개체|<xref:Microsoft.SqlServer.Management.Smo.ServerRole> 개체입니다.|  
|SQLObjectList 개체|<xref:Microsoft.SqlServer.Management.Smo.SqlSmoObject> 배열입니다.|  
|SQLServer 개체 및 SQLServer2 개체|<xref:Microsoft.SqlServer.Management.Smo.Server> 개체입니다.|  
|StoredProcedure 개체 및 StoredProcedure2 개체|<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> 및 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> 개체입니다.|  
|Subscriber 개체 및 Subscriber2 개체|<xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|SystemDatatype 개체 및 SystemDatatype2 개체|<xref:Microsoft.SqlServer.Management.Smo.DataType> 개체입니다.|  
|Table 개체 및 Table2 개체|<xref:Microsoft.SqlServer.Management.Smo.Table> 개체입니다.|  
|TargetServer 개체|<xref:Microsoft.SqlServer.Management.Smo.Agent> 네임스페이스로 이동되었습니다.|  
|TargetServerGroup 개체|<xref:Microsoft.SqlServer.Management.Smo.Agent> 네임스페이스로 이동되었습니다.|  
|TransactionLog 개체|<xref:Microsoft.SqlServer.Management.Smo.Database> 개체로 기능이 이동되었습니다.|  
|TransArticle 개체 TransArticle2 개체|<xref:Microsoft.SqlServer.Replication.TransArticle> 개체입니다. <xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|Transfer 메서드 및 Transfer2 개체|<xref:Microsoft.SqlServer.Management.Smo.Transfer> 개체입니다.|  
|TransPublication 개체 및 TransPublication2 개체|<xref:Microsoft.SqlServer.Replication.TransPublication> 개체입니다. <xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|TransPullSubscription 개체 및 TransPullSubscription2 개체|<xref:Microsoft.SqlServer.Replication.TransPullSubscription> 개체입니다. <xref:Microsoft.SqlServer.Replication> 네임스페이스로 이동되었습니다.|  
|Trigger 개체 및 Trigger2 개체|<xref:Microsoft.SqlServer.Management.Smo.Trigger> 개체입니다.|  
|User 개체 및 User2 개체|<xref:Microsoft.SqlServer.Management.Smo.User> 개체입니다.|  
|UserDefinedDatatype 개체 및 UserDefinedDataType2 개체|<xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> 개체입니다.|  
|UserDefinedFunction 개체|<xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> 및 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter> 개체입니다.|  
|View 개체 및 View2 개체|<xref:Microsoft.SqlServer.Management.Smo.View> 개체입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SMO&#40;SQL Server 관리 개체&#41; 프로그래밍 가이드](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
