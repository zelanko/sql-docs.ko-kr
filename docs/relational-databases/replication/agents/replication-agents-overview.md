---
title: 복제 에이전트 개요 | Microsoft 문서
description: SQL Server 복제에서 변경 내용 추적 및 데이터 배포와 관련된 작업을 수행하는 데 사용하는 에이전트에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distribution Agent
- agents [SQL Server replication]
- Queue Reader Agent, about Queue Reader Agent
- Queue Reader Agent
- Merge Agent, about Merge Agent
- Log Reader Agent, about Log Reader Agent
- replication [SQL Server], agents and profiles
- Log Reader Agent
- Distribution Agent, about Distribution Agent
- agents [SQL Server replication], about agents
- Merge Agent
- Snapshot Agent, about Snapshot Agent
- Snapshot Agent
ms.assetid: a35ecd7d-f130-483c-87e3-ddc8927bb91b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: a60d78abb92552e6413fd827d2223e507a0a439e
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890953"
---
# <a name="replication-agents-overview"></a>복제 에이전트 개요
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  복제는 에이전트라는 여러 독립 실행형 프로그램을 사용하여 변경 내용 추적 및 데이터 배포와 연관된 태스크를 수행합니다. 기본적으로 복제 에이전트는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트에서 예약된 작업으로 실행되므로 해당 작업을 실행하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트가 실행 중이어야 합니다. 복제 에이전트는 명령줄이나 RMO(복제 관리 개체)를 사용하는 애플리케이션에서 실행할 수도 있습니다. 복제 에이전트는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 모니터 및 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 관리할 수 있습니다.  
  
## <a name="sql-server-agent"></a>SQL Server 에이전트  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트는 복제에 사용되는 에이전트를 호스팅 및 예약하고 복제 에이전트를 쉽게 실행하는 방법을 제공합니다. 또한[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트는 복제 이외의 작업을 제어하고 모니터링합니다. 자세한 내용은 [Configure SQL Server Agent](../../../ssms/agent/configure-sql-server-agent.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가 설치될 때 사용자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 서비스를 자동으로 시작하도록 명시적으로 선택하지 않으면 기본적으로 이 서비스는 해제됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 서비스를 시작하는 방법은 [SQL Server 에이전트 서비스 시작, 중지 또는 일시 중지](../../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)를 참조하세요.  
  
## <a name="snapshot-agent"></a>스냅샷 에이전트  
 일반적으로 스냅샷 에이전트는 모든 복제 유형에서 사용됩니다. 스냅샷 에이전트는 게시된 테이블과 다른 개체의 스키마 및 초기 데이터 파일을 준비하고, 스냅샷 파일을 저장하고, 배포 데이터베이스의 동기화에 대한 정보를 기록합니다. 배포자에서 스냅샷 에이전트를 실행합니다. 자세한 내용은 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)을 참조하세요.  
  
## <a name="log-reader-agent"></a>로그 판독기 에이전트  
 로그 판독기 에이전트는 트랜잭션 복제와 함께 사용되며 복제 표시된 트랜잭션을 게시자의 트랜잭션 로그에서 배포 데이터베이스로 이동합니다. 트랜잭션 복제를 사용하여 게시한 각 데이터베이스에는 배포자에서 실행되고 게시자로 연결되는 자체 로그 판독기 에이전트가 있습니다. 배포자는 게시자와 동일한 컴퓨터에 있을 수 있습니다. 자세한 내용은 [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)을 참조하세요.  
  
## <a name="distribution-agent"></a>배포 에이전트  
 배포 에이전트는 스냅샷 복제 및 트랜잭션 복제와 함께 사용되며 초기 스냅샷을 구독자에 적용하고 배포 데이터베이스의 트랜잭션을 구독자로 이동합니다. 배포 에이전트는 밀어넣기 구독을 위한 배포자 또는 끌어오기 구독을 위한 구독자에서 실행됩니다. 자세한 내용은 [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)을 참조하세요.  
  
## <a name="merge-agent"></a>병합 에이전트  
 병합 에이전트는 병합 복제와 함께 사용되며 초기 스냅샷을 구독자에 적용하고 발생한 증분 데이터 변경 내용을 이동 및 조정합니다. 각 병합 구독에는 게시자 및 구독자 모두에 연결되고 모두를 업데이트하는 자체 병합 에이전트가 있습니다. 병합 에이전트는 밀어넣기 구독을 위한 배포자 또는 끌어오기 구독을 위한 구독자에서 실행됩니다. 기본적으로 병합 에이전트는 변경 내용을 구독자에서 게시자로 업로드한 다음 게시자에서 구독자로 변경 내용을 다운로드합니다. 자세한 내용은 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)을(를) 참조하세요.  
  
## <a name="queue-reader-agent"></a>큐 판독기 에이전트  
 큐 판독기 에이전트는 지연 업데이트 옵션이 있는 트랜잭션 복제와 함께 사용됩니다. 이 에이전트는 배포자에서 실행되며 구독자에서 적용한 변경 내용을 게시자로 다시 보냅니다. 배포 에이전트 및 병합 에이전트와는 달리 지정한 배포 데이터베이스에 대한 모든 게시자 및 게시에 대해 하나의 큐 판독기 인스턴스만 사용됩니다. 큐 판독기 에이전트에 대한 자세한 내용은 [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)를 참조하십시오. 업데이트할 수 있는 구독에 대한 자세한 내용은 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)을 참조하십시오.  
  
## <a name="replication-maintenance-jobs"></a>복제 유지 관리 작업  
 복제에는 예약 및 요청 시 유지 관리를 수행하는 여러 유지 관리 작업이 있습니다. 자세한 내용은 [복제 에이전트 관리](../../../relational-databases/replication/agents/replication-agent-administration.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [복제 유지 관리 작업 실행&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [복제 에이전트 관리](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
