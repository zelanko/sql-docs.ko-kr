---
description: 게시자 정보, 구독 조사 목록(트랜잭션)
title: 게시자 정보, 구독 조사 목록(트랜잭션) | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publisherinfo.subscriptionssummary.tran.f1
ms.assetid: 6bc64ddb-5c86-4681-a391-77fc1d3c4e6e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 4d335464f07ad5573a2c45fb7258152fc71d930a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470172"
---
# <a name="publisher-information-subscription-watch-list-transactional"></a>게시자 정보, 구독 조사 목록(트랜잭션)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **구독 조사 목록** 탭은 SQL Server 2005 이상 버전을 실행하는 배포자에 대해 사용할 수 있으며 선택한 게시자에서 사용 가능한 모든 게시의 구독 정보를 표시합니다. 구독 목록을 필터링하여 오류, 경고 및 성능이 저조한 구독을 볼 수 있습니다. 이 탭에서는 관리자가 게시자에서의 모든 복제 작업을 모니터링할 수 있는 단일 위치를 제공합니다. 복제 모니터는 선택한 복제 유형과 **표시** 드롭다운 목록 상자에서 선택한 옵션에 기반하여 주의가 필요한 모든 구독을 표시합니다. 이 탭에 표시되는 항목은 현재 상태와 성능에 기반하기 때문에 현재 **표시** 목록 상자의 옵션과 일치하는 구독만 이 페이지에 표시됩니다.  
  
## <a name="options"></a>옵션  
 자세한 내용 및 구독과 관련된 태스크를 보려면 해당 구독에 대한 행을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 옵션을 클릭합니다. 표에서 데이터를 표시하는 방식을 변경하려면 표를 마우스 오른쪽 단추로 클릭한 후 다음 옵션 중 하나를 클릭합니다.  
  
-   **정렬**: **열 정렬** 대화 상자에서 한 개 이상의 열에 대해 정렬합니다.  
  
-   **표시할 열 선택**: **열 선택** 대화 상자에서 표시할 열 및 해당 열이 표시되는 순서를 선택합니다.  
  
-   **필터**: **필터 설정** 대화 상자의 열 값에 따라 표의 행을 필터링합니다.  
  
-   **필터 지우기**: 표에 대한 모든 필터 설정을 지웁니다.  
  
 필터 설정은 각 표에 대해 지정됩니다. 열 선택 및 정렬은 각 게시자에 대한 게시 표와 같이 동일한 유형의 모든 표에 적용됩니다.  
  
 **트랜잭션 구독 표시**  
 선택한 게시자에 대해 표시할 구독 유형(트랜잭션, 스냅샷 또는 병합)을 선택합니다.  
  
 **표시**  
 선택한 구독 유형에 대해 표시할 구독 상태를 선택합니다. 예를 들어 오류가 있는 구독만 표시하도록 선택할 수 있습니다.  
  
 **상태**  
 배포 에이전트 또는 로그 판독기 에이전트의 상태로 파악할 수 있는 각 구독의 상태입니다. 우선 순위가 높은 상태가 표시되며 지연 업데이트 구독을 사용하는 경우 큐 판독기 에이전트로 상태를 파악할 수도 있습니다.  
  
 기본적으로 구독 정보가 들어 있는 표는 **상태** 열을 기준으로 정렬한 다음 상태가 같은 구독을 **성능** 열을 기준으로 정렬합니다. 다음 목록에서는 가능한 상태 값 및 값 정렬 순서를 보여 줍니다. 예를 들어 오류는 항상 표의 맨 위에 표시됩니다.  
  
-   Error  
  
-   성능 심각  
  
-   곧 만료됨/만료됨  
  
-   초기화되지 않은 구독  
  
-   실패한 명령 다시 시도 중  
  
-   실행 중이 아님  
  
-   실행 중  
  
 정렬 순서는 지정한 구독의 상태가 두 가지 이상일 경우에 표시할 값도 결정합니다. 예를 들어 구독에 오류가 있고 곧 만료될 예정이면 **상태** 열에 **오류**가 표시됩니다.  
  
 **성능 심각**, **곧 만료됨/만료됨**및 **초기화되지 않은 구독** 상태 값은 경고입니다. 경고를 표시할 때 **상태** 열은 에이전트가 실행 중인지 여부도 표시합니다. 예를 들어 상태가 **실행 중, 성능 심각**과 같이 표시될 수 있습니다.  
  
 **성능 심각** 및 **곧 만료됨/만료됨** 상태 값은 임계값이 설정된 경우에만 표시됩니다. 성능 측정 및 임계값 설정에 대한 자세한 내용은 [복제 모니터로 성능 모니터링](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) 및 [복제 모니터에 임계값 및 경고 설정](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)을 참조하세요.  
  
 **구독**  
 각 구독의 이름으로 *SubscriberName: SubscriptionDatabaseName*형식입니다.  
  
 **게시**  
 구독을 동기화할 게시의 이름이며 *PublicationDatabaseName: PublicationName*형식입니다.  
  
 **성능**  
 각 구독의 성능 등급은 복제 모니터에서 측정한 가장 최근의 측정값을 기반으로 하며 이전 성능은 반영하지 않습니다. 성능 임계값이 정의된 게시의 구독에 대해 성능을 측정합니다. 게시에 대해 성능 임계값을 정의하지 않으면 이 열에 **사용 안 함**이 표시됩니다. 성능 등급은 다음 값 중 하나입니다.  
  
-   우수  
  
-   좋음  
  
-   보통  
  
-   나쁨  
  
-   위험  
  
 성능 상태가 심각하면 **상태** 열에 **성능 심각** 이 표시됩니다. 성능 등급 정의 방법 및 성능 임계값 설정 방법은 [복제 모니터로 성능 모니터링](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)을 참조하세요.  
  
 **대기 시간**  
 게시자에서 트랜잭션이 커밋되는 시점과 구독자에서 해당 트랜잭션이 커밋되는 시점 간의 평균 시간입니다. 표시되는 대기 시간은 복제 모니터에서 측정한 가장 최근의 측정값을 기반으로 합니다. 대기 시간 측정에 대한 자세한 내용은 [트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)를 참조하세요.  
  
 **마지막 동기화**  
 배포 에이전트가 마지막으로 실행된 시간입니다. 동기화가 진행 중인 경우 **진행 중** 이 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [게시자에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
