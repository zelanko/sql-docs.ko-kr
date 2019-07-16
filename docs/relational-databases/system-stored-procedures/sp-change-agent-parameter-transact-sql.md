---
title: sp_change_agent_parameter (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_change_agent_parameter_TSQL
- sp_change_agent_parameter
helpviewer_keywords:
- sp_change_agent_parameter
ms.assetid: f1fbecc7-e64f-405c-8067-6b38c1f3c0a0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 610d63df2bf3496abaed8682ac83a72883e184b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045899"
---
# <a name="spchangeagentparameter-transact-sql"></a>sp_change_agent_parameter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  에 저장 된 복제 에이전트 프로필의 매개 변수를 변경 합니다 [MSagent_parameters](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) 시스템 테이블입니다. 이 저장 프로시저는 에이전트가 실행되고 있는 모든 데이터베이스의 배포자에서 실행될 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_change_agent_parameter [ @profile_id= ] profile_id, [ @parameter_name= ] 'parameter_name', [ @parameter_value= ] 'parameter_value'  
```  
  
## <a name="arguments"></a>인수  
`[ @profile_id = ] profile_id,` 프로필의 ID입니다. *profile_id* 됩니다 **int**, 기본값은 없습니다.  
  
`[ @parameter_name = ] 'parameter_name'` 매개 변수의 이름이입니다. *parameter_name* 됩니다 **sysname**, 기본값은 없습니다. 시스템 프로필의 경우 변경될 수 있는 매개 변수는 에이전트의 유형에 따라 달라집니다 에이전트의 유형을 알아보려면이 알아보려면 *profile_id* 나타내는 찾습니다는 *profile_id* 열에는 **Msagent_profiles** 테이블 및 참고는 *agent_type*  값입니다.  
  
> [!NOTE]  
>  매개 변수는에 대 한 지원 되는 경우를 지정 *agent_type*, 에이전트 프로필에 정의 되지 않은 하지만 오류가 반환 됩니다. 실행 해야 하는 에이전트 프로필 매개 변수를 추가할 [sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)합니다.  
  
 스냅숏 에이전트 (*agent_type*=**1**), 프로필에 정의 된 경우 다음 속성을 변경할 수 있습니다.  
  
-   **70Subscribers**  
  
-   **BcpBatchSize**  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxNetworkOptimization**  
  
-   **출력**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **QueryTimeout**  
  
-   **StartQueueTimeout**  
  
-   **UsePerArticleContentsView**  
  
 로그 판독기 에이전트 (*agent_type*=**2**), 프로필에 정의 된 경우 다음 속성을 변경할 수 있습니다.  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **MessageInterval**  
  
-   **출력**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **ReadBatchSize**  
  
-   **ReadBatchThreshold**  
  
 배포 에이전트 (*agent_type*=**3**), 프로필에 정의 된 경우 다음 속성을 변경할 수 있습니다.  
  
-   **BcpBatchSize**  
  
-   **CommitBatchSize**  
  
-   **CommitBatchThreshold**  
  
-   **FileTransferType**  
  
-   **HistoryVerboseLevel**  
  
-   **KeepAliveMessageInterval**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxDeliveredTransactions**  
  
-   **MessageInterval**  
  
-   **출력**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **QuotedIdentifier**  
  
-   **SkipErrors**  
  
-   **TransactionsPerHistory**  
  
 병합 에이전트 (*agent_type*=**4**), 프로필에 정의 된 경우 다음 속성을 변경할 수 있습니다.  
  
-   **AltSnapshotFolder**  
  
-   **BcpBatchSize**  
  
-   **ChangesPerHistory**  
  
-   **DestThreads**  
  
-   **DownloadGenerationsPerBatch**  
  
-   **DownloadReadChangesPerBatch**  
  
-   **DownloadWriteChangesPerBatch**  
  
-   **DynamicSnapshotLocation**  
  
-   **ExchangeType**  
  
-   **FastRowCount**  
  
-   **FileTransferType**  
  
-   **GenerationChangeThreshold**  
  
-   **HistoryVerboseLevel**  
  
-   **InputMessageFile**  
  
-   **InteractiveResolution**  
  
-   **InterruptOnMessagePattern**  
  
-   **KeepAliveMessageInterval**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxDownloadChanges**  
  
-   **MaxUploadChanges**  
  
-   **MetadataRetentionCleanup**  
  
-   **NumDeadlockRetries**  
  
-   **출력**  
  
-   **OutputMessageFile**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **ParallelUploadDownload**  
  
-   **PauseOnMessagePattern**  
  
-   **PauseTime**  
  
-   **PollingInterval**  
  
-   **ProcessMessagesAtPublisher**  
  
-   **ProcessMessagesAtSubscriber**  
  
-   **QueryTimeout**  
  
-   **QueueSizeMultiplier**  
  
-   **SrcThreads**  
  
-   **StartQueueTimeout**  
  
-   **SyncToAlternate**  
  
-   **UploadGenerationsPerBatch**  
  
-   **UploadReadChangesPerBatch**  
  
-   **UploadWriteChangesPerBatch**  
  
-   **UseInprocLoader**  
  
-   **유효성 검사**  
  
-   **ValidateInterval**  
  
 큐 판독기 에이전트 (*agent_type*=**9**), 프로필에 정의 된 경우 다음 속성을 변경할 수 있습니다.  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **출력**  
  
-   **OutputVerboseLevel**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **ResolverState**  
  
-   **SQLQueueMode**  
  
 지정된 된 프로필에 정의 된 매개 변수를 보려면 실행 **sp_help_agent_profile** 확인 합니다 *profile_name* 연관 합니다 *profile_id*. 적절 한 *profile_id*, 다음 실행 **sp_help_agent_parameters** 는 사용 하 여 *profile_id* 프로필과 연결 된 매개 변수를 보려면. 매개 변수는 실행 하 여 프로필을 추가할 수 있습니다 [sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)합니다.  
  
`[ @parameter_value = ] 'parameter_value'` 매개 변수의 새 값이입니다. *parameter_value* 됩니다 **nvarchar(255)** , 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_change_agent_parameter** 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_change_agent_parameter**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 에이전트 프로필](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [복제 배포 에이전트](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [복제 로그 판독기 에이전트](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [복제 병합 에이전트](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [복제 큐 판독기 에이전트](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [sp_add_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_drop_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
