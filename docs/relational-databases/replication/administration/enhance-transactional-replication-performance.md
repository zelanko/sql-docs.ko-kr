---
title: "트랜잭션 복제 성능 향상 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "게시물 [SQL Server 복제], 디자인 및 성능"
  - "성능 [SQL Server 복제], 트랜잭션 복제"
  - "데이터베이스 디자인 [SQL Server], 복제 성능"
  - "성능 [SQL Server 복제], 스냅숏 복제"
  - "스냅숏 복제 [SQL Server], 성능"
  - "구독 [SQL Server 복제], 성능 고려 사항"
  - "에이전트 [SQL Server 복제], 성능"
  - "배포 에이전트, 성능"
  - "트랜잭션 복제, 성능"
  - "로그 판독기 에이전트, 성능"
ms.assetid: 67084a67-43ff-4065-987a-3b16d1841565
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 트랜잭션 복제 성능 향상
  [일반적인 복제 성능 향상](../../../relational-databases/replication/administration/enhance-general-replication-performance.md)에 설명된 일반 성능 팁을 살펴본 후에 트랜잭션 복제에 해당하는 이러한 추가 영역을 살펴보십시오.  
  
## 데이터베이스 디자인  
  
-   응용 프로그램 디자인에서 트랜잭션 크기를 최소화합니다.  
  
     기본적으로 트랜잭션 복제는 트랜잭션 경계에 따라 변경 내용을 전파합니다. 트랜잭션이 작을수록 배포 에이전트가 네트워크 문제로 인해 트랜잭션을 다시 전송해야 할 확률이 낮아집니다. 에이전트가 트랜잭션을 다시 전송해야 할 경우 보내는 데이터 양은 적어집니다.  
  
## 배포자 구성  
  
-   전용 서버에서 배포자를 구성합니다.  
  
     원격 배포자를 구성하여 게시자에서 처리 오버헤드를 줄일 수 있습니다. 자세한 내용은 참조 [배포 구성](../../../relational-databases/replication/configure-distribution.md)합니다.  
  
-   배포 데이터베이스 크기를 적절히 조정합니다.  
  
     시스템에서 명령 저장에 필요한 공간을 결정할 수 있도록 일반적인 로드 상태에서 복제를 테스트합니다. 데이터베이스는 자주 자동 증가되지 않고도 명령을 저장할 수 있을 만큼 충분히 커야 합니다. 데이터베이스의 크기를 변경 하는 방법에 대 한 자세한 내용은 참조 [ALTER DATABASE & #40; TRANSACT-SQL & #41;](../../../t-sql/statements/alter-database-transact-sql.md)합니다.  
  
## 게시 디자인  
  
-   게시된 테이블을 일괄로 업데이트할 때 저장 프로시저 실행을 복제합니다.  
  
     구독자의 다수 행에 가끔씩 영향을 미치는 일괄 처리 업데이트가 있는 경우 저장 프로시저를 사용하여 게시된 테이블을 업데이트하고 저장 프로시저의 실행을 게시해 보십시오. 배포 에이전트는 영향을 받은 모든 행의 업데이트나 삭제를 보내는 대신 구독자에서 같은 매개 변수 값으로 동일한 프로시저를 실행합니다. 자세한 내용은 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)를 참조하세요.  
  
-   여러 게시 간에 아티클을 분산시킵니다.  
  
     사용할 수 없는 경우는 **-SubscriptionStreams** 매개 변수 (이 항목의 뒷부분에 설명)과 여러 게시를 만드는 것이 좋습니다. 이러한 게시에 아티클을 분산시키면 복제가 구독자에게 변경 내용을 병렬로 적용할 수 있습니다.  
  
## 구독 고려 사항  
  
-   같은 게시자에 여러 게시가 있을 경우 공유 에이전트가 아닌 독립 에이전트를 사용합니다. 새 게시 마법사에서는 이것이 기본값입니다.  
  
-   에이전트를 잦은 간격으로 실행하는 대신 계속 실행합니다.  
  
     일정을 분 단위처럼 자주 실행하도록 설정하는 대신 계속 실행되도록 설정하면 에이전트를 시작하고 중지할 필요가 없으므로 복제 성능이 향상됩니다. 배포 에이전트가 계속 실행되도록 설정하면 변경 내용이 토폴로지에 연결된 다른 서버로 짧은 대기 시간 내에 전파됩니다. 참조 항목:  
  
    -   [! INCLUDE [ssManStudioFull] (.. / Token/ssManStudioFull_md.md)]: [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
## 배포 에이전트 및 로그 판독기 에이전트 매개 변수  
  
-   사용 하 여 실수로 일회성 병목 상태를 해결 하려면는 **– MaxCmdsInTran** 로그 판독기 에이전트에 대 한 매개 변수입니다.  
  
     **–MaxCmdsInTran** 매개 변수는 로그 판독기가 배포 데이터베이스에 대해 명령을 쓸 때 트랜잭션으로 그룹화된 최대 문 개수를 지정합니다. 이 매개 변수를 사용하면 구독자에서 명령을 적용할 때 로그 판독기 에이전트와 배포 에이전트가 게시자에서 큰 트랜잭션(여러 명령으로 구성됨)을 여러 개의 작은 트랜잭션으로 나눌 수 있습니다. 이 매개 변수를 지정하면 배포자에서 경합을 줄일 수 있고 게시자와 구독자 간 대기 시간을 줄일 수 있습니다. 원래 트랜잭션이 작은 단위로 적용되므로 구독자는 엄격한 트랜잭션 원자성을 깨고 원래 트랜잭션이 끝나기 전에 큰 논리적 게시자 트랜잭션의 행에 액세스할 수 있습니다. 기본값은 **0**으로 게시자의 트랜잭션 경계를 유지합니다. 이 매개 변수는 Oracle 게시자에는 적용되지 않습니다.  
  
    > [!WARNING]  
    >  **MaxCmdsInTran** 은 항상 설정되도록 설계되지 않았습니다. 단일 트랜잭션에 많은 DML 작업을 실수로 수행한 경우의 문제(전체 트랜잭션이 배포 데이터베이스에 있고 잠금이 보유될 때까지 명령 배포에 지연 발생)를 해결하기 위한 것입니다. 정기적으로 이 상황이 발생하는 경우 응용 프로그램을 검토하고 트랜잭션 크기를 줄일 수 있는 방법을 찾아야 합니다.  
  
-   배포 에이전트에 대해 **–SubscriptionStreams** 매개 변수를 사용합니다.  
  
     **–SubscriptionStreams** 매개 변수는 집계 복제 처리량을 크게 높일 수 있습니다. 이 매개 변수는 변경 내용의 일괄 처리를 병렬로 적용하기 위해 구독자에 여러 연결을 설정하도록 허용하지만 단일 스레드를 사용할 때 나타나는 여러 가지 트랜잭션 특징을 유지합니다. 여러 연결 중 하나가 실행 또는 커밋되지 않으면 모든 연결에서 현재 일괄 처리를 중지하고 에이전트가 단일 스트림을 사용하여 실패한 일괄 처리를 다시 시도합니다. 이러한 재시도 단계가 완료되기 전에는 구독자에 임시 트랜잭션 불일치가 발생할 수 있으며 실패한 일괄 처리가 성공적으로 커밋되면 구독자의 트랜잭션 일관성이 다시 유지됩니다.  
  
     사용 하 여이 에이전트 매개 변수의 값을 지정할 수는 **@subscriptionstreams** 의 [sp_addsubscription (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다.  
  
-   값 늘리기는 **-ReadBatchSize** 로그 판독기 에이전트에 대 한 매개 변수입니다.  
  
     로그 판독기 에이전트와 배포 에이전트는 트랜잭션 읽기 및 커밋 작업을 위한 일괄 처리 크기를 지원합니다. 일괄 처리 크기는 기본적으로 500개 트랜잭션입니다. 로그 판독기 에이전트는 트랜잭션의 복제 표시 여부에 상관없이 로그에서 특정 트랜잭션 수를 읽습니다. 많은 수의 트랜잭션이 게시 데이터베이스에 기록 됩니다 하는 경우 그 중 작은 하위 집합만 복제용으로 표시 되어 사용 해야는 **-ReadBatchSize** 매개 변수는 로그 판독기 에이전트의 읽기 일괄 처리 크기를 늘려야 합니다. 이 매개 변수는 Oracle 게시자에는 적용되지 않습니다.  
  
-   값 늘리기는 **-CommitBatchSize** 배포 에이전트에 대 한 매개 변수입니다.  
  
     트랜잭션 세트를 커밋할 때 오버헤드는 고정되어 있습니다. 그러므로 다수의 트랜잭션을 커밋하는 횟수를 줄이면 오버헤드가 대량의 데이터에 분산됩니다. 그러나 변경 내용 적용 비용은 로그가 포함된 디스크의 최대 I/O와 같은 다른 요인에 의해 제어되므로 이 매개 변수를 늘려서 얻을 수 있는 장점이 줄어듭니다. 또한 배포 에이전트를 다시 시작해야 하는 오류가 발생할 경우 많은 수의 트랜잭션을 롤백하고 다시 적용해야 한다는 것을 고려해야 합니다. 네트워크가 불안정한 경우 값을 낮게 설정하면 오류 발생 빈도가 줄어들고 오류가 발생해도 적은 수의 트랜잭션을 롤백하고 다시 적용하면 됩니다.  
  
-   값을 줄이려면는 **-PollingInterval** 로그 판독기 에이전트에 대 한 매개 변수입니다.  
  
      **-PollingInterval** 매개 변수 게시 데이터베이스의 트랜잭션 로그가 복제할 트랜잭션에 대해 쿼리 되는 빈도 지정 합니다. 기본값은 5초입니다. 이 값을 줄이면 로그가 더 자주 폴링되므로 게시 데이터베이스에서 배포 데이터베이스로 트랜잭션을 배달할 때 대기 시간을 줄일 수 있습니다. 그러나 자주 폴링하면 서버의 로드가 증가하므로 적절한 대기 시간과 서버 로드 간의 균형을 맞춰야 합니다.  
  
 에이전트 프로필 및 명령줄에서 에이전트 매개 변수를 지정할 수 있습니다. 참조 항목:  
  
-   [복제 에이전트 프로필 작업](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [보기 및 복제 에이전트 명령 프롬프트 매개 변수 & #40; 수정 SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)  
  
-   [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  