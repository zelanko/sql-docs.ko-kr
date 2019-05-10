---
title: 가용성 그룹의 보조 복제본으로 읽기 전용 워크로드 오프로드
description: 읽기 전용 쿼리 및 보고서를 SQL Server에서 Always On 가용성 그룹의 보조 복제본으로 오프로드하는 방법에 대해 알아봅니다.
ms.custom: seodec18
ms.date: 06/06/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- connection access to availability replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- readable secondary replicas
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 78f3f81a-066a-4fff-b023-7725ff874fdf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 653171f45dff58afe617f1d70380e4ce9f3ee600
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206272"
---
# <a name="offload-read-only-workload-to-secondary-replica-of-an-always-on-availability-group"></a>Always On 가용성 그룹의 보조 복제본으로 읽기 전용 워크로드 오프로드
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 활성 보조 기능에는 하나 이상의 보조 복제본(*읽기 가능한 보조 복제본*)에 대한 읽기 전용 액세스 지원이 포함됩니다. 읽을 수 있는 보조 복제본은 동기 커밋 가용성 모드나 비동기 커밋 가용성 모드가 될 수 있습니다. 읽기 가능한 보조 복제본은 해당 보조 데이터베이스 모두에 대한 읽기 전용 액세스를 허용합니다. 하지만 읽기 가능한 보조 데이터베이스는 읽기 전용으로 설정되지 않습니다. 이러한 데이터베이스는 동적입니다. 해당 주 데이터베이스에서 변경 내용이 발생하면 보조 데이터베이스도 변경됩니다. 일반적인 보조 복제본의 경우 보조 데이터베이스의 내구성이 있는 메모리 액세스에 최적화된 테이블을 포함한 데이터는 거의 실시간 데이터입니다. 또한 전체 텍스트 인덱스는 보조 데이터베이스와 동기화됩니다. 대부분의 경우 주 데이터베이스와 해당하는 보조 데이터베이스 간의 데이터 대기 시간은 몇 초 이내입니다.  
  
 주 데이터베이스에서 적용되는 보안 설정은 보조 데이터베이스에서도 유지됩니다. 여기에는 사용자, 데이터베이스 역할 및 애플리케이션 역할과 함께 각각의 사용 권한이 포함되며 주 데이터베이스에 TDE(투명한 데이터 암호화)가 설정되어 있는 경우 TDE도 포함됩니다.  
  
> [!NOTE]  
>  보조 데이터베이스에 데이터를 쓸 수는 없지만 **tempdb**와 같은 시스템 데이터베이스, 사용자 데이터베이스를 비롯하여 보조 복제본을 호스트하는 서버 인스턴스의 읽기/쓰기 데이터베이스에는 데이터를 쓸 수 있습니다.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 은 읽기 전용 연결 요청을 읽기 가능한 보조 복제본으로 다시 라우팅하는 기능(*읽기 전용 라우팅*)도 지원합니다. 읽기 전용 라우팅에 대한 자세한 내용은 [수신기를 사용하여 읽기 전용 보조 복제본(읽기 전용 라우팅)에 연결](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)을 참조하세요.  
  
##  <a name="bkmk_Benefits"></a> 이점  
 읽기 가능한 보조 복제본에 대한 읽기 전용 연결을 허용하면 다음과 같은 이점이 있습니다.  
  
-   주 복제본에서 보조 읽기 전용 작업을 줄여 주므로 중요한 작업을 위해 주 복제본의 리소스를 절약할 수 있습니다. 매우 중요한 읽기 작업이 있거나 대기 시간을 허용할 수 없는 작업이 있으면 주 복제본에서 실행해야 합니다.  
  
-   읽기 가능한 보조 복제본을 호스팅하는 시스템에 대한 투자 수익을 향상시킵니다.  
  
 또한 읽기 가능한 보조 복제본은 다음과 같이 읽기 전용 작업을 지원합니다.  
  
-   읽기 가능한 보조 데이터베이스에 대한 자동 임시 통계를 통해 디스크 기반 테이블의 읽기 전용 쿼리를 최적화할 수 있습니다. 메모리 액세스에 최적화된 테이블의 경우 누락 통계가 자동으로 생성됩니다. 하지만 부실 통계의 자동 업데이트는 없습니다. 주 복제본에서 통계를 수동으로 업데이트해야 합니다. 자세한 내용은 이 항목 뒷부분에 있는 [읽기 전용 액세스 데이터베이스에 대한 통계](#Read-OnlyStats)를 참조하세요.  
  
-   디스크 기반 테이블에 대한 읽기 전용 작업에서는 행 버전 관리를 사용하여 보조 데이터베이스에 대한 차단 경합을 제거합니다. 보조 데이터베이스에 대해 실행되는 모든 쿼리는 스냅숏 격리 트랜잭션 수준에 자동으로 매핑되며, 이는 다른 트랜잭션 격리 수준이 명시적으로 설정되어 있는 경우에도 해당됩니다. 또한 모든 잠금 힌트가 무시됩니다. 따라서 읽기/쓰기 경합이 없어집니다.  
  
-   메모리 액세스에 최적화된 지속성 테이블에 대한 읽기 전용 작업은 동일한 트랜잭션 격리 수준 제한이 있는 네이티브 저장 프로시저 또는 SQL 상호 운용성을 사용하여 주 데이터베이스에서 액세스하는 것과 정확히 동일한 방법으로 데이터에 액세스합니다( [데이터베이스 엔진의 격리 수준](https://msdn.microsoft.com/8ac7780b-5147-420b-a539-4eb556e908a7)참조). 주 복제본에서 실행하는 보고 작업이나 읽기 전용 쿼리는 변경할 필요 없이 보조 복제본에서 실행할 수 있습니다. 마찬가지로, 보조 복제본에서 실행하는 보고 작업이나 읽기 전용 쿼리는 변경할 필요 없이 주 복제본에서 실행할 수 있습니다.  디스크 기반 테이블과 유사하게 보조 데이터베이스에 대해 실행되는 모든 쿼리는 스냅숏 격리 트랜잭션 수준에 자동으로 매핑되며, 이는 다른 트랜잭션 격리 수준이 명시적으로 설정되어 있는 경우에도 해당됩니다.  
  
-   보조 복제본에서는 디스크 기반 및 메모리 액세스에 최적화된 테이블 유형 모두에 대해 테이블 변수에서 DML 작업이 허용됩니다.  
  
##  <a name="bkmk_Prerequisites"></a> 가용성 그룹에 대한 필수 구성 요소  
  
-   **읽기 가능한 보조 복제본(필수)**  
  
     데이터베이스 관리자는 하나 이상의 복제본을 보조 역할로 실행할 때 모든 연결을 허용하거나(읽기 전용 액세스의 경우에만) 읽기 전용 연결만 허용하도록 구성해야 합니다.  
  
    > [!NOTE]  
    >  필요한 경우 데이터베이스 관리자는 임의의 가용성 복제본을 주 역할로 실행할 때 읽기 전용 연결을 제외하도록 구성할 수도 있습니다.  
  
     자세한 내용은 이 항목 뒷부분에 있는 [가용성 복제본에 대한 클라이언트 연결 액세스 정보&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)와 같은 시스템 데이터베이스, 사용자 데이터베이스를 비롯하여 보조 복제본을 호스트하는 서버 인스턴스의 읽기/쓰기 데이터베이스에는 데이터를 쓸 수 있습니다.  
  
-   **가용성 그룹 수신기**  
  
     읽기 전용 라우팅을 지원하려면 가용성 그룹에 [가용성 그룹 수신기](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)가 있어야 합니다. 읽기 전용 클라이언트는 해당 연결 요청을 이 수신기에 전달해야 하며, 클라이언트의 연결 문자열에서는 애플리케이션 의도를 "읽기 전용"으로 지정해야 합니다. 즉, 해당 연결 요청은 *읽기 전용 연결 요청*이어야 합니다.  
  
-   **읽기 전용 라우팅**  
  
     *읽기 전용 라우팅* 이란 가용성 그룹 수신기에 전달된 들어오는 읽기 전용 연결 요청을 사용 가능하고 읽기 가능한 보조 복제본으로 라우팅하는 SQL Server 기능을 말합니다. 읽기 전용 라우팅을 위한 필수 구성 요소은 다음과 같습니다.  
  
    -   읽기 전용 라우팅을 지원하려면 읽기 가능한 보조 복제본에 읽기 전용 라우팅 URL이 있어야 합니다. 이 URL은 로컬 복제본이 보조 역할로 실행되는 경우에만 적용됩니다. 필요에 따라 복제본별로 읽기 전용 라우팅 URL을 지정해야 합니다. 각 읽기 전용 라우팅 URL은 읽기 전용 연결 요청을 지정된 읽기 가능한 보조 복제본으로 라우팅하는 데 사용됩니다. 일반적으로 모든 읽기 가능한 보조 복제본에는 읽기 전용 라우팅 URL이 할당됩니다.  
  
    -   주 복제본으로 사용될 때 읽기 전용 라우팅을 지원하도록 할 각 가용성 복제본에 읽기 전용 라우팅 목록이 있어야 합니다. 지정된 읽기 전용 라우팅 목록은 로컬 복제본이 주 역할로 실행되는 경우에만 적용됩니다. 필요에 따라 복제본별로 이 목록을 지정해야 합니다. 일반적으로 각 읽기 전용 라우팅 목록의 끝에는 로컬 복제본의 URL과 함께 모든 읽기 전용 라우팅 URL이 포함됩니다.  
  
        > [!NOTE]  
        >  읽기 전용 연결 요청은 복제본에 부하를 분산할 수 있습니다. 자세한 내용은 [읽기 전용 복제본에 대한 부하 분산 구성](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing)을 참조하세요.  
  
     자세한 내용은 이 항목 뒷부분에 있는 [가용성 그룹에 대한 읽기 전용 라우팅 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)와 같은 시스템 데이터베이스, 사용자 데이터베이스를 비롯하여 보조 복제본을 호스트하는 서버 인스턴스의 읽기/쓰기 데이터베이스에는 데이터를 쓸 수 있습니다.  
  
> [!NOTE]  
>  가용성 그룹 수신기 및 읽기 전용 라우팅에 대한 자세한 내용은 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)와 같은 시스템 데이터베이스, 사용자 데이터베이스를 비롯하여 보조 복제본을 호스트하는 서버 인스턴스의 읽기/쓰기 데이터베이스에는 데이터를 쓸 수 있습니다.  
  
##  <a name="bkmk_LimitationsRestrictions"></a> 제한 사항  
 일부 작업은 다음과 같이 완전히 지원되지 않습니다.  
  
-   읽기 가능한 복제본이 읽기에 대해 활성화되는 즉시 보조 데이터베이스에 대한 연결 수락을 시작할 수 있습니다. 하지만 주 데이터베이스에 활성 트랜잭션이 있는 경우 해당 보조 데이터베이스에서 행 버전을 완전히 사용할 수 없습니다. 보조 복제본을 구성할 때 주 복제본에 있던 활성 트랜잭션은 커밋하거나 롤백해야 합니다. 이 프로세스가 완료될 때까지 보조 데이터베이스의 트랜잭션 격리 수준 매핑은 완전하지 않으며 쿼리가 일시적으로 차단됩니다.  
  
    > [!WARNING]  
    >  디스크 기반 테이블과 메모리 액세스에 최적화된 테이블 모두, 경우 장기 트랜잭션을 실행하면 유지되는 버전 관리 행 수에 영향을 줍니다.  
  
-   메모리 액세스에 최적화된 테이블이 있는 보조 데이터베이스에서는 메모리 액세스에 최적화된 테이블에 대해 행 버전이 항상 생성되더라도 보조 복제본이 활성화될 때 주 복제본에 있던 모든 활성 트랜잭션이 완료될 때까지 쿼리가 차단됩니다. 그러면 디스크 기반 테이블과 메모리 액세스에 최적화된 테이블을 보고 작업과 읽기 전용 쿼리에 모두 동시에 사용할 수 있습니다.  
  
-   읽기 가능한 보조 복제본에 속하는 보조 데이터베이스에서는 변경 내용 추적 및 변경 데이터 캡처가 지원되지 않습니다.  
  
    -   변경 내용 추적은 보조 데이터베이스에서 명시적으로 해제되고  
  
    -   변경 데이터 캡처는 보조 복제본 데이터베이스에서만 사용할 수 없습니다. 주 복제본 데이터베이스에서는 변경 데이터 캡처를 사용할 수 있고 보조 복제본 데이터베이스의 함수를 사용하여 CDC 테이블에서 변경 내용을 읽을 수 있습니다.  
  
-   읽기 작업은 스냅숏 격리 트랜잭션 수준으로 매핑되므로 주 복제본에서 삭제할 레코드의 삭제 작업이 하나 이상의 보조 복제본의 트랜잭션에 의해 차단될 수 있습니다. 삭제할 레코드 정리 태스크는 주 복제본에 있는 디스크 기반 테이블에 대한 삭제할 레코드가 보조 복제본에 더 이상 필요하지 않을 때 해당 레코드를 자동으로 정리합니다.  이러한 동작은 주 복제본에서 트랜잭션을 실행할 때 수행되는 동작과 유사합니다. 극단적인 경우에는 보조 데이터베이스에서 삭제할 레코드 정리를 차단하는 장기 실행 읽기 쿼리를 중지해야 할 수 있습니다. 삭제할 레코드 정리는 보조 복제본의 연결이 끊어지거나 보조 데이터베이스에서 데이터 이동이 일시 중지되는 경우 차단될 수 있습니다. 이 상태에서는 로그 잘림이 방지되므로 이 상태가 지속될 경우 가용성 그룹에서 이 보조 데이터베이스를 제거하는 것이 좋습니다. 행 버전이 메모리 내에 유지되고 주 복제본의 행 버전과 독립적이기 때문에 메모리 액세스에 최적화된 테이블에는 삭제할 레코드 정리 문제가 없습니다.  
  
-   주 복제본에서 디스크 기반 테이블이 포함된 파일에 대해 DBCC SHRINKFILE 작업을 수행할 경우 해당 파일에 삭제할 레코드가 포함되어 있고 이 레코드가 보조 복제본에서 여전히 필요하면 작업이 실패할 수 있습니다.  
  
-   [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]부터 사용자 동작 또는 실패로 인해 주 복제본이 오프라인인 경우에도 읽기 가능한 보조 복제본은 온라인 상태를 유지할 수 있습니다. 하지만 이 상황에서는 가용성 그룹 수신기도 오프라인 상태가 되므로 읽기 전용 라우팅이 작동하지 않습니다. 클라이언트는 읽기 전용 작업을 위해 읽기 전용 보조 복제본에 직접 연결해야 합니다.  
  
> [!NOTE]  
>  읽기 가능한 보조 복제본을 호스트하는 서버 인스턴스에서 [sys.dm_db_index_physical_stats](../../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) 동적 관리 뷰를 쿼리할 경우 REDO 차단 문제가 발생할 수 있습니다. 이는 이 동적 관리 뷰가 지정된 사용자 테이블 또는 뷰에 대한 IS 잠금을 획득하여 REDO 스레드에서의 해당 사용자 테이블 또는 뷰에 대한 X 잠금 요청이 차단되기 때문입니다.  
  
##  <a name="bkmk_Performance"></a> 성능 고려 사항  
 이 섹션에서는 읽기 가능한 보조 데이터베이스에 대한 몇 가지 성능 고려 사항에 설명합니다.  
  
 **섹션 내용**  
  
-   [데이터 대기 시간](#DataLatency)  
  
-   [읽기 전용 작업의 영향](#ReadOnlyWorkloadImpact)  
  
-   [인덱싱](#bkmk_Indexing)  
  
-   [읽기 전용 액세스 데이터베이스에 대한 통계](#Read-OnlyStats)  
  
###  <a name="DataLatency"></a> 데이터 대기 시간  
 읽기 전용 작업에 약간의 데이터 대기 시간을 허용할 수 있는 경우 보조 복제본에 대한 읽기 전용 액세스를 구현하는 것이 좋습니다. 데이터 대기 시간이 허용 가능하지 않은 경우에는 주 복제본에 대해 읽기 전용 작업을 실행하는 것이 좋습니다.  
  
 주 복제본은 주 데이터베이스의 변경 내용에 대한 로그 레코드를 보조 복제본으로 보냅니다. 각 보조 데이터베이스에서 전용 다시 실행 스레드가 이 로그 레코드를 적용합니다. 읽기 액세스 보조 데이터베이스에서는 변경 내용이 포함된 로그 레코드가 보조 데이터베이스에 적용되고 트랜잭션이 주 데이터베이스에서 커밋될 때까지는 쿼리 결과에 지정된 데이터 변경 내용이 나타나지 않습니다.  
  
 이로 인해 주 복제본과 보조 복제본 사이에는 대개 몇 초 내외의 대기 시간이 있습니다. 하지만 네트워크 문제로 인해 처리량이 줄어드는 경우와 같은 특수한 경우에는 대기 시간이 중요할 수 있습니다. I/O 병목이 발생하고 데이터 이동이 일시 중지되면 대기 시간이 증가합니다. 일시 중지된 데이터 이동을 모니터링하려면 [Always On 대시보드](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md) 또는 [sys.dm_hadr_database_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) 동적 관리 뷰를 사용하면 됩니다.  
  
####  <a name="bkmk_LatencyWithInMemOLTP"></a> 메모리 최적화 테이블이 포함된 데이터베이스의 데이터 대기 시간  
 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]에서는 활성 보조 데이터베이스의 데이터 대기 시간과 관련된 특별한 고려 사항이 있었습니다([[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 활성 보조: 읽기 가능한 보조 복제본](https://technet.microsoft.com/library/ff878253(v=sql.120).aspx)을 참조하세요). [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] 시작에는 메모리 최적화 테이블의 데이터 대기 시간과 관련된 특별 고려 사항이 없습니다. 메모리 액세스에 최적화된 테이블의 예상 데이터 대기 시간은 디스크 기반 테이블의 대기 시간과 비슷합니다.  
  
###  <a name="ReadOnlyWorkloadImpact"></a> 읽기 전용 작업의 영향  
 읽기 전용 액세스를 사용하도록 보조 복제본을 구성하면 특히 디스크 기반 테이블의 읽기 전용 작업이 I/O를 매우 많이 사용하는 경우 보조 데이터베이스의 읽기 전용 작업은 다시 실행 스레드의 CPU 및 I/O(디스크 기반 테이블의 경우)와 같은 시스템 리소스를 소비합니다. 모든 행이 메모리 내에 상주하기 때문에 메모리 액세스에 최적화된 테이블에 액세스할 때 IO의 영향이 없습니다.  
  
 또한 보조 복제본에 대한 읽기 전용 작업은 로그 레코드를 통해 적용되는 DDL(데이터 정의 언어) 변경을 차단할 수도 있습니다.  
  
-   행 버전 관리로 인해 읽기 작업에서는 공유 잠금을 사용하지는 않지만, DDL 변경을 적용하는 다시 실행 작업을 차단할 수 있는 스키마 안정성(Sch-S) 잠금을 사용합니다. DDL 작업에는 ALTER/DROP 테이블과 뷰가 포함되지만 저장 프로시저의 DROP 또는 ALTER는 포함되지 않습니다. 따라서 예를 들어 주 에서 디스크 기반 또는 메모리 액세스에 최적화된 테이블을 삭제할 경우, REDO 스레드가 테이블을 삭제하기 위한 로그 레코드를 처리할 때는 테이블에서 SCH_M 잠금을 획득해야 하며 테이블에 액세스하는 실행 중인 쿼리를 통해 차단될 수 있습니다.  테이블의 삭제가 사용자 세션의 일부로 수행되고 RODO 스레드가 아닌 경우를 제외하고 이 동작은 주 복제본에서도 동일합니다.  
  
-   추가로 차단하는 메모리 액세스에 최적화된 테이블이 있습니다. 보조 복제본에 네이티브 저장 프로시저의 동시 실행이 있는 경우 네이티브 저장 프로시저를 삭제하면 REDO 스레드가 차단될 수 있습니다. 저장 프로시저의 삭제가 사용자 세션의 일부로 수행되고 RODO 스레드가 아닌 경우를 제외하고 이 동작은 주 복제본에서도 동일합니다.  
  
 쿼리 작성에 대한 최선의 방법을 알고 보조 데이터베이스에서 이러한 최선의 방법을 따라야 합니다. 예를 들어 데이터 집계와 같은 장기 실행 쿼리는 작업량이 적은 시간에 예약합니다.  
  
> [!NOTE]  
>  다시 실행 스레드가 보조 복제본에 대한 쿼리에 의해 차단되면 **sqlserver.lock_redo_blocked** XEvent가 발생합니다.  
  
###  <a name="bkmk_Indexing"></a> 인덱싱  
 읽기 가능한 보조 복제본에서 읽기 전용 작업을 최적화하기 위해 보조 데이터베이스의 테이블에 인덱스를 만들 수 있습니다. 보조 데이터베이스의 스키마나 데이터는 변경할 수 없으므로 주 데이터베이스에 인덱스를 만들고 다시 실행 프로세스를 통해 변경 내용이 보조 데이터베이스에 전송될 수 있도록 합니다.  
  
 보조 복제본의 인덱스 사용 동작을 모니터링하려면 **sys.dm_db_index_usage_stats**동적 관리 뷰의 **user_seeks**, **user_scans** 및 [user_lookups](../../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md) 열을 쿼리합니다.  
  
###  <a name="Read-OnlyStats"></a> 읽기 전용 액세스 데이터베이스에 대한 통계  
 테이블 및 인덱싱된 뷰의 열에 대한 통계는 쿼리 계획을 최적화하는 데 사용됩니다. 가용성 그룹의 경우 주 데이터베이스에 만들어져 유지 관리되는 통계는 트랜잭션 로그 레코드가 적용되는 도중 보조 데이터베이스에 자동 보존됩니다. 그러나 보조 데이터베이스에 대한 읽기 전용 작업에는 주 데이터베이스에 만들어지는 통계와 다른 통계가 필요할 수 있습니다. 하지만 보조 데이터베이스는 읽기 전용 액세스로 제한되므로 보조 데이터베이스에는 통계를 만들 수 없습니다.  
  
 이 문제를 해결하기 위해 보조 복제본은 **tempdb**에 보조 데이터베이스에 대한 임시 통계를 만들어 유지 관리합니다. 주 데이터베이스에 보존되는 영구적 통계와 구별하기 위해 임시 통계의 이름에는 _readonly_database_statistic라는 접미사가 추가됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서만 임시 통계를 만들고 업데이트할 수 있습니다. 하지만 영구적 통계에 사용하는 것과 동일한 도구를 사용하여 임시 통계를 삭제하고 해당 속성을 모니터링할 수 있습니다.  
  
-   [DROP STATISTICS](../../../t-sql/statements/drop-statistics-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용하여 임시 통계를 삭제합니다.  
  
-   **sys.stats** 및 **sys.stats_columns** 카탈로그 뷰를 사용하여 통계를 모니터링합니다. **sys_stats** 에는 영구적 통계와 임시 통계를 나타내는 **is_temporary**열이 포함되어 있습니다.  
  
 주 복제본이나 보조 복제본에는 메모리 액세스에 최적화된 테이블의 자동 통계 업데이트에 대한 지원이 없습니다. 보조 복제본에서 쿼리 성능과 계획을 모니터링하고 필요한 경우 주 복제본에서 통계를 수동으로 업데이트해야 합니다. 하지만 주 복제본 및 보조 복제본 모두에서 누락 통계는 자동으로 생성됩니다.  
  
 SQL Server 통계에 대한 자세한 내용은 [통계](../../../relational-databases/statistics/statistics.md)를 참조하세요.  
  
 **섹션 내용**  
  
-   [보조 데이터베이스의 유효하지 않은 영구적 통계](#StalePermStats)  
  
-   [제한 사항](#StatsLimitationsRestrictions)  
  
####  <a name="StalePermStats"></a> 보조 데이터베이스의 유효하지 않은 영구적 통계  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 보조 데이터베이스에 대한 영구적 통계가 유효하지 않은 경우 이를 감지합니다. 그러나 주 데이터베이스의 변경을 통하지 않고는 영구적 통계를 변경할 수 없습니다. 쿼리 최적화를 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 보조 데이터베이스에 디스크 기반 테이블에 대한 임시 통계를 만들고 이 통계를 유효하지 않은 영구적 통계 대신 사용합니다.  
  
 주 데이터베이스에서 영구적 통계가 업데이트되면 이 통계는 자동으로 보조 데이터베이스에 저장됩니다. 그런 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 임시 통계보다 최신 상태인 업데이트된 영구적 통계를 사용합니다.  
  
 가용성 그룹에서 장애 조치(failover)가 수행되면 모든 보조 복제본에서 임시 통계가 삭제 됩니다.  
  
####  <a name="StatsLimitationsRestrictions"></a> 제한 사항  
  
-   임시 통계는 **tempdb**에 저장되므로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스를 다시 시작하면 모든 임시 통계가 사라집니다.  
  
-   접미사 _readonly_database_statistic은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 생성하는 통계용으로 예약되어 있습니다. 따라서 주 데이터베이스에서 통계를 만들 때 이 접미사를 사용할 수 없습니다. 자세한 내용은 [Statistics](../../../relational-databases/statistics/statistics.md)을(를) 참조하세요.  
  
##  <a name="bkmk_AccessInMemTables"></a> 보조 복제본에서 메모리 최적화 테이블 액세스  
 보조 복제본의 메모리 액세스에 최적화된 테이블에 사용할 수 있는 트랜잭션 격리 수준은 주 복제본의 경우와 동일합니다. 세션 수준 격리 수준을 READ COMMITTED로 설정하고 데이터베이스 수준 옵션 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT을 ON으로 설정하는 것이 좋습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```sql  
ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON  
GO  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED  
GO  
SELECT SUM(UnitPrice*OrderQty)   
FROM Sales.SalesOrderDetail_inmem  
GO  
  
```  
  
##  <a name="bkmk_CapacityPlanning"></a> 용량 계획 고려 사항  
  
-   디스크 기반 테이블의 경우 다음 두 가지 이유로 읽기 가능한 보조 복제본에는 **tempdb** 에 공간이 필요할 수 있습니다.  
  
    -   스냅숏 격리 수준은 행 버전을 **tempdb**로 복사합니다.  
  
    -   보조 데이터베이스의 임시 통계는 **tempdb**에 생성되고 유지 관리됩니다. 임시 통계로 인해 **tempdb**의 크기가 약간 증가할 수 있습니다. 자세한 내용은 이 섹션 뒷부분에 있는 [읽기 전용 액세스 데이터베이스에 대한 통계](#Read-OnlyStats)를 참조하세요.  
  
-   디스크 기반 테이블의 경우 하나 이상의 보조 복제본에 대해 읽기 액세스를 구성하면 주 데이터베이스에서는 삭제, 수정 또는 삽입된 데이터 행에 14바이트의 오버헤드를 추가하여 보조 데이터베이스의 행 버전에 대한 포인터를 저장합니다. 이 14바이트 오버헤드는 보조 데이터베이스에 전달됩니다. 14바이트의 오버헤드가 데이터 행에 추가되므로 페이지 분할이 발생할 수 있습니다.  
  
     행 버전 데이터는 주 데이터베이스에 의해 생성되지 않습니다. 대신 보조 데이터베이스는 행 버전을 생성합니다. 하지만 행 버전 관리는 주 데이터베이스와 보조 데이터베이스 모두의 데이터 스토리지를 늘립니다.  
  
     행 버전 데이터 추가는 주 데이터베이스의 스냅숏 격리 또는 RCSI(읽기 커밋된 스냅숏 격리) 수준에 따라 달라집니다. 다음 표에서는 디스크 기반 테이블에서 여러 설정에 따른 읽기 가능한 보조 데이터베이스의 버전 관리 동작에 대해 설명합니다.  
  
    |읽기 가능한 보조 복제본인지 여부|스냅숏 격리 또는 RCSI 수준이 설정되었는지 여부|주 데이터베이스|보조 데이터베이스|  
    |---------------------------------|-----------------------------------------------|----------------------|------------------------|  
    |아니오|아니오|행 버전이 없거나 14바이트 오버헤드임|행 버전이 없거나 14바이트 오버헤드임|  
    |아니오|예|행 버전이 있고 14바이트 오버헤드임|행 버전이 없지만 14바이트 오버헤드임|  
    |예|아니오|행 버전이 없지만 14바이트 오버헤드임|행 버전이 있고 14바이트 오버헤드임|  
    |예|예|행 버전이 있고 14바이트 오버헤드임|행 버전이 있고 14바이트 오버헤드임|  
  
##  <a name="bkmk_RelatedTasks"></a> 관련 태스크  
  
-   [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [가용성 그룹에 대한 읽기 전용 라우팅 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
-   [가용성 복제본 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 복제본에 대한 클라이언트 연결 액세스 정보&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [통계](../../../relational-databases/statistics/statistics.md)  
  
  
