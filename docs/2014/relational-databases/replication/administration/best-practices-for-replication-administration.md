---
title: 복제 관리에 대한 모범 사례 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- administering replication, best practices
- replication [SQL Server], administering
ms.assetid: 850e8a87-b34c-4934-afb5-a1104f118ba8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fb7a972d865f7afe1295c5dbdf5ad3ce0c886556
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62629635"
---
# <a name="best-practices-for-replication-administration"></a>최선의 복제 관리 방법
  복제를 구성한 후에는 복제 토폴로지 관리 방법을 이해하는 것이 중요합니다. 이 항목에서는 다양한 영역의 작업에 대한 기본적인 수행 방법과 각 영역에 대한 추가 정보를 제공하는 링크를 제공합니다. 이 항목에 제시 된 최선의 방법 지침을 수행 하는 것 외에도 숙지 일반적인 질문 사항과 문제점에 자주 묻는 질문 항목을 고려 합니다. [복제 관리자를 위한 질문과 대답](frequently-asked-questions-for-replication-administrators.md).  
  
 최선의 수행 방법을 다음과 같은 두 가지 영역으로 나누면 이해가 쉽습니다.  
  
-   다음 정보는 모든 복제 토폴로지에 대해 구현해야 하는 최선의 방법에 대해 설명합니다.  
  
    -   백업과 복원 전략 개발 및 테스트  
  
    -   복제 토폴로지 스크립팅  
  
    -   임계값 및 경고 만들기  
  
    -   복제 토폴로지 모니터링  
  
    -   성능 기준선 설정 및 복제 튜닝(필요한 경우)  
  
-   다음 정보는 토폴로지에 대해 고려할 최선의 방법입니다(필수는 아님).  
  
    -   주기적으로 데이터 유효성 검사  
  
    -   프로필을 통해 에이전트 매개 변수 조정  
  
    -   게시 및 배포 보존 기간 조정  
  
    -   애플리케이션 요구 사항이 변경된 경우 아티클 및 게시 속성을 변경하는 방법 이해  
  
    -   애플리케이션 요구 사항이 변경된 경우 스키마를 변경하는 방법 이해  
  
## <a name="develop-and-test-a-backup-and-restore-strategy"></a>백업과 복원 전략 개발 및 테스트  
 모든 데이터베이스는 정기적으로 백업되어야 하고 이러한 백업을 복원하는 기능도 정기적으로 테스트해야 합니다. 복제된 데이터베이스도 마찬가지입니다. 다음 데이터베이스는 반드시 정기적으로 백업되어야 합니다.  
  
-   게시 데이터베이스  
  
-   배포 데이터베이스  
  
-   구독 데이터베이스  
  
-   게시자, 배포자 및 모든 구독자의**msdb** 데이터베이스 및 **master** 데이터베이스  
  
 복제된 데이터베이스의 경우 데이터를 백업 및 복원할 때 특별히 주의를 기울여야 합니다. 자세한 내용은 [복제된 데이터베이스 백업 및 복원](back-up-and-restore-replicated-databases.md)을 참조하세요.  
  
## <a name="script-the-replication-topology"></a>복제 토폴로지 스크립팅  
 토폴로지의 모든 복제 구성 요소는 재해 복구 계획의 일부로 스크립팅되어야 하며 반복 태스크를 자동화하는 데도 스크립트를 사용할 수 있습니다. 스크립트에는 게시 또는 구독과 같이 스크립팅된 복제 구성 요소를 구현하는 데 필요한 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 시스템 저장 프로시저가 포함되어 있습니다. 구성 요소를 만든 후에 마법사(예: 새 게시 마법사) 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 에서 스크립트를 만들 수 있습니다. [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 **sqlcmd**를 사용하여 스크립트를 확인, 수정 및 실행할 수 있습니다. 백업 파일과 함께 스크립트를 저장하여 복제 토폴로지를 다시 구성할 때 사용할 수 있습니다. 자세한 내용은 [Scripting Replication](../scripting-replication.md)을 참조하세요.  
  
 속성이 변경된 경우 구성 요소를 다시 스크립팅해야 합니다. 트랜잭션 복제에서 사용자 지정 저장 프로시저를 사용할 경우 각 프로시저의 복사본을 스크립트와 함께 저장해야 합니다. 프로시저가 변경되면 복사본도 업데이트해야 합니다. 일반적으로 프로시저는 스키마가 변경되거나 애플리케이션 요구 사항이 변경될 때 업데이트됩니다. 사용자 지정 프로시저에 대한 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
## <a name="establish-performance-baselines-and-tune-replication-if-necessary"></a>성능 기준선 설정 및 복제 튜닝(필요한 경우)  
 복제를 구성하기 전에 복제 성능에 영향을 주는 요소를 익혀 두는 것이 좋습니다.  
  
-   서버 및 네트워크 하드웨어  
  
-   데이터베이스 디자인  
  
-   배포자 구성  
  
-   게시 디자인 및 옵션  
  
-   필터 디자인 및 사용  
  
-   구독 옵션  
  
-   스냅숏 옵션  
  
-   에이전트 매개 변수  
  
-   유지 관리  
  
 복제를 구성한 다음에는 애플리케이션 및 토폴로지에 일반적으로 사용되는 작업과의 복제 작동 방식을 결정할 수 있는 성능 기준선을 만드는 것이 좋습니다. 복제 모니터 및 시스템 모니터를 사용하여 다음과 같은 5가지 복제 성능의 일반적인 수치를 확인할 수 있습니다.  
  
-   대기 시간: 복제 토폴로지의 노드 간에 데이터 변경 내용을 전파하는 데 소요되는 시간  
  
-   처리량: 시간에 따라 시스템에서 지속할 수 있는 복제 작업의 양(특정 기간 동안 배달된 명령으로 측정)  
  
-   동시성: 시스템에서 동시에 작동될 수 있는 복제 프로세스의 수  
  
-   동기화 기간: 지정된 동기화를 완료하는 데 소요되는 시간  
  
-   리소스 소비량: 복제 처리의 결과로 사용되는 하드웨어 및 네트워크 리소스  
  
 트랜잭션 복제를 기반으로 구축된 시스템은 일반적으로 짧은 대기 시간과 높은 처리량을 요구하므로 대기 시간과 처리량은 트랜잭션 복제에서 가장 중요한 요소입니다. 병합 복제 위에 구축된 시스템에는 대개 많은 수의 구독자가 존재하며 게시자와 이러한 구독자 간에 상당히 많은 동시 동기화 작업이 수행될 수 있으므로 동시성과 동기화 기간은 병합 복제에서 가장 중요한 요소입니다.  
  
 기준 수치를 설정한 후에 복제 모니터에서 임계값을 설정합니다. 자세한 내용은 [복제 모니터에 임계값 및 경고 설정](../monitor/set-thresholds-and-warnings-in-replication-monitor.md) 및 [복제 에이전트 이벤트에 대한 경고 사용](../agents/use-alerts-for-replication-agent-events.md)을 참조하세요. 성능 문제가 발생하면 위에 나열된 성능 향상 항목의 제안 사항을 읽어 보고 발생한 문제점에 영향을 주는 영역에서 필요한 사항을 변경하는 것이 좋습니다.  
  
## <a name="create-thresholds-and-alerts"></a>임계값 및 경고 만들기  
 복제 모니터를 사용하면 상태 및 성능과 관련된 여러 임계값을 설정할 수 있습니다. 사용하는 토폴로지에 적합한 임계값을 설정하는 것이 좋습니다. 임계값에 도달하면 경고가 표시되며 선택적으로 경고를 전자 메일 계정, 호출기 또는 다른 디바이스로 보낼 수 있습니다. 자세한 내용은 [복제 모니터에 임계값 및 경고 설정](../monitor/set-thresholds-and-warnings-in-replication-monitor.md)를 참조하세요.  
  
 모니터링 임계값과 연결시킬 수 있는 경고 외에 복제는 복제 에이전트 동작에 응답하는 미리 정의된 여러 가지 경고를 제공합니다. 관리자가 이러한 경고를 사용하면 복제 토폴로지의 상태에 대한 정보를 계속 받아볼 수 있습니다. 경고에 대해 설명하는 항목을 자세히 읽고 관리 요구 사항에 맞는 경고를 사용하는 것이 좋습니다. 필요한 경우에는 추가 경고를 만들 수도 있습니다. 자세한 내용은 [복제 에이전트 이벤트에 대한 경고 사용](../agents/use-alerts-for-replication-agent-events.md)을 참조하세요.  
  
## <a name="monitor-the-replication-topology"></a>복제 토폴로지 모니터링  
 복제 토폴로지를 적용하고 임계값과 경고를 구성한 다음에는 복제를 정기적으로 모니터링하는 것이 좋습니다. 복제 토폴로지의 모니터링은 복제 배포의 중요한 부분입니다. 복제 작업이 배포되므로 복제에 관련된 모든 컴퓨터에서 활동 및 상태를 추적해야 합니다. 다음 도구를 사용하여 복제를 모니터링할 수 있습니다.  
  
-   복제 모니터는 복제를 모니터링하는 가장 중요한 도구로 이를 사용하여 복제 토폴로지의 전체적 상태를 모니터링할 수 있습니다. 자세한 내용은 [Monitoring Replication](../monitoring-replication.md)을 참조하세요.  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] 및 RMO(복제 관리 개체)는 복제 모니터링을 위한 인터페이스를 제공합니다. 자세한 내용은 [Monitoring Replication](../monitoring-replication.md)을 참조하세요.  
  
-   복제 성능을 모니터링하는 데에는 시스템 모니터도 유용할 수 있습니다. 자세한 내용은 [Monitoring Replication with System Monitor](../monitor/monitoring-replication-with-system-monitor.md)을 참조하세요.  
  
## <a name="validate-data-periodically"></a>주기적으로 데이터 유효성 검사  
 복제에 대해 유효성 검사를 반드시 수행할 필요는 없지만 트랜잭션 복제 및 병합 복제에 대해 주기적으로 유효성 검사를 실행하는 것이 좋습니다. 유효성 검사를 사용하면 구독자의 데이터가 게시자의 데이터와 일치하는지 확인할 수 있습니다. 유효성 검사 성공은 검사를 수행한 시점에 게시자의 모든 변경 내용이 구독자로 복제되어(구독자에 업데이트가 지원되는 경우에는 구독자에서 게시자로도 복제됨) 두 데이터베이스가 동기화 상태에 있음을 나타냅니다.  
  
 유효성 검사를 게시 데이터베이스의 백업 일정에 따라 수행하는 것이 좋습니다. 예를 들어 게시 데이터베이스를 일주일에 한 번 전체 백업하면 유효성 검사도 일주일에 한 번 백업이 완료된 후에 실행할 수 있습니다. 자세한 내용은 [복제된 데이터의 유효성 검사](../validate-data-at-the-subscriber.md)를 참조하세요.  
  
## <a name="use-agent-profiles-to-change-agent-parameters-if-necessary"></a>에이전트 프로필을 사용하여 에이전트 매개 변수 변경(필요한 경우)  
 에이전트 프로필은 복제 에이전트 매개 변수를 설정하는 편리한 방법을 제공합니다. 매개 변수를 에이전트 명령줄에서 지정할 수도 있지만 일반적으로 미리 정의된 에이전트 프로필을 사용하거나 매개 변수 값을 변경해야 할 경우에는 새 프로필을 만드는 것이 더 적합합니다. 예를 들어 병합 복제를 사용하고 구독자가 광대역 연결에서 전화 접속 연결로 이동하는 경우에는 병합 에이전트에 대해 느린 통신 연결에 더 적합한 매개 변수 집합을 사용하는 **느린 연결** 프로필을 사용하십시오. 자세한 내용은 [Replication Agent Profiles](../agents/replication-agent-profiles.md)을(를) 참조하세요.  
  
## <a name="adjust-publication-and-distribution-retention-periods-if-necessary"></a>게시 및 배포 보존 기간 조정(필요한 경우)  
 트랜잭션 복제 및 병합 복제는 보존 기간을 사용하여 각각 트랜잭션이 배포 데이터베이스에 저장되는 기간과 구독이 동기화되어야 하는 빈도를 결정합니다. 설정을 조정해야 할지 여부를 판단하기 위해 토폴로지를 모니터링하는 경우에는 초기 기본 설정을 사용하는 것이 좋습니다. 예를 들어 병합 복제의 경우 게시 보존 기간(기본값: 14일)은 시스템 테이블에 메타데이터를 저장하는 기간을 결정합니다. 구독이 항상 5일 이내에 동기화되는 경우 설정을 낮게 조정하면 메타데이터가 줄어들고 성능이 향상될 수 있습니다. 자세한 내용은 [Subscription Expiration and Deactivation](../subscription-expiration-and-deactivation.md)을 참조하세요.  
  
## <a name="understand-how-to-modify-publications-if-application-requirements-change"></a>애플리케이션 요구 사항이 변경된 경우 게시 수정 방법 이해  
 게시를 만든 후에 아티클을 추가 또는 삭제하거나 게시 및 아티클 속성을 변경해야 할 수 있습니다. 게시가 생성된 후에는 대부분의 변경이 허용되지만 일부 경우에 게시에 대한 스냅숏을 새로 생성하거나 게시에 대한 구독을 다시 초기화해야 합니다. 자세한 내용은 [게시 및 아티클 속성 변경](../publish/change-publication-and-article-properties.md) 및 [기존 게시에 대한 아티클 추가 및 삭제](../publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.  
  
## <a name="understand-how-to-make-schema-changes-if-application-requirements-change"></a>애플리케이션 요구 사항이 변경된 경우 스키마 변경 방법 이해  
 _대부분의 경우 애플리케이션을 제작한 후에 스키마를 변경해야 합니다. 복제 토폴로지에서는 이러한 변경 내용을 모든 구독자에 전파해야 하는 경우가 많습니다. 복제는 게시된 개체에 대한 다양한 스키마 변경을 지원합니다.  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 게시자에 게시된 개체에 대해 다음 스키마 변경을 수행하면 기본적으로 모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구독자에 변경 내용이 전파됩니다.  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 자세한 내용은 [게시 데이터베이스의 스키마 변경](../publish/make-schema-changes-on-publication-databases.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [복제 관리 FAQ](frequently-asked-questions-for-replication-administrators.md)  
  
  
