---
title: 복제 토폴로지 정지(복제 SP)
description: 복제 저장 프로시저를 사용하여 SQL Server의 복제 토폴로지를 정지하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- administering replication, quiescing
- quiesce [SQL Server replication]
- transactional replication, backup and restore
ms.assetid: 7626d575-9994-47be-b772-5b6f1b7ef7ca
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 1db75568779b7675a072467678e6be4004ec2698
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86158881"
---
# <a name="quiesce-a-replication-topology-replication-transact-sql-programming"></a>복제 토폴로지 정지(복제 Transact-SQL 프로그래밍)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/applies-to-version/sql-asdbmi.md)]
  시스템*정지* 과정에서는 모든 노드에서 게시된 테이블에 대한 작업을 중지하고 각 노드가 다른 모든 노드의 변경 내용을 받았는지 확인합니다. 이 항목에서는 여러 가지 관리 태스크에 필요한 복제 토폴로지 정지 방법과 노드가 다른 노드의 변경 내용을 모두 받았는지 확인하는 방법을 설명합니다.  
  
### <a name="to-quiesce-a-transactional-replication-topology-with-read-only-subscriptions"></a>읽기 전용 구독이 포함된 트랜잭션 복제 토폴로지를 정지하려면  
  
1.  게시자에서 게시된 모든 테이블에 대한 작업을 중지합니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_posttracertoken&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql.md)을 실행합니다.  
  
3.  게시 데이터베이스의 게시자에서 [sp_helptracertokenhistory](../../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)를 실행합니다.  
  
4.  각 구독자가 추적 프로그램 토큰을 받았는지 확인합니다.  

### <a name="to-quiesce-a-transactional-replication-topology-with-updatable-subscriptions"></a>업데이트 가능 구독이 포함된 트랜잭션 복제 토폴로지를 정지하려면  
  
1.  게시자 및 모든 구독자에서 게시된 모든 테이블에 대한 작업을 중지합니다.  
  
2.  구독자가 지연 업데이트 구독을 사용하는 경우  
  
    1.  큐 판독기 에이전트가 연속 모드로 실행되지 않는 경우 해당 에이전트를 실행합니다. 에이전트 실행에 대한 자세한 내용은 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) 또는 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)를 참조하세요.  
  
    2.  큐가 비어 있는지 확인하려면 각 구독자에서 [sp_replqueuemonitor](../../../relational-databases/system-stored-procedures/sp-replqueuemonitor-transact-sql.md) 를 실행합니다.  
  
3.  게시 데이터베이스의 게시자에서 [sp_posttracertoken](../../../relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql.md)을 실행합니다.  
  
4.  게시 데이터베이스의 게시자에서 [sp_helptracertokenhistory](../../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)를 실행합니다.  
  
5.  각 구독자가 추적 프로그램 토큰을 받았는지 확인합니다.  
  
### <a name="to-quiesce-a-peer-to-peer-transactional-replication-topology"></a>피어 투 피어 트랜잭션 복제 토폴로지를 정지하려면  
  
1.  모든 노드에서 게시된 모든 테이블에 대한 작업을 중지합니다.  
  
2.  토폴로지의 각 게시 데이터베이스에서 [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) 를 실행합니다.  
  
3.  로그 판독기 에이전트 또는 배포 에이전트가 연속 모드로 실행되지 않는 경우 해당 에이전트를 실행합니다. 로그 판독기 에이전트는 배포 에이전트보다 먼저 시작해야 합니다. 에이전트 실행에 대한 자세한 내용은 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) 또는 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)를 참조하세요.  
  
4.  토폴로지의 각 게시 데이터베이스에서 [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) 를 실행합니다. 결과 집합에 각각의 다른 노드에서 받은 응답이 들어 있는지 확인합니다.  
  
### <a name="to-ensure-a-peer-to-peer-node-has-received-all-prior-changes"></a>피어 투 피어 노드가 이전의 모든 변경 내용을 받았는지 확인하려면  
  
1.  확인할 노드의 게시 데이터베이스에서 [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) 를 실행합니다.  
  
2.  로그 판독기 에이전트 또는 배포 에이전트가 연속 모드로 실행되지 않는 경우 해당 에이전트를 실행합니다. 로그 판독기 에이전트는 배포 에이전트보다 먼저 시작해야 합니다. 에이전트 실행에 대한 자세한 내용은 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) 또는 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)를 참조하세요.  
  
3.  확인할 노드의 게시 데이터베이스에서 [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) 를 실행합니다. 결과 집합에 각각의 다른 노드에서 받은 응답이 들어 있는지 확인합니다.  
  
### <a name="to-quiesce-a-merge-replication-topology"></a>병합 복제 토폴로지를 정지하려면  
  
1.  게시자 및 모든 구독자에서 게시된 모든 테이블에 대한 작업을 중지합니다.  
  
2.  각 구독에 대해 병합 에이전트를 두 번 실행합니다. 첫 번째 실행에서는 모든 구독을 동기화하고 두 번째 실행에서는 각 구독을 동기화합니다. 이렇게 하면 모든 변경 내용이 모든 노드에 복제됩니다. 에이전트 실행에 대한 자세한 내용은 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) 또는 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)를 참조하세요.  
  
    > [!NOTE]  
    >  동기화 중 충돌이 발생하면 병합 에이전트를 두 번 실행한 후 충돌 해결에 필요한 변경 내용이 모든 노드에 전파되지 않을 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [피어 투 피어 토폴로지 관리&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
