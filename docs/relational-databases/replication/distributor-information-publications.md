---
description: 배포자 정보, 게시
title: 배포자 정보, 게시 | Microsoft 문서
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.Distributor.Publications.f1
- sql13.rep.monitor.Distributor.commonjobs..f1
- sql13.rep.monitor.Distributor.SubscriptionSummary.merge.f1
- sql13.rep.monitor.Distributor.SubscriptionSummary.snapshot.f1
- sql13.rep.monitor.Distributor.SubscriptionSummary.tran.f1
ms.assetid: 1f499277-7f12-42ba-8cf4-52b683434944
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: b5fb4f1788ed3812490ca0e730f854b18c64e6ad
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464794"
---
# <a name="distributor-information-publications"></a>배포자 정보, 게시
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **게시** 탭은 왼쪽 창에서 선택한 배포자에서의 모든 게시에 대한 요약 정보를 제공합니다.  
  
배포자에서 지원하는 게시에 대해 표시되는 정보에는 게시자의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 있는 열이 포함됩니다. 그 밖에 표시되는 게시 정보는 복제 모니터의 게시자 뷰에서 게시를 볼 때 제공되는 게시 정보와 같습니다. **게시** 탭의 열에 대한 자세한 내용은 [Publisher Information, Publications](../../relational-databases/replication/publisher-information-publications.md)를 참조하십시오.  

## <a name="subscription-watch-list"></a>구독 조사 목록

### <a name="transactional-replication"></a>트랜잭션 복제
  트랜잭션 구독 정보는 게시자 이름을 포함합니다. 그 밖에 이 대화 상자에 제공되는 기능 및 정보는 게시자 뷰와 동일합니다. 이 대화 상자를 사용하는 방법은 [게시자 정보, 구독 조사 목록&#40;트랜잭션 게시, SQL Server 2005 이상&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-transactional.md)을 참조하세요. 

### <a name="merge-replication"></a>병합 복제
  병합 게시 구독 정보는 게시자 이름을 포함합니다. 그 밖에 이 대화 상자에 제공되는 기능 및 정보는 게시자 뷰와 동일합니다. 이 대화 상자를 사용하는 방법은 [게시자 정보, 구독 조사 목록&#40;병합 게시, SQL Server 2005 이상&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-merge-publication.md)을 참조하세요.  

### <a name="snapshot-replication"></a>스냅샷 복제 
  스냅샷 게시 구독 정보는 게시자 이름을 포함합니다. 그 밖에 이 대화 상자에 제공되는 기능 및 정보는 게시자 뷰와 동일합니다. 이 대화 상자를 사용하는 방법은 [게시자 정보, 구독 조사 목록&#40;스냅샷 게시, SQL Server 2005 이상&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-snapshot.md)을 참조하세요.  

## <a name="agents"></a>에이전트
**에이전트** 탭에는 게시자 및 구독자와 연결된 에이전트 및 유지 관리 작업에 대한 정보가 표시됩니다.  
  
 배포자 뷰의 배포자에 대한 **에이전트** 탭에서 사용할 수 있는 에이전트에는 게시자에 대한 **에이전트** 탭에서 사용할 수 있는 모든 에이전트가 포함됩니다. 그러나 배포자 뷰의 배포자에 대한 **에이전트** 탭에는 배포자 에이전트와 병합 에이전트도 포함됩니다.  
  
 스냅샷, 로그 판독기 및 큐 판독기 에이전트와 유지 관리 작업에 대한 자세한 내용은 [Publisher Information, Agents](../../relational-databases/replication/publisher-information-agents.md)를 참조하십시오. 배포자에 대한 **에이전트** 탭에 있는 에이전트 정보를 표시하면 스냅샷 및 로그 판독기 에이전트에 대한 게시자 정보가 제공됩니다. 그러나 배포자 뷰의 배포자에 대한 **에이전트** 탭에서는 **배포자 에이전트** 및 **병합 에이전트** 를 선택할 수도 있습니다.  
  
### <a name="options"></a>옵션  
 다음 섹션에서는 이 탭에서 배포자 에이전트 및 병합 에이전트에 대해 표시되는 데이터를 설명합니다.  
  
### <a name="distributor-agent"></a>배포자 에이전트  
 **상태**  
 에이전트의 상태입니다. 다음 목록에서는 가능한 상태 값을 보여 줍니다.  
  
-   오류    
-   재시도    
-   실행 중    
-   실행 중이 아님   
-   시작한 적 없음  
  
 **게시자**  
 게시자의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스입니다.  
  
 **게시**  
 에이전트와 연결된 게시의 이름입니다.  
  
 **구독**  
 [*SubscriberName*].[*Database*]와(과) 같은 형식의 구독 이름입니다.  
  
 **유형**  
 복제 유형(밀어넣기, 끌어오기 또는 익명)입니다.  
  
 **마지막 시작 시간**  
 마지막으로 에이전트가 시작된 시간입니다.  
  
 **Duration**  
 에이전트가 실행된 기간입니다. 에이전트가 현재 실행되고 있는 경우 이 시간은 경과된 시간을 나타내고 에이전트가 이전에 실행된 경우에는 총 시간을 나타냅니다.  
  
 **마지막 동작**  
 가장 최근의 에이전트 실행에서 수행된 마지막 동작입니다.  
  
 **배달 속도**  
 가장 최근에 에이전트를 실행할 때 배포 데이터베이스에서 초기화 명령이 커밋된 속도(초당 명령 수)입니다.  
  
 **대기 시간**  
 게시 데이터베이스에서 가장 최근의 변경 내용이 커밋된 후 배포 데이터베이스에서 해당 명령이 커밋될 때까지 경과된 시간(초)입니다.  
  
 **#Trans**  
 가장 최근에 에이전트를 실행할 때 배포 데이터베이스에서 커밋된 트랜잭션의 수입니다.  
  
 **#Cmds**  
 가장 최근에 에이전트를 실행할 때 배포 데이터베이스에서 커밋된 명령의 수입니다. 명령은 업데이트와 같은 데이터 변경과 동일합니다.  
  
 **평균 명령 수**  
 가장 최근에 에이전트를 실행할 때의 트랜잭션당 평균 명령 수입니다.  
  
### <a name="merge-agent"></a>병합 에이전트  
 **상태**  
 에이전트의 상태입니다. 다음 목록에서는 가능한 상태 값을 보여 줍니다.  
  
-   오류  
  
-   재시도  
  
-   실행 중  
  
-   실행 중이 아님  
  
-   시작한 적 없음  
  
 **게시자**  
 게시자의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스입니다.  
  
 **게시**  
 에이전트와 연결된 게시의 이름입니다.  
  
 **구독**  
 [*SubscriberName*].[*Database*]와(과) 같은 형식의 구독 이름입니다.  
  
 **유형**  
 복제 유형(밀어넣기, 끌어오기 또는 익명)입니다.  
  
 **마지막 시작 시간**  
 마지막으로 에이전트가 시작된 시간입니다.  
  
 **Duration**  
 에이전트가 실행된 기간입니다. 에이전트가 현재 실행되고 있는 경우 이 시간은 경과된 시간을 나타내고 에이전트가 이전에 실행된 경우에는 총 시간을 나타냅니다.  
  
 **마지막 동작**  
 가장 최근의 에이전트 실행에서 수행된 마지막 동작입니다.  
  
 **배달 속도**  
 배포 데이터베이스에서 변경 내용이 커밋된 속도(초당 명령 수)입니다.  
  
 **게시자 삽입**  
 게시자에서 적용된 INSERT 명령 수입니다.  
  
 **게시자 업데이트**  
 게시자에서 적용된 UPDATE 명령 수입니다.  
  
 **게시자 삭제**  
 게시자에서 적용된 DELETE 명령 수입니다.  
  
 **게시자 충돌**  
 병합 프로세스 중에 게시자에서 발생한 충돌 수입니다.  
  
 **구독자 삽입**  
 구독자에서 적용된 INSERT 명령 수입니다.  
  
 **구독자 업데이트**  
 구독자에서 적용된 UPDATE 명령 수입니다.  
  
 **구독자 삭제**  
 구독자에서 적용된 DELETE 명령 수입니다.  
  
 **구독자 충돌**  
 병합 프로세스 중에 구독자에서 발생한 충돌 수입니다.  

  
## <a name="see-also"></a>참고 항목  
 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [복제 모니터링](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)  
  
  
