---
title: 메모리 내 OLTP 데이터베이스에 대한 고가용성 지원 | Microsoft 문서
ms.custom: ''
ms.date: 08/31/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2113a916-3b1e-496c-8650-7f495e492510
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: bfa915330d869c78f79f5abed38b1123ec8fa798
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63047687"
---
# <a name="high-availability-support-for-in-memory-oltp-databases"></a>메모리 내 OLTP 데이터베이스에 대한 고가용성 지원
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  고유하게 컴파일된 저장 프로시저가 있거나 없이 메모리 최적화 테이블을 포함하는 데이터베이스는 Always On 가용성 그룹에서 완전히 지원됩니다.  [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 개체를 포함하는 데이터베이스의 구성과 지원 방식은 이러한 개체를 포함하지 않는 데이터베이스의 경우와 차이가 없습니다.  
  
 Always On 가용성 그룹에서 메모리 내 OLTP 데이터베이스를 배포하면 주 복제본의 메모리 최적화 테이블에 대한 변경 내용이 REDO 적용 시 메모리 내에서 보조 복제본의 테이블에 적용됩니다. 즉, 데이터가 이미 메모리에 있으므로 보조 복제본 장애 조치(failover)가 매우 신속하게 진행될 수 있습니다. 또한 읽기용으로 구성된 보조 복제본에 대한 쿼리에서 테이블을 사용할 수 있습니다.  
  
## <a name="always-on-availability-groups-and-in-memory-oltp-databases"></a>Always On 가용성 그룹 및 메모리 내 OLTP 데이터베이스  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 구성 요소를 통한 데이터베이스 구성에는 다음과 같은 장점이 있습니다.  
  
-   **완전 통합 환경**   
    동기 및 비동기 보조 복제본에 대해 동일한 지원 수준으로 동일한 마법사를 사용하여 메모리 최적화 테이블을 포함하는 데이터베이스를 구성할 수 있습니다. 또한 SQL Server Management Studio의 친숙한 Always On 대시보드를 사용하여 상태 모니터링이 제공됩니다.  
  
-   **동등한 장애 조치(failover) 시간**   
    보조 복제본은 메모리 최적화 지속형 테이블의 메모리 내 상태를 유지합니다. 복구가 필요하지 않으므로, 자동 또는 강제 장애 조치 발생 시 새로운 주 항목으로의 페일오버 시간이 디스크 기반 테이블과 비슷합니다. SCHEMA_ONLY로 생성되는 메모리 액세스에 최적화된 테이블이 이 구성에서 지원됩니다. 그러나 이러한 테이블에 대한 변경 사항은 기록되지 않으므로 보조 복제본의 이 테이블에는 데이터가 존재하지 않습니다.  
  
-   **읽기용 보조**   
    읽기용으로 구성된 경우 보조 복제본의 메모리 최적화 테이블을 액세스 및 쿼리할 수 있습니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 보조 복제본의 읽기 타임스탬프는 주 복제본의 읽기 타임스탬프와 매우 근접하게 동기화되므로 주 복제본의 변경 내용이 보조 복제본에 매우 빠르게 표시됩니다. 이와 같은 근접 동기화 동작은 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 메모리 내 OLTP와는 다릅니다.  
  
## <a name="failover-clustering-instance-fci-and-in-memory-oltp-databases"></a>장애 조치 클러스터링 인스턴스(FCI) 및 메모리 내 OLTP 데이터베이스  
 공유 저장소 구성에서 고가용성을 유지하려는 경우 메모리 최적화 테이블이 포함된 하나 이상의 데이터베이스를 통해 인스턴스에서 장애 조치(failover) 클러스터링을 설정할 수 있습니다. FCI는 설정의 일부로 다음과 같은 요소를 고려해야 합니다.  
  
-   **복구 시간 목표**   
    메모리 최적화 테이블을 메모리에 로드해야 데이터베이스를 사용할 수 있으므로 장애 조치(failover) 시간이 더 길어질 수 있습니다.  
  
-   **SCHEMA_ONLY 테이블**   
    장애 조치(failover) 후 SCHEMA_ONLY 테이블은 행 없이 비어 있게 됩니다. 이것이 애플리케이션에서 설계 및 정의한 방식입니다. 하나 이상의 SCHEMA_ONLY 테이블이 있는 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 데이터베이스를 다시 시작할 때도 똑같이 작동합니다.  
  
## <a name="support-for-transaction-replication-in-in-memory-oltp"></a>메모리 내 OLTP에서 트랜잭션 복제 지원  
 피어 투 피어 트랜잭션 복제를 제외하고 트랜잭션 복제 구독자 역할을 수행하는 테이블은 메모리 최적화 테이블로 구성할 수 있습니다. 다른 복제 구성은 메모리 최적화 테이블과 호환되지 않습니다.  자세한 내용은 [메모리 액세스에 최적화된 테이블 구독자로 복제](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹(SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [활성 보조 복제본: 읽기 가능한 보조 복제본(Always On 가용성 그룹)](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [메모리 액세스에 최적화된 테이블 구독자로 복제](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)  
  
  
