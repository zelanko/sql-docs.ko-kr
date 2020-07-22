---
title: 트랜잭션 복제 성능 향상 | Microsoft 문서
description: SQL Server에서 복제 성능을 개선할 수 있는 일반적인 성능 팁과 트랜잭션 복제를 위한 추가 기법을 알아봅니다.
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- performance [SQL Server replication], transactional replication
- designing databases [SQL Server], replication performance
- performance [SQL Server replication], snapshot replication
- snapshot replication [SQL Server], performance
- subscriptions [SQL Server replication], performance considerations
- agents [SQL Server replication], performance
- Distribution Agent, performance
- transactional replication, performance
- Log Reader Agent, performance
ms.assetid: 67084a67-43ff-4065-987a-3b16d1841565
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: d3af77a60678e8286fadfbafcf46f742439e9bf7
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86902556"
---
# <a name="enhance-transactional-replication-performance"></a>트랜잭션 복제 성능 향상
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  [일반적인 복제 성능 향상](../../../relational-databases/replication/administration/enhance-general-replication-performance.md)에 설명된 일반 성능 팁을 살펴본 후에 트랜잭션 복제에 해당하는 이러한 추가 영역을 살펴보십시오.  
  
## <a name="database-design"></a>데이터베이스 디자인  
  
-   애플리케이션 디자인에서 트랜잭션 크기를 최소화합니다.  
  
     기본적으로 트랜잭션 복제는 트랜잭션 경계에 따라 변경 내용을 전파합니다. 트랜잭션이 작을수록 배포 에이전트가 네트워크 문제로 인해 트랜잭션을 다시 전송할 가능성이 작아집니다. 에이전트가 트랜잭션을 다시 전송해야 할 경우 보내는 데이터 양은 적어집니다. 

  
## <a name="distributor-configuration"></a>배포자 구성  
  
-   전용 서버에서 배포자를 구성합니다.  
  
     원격 배포자를 구성하여 게시자에서 처리 오버헤드를 줄일 수 있습니다. 자세한 내용은 [Configure Distribution](../../../relational-databases/replication/configure-distribution.md)를 참조하세요.  
  
-   배포 데이터베이스 크기를 적절히 조정합니다.  
  
     시스템에서 명령 저장에 필요한 공간을 결정할 수 있도록 일반적인 로드 상태에서 복제를 테스트합니다. 데이터베이스는 자주 자동 증가되지 않고도 명령을 저장할 수 있을 만큼 충분히 커야 합니다. 데이터베이스의 크기 변경에 대한 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
## <a name="publication-design"></a>게시 디자인  
  
-   게시된 테이블을 일괄로 업데이트할 때 저장 프로시저 실행을 복제합니다.  
  
     구독자의 다수 행에 가끔씩 영향을 미치는 일괄 처리 업데이트가 있는 경우 저장 프로시저를 사용하여 게시된 테이블을 업데이트하고 저장 프로시저의 실행을 게시해 보십시오. 배포 에이전트는 영향을 받은 모든 행의 업데이트나 삭제를 보내는 대신 구독자에서 같은 매개 변수 값으로 동일한 프로시저를 실행합니다. 자세한 내용은 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)를 참조하세요.  
  
-   여러 게시 간에 아티클을 분산시킵니다.  
  
     [ **-SubscriptionStreams** 매개 변수](#subscriptionstreams)를 사용할 수 없는 경우 여러 게시를 만들어 보세요. 이러한 게시에 아티클을 분산시키면 복제가 구독자에게 변경 내용을 병렬로 적용할 수 있습니다.  
  
## <a name="subscription-considerations"></a>구독 고려 사항  
  
-   같은 게시자에 여러 게시가 있을 경우 공유 에이전트가 아닌 독립 에이전트를 사용합니다. 새 게시 마법사에서는 이것이 기본값입니다.  
  
-   에이전트를 잦은 간격으로 실행하는 대신 계속 실행합니다.  
  
     일정을 분 단위처럼 자주 실행하도록 설정하는 대신 계속 실행되도록 설정하면 에이전트를 시작하고 중지할 필요가 없으므로 복제 성능이 향상됩니다. 배포 에이전트가 계속 실행되도록 설정하면 변경 내용이 토폴로지에 연결된 다른 서버로 짧은 대기 시간 내에 전파됩니다. 자세한 내용은 다음을 참조하세요.  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [동기화 일정 지정](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
## <a name="distribution-agent-and-log-reader-agent-parameters"></a>배포 에이전트 및 로그 판독기 에이전트 매개 변수  
트래픽이 많은 OLTP 시스템에서 로그 판독기 및 배포 에이전트의 처리량을 늘리기 위해 종종 에이전트 프로필 매개 변수를 조정합니다. 

로그 판독기 및 배포 에이전트의 성능을 개선할 최상의 값을 확인하기 위해 테스트가 수행되었습니다. 이 테스트의 결과에 따르면 어떤 상황에서 어떤 값이 작동하는지를 결정하는 요소는 워크로드였고, 모든 상황에서 성능을 개선하는 하나의 값 조정은 없습니다. 

결과: 
- 더 작은 트랜잭션(500개 미만의 명령)의 워크로드가 있는 ‘로그 판독기 에이전트’의 경우 **ReadBatchSize** 값이 높으면 처리량이 향상될 수 있습니다. 그러나 큰 트랜잭션이 있는 워크로드의 경우 이 값을 변경해도 성능이 향상되지 않습니다. 
    - 동일한 서버에서 병렬로 실행되는 여러 배포 에이전트 및 여러 로그 판독기 에이전트가 있는 경우 **ReadBatchSize** 값이 높으면 배포 데이터베이스에서 경합이 발생합니다. 
- ‘배포 에이전트’의 경우
    - **CommitBatchSize**를 늘리면 처리량이 향상될 수 있습니다. 하지만 오류가 발생하는 경우에는 배포 에이전트가 많은 트랜잭션을 롤백하고 다시 시작하여 다시 적용해야 한다는 것을 고려해야 합니다. 
    - **SubscriptionStreams** 값을 늘리면 구독자에 대한 여러 연결이 변경 내용의 일괄 처리를 병렬로 적용하므로 배포 에이전트의 전체 처리량에 도움이 됩니다. 그러나 프로세서 및 기타 메타데이터 조건(예: 기본 키, 외래 키, 고유 제약 조건 및 인덱스)의 수에 따라 SubscriptionStreams 값이 높으면 실제로 부정적인 영향을 줄 수 있습니다. 또한 스트림이 실행 또는 커밋되지 않으면 배포 에이전트는 대신에 단일 스트림을 사용하여 실패한 일괄 처리를 다시 시도합니다.


이 테스트에 대한 자세한 내용은 [Optimizing replication agent profile parameters for better performance](https://blogs.msdn.microsoft.com/sql_server_team/optimizing-replication-agent-profile-parameters-for-better-performance/)(성능 향상을 위해 복제 에이전트 프로필 매개 변수 최적화)를 참조하세요.


### <a name="log-reader-agent"></a>로그 판독기 에이전트

#### <a name="readbatchsize"></a>ReadBatchSize
- 로그 판독기 에이전트에 대해 **-ReadBatchSize** 매개 변수의 값을 늘립니다.  
  
로그 판독기 에이전트와 배포 에이전트는 트랜잭션 읽기 및 커밋 작업을 위한 일괄 처리 크기를 지원합니다. 일괄 처리 크기는 기본적으로 500개 트랜잭션입니다. 로그 판독기 에이전트는 트랜잭션의 복제 표시 여부에 상관없이 로그에서 특정 트랜잭션 수를 읽습니다. 많은 트랜잭션이 게시 데이터베이스에 기록되는데 그중 일부 하위 집합만이 복제용으로 표시되는 경우 **-ReadBatchSize** 매개 변수를 사용하여 로그 판독기 에이전트의 읽기 일괄 처리 크기를 늘려야 합니다. 이 매개 변수는 Oracle 게시자에는 적용되지 않습니다.  

   - 더 작은 트랜잭션(500개 미만의 명령)의 워크로드는 **ReadBatchSize**가 최대 5000으로 증가할 경우 초당 처리되는 명령 수가 증가합니다. 
   - 더 큰 워크로드(500~1000개의 명령이 있는 트랜잭션)의 경우 **ReadBatchSize**를 늘려도 성능이 거의 향상되지 않습니다. **ReadBatchSize**를 늘리면 한 번 왕복으로 배포 데이터베이스에 기록되는 트랜잭션 수가 증가합니다. 이에 따라 트랜잭션 및 명령이 배포 에이전트에 표시되는 시간이 증가하고 복제 프로세스에 대기 시간이 도입됩니다.  

#### <a name="pollinginterval"></a>PollingInterval
- 로그 판독기 에이전트에 대해 **-PollingInterval** 매개 변수의 값을 줄입니다.  
  
**-PollingInterval** 매개 변수는 게시된 데이터베이스의 트랜잭션 로그에서 복제할 트랜잭션을 쿼리할 빈도를 지정합니다. 기본값은 5초입니다. 이 값을 줄이면 로그가 더 자주 폴링되므로 게시 데이터베이스에서 배포 데이터베이스로 트랜잭션을 배달할 때 대기 시간을 줄일 수 있습니다. 그러나 자주 폴링하면 서버의 로드가 증가하므로 적절한 대기 시간과 서버 로드 간의 균형을 맞춰야 합니다.   
  
#### <a name="maxcmdsintran"></a>MaxCmdsInTran
- 의도치 않게 발생하는 일회성 병목 현상을 해결하려면 로그 판독기 에이전트에 **–MaxCmdsInTran** 매개 변수를 사용하세요.  
  
**–MaxCmdsInTran** 매개 변수는 로그 판독기가 배포 데이터베이스에 대해 명령을 쓸 때 트랜잭션으로 그룹화된 최대 문 개수를 지정합니다. 이 매개 변수를 사용하면 구독자에서 명령을 적용할 때 로그 판독기 에이전트와 배포 에이전트가 게시자에서 큰 트랜잭션(여러 명령으로 구성됨)을 여러 개의 작은 트랜잭션으로 나눌 수 있습니다. 이 매개 변수를 지정하면 배포자에서 경합을 줄일 수 있고 게시자와 구독자 간 대기 시간을 줄일 수 있습니다. 원래 트랜잭션이 작은 단위로 적용되므로 구독자는 엄격한 트랜잭션 원자성을 깨고 원래 트랜잭션이 끝나기 전에 큰 논리적 게시자 트랜잭션의 행에 액세스할 수 있습니다. 기본값은 **0**으로 게시자의 트랜잭션 경계를 유지합니다. 이 매개 변수는 Oracle 게시자에는 적용되지 않습니다.  
  
   > [!WARNING]  
   >  **MaxCmdsInTran** 은 항상 설정되도록 설계되지 않았습니다. 단일 트랜잭션에 많은 DML 작업을 실수로 수행한 경우의 문제(전체 트랜잭션이 배포 데이터베이스에 있고 잠금이 보유될 때까지 명령 배포에 지연 발생)를 해결하기 위한 것입니다. 정기적으로 이 상황이 발생하는 경우 애플리케이션을 검토하고 트랜잭션 크기를 줄이는 방법을 찾으세요.  
  
### <a name="distribution-agent"></a>배포 에이전트

#### <a name="subscriptionstreams"></a>SubscriptionStreams
- 배포 에이전트에 대한 **–SubscriptionStreams** 매개 변수를 늘립니다.  
  
**–SubscriptionStreams** 매개 변수는 집계 복제 처리량을 크게 높일 수 있습니다. 이 매개 변수는 변경 내용의 일괄 처리를 병렬로 적용하기 위해 구독자에 여러 연결을 설정하도록 허용하지만 단일 스레드를 사용할 때 나타나는 여러 가지 트랜잭션 특징을 유지합니다. 여러 연결 중 하나가 실행 또는 커밋되지 않으면 모든 연결에서 현재 일괄 처리를 중지하고 에이전트가 단일 스트림을 사용하여 실패한 일괄 처리를 다시 시도합니다. 이러한 재시도 단계가 완료되기 전에는 구독자에 임시 트랜잭션 불일치가 발생할 수 있으며 실패한 일괄 처리가 성공적으로 커밋되면 구독자의 트랜잭션 일관성이 다시 유지됩니다.  
  
[sp_addsubscription&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)의 `@subscriptionstreams`를 사용하여 이 에이전트 매개 변수의 값을 지정할 수 있습니다.  

구독 스트림 구현에 대한 자세한 내용은 [Navigating SQL replication subscriptionStream setting](https://blogs.msdn.microsoft.com/repltalk/2010/03/01/navigating-sql-replication-subscriptionstreams-setting)(SQL 복제 subscriptionStream 설정 살펴보기)을 참조하세요.
  
### <a name="blocking-monitor-thread"></a>차단 모니터 스레드

배포 에이전트는 세션 간에 차단을 검색하는 차단 모니터 스레드를 유지 관리합니다. 차단 모니터 스레드가 세션 간의 차단을 검색하면 배포 에이전트는 하나의 세션을 이전에 적용할 수 없는 명령의 현재 일괄 처리를 다시 적용하는 데 사용하도록 전환합니다.

차단 모니터 스레드는 배포 에이전트 세션 간에 차단을 검색할 수 있습니다. 그러나 차단 모니터 스레드는 다음과 같은 상황에서 차단을 검색할 수 없습니다.
- 차단이 발생하는 세션 중 하나가 배포 에이전트 세션이 아닌 경우
- 세션 교착 상태로 인해 배포 에이전트의 작업을 중단하는 경우

이 경우에 배포 에이전트는 해당 명령이 실행되는 즉시 모든 세션을 함께 커밋하도록 조정합니다. 다음 조건이 true인 경우 세션 간에 교착 상태가 발생합니다.

- 배포 에이전트 세션과 배포 에이전트 세션이 아닌 세션 간에 차단이 발생합니다.
- 배포 에이전트가 모든 세션을 함께 커밋하도록 조정하기 전에 모든 세션이 해당 명령 실행을 완료하기를 기다리고 있었습니다.

예를 들어 *SubscriptionStreams* 매개 변수를 8로 구성했습니다. 10 세션부터 17 세션까지는 배포 에이전트 세션입니다. 18 세션은 배포 에이전트 세션이 아닙니다. 10 세션이 18 세션에 의해 차단되고 18 세션이 11 세션에 의해 차단되었습니다. 또한 10 세션 및 11 세션은 함께 커밋해야 합니다. 그러나 배포 에이전트는 차단 때문에 10 세션 및 11 세션을 함께 커밋할 수 없습니다. 따라서 배포 에이전트는 10 세션 및 11 세션이 해당 명령의 실행을 완료할 때까지 이러한 8개의 세션을 함께 커밋하도록 조정할 수 없습니다.

이 예제에서는 해당 명령을 실행하는 세션이 없는 상태가 발생합니다. **QueryTimeout** 속성에서 지정된 시간에 도달하면 배포 에이전트는 모든 세션을 취소합니다.

> [!Note]
> 기본적으로 **QueryTimeout** 속성 값은 5분입니다.

이 쿼리 시간 제한 동안 배포 에이전트 성능 카운터에서 다음과 같은 추세를 확인할 수 있습니다. 

- **Dist: Delivered Cmds/sec** 성능 카운터 값은 항상 0입니다.
- **Dist: Delivered Trans/sec** 성능 카운터 값은 항상 0입니다.
- **Dist: Delivery Latency** 성능 카운터는 스레드 교착 상태가 해결될 때까지 값이 증가한다고 보고합니다.

SQL Server 온라인 설명서의 "복제 배포 에이전트" 항목에는 *SubscriptionStreams* 매개 변수에 대한 다음 설명이 포함되어 있습니다. "여러 연결 중 하나가 실행 또는 커밋되지 않으면 모든 연결에서 현재 일괄 처리를 중지하고 에이전트가 단일 스트림을 사용하여 실패한 일괄 처리를 다시 시도합니다."

배포 에이전트는 하나의 세션을 사용하여 적용될 수 없는 일괄 처리를 다시 시도합니다. 배포 에이전트가 성공적으로 일괄 처리를 적용한 후에 다시 시작하지 않고 여러 세션을 사용하여 다시 시작됩니다.

#### <a name="commitbatchsize"></a>CommitBatchSize
- 배포 에이전트에 대해 **-CommitBatchSize** 매개 변수의 값을 늘립니다.  
  
트랜잭션 세트를 커밋할 때 오버헤드는 고정되어 있습니다. 그러므로 다수의 트랜잭션을 커밋하는 횟수를 줄이면 오버헤드가 대량의 데이터에 분산됩니다.  CommitBatchSize(최대 200)를 늘리면 더 많은 트랜잭션이 구독자에 커밋되므로 성능을 개선할 수 있습니다. 그러나 변경 내용 적용 비용은 로그가 포함된 디스크의 최대 I/O와 같은 다른 요인에 의해 제어되므로 이 매개 변수를 늘려서 얻을 수 있는 장점이 줄어듭니다. 또한 배포 에이전트를 다시 시작해야 하는 오류가 발생할 경우 많은 수의 트랜잭션을 롤백하고 다시 적용해야 한다는 것을 고려해야 합니다. 네트워크가 불안정한 경우 값을 낮게 설정하면 오류 발생 빈도가 줄어들고 오류가 발생해도 적은 수의 트랜잭션을 롤백하고 다시 적용하면 됩니다.  
  

## <a name="see-more"></a>자세히 보기
  
[복제 에이전트 프로필 작업](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
[복제 에이전트의 명령 프롬프트 매개 변수 보기 및 수정&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
[Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  
