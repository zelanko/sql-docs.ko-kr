---
title: "개발자 가이드: 방법 도움말 항목(복제) | Microsoft 문서"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: c6c15ae6-da52-4638-93d3-61c7242e8a0b
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 288ed137e701d6cfb416d12b6ff2176c59ec0278
ms.lasthandoff: 04/11/2017

---
# <a name="developer39s-guide-how-to-topics-replication"></a>개발자 가이드: 방법 도움말 항목(복제)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 복제 관련 태스크를 프로그래밍 방식으로 수행하는 방법에 대한 정보를 제공합니다.  
  
## <a name="securing-a-replication-topology"></a>복제 토폴로지 보안  
  
-   [복제 보안 설정 보기 및 수정](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
-   [게시 액세스 목록에서 로그인 관리](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md)  
  
## <a name="configuring-modifying-and-disabling-publishing-and-distribution-replication"></a>게시 및 배포의 구성, 수정 및 해제(복제)  
  
-   [게시 및 배포 구성](../../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
-   [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [게시 및 배포 해제](../../../relational-databases/replication/disable-publishing-and-distribution.md)  
  
## <a name="creating-modifying-and-deleting-publications-and-articles"></a>게시 및 아티클 작성, 수정 및 삭제  
  
-   [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [아티클 정의](../../../relational-databases/replication/publish/define-an-article.md)  
  
-   [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [아티클 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
-   [게시 삭제](../../../relational-databases/replication/publish/delete-a-publication.md)  
  
-   [아티클 삭제](../../../relational-databases/replication/publish/delete-an-article.md)  
  
-   [Oracle 데이터베이스에서 게시 만들기](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)  
  
-   [구독에 대한 만료 기간 설정](../../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)  
  
-   [스키마 옵션 지정](../../../relational-databases/replication/publish/specify-schema-options.md)  
  
-   [스키마 변경 내용 복제](../../../relational-databases/replication/publish/replicate-schema-changes.md)  
  
-   [ID 열 관리](../../../relational-databases/replication/publish/manage-identity-columns.md)  
  
-   [병합 게시에 대한 호환성 수준 설정](../../../relational-databases/replication/publish/set-the-compatibility-level-for-merge-publications.md)  
  
### <a name="snapshot-options"></a>스냅숏 옵션  
  
-   [스냅숏 속성 구성&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
-   [FTP를 통해 스냅숏 배달](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)  
  
### <a name="filtering-data"></a>데이터 필터링  
  
-   [열 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)  
  
-   [정적 행 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)  
  
-   [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
-   [매개 변수가 있는 행 필터 최적화](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md)  
  
-   [병합 아티클 사이에서 조인 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
### <a name="transactional-replication-options"></a>트랜잭션 복제 옵션  
  
-   [트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법 설정](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)  
  
-   [트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
### <a name="merge-replication-options"></a>병합 복제 옵션  
  
-   [병합 테이블 아티클 간의 논리적 레코드 관계 정의](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)  
  
-   [병합 테이블 아티클의 처리 순서 지정&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/publish/specify-the-processing-order-of-merge-table-articles.md)  
  
-   [새 병합 테이블 아티클을 다운로드 전용으로 지정](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md)  
  
-   [병합 아티클에 대해 삭제가 추적되지 않도록 지정&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
-   [병합 아티클의 충돌 추적 및 해결 수준 지정](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)  
  
-   [병합 아티클 해결 프로그램 지정](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
-   [병합 아티클에 대한 상호 충돌 해결 프로그램 지정](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)  
  
## <a name="creating-modifying-and-deleting-subscriptions"></a>구독 만들기, 수정 및 삭제  
  
-   [끌어오기 구독 만들기](../../../relational-databases/replication/create-a-pull-subscription.md)  
  
-   [끌어오기 구독 속성 보기 및 수정](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  
  
-   [끌어오기 구독 삭제](../../../relational-databases/replication/delete-a-pull-subscription.md)  
  
-   [밀어넣기 구독 만들기](../../../relational-databases/replication/create-a-push-subscription.md)  
  
-   [밀어넣기 구독 속성 보기 및 수정](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)  
  
-   [밀어넣기 구독 삭제](../../../relational-databases/replication/delete-a-push-subscription.md)  
  
-   [동기화 일정 지정](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
-   [트랜잭션 게시에 대해 업데이트할 수 있는 구독 만들기](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md)
  
-   [SQL Server 이외 구독자에 대한 구독 만들기](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)  
  
## <a name="synchronizing-subscriptions"></a>구독 동기화  
  
-   [초기 스냅숏 만들기 및 적용](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [매개 변수가 있는 필터로 병합 게시에 대한 스냅숏 만들기](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [백업에서 트랜잭션 구독 초기화&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [수동 구독 초기화](../../../relational-databases/replication/initialize-a-subscription-manually.md)  
  
-   [끌어오기 구독 동기화](../../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [밀어넣기 구독 동기화](../../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
-   [구독 다시 초기화](../../../relational-databases/replication/reinitialize-a-subscription.md)  
  
-   [동기화 중 스크립트 실행&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [병합 아티클에 대한 비즈니스 논리 처리기 구현](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [비즈니스 논리 처리기 디버깅&#40;복제 프로그래밍&#41;](../../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)  
  
-   [동기화하는 동안 트리거 및 제약 조건 동작 제어&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [병합 아티클용 사용자 지정 충돌 해결 프로그램 구현](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="administering-a-replication-topology"></a>복제 토폴로지 관리  
  
-   [복제 에이전트 프로필 작업](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [구독자에서 데이터 유효성 검사](../../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
-   [매개 변수가 있는 필터로 병합 게시에 대한 파티션 관리](../../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [병합 게시에서 데이터를 테이블로 대량 로드&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/bulk-load-data-into-tables-in-a-merge-publication.md)  
  
-   [병합 메타데이터 정리&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/administration/clean-up-merge-metadata-replication-transact-sql-programming.md)  
  
-   [병합 아티클에 대해 더미 업데이트 수행&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/administration/perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming.md)  
  
-   [배포 데이터베이스의 복제된 명령 및 기타 정보 보기&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md)  
  
-   [트랜잭션 복제에 대해 통합 백업 사용&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)  
  
-   [피어 투 피어 토폴로지 관리&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)  
  
-   [복제 토폴로지 정지&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)  
  
-   [Oracle 게시자에 대한 트랜잭션 집합 작업 구성&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)  
  
-   [복제 스크립트 업그레이드&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)  
  
## <a name="monitoring-a-replication-topology"></a>복제 토폴로지 모니터링  
  
-   [비관리자의 복제 모니터 사용 허용](../../../relational-databases/replication/monitor/allow-non-administrators-to-use-replication-monitor.md)  
  
-   [프로그래밍 방식으로 복제 모니터링](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
-   [배포 데이터베이스의 복제된 명령 및 기타 정보 보기&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md)  
  
-   [병합 게시에 대한 충돌 정보 보기&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)  
  
-   [트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
