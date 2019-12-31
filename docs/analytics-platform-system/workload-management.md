---
title: 워크로드 관리
description: 분석 플랫폼 시스템의 워크 로드 관리
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: d14714cb23a9f6b0d6cc63ddca5049cb6741017c
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399441"
---
# <a name="workload-management-in-analytics-platform-system"></a>분석 플랫폼 시스템의 워크 로드 관리

SQL Server PDW의 워크 로드 관리 기능을 사용 하 여 사용자와 관리자는 미리 설정 된 메모리 구성 및 동시성에 대 한 요청을 할당할 수 있습니다. 작업 관리를 사용 하 여 요청을 함으로써 하지 않고 적절 한 리소스를 요청에 포함 하 여 일관 되거나 혼합 된 작업의 성능을 향상 시킬 수 있습니다.  
  
예를 들어 SQL Server PDW의 워크 로드 관리 기술을 사용 하 여 다음을 할 수 있습니다.  
  
-   많은 수의 리소스를 로드 작업에 할당 합니다.  
  
-   Columnstore 인덱스를 빌드하기 위한 추가 리소스를 지정 합니다.  
  
-   속도가 느려지는 해시 조인 문제를 해결 하 여 더 많은 메모리가 필요한 경우이를 확인 하 고 더 많은 메모리를 제공 합니다.  
  
## <a name="Basics"></a>워크 로드 관리 기본 사항  
  
### <a name="key-terms"></a>주요 용어  
워크로드 관리  
*워크 로드 관리* 는 동시 요청에 대 한 최상의 성능을 얻기 위해 시스템 리소스 사용률을 이해 하 고 조정 하는 기능입니다.  
  
리소스 클래스  
SQL Server PDW에서 *리소스 클래스* 는 메모리 및 동시성에 대해 미리 할당 된 제한을 포함 하는 기본 제공 서버 역할입니다. SQL Server PDW은 요청을 전송 하는 로그인의 리소스 클래스 서버 역할 멤버 자격에 따라 요청에 리소스를 할당 합니다.  
  
계산 노드에서 리소스 클래스의 구현은 SQL Server의 Resource Governor 기능을 사용 합니다. Resource Governor에 대 한 자세한 내용은 MSDN의 [Resource Governor](../relational-databases/resource-governor/resource-governor.md) 를 참조 하십시오.  
  
### <a name="understand-current-resource-utilization"></a>현재 리소스 사용률 이해  
현재 실행 중인 요청에 대 한 시스템 리소스 사용률을 이해 하려면 SQL Server PDW 동적 관리 뷰를 사용 합니다. 예를 들어 Dmv를 사용 하 여 더 많은 메모리를 사용 하 여 느리게 실행 되는 큰 해시 조인이 이점을 얻을 수 있는지 파악할 수 있습니다.  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>리소스 할당 조정  
리소스 사용률을 조정 하려면 요청을 제출 하는 로그인의 리소스 클래스 멤버 자격을 변경 합니다. 리소스 클래스 서버 역할의 이름은 **mediumrc**, **largerc**및 **xlargerc**입니다. 중간, 대형 및 초대형 리소스 할당을 각각 나타냅니다.  
  
예를 들어 요청에 많은 양의 시스템 리소스를 할당 하려면 **largerc** 서버 역할에 요청을 제출 하는 로그인을 추가 합니다. 다음 ALTER SERVER ROLE 문은 로그인 Anna을 largerc 서버 역할에 추가 합니다.  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>리소스 클래스 설명  
다음 표에서는 리소스 클래스 및 해당 시스템 리소스 할당에 대해 설명 합니다.  
  
|리소스 클래스|요청 중요도|최대 메모리 사용량 *|동시성 슬롯 (최대값 = 32)|설명|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|기본값|중간|400 MB|1|기본적으로 각 로그인은 적은 양의 메모리와 해당 요청에 대 한 동시성 리소스를 허용 합니다.<br /><br />리소스 클래스에 로그인을 추가 하면 새 클래스가 우선적으로 적용 됩니다. 모든 리소스 클래스에서 로그인을 삭제 하면 해당 로그인은 기본 리소스 할당으로 돌아갑니다.|  
|MediumRC|중간|1200 M B|3|중간 리소스 클래스가 필요할 수 있는 요청의 예는 다음과 같습니다.<br /><br />해시 조인이 많은 CTAS 작업<br /><br />디스크로의 캐싱을 방지 하기 위해 더 많은 메모리가 필요한 작업을 선택 합니다.<br /><br />클러스터형 columnstore 인덱스에 데이터를 로드 하는 중입니다.<br /><br />10-15 개의 열이 있는 작은 테이블에 대 한 클러스터형 columnstore 인덱스를 작성, 다시 작성 및 다시 구성 합니다.|  
|Largerc|높음|2.8 GB|7|대량 리소스 클래스가 필요할 수 있는 요청의 예는 다음과 같습니다.<br /><br />매우 큰 해시 조인이 있거나 큰 ORDER BY 또는 GROUP BY 절과 같은 대규모 집계를 포함 하는 매우 큰 CTAS 작업<br /><br />해시 조인과 같은 작업에 대해 매우 많은 양의 메모리가 필요한 작업 또는 ORDER BY 또는 GROUP BY 절과 같은 집계를 선택 합니다.<br /><br />클러스터형 columnstore 인덱스에 데이터를 로드 하는 중입니다.<br /><br />10-15 개의 열이 있는 작은 테이블에 대 한 클러스터형 columnstore 인덱스를 작성, 다시 작성 및 다시 구성 합니다.|  
|xlargerc|높음|8.4 GB|22|추가 대형 리소스 클래스는 런타임에 추가 리소스 소비가 필요할 수 있는 요청에 대 한 것입니다.|  
  
<sup>*</sup>최대 메모리 사용량은 근사값입니다.  
  
### <a name="request-importance"></a>요청 중요도  
요청 중요도는 계산 노드에서 실행 되는 SQL Server이 요청에 제공 하는 CPU 시간의 양에 매핑됩니다.  우선 순위가 더 높은 요청은 더 많은 CPU 시간을 받습니다.  
  
### <a name="maximum-memory-usage"></a>최대 메모리 사용량  
최대 메모리 사용량은 요청에서 각 처리 공간 내에 사용할 수 있는 최대 메모리 양입니다. 예를 들어 mediumrc 요청은 각 배포 내에서 처리 하는 데 최대 1200 MB를 사용할 수 있습니다. 대부분의 작업을 수행 하는 몇 가지 배포가 발생 하지 않도록 하기 위해 데이터가 왜곡 되지 않도록 하는 것도 중요 합니다.  
  
### <a name="concurrency-slots"></a>동시성 슬롯  
1, 3, 7 및 22 동시성 슬롯을 할당 하는 목표는 대량 프로세스가 실행 중일 때 작은 프로세스를 차단 하지 않고 크고 작은 프로세스를 동시에 실행할 수 있도록 하는 것입니다.  예 SQL Server PDW를 들어 최대 32 개의 동시성 슬롯을 할당 하 여 1 개의 추가 대량 요청 (22 개 슬롯), 1 개의 대량 요청 (7 개 슬롯) 및 1 개의 중간 요청 (3 개 슬롯)을 동시에 실행할 수 있습니다.  
  
동시 요청에 최대 32의 동시성 슬롯을 할당 하는 예제:  
  
-   28 슬롯 = 4 큼  
  
-   30 개 슬롯 = 10medium  
  
-   32 슬롯 = 32 기본값  
  
-   32 슬롯 = 1 매우 큼 + 1 큼 + 1 중간  
  
-   32 슬롯 = 2 큼 + 4 중간 + 6 기본값  
  
6 개의 대량 요청이 SQL Server PDW 전송 된 다음 10 개의 기본 요청이 전송 된다고 가정 합니다. SQL Server PDW는 다음과 같이 요청을 우선 순위 순서 대로 처리 합니다.  
  
-   메모리를 사용할 수 있게 되 면 28 개의 동시성 슬롯을 할당 하 여 4 개의 대량 요청 처리를 시작 하 고 두 개의 대량 요청을 큐에 유지 합니다.  
  
-   4 개의 동시성 슬롯을 할당 하 여 4 개의 기본 요청 처리를 시작 하 고 대기 큐에 6 개의 기본 요청을 유지 합니다.  
  
요청을 완료 하 고 동시성 슬롯을 사용할 수 있게 되 면 사용 가능한 리소스 및 우선 순위에 따라 남은 요청을 할당 SQL Server PDW 합니다. 예를 들어 동시성 슬롯이 7 개 열려 있는 경우 대기 중인 큰 요청은 중간 요청을 대기 하는 것 보다 7 개 슬롯의 우선 순위가 높습니다.  6 개의 슬롯이 열리면 SQL Server PDW은 6 개 이상의 기본 크기 요청을 할당 합니다. 그러나 SQL Server PDW 요청을 실행 하려면 메모리 및 동시성 슬롯을 모두 사용할 수 있어야 합니다.  
  
각 리소스 클래스 내에서 요청은 FIFO (선입 선출) 순서 대로 실행 됩니다.  
  
## <a name="GeneralRemarks"></a>일반적인 주의 사항  
로그인이 둘 이상의 리소스 클래스의 멤버인 경우 리소스가 가장 많은 클래스가 우선적으로 적용 됩니다.  
  
리소스 클래스에서 로그인을 추가 하거나 삭제 하면 이후의 모든 요청에 대해 변경 내용이 즉시 적용 됩니다. 실행 중이거나 대기 중인 현재 요청은 영향을 받지 않습니다. 변경 내용을 발생 시키려면 로그인의 연결을 끊고 다시 연결 해야 합니다.  
  
각 로그인에 대해 리소스 클래스 설정은 세션이 아닌 개별 문과 작업에 적용 됩니다.  
  
SQL Server PDW 문을 실행 하기 전에 요청에 필요한 동시성 슬롯을 가져오려고 시도 합니다. 충분 한 동시성 슬롯을 획득할 수 없는 경우 SQL Server PDW은 요청을 실행 대기 중 상태로 이동 합니다. 요청에 이미 할당 된 모든 리소스 시스템은 시스템으로 다시 반환 됩니다.  
  
대부분의 SQL 문에는 항상 기본 리소스 할당이 필요 하므로 리소스 클래스에 의해 제어 되지 않습니다. 예를 들어 CREATE login은 적은 양의 리소스만 필요 하며, CREATE LOGIN을 호출 하는 로그인이 리소스 클래스의 멤버인 경우에도 기본 리소스가 할당 됩니다.  예를 들어 Anna가 largerc 리소스 클래스의 멤버이 고 CREATE LOGIN 문을 전송 하는 경우 CREATE LOGIN 문은 기본 리소스 수로 실행 됩니다.  
  
리소스 클래스에 의해 제어 되는 SQL 문 및 작업:  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   ALTER TABLE REBUILD  
  
-   클러스터형 인덱스 만들기  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   CREATE TABLE AS SELECT  
  
-   CREATE REMOTE TABLE AS SELECT  
  
-   **Dwloader**를 사용 하 여 데이터를 로드 하는 중입니다.  
  
-   INSERT-SELECT  
  
-   UPDATE  
  
-   삭제  
  
-   더 많은 계산 노드를 사용 하 여 어플라이언스로 복원할 때 데이터베이스를 복원 합니다.  
  
-   DMV 전용 쿼리를 제외 하 고 선택  
  
## <a name="Limits"></a>제한 사항  
리소스 클래스는 메모리 및 동시성 할당을 제어 합니다.  이러한 작업은 입/출력 작업을 제어 하지 않습니다.  
  
## <a name="Metadata"></a>메타  
리소스 클래스 및 리소스 클래스 멤버에 대 한 정보를 포함 하는 Dmv입니다.  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
요청 상태와 필요한 리소스에 대 한 정보를 포함 하는 Dmv:  
  
-   [sys. dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys. dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
계산 노드의 SQL Server Dmv에서 노출 되는 관련 시스템 뷰입니다. MSDN의 이러한 Dmv에 대 한 링크는 [SQL Server 동적 관리 뷰](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) 를 참조 하세요.  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodes_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys. dm_pdw_nodws_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_exec_sessions  
  
-   sys.dm_pdw_nodes_exec_requests  
  
-   sys.dm_pdw_nodes_exec_query_memory_grants  
  
-   sys.dm_pdw_nodes_exec_query_resource_semaphores  
  
-   sys.dm_pdw_nodes_os_memory_brokers  
  
-   sys.dm_pdw_nodes_os_memory_cache_entries  
  
-   sys.dm_pdw_nodes_exec_cached_plans  
  
## <a name="RelatedTasks"></a>관련 태스크  
[작업 관리 작업](workload-management-tasks.md)  
  
<!-- MISSING LINKS
See the Workload Management section of [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md) for the following tasks:  
  
1.  Find the number of active requests for each resource group.  
  
2.  Determine if my requests need more memory  
  
3.  Determine if there are a high number of query optimizations or suboptimal plan generations.  
  
4.  Determine Average CPU time per request in each resource pool to date  
  
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
