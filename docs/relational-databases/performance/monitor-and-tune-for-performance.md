---
title: 성능 모니터링 및 튜닝 | Microsoft 문서
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- instances of SQL Server, monitoring performance
- monitoring server performance [SQL Server]
- Database Engine [SQL Server], performance
- monitoring performance [SQL Server], about performance
- server performance [SQL Server]
- monitoring performance [SQL Server]
- database performance [SQL Server], about performance
- tuning databases [SQL Server], about performance
- status information [SQL Server], performance monitoring
- database monitoring [SQL Server], about performance
- monitoring [SQL Server], queries performance
- server performance [SQL Server], about performance
- tuning databases [SQL Server]
- database performance [SQL Server]
- monitoring [SQL Server], server performance
- database monitoring [SQL Server]
- monitoring server performance [SQL Server], about monitoring server performance
ms.assetid: 87f23f03-0f19-4b2e-bfae-efa378f7a0d4
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fd6fdf81a74e015995f5bf9bd5500f196ccf5cc5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68020252"
---
# <a name="monitor-and-tune-for-performance"></a>성능 모니터링 및 튜닝
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  데이터베이스 모니터링의 목표는 서버의 성능을 평가하는 것입니다. 효과적인 모니터링을 위해서는 현재 성능에 대한 스냅샷을 정기적으로 만들어 문제를 일으키는 프로세스를 격리하고 데이터를 지속적으로 수집하여 성능 경향을 추적해야 합니다.  
  
 지속적인 데이터베이스 성능 평가를 수행하면 응답 시간을 최소화하고 처리량을 최대화할 수 있으므로 성능이 최적화됩니다. 효율적인 네트워크 소통량, 디스크 I/O 및 CPU 사용량을 통해 성능을 최적화할 수 있습니다. 애플리케이션 요구 사항을 완벽하게 분석하고, 데이터의 논리적 및 물리적 구조를 이해하고, 데이터베이스 사용량을 평가하고, OLTP(온라인 트랜잭션 처리) 및 의사 결정 지원과 같이 서로 상충되는 상황인 경우 타협점을 찾아야 합니다.  
  
## <a name="monitoring-and-tuning-databases-for-performance"></a>데이터베이스 성능 모니터링 및 튜닝  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Microsoft Windows 운영 체제에서는 데이터베이스의 현재 상태를 확인하고 상태 변화에 따른 성능을 추적하는 유틸리티를 제공합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 모니터링하는 데 사용할 수 있는 다양한 도구와 기술이 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 모니터링하면 다음 작업에 도움이 됩니다.  
  
-   성능을 향상시킬 수 있는지 알 수 있습니다. 예를 들어 자주 사용하는 쿼리의 응답 시간을 모니터링하면 테이블에 있는 쿼리나 인덱스에 대한 변경이 필요한지 알 수 있습니다.  
  
-   사용자 작업을 평가할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결을 시도하는 사용자를 모니터링하여 보안 설정이 적당한지 확인하고 애플리케이션이나 개발 시스템을 테스트할 수 있습니다. 예를 들어 SQL 쿼리의 실행을 모니터링하면 쿼리가 올바르게 작성되었는지, 결과를 제대로 생성하는지 알 수 있습니다.  
  
-   문제를 해결하거나 저장 프로시저와 같은 애플리케이션 구성 요소를 디버깅할 수 있습니다.  
  
## <a name="monitoring-in-a-dynamic-environment"></a>동적 환경의 모니터링  
조건을 변경하면 성능이 변경됩니다. 평가를 통해 사용자 수 증가, 사용자 액세스 및 연결 방법 변경, 데이터베이스 내용 증가, 클라이언트 애플리케이션 변경, 애플리케이션의 데이터 변경, 쿼리 복잡성 증가, 네트워크 소통량 증가 등에 따라 성능이 바뀌는 것을 알 수 있습니다. 도구를 사용하여 성능을 모니터링하면 변경된 조건 및 복잡한 쿼리에 성능 변경 내용을 연결할 수 있습니다. **예:**  
  
-   자주 사용하는 쿼리의 응답 시간을 모니터링하면 쿼리를 실행할 테이블에 있는 쿼리나 인덱스 변경이 필요한지 여부를 확인할 수 있습니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 실행할 때 모니터링하면 쿼리가 올바르게 작성되며 결과가 예상대로 나타나는지 여부를 확인할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결을 시도하는 사용자를 모니터링하면 보안 설정이 적절한지 여부를 확인하고 애플리케이션이나 개발 시스템을 테스트할 수 있습니다.  
  
응답 시간이란 쿼리가 처리됨을 시각적 확인 형식으로 사용자에게 반환하기 위해 설정된 결과의 첫 행에 필요한 시간의 길이를 말합니다. 처리량이란 지정한 시간 동안 서버에서 처리한 총 쿼리 수를 말합니다.  
  
사용자 수가 증가하면 서버 리소스에 대한 경쟁도 증가하여 응답 시간은 증가하고 전체 처리량은 감소됩니다.  
  
## <a name="monitoring-and-performance-tuning-tasks"></a>모니터링 및 성능 튜닝 태스크  
  
|항목| Task|  
|-----------|----------------------|  
|[SQL Server 구성 요소 모니터링](../../relational-databases/performance/monitor-sql-server-components.md)|작업 모니터, 확장 이벤트 및 동적 관리 뷰 및 함수 등과 같은 모든 SQL Server 구성 요소를 모니터링하는 필수 단계입니다.|  
|[성능 모니터링 및 튜닝 도구](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)|활성 쿼리 통계와 같은 SQL Server 및 데이터베이스 엔진 튜닝 관리자에서 사용 가능한 모니터링 및 튜닝 도구를 나열합니다.|  
|[쿼리 튜닝 도우미를 사용하여 데이터베이스 업그레이드](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)|최신 데이터베이스 호환성 수준으로 업그레이드하는 동안 워크로드 성능 안정성을 유지합니다.|  
|[쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)|쿼리 저장소를 사용하여 쿼리, 계획 및 런타임 통계의 기록을 자동으로 캡처하고 사용자 검토를 위해 보관합니다.|  
|[성능 기준선 설정](../../relational-databases/performance/establish-a-performance-baseline.md)|성능 기준선 설정 방법|  
|[성능 문제 격리](../../relational-databases/performance/isolate-performance-problems.md)|데이터베이스 성능 문제를 격리합니다.|  
|[병목 상태 식별](../../relational-databases/performance/identify-bottlenecks.md)|서버 성능을 모니터링하고 추적하여 병목 상태를 식별합니다.|  
|[DMV를 사용하여 뷰의 사용 통계 및 성능 확인](../../relational-databases/performance/use-dmvs-determine-usage-performance-views.md)|쿼리 성능에 대한 정보를 가져오는 데 사용되는 방법 및 스크립트를 설명합니다.|  
|[서버 성능 및 작업 모니터링](../../relational-databases/performance/server-performance-and-activity-monitoring.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 Windows 성능 및 활동 모니터링 도구를 사용합니다.|  
|[리소스 사용 모니터링](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)|시스템 모니터(perfmon이라고도 함)를 통해 성능 카운터를 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 성능을 측정합니다.|  

  
## <a name="see-also"></a>참고 항목  
 [기업 내 관리 자동화](../../ssms/agent/automated-administration-across-an-enterprise.md)    
 [실행 계획 비교 및 분석](../../relational-databases/performance/compare-and-analyze-execution-plans.md)    
 [실행 계획 표시 및 저장](../../relational-databases/performance/display-and-save-execution-plans.md)    
  
  
