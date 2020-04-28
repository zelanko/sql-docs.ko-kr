---
title: sp_change_agent_parameter (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: cd737be5a1e71e46750f6c80fd68ad254cb6436f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68768939"
---
# <a name="sp_change_agent_parameter-transact-sql"></a>sp_change_agent_parameter(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [MSagent_parameters](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) 시스템 테이블에 저장 된 복제 에이전트 프로필의 매개 변수를 변경 합니다. 이 저장 프로시저는 에이전트가 실행되고 있는 모든 데이터베이스의 배포자에서 실행될 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_change_agent_parameter [ @profile_id= ] profile_id, [ @parameter_name= ] 'parameter_name', [ @parameter_value= ] 'parameter_value'  
```  
  
## <a name="arguments"></a>인수  
`[ @profile_id = ] profile_id,`프로필의 ID입니다. *profile_id* 는 **int**이며 기본값은 없습니다.  
  
`[ @parameter_name = ] 'parameter_name'`매개 변수의 이름입니다. *parameter_name* 는 **sysname**이며 기본값은 없습니다. 시스템 프로필의 경우 변경될 수 있는 매개 변수는 에이전트의 유형에 따라 달라집니다 이 *profile_id* 나타내는 에이전트 유형을 확인 하려면 **Msagent_profiles** 테이블에서 *profile_id* 열을 찾아 *agent_type* 값을 확인 합니다.  
  
> [!NOTE]  
>  매개 변수가 지정 된 *agent_type*에 대해 지원 되지만 에이전트 프로필에 정의 되지 않은 경우 오류가 반환 됩니다. 에이전트 프로필에 매개 변수를 추가 하려면 [sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)를 실행 해야 합니다.  
  
 프로필에 스냅숏 에이전트 (*agent_type*=**1**)가 정의 된 경우 다음 속성을 변경할 수 있습니다.  
  
-   **70 구독자**  
  
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
  
 프로필에 로그 판독기 에이전트 (*agent_type*=**2**)가 정의 된 경우 다음 속성을 변경할 수 있습니다.  
  
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
  
 프로필에 배포 에이전트 (*agent_type*=**3**)가 정의 된 경우 다음 속성을 변경할 수 있습니다.  
  
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
  
 프로필에 병합 에이전트 (*agent_type*=**4**)가 정의 된 경우 다음 속성을 변경할 수 있습니다.  
  
-   **AltSnapshotFolder**  
  
-   **BcpBatchSize**  
  
-   **변경 내용**  
  
-   **DestThreads**  
  
-   **DownloadGenerationsPerBatch**  
  
-   **Downloadreaddemand Perbatch**  
  
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
  
-   **Metadata보존**  
  
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
  
 프로필에 큐 판독기 에이전트 (*agent_type*=**9**)가 정의 된 경우 다음 속성을 변경할 수 있습니다.  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **출력**  
  
-   **OutputVerboseLevel**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **ResolverState**  
  
-   **SQLQueueMode**  
  
 지정 된 프로필에 대해 정의 된 매개 변수를 보려면 **sp_help_agent_profile** 를 실행 하 고 *profile_id*와 연결 된 *profile_name* 를 확인 합니다. 적절 한 *profile_id*를 사용 하 여 **sp_help_agent_parameters** 다음 실행 sp_help_agent_parameters *profile_id* 사용 하 여 프로필에 연결 된 매개 변수를 확인 합니다. [Sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)를 실행 하 여 프로필에 매개 변수를 추가할 수 있습니다.  
  
`[ @parameter_value = ] 'parameter_value'`매개 변수의 새 값입니다. *parameter_value* 은 **nvarchar (255)** 이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_change_agent_parameter** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_change_agent_parameter**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 에이전트 프로필](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [복제 배포 에이전트](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [복제 로그 판독기 에이전트](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [복제 병합 에이전트](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [복제 큐 판독기 에이전트](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [복제 스냅숏 에이전트](../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [Transact-sql&#41;sp_add_agent_parameter &#40;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [Transact-sql&#41;sp_drop_agent_parameter &#40;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [Transact-sql&#41;sp_help_agent_parameter &#40;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
