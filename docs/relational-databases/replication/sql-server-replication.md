---
title: SQL Server 복제 | Microsoft 문서
description: 데이터베이스 간에 데이터 및 데이터베이스 개체를 복사 및 배포하고 데이터베이스 간에 동기화하는 기술인 SQL Server의 복제에 대해 알아봅니다.
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], about
- replication [SQL Server]
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 0690ad04a9b4dfdb2edd22c4e882616c2f8bf73f
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869505"
---
# <a name="sql-server-replication"></a>SQL Server 복제
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  복제는 한 데이터베이스에서 다른 데이터베이스로 데이터와 데이터베이스 개체를 복사 및 배포한 다음 데이터베이스 간에 동기화를 수행하여 일관성을 유지하는 일련의 기술입니다. 복제를 사용하면 LAN 및 WAN, 전화 접속 연결, 무선 연결 및 인터넷을 통해 데이터를 여러 다른 위치로 배포하고 원격 또는 모바일 사용자에게 배포할 수 있습니다.  
  
 트랜잭션 복제는 일반적으로 확장성 및 가용성 향상, 데이터 웨어하우징 및 보고, 여러 사이트의 데이터 통합, 다른 유형의 데이터 통합, 일괄 처리 작업 오프로드 등을 포함하여 높은 처리량이 필요한 서버 간 시나리오에서 사용됩니다. 병합 복제는 주로 데이터 충돌 가능성이 있는 모바일 애플리케이션이나 분산 서버 애플리케이션에 사용됩니다. 일반적인 시나리오에는 모바일 사용자와 데이터 교환, 소비자 POS(Point of Sale) 애플리케이션, 여러 사이트의 데이터 통합 등이 있습니다. 스냅샷 복제는 트랜잭션 및 병합 복제에 초기 데이터 집합을 제공하는 데 사용되며 전체 데이터 새로 고침이 적합한 경우에도 사용할 수 있습니다. 이러한 3가지 복제 유형을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 엔터프라이즈 데이터를 동기화하는 강력하고 유연성 있는 시스템을 제공합니다. SQLCE 3.5 및 SQLCE 4.0에 대한 복제는 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 및 [!INCLUDE[win8](../../includes/win8-md.md)]에서 지원됩니다.  


## <a name="whats-new"></a>새로운 기능 
- SQL Server 2017은 중요한 새로운 기능을 SQL Server 복제에 도입하지 않았습니다. 
- SQL Server 2016은 중요한 새로운 기능을 SQL Server 복제에 도입하지 않았습니다. 

이전 버전과의 호환성 정보는 [복제의 이전 버전과의 호환성](replication-backward-compatibility.md)을 참조하세요. 


 ## <a name="replication-security"></a>복제 보안
  
-   [복제 보안 설정 보기 및 수정](security/view-and-modify-replication-security-settings.md)  
-   [게시 액세스 목록에서 로그인 관리](security/manage-logins-in-the-publication-access-list.md)  
  
## <a name="publishing-and-distribution"></a>게시 및 배포  
  
-   [게시 및 배포 구성](configure-publishing-and-distribution.md)   
-   [게시 속성 보기 및 수정](publish/view-and-modify-publication-properties.md)   
-   [게시 및 배포 해제](disable-publishing-and-distribution.md)  
  
## <a name="publications-and-articles"></a>게시 및 문서 
  
-   [게시 만들기](publish/create-a-publication.md)    
-   [아티클 정의](publish/define-an-article.md)   
-   [게시 속성 보기 및 수정](publish/view-and-modify-publication-properties.md)   
-   [아티클 속성 보기 및 수정](publish/view-and-modify-article-properties.md)    
-   [게시 삭제](publish/delete-a-publication.md)   
-   [아티클 삭제](publish/delete-an-article.md)    
-   [Oracle 데이터베이스에서 게시 만들기](publish/create-a-publication-from-an-oracle-database.md)   
-   [구독에 대한 만료 기간 설정](publish/set-the-expiration-period-for-subscriptions.md)  
-   [스키마 옵션 지정](publish/specify-schema-options.md)  
-   [스키마 변경 내용 복제](publish/replicate-schema-changes.md)    
-   [ID 열 관리](publish/manage-identity-columns.md)   
-   [병합 게시에 대한 호환성 수준 설정](publish/set-the-compatibility-level-for-merge-publications.md)  
  
### <a name="snapshot-options"></a>Snapshot Options  
  
-   [스냅샷 속성 구성](publish/configure-snapshot-properties-replication-transact-sql-programming.md)    
-   [FTP를 통해 스냅샷 배달](publish/deliver-a-snapshot-through-ftp.md) 
  
### <a name="filter-data"></a>데이터 필터링  
  
-   [열 필터 정의 및 수정](publish/define-and-modify-a-column-filter.md)    
-   [정적 행 필터 정의 및 수정](publish/define-and-modify-a-static-row-filter.md)    
-   [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)    
-   [매개 변수가 있는 행 필터 최적화](publish/optimize-parameterized-row-filters.md)    
-   [병합 아티클 사이에서 조인 필터 정의 및 수정](publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
### <a name="transactional-replication-options"></a>트랜잭션 복제 옵션  
  
-   [트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법 설정](publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)    
-   [트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정](publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
### <a name="merge-replication-options"></a>병합 복제 옵션  
  
-   [병합 테이블 아티클 간의 논리적 레코드 관계 정의](publish/define-a-logical-record-relationship-between-merge-table-articles.md)    
-   [병합 복제 속성 지정](merge/specify-merge-replication-properties.md)    
-   [병합 아티클 해결 프로그램 지정](publish/specify-a-merge-article-resolver.md)    

  
## <a name="manage-subscriptions"></a>구독 관리  
  
-   [끌어오기 구독 만들기](create-a-pull-subscription.md)    
-   [끌어오기 구독 속성 보기 및 수정](view-and-modify-pull-subscription-properties.md)    
-   [끌어오기 구독 삭제](delete-a-pull-subscription.md)    
-   [밀어넣기 구독 만들기](create-a-push-subscription.md)   
-   [밀어넣기 구독 속성 보기 및 수정](view-and-modify-push-subscription-properties.md)   
-   [밀어넣기 구독 삭제](delete-a-push-subscription.md)   
-   [동기화 일정 지정](specify-synchronization-schedules.md)    
-   [트랜잭션 게시에 대해 업데이트할 수 있는 구독 만들기](publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
-   [SQL Server 이외 구독자에 대한 구독 만들기](create-a-subscription-for-a-non-sql-server-subscriber.md)  
  
## <a name="synchronize-subscriptions"></a>구독 동기화  
  
-   [초기 스냅샷 만들기 및 적용](create-and-apply-the-initial-snapshot.md)   
-   [매개 변수가 있는 필터로 병합 게시에 대한 스냅샷 만들기](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)    
-   [백업에서 트랜잭션 구독 초기화&#40;복제 Transact-SQL 프로그래밍&#41;](initialize-a-transactional-subscription-from-a-backup.md)    
-   [수동 구독 초기화](initialize-a-subscription-manually.md)    
-   [끌어오기 구독 동기화](synchronize-a-pull-subscription.md)    
-   [밀어넣기 구독 동기화](synchronize-a-push-subscription.md)   
-   [구독 다시 초기화](reinitialize-a-subscription.md)    
-   [동기화 중 스크립트 실행&#40;복제 Transact-SQL 프로그래밍&#41;](execute-scripts-during-synchronization-replication-transact-sql-programming.md)    
-   [병합 아티클에 대한 비즈니스 논리 처리기 구현](implement-a-business-logic-handler-for-a-merge-article.md)  
-   [비즈니스 논리 처리기 디버깅&#40;복제 프로그래밍&#41;](debug-a-business-logic-handler-replication-programming.md)    
-   [동기화하는 동안 트리거 및 제약 조건 동작 제어&#40;복제 Transact-SQL 프로그래밍&#41;](control-behavior-of-triggers-and-constraints-in-synchronization.md)    
-   [병합 아티클용 사용자 지정 충돌 해결 프로그램 구현](implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="administration"></a>관리 
  
-   [복제 에이전트 프로필 작업](agents/work-with-replication-agent-profiles.md)   
-   [구독자에서 데이터 유효성 검사](validate-data-at-the-subscriber.md)    
-   [매개 변수가 있는 필터로 병합 게시에 대한 파티션 관리](publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)    
-   [병합 게시에서 데이터를 테이블로 대량 로드&#40;복제 Transact-SQL 프로그래밍&#41;](bulk-load-data-into-tables-in-a-merge-publication.md)    
-   [병합 메타데이터 정리&#40;복제 Transact-SQL 프로그래밍&#41;](administration/clean-up-merge-metadata-replication-transact-sql-programming.md)    
-   [병합 아티클에 대해 더미 업데이트 수행&#40;복제 Transact-SQL 프로그래밍&#41;](administration/perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming.md)    
-   [배포 데이터베이스의 복제된 명령 및 기타 정보 보기&#40;복제 Transact-SQL 프로그래밍&#41;](monitor/view-replicated-commands-and-information-in-distribution-database.md)    
-   [트랜잭션 복제에 대해 통합 백업 사용&#40;복제 Transact-SQL 프로그래밍&#41;](administration/enable-coordinated-backups-for-transactional-replication.md)   
-   [피어 투 피어 토폴로지 관리&#40;복제 Transact-SQL 프로그래밍&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)    
-   [복제 토폴로지 정지&#40;복제 Transact-SQL 프로그래밍&#41;](administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)    
-   [Oracle 게시자에 대한 트랜잭션 집합 작업 구성&#40;복제 Transact-SQL 프로그래밍&#41;](administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
-   [복제 스크립트 업그레이드&#40;복제 Transact-SQL 프로그래밍&#41;](administration/upgrade-replication-scripts-replication-transact-sql-programming.md)  
  
## <a name="monitor"></a>모니터
  
-   [비관리자의 복제 모니터 사용 허용](monitor/allow-non-administrators-to-use-replication-monitor.md)    
-   [프로그래밍 방식으로 복제 모니터링](monitor/programmatically-monitor-replication.md)    
-   [배포 데이터베이스의 복제된 명령 및 기타 정보 보기&#40;복제 Transact-SQL 프로그래밍&#41;](monitor/view-replicated-commands-and-information-in-distribution-database.md)    
-   [병합 게시에 대한 충돌 정보 보기&#40;복제 Transact-SQL 프로그래밍&#41;](./view-and-resolve-data-conflicts-for-merge-publications.md) 
-   [트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
