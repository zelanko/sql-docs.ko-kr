---
title: 분석 플랫폼 시스템에서 작업 관리 | Microsoft Docs
description: 분석 플랫폼 시스템에서 작업 관리입니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: a4f748ed39705f865a303f1b59ae352068f93431
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707101"
---
# <a name="workload-management-in-analytics-platform-system"></a>분석 플랫폼 시스템에서 작업 관리

SQL Server PDW 작업 관리 기능에는 사용자와 관리자가 미리 메모리 및 동시성의 구성 설정에 대 한 요청을 할당 하려면 허용 합니다. 작업 관리를 사용 하 여 모든 요청을 무기한 함으로써 적절 한 리소스에 요청을 허용 하 여 일관 된 또는 혼합 워크 로드의 성능을 향상 합니다.  
  
예를 들어 SQL Server PDW에서 작업 관리 기법을 사용 하면 수행할 수 있습니다.  
  
-   많은 수의 로드 작업을 하는 리소스를 할당 합니다.  
  
-   Columnstore 인덱스 구축을 위한 더 많은 리소스를 지정 합니다.  
  
-   더 많은 메모리를 해야 하는 경우를 확인 하려면 수행이 속도가 느린 해시 조인 문제를 해결 하 고 더 많은 메모리 부여 합니다.  
  
## <a name="Basics"></a>작업 관리 기본 사항  
  
### <a name="key-terms"></a>주요 용어  
작업 관리  
*작업 관리* 이해 하 고 동시 요청에 대 한 최상의 성능을 얻기 위해 시스템 리소스 사용률을 조정 하는 기능입니다.  
  
리소스 클래스입니다.  
SQL Server PDW에서는 *리소스 클래스* 는 메모리와 동시성에 대 한 미리 할당 된 제한에 있는 기본 제공 서버 역할입니다. SQL Server PDW는 요청을 제출 하는 로그인의 리소스 클래스 서버 역할 멤버 자격에 따라 요청 하는 리소스를 할당 합니다.  
  
계산 노드에서 리소스 클래스의 구현 SQL Server의 리소스 관리자 기능을 사용합니다. 리소스 관리자에 대 한 자세한 내용은 참조 하십시오. [리소스 관리자](http://msdn.microsoft.com/library/bb933866(v=sql.11).aspx) msdn 합니다.  
  
### <a name="understand-current-resource-utilization"></a>현재 리소스 사용률을 이해  
현재 실행 중인 요청에 대 한 시스템 리소스 사용률을 이해 하려면 SQL Server PDW 동적 관리 뷰를 사용 합니다. 예를 들어 더 많은 메모리를 포함 하면 실행 속도가 느린 큰 해시 조인이 유리한 경우를 이해 하려면 Dmv를 사용할 수 있습니다.  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>리소스 할당을 조정 합니다.  
리소스 사용률을 조정 하려면 요청을 제출 하는 로그인의 리소스 클래스 멤버 자격을 변경 합니다. 리소스 클래스 서버 역할 이름은 **mediumrc**, **largerc**, 및 **xlargerc**합니다. 중형, 대형 및 초대형 리소스 할당을 각각 나타냅니다.  
  
예를 들어 많은 양의 요청에 시스템 리소스를 할당 하려면 요청을 전송 하는 로그인을 추가 **largerc** 서버 역할입니다. 다음 ALTER SERVER ROLE 문을 largerc 서버 역할에 로그인 Anna를 추가합니다.  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>리소스 클래스 설명  
다음 표에서 리소스 클래스 및 해당 시스템 리소스 할당을 설명합니다.  
  
|리소스 클래스입니다.|요청 중요도|최대 메모리 사용 *|동시성 슬롯 (최대 32 =)|Description|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|기본|보통|400MB|1|기본적으로 각 로그인에는 약간의 메모리 및 동시성 리소스의 요청에 대 한 허용 됩니다.<br /><br />로그인 리소스 클래스에 추가 되 면 새 클래스 우선적으로 적용 합니다. 로그인은 모든 리소스 클래스에서 삭제 되 면 기본 리소스 할당에 다시 로그인이 되돌립니다.|  
|MediumRC|보통|1200MB|3|중간 리소스 클래스를 할 수 있는 요청의 예:<br /><br />큰이 있는 CTAS에는 작업 해시 조인 합니다.<br /><br />디스크에 대 한 캐싱을 방지 하기 위해 더 많은 메모리를 필요로 하는 작업을 선택 합니다.<br /><br />클러스터형된 columnstore 인덱스에 데이터를 로드 합니다.<br /><br />빌드, 다시 작성 및 10-15 열이 있는 작은 테이블에 대 한 클러스터형된 columnstore 인덱스 다시 구성 합니다.|  
|largerc|높음|2.8 G B|7|큰 리소스 클래스를 할 수 있는 요청의 예:<br /><br />큰 해시 조인 또는 큰 ORDER BY 또는 GROUP BY 절 등의 많은 집계를 포함 하는 매우 큰 CTAS에는 작업입니다.<br /><br />해시 조인 등의 작업 또는 ORDER BY 또는 GROUP BY 절 같은 집계에 대 한 매우 많은 양의 메모리를 필요로 하는 작업을 선택 합니다.<br /><br />클러스터형된 columnstore 인덱스에 데이터를 로드 합니다.<br /><br />빌드, 다시 작성 및 10-15 열이 있는 작은 테이블에 대 한 클러스터형된 columnstore 인덱스 다시 구성 합니다.|  
|xlargerc|높음|8.4 GB|22|런타임 시 초대형 리소스 소비 해야 하는 요청에 대 한 초대형 리소스 클래스가입니다.|  
  
<sup>*</sup>최대 메모리 사용량은 추정치입니다.  
  
### <a name="request-importance"></a>요청 중요도  
요청 중요도 계산 노드에서 실행 되는 SQL Server에서 요청에 제공 하는 CPU 시간에 매핑됩니다.  요청 우선 순위가 높은 더 많은 CPU 시간을 수신 합니다.  
  
### <a name="maximum-memory-usage"></a>최대 메모리 사용량  
최대 메모리 사용량은 요청이 각 처리 공간 내에서 사용할 수는 사용 가능한 메모리의 최대 크기입니다. 예를 들어 mediumrc 요청이 각 배포 내에서 처리를 위해 최대 1200MB를 사용할 수 있습니다. 아직 데이터가 대부분의 작업을 수행 하는 몇 가지 배포 하지 않아도 되도록 비대칭 하지 확인 하는 것이 유용 합니다.  
  
### <a name="concurrency-slots"></a>동시성 슬롯  
1, 3, 7 및 22 동시성 슬롯 할당의 목표는 크고 작은 프로세스를 큰 프로세스가 실행 중일 때 작은 프로세스를 차단 하지 않고 동시에 실행할 수 있도록입니다.  예를 들어 SQL Server PDW 최대 한 번에 1 초대형 요청 (22 슬롯), 1 큰 요청 (7), 슬롯 및 1 중간 요청 (3 슬롯)를 실행 하는 32 동시성 슬롯을 할당할 수 있습니다.  
  
동시 요청에 최대 32 동시성 슬롯을 할당의 예:  
  
-   28 슬롯 = 큰 4  
  
-   30 슬롯 = 10 보통  
  
-   32 슬롯 = 32 기본값  
  
-   32 슬롯 = 초대형 1 + 1 큰 + 1 중간  
  
-   32 슬롯 = 2 큰 + 4 중간 + 6 기본값  
  
SQL Server PDW에 6 큰 요청을 전송할 10 기본 요청이 제출 되는 다음 한다고 가정 합니다. SQL Server PDW 우선 순위에 따라 요청을 다음과 같이 처리 됩니다.  
  
-   메모리를 사용할 수 있게 되 면 4 큰 요청을 처리 하기 시작 28 동시성 슬롯을 할당 하 고 2 큰 요청을 큐에 유지 합니다.  
  
-   4 기본 요청 처리를 시작 하려면 4 동시성 슬롯을 할당 하 고 6 기본 요청 대기 큐에 유지 합니다.  
  
요청 완료와 동시성 슬롯을 사용할 수 SQL Server PDW 사용 가능한 리소스 및 우선 순위에 따라 나머지 요청을 할당 합니다. 예를 들어 슬롯 열고 7 동시성을 대기 중인 큰 요청 됩니다 보다 우선 순위가 더 높은 7 슬롯에 대 한 대기 중인 중간 요청 합니다.  6 개의 슬롯을 여는 경우 SQL Server PDW 6 더 많은 기본 크기의 요청을 할당 합니다. 그러나 메모리와 동시성 슬롯 모두 제공 해야 SQL Server PDW 실행 하 라는 요청을 허용 합니다.  
  
각 리소스 클래스 내에서 요청에서 첫 번째로 FIFO (선입 선출) 순서로 실행 됩니다.  
  
## <a name="GeneralRemarks"></a>일반적인 주의 사항  
둘 이상의 리소스 클래스의 멤버인 로그인을 사용 하는 경우 가장 많은 리소스를 사용 하 여 클래스 우선적으로 적용 합니다.  
  
변경 내용이 모든 향후 요청;에 대해 즉시 적용 로그인에 추가 또는 리소스 클래스에서 삭제 된 경우 현재 요청을 실행 하거나 대기 하는 영향을 받지 않습니다. 로그인의 되려면 변경 끊었다가 필요가 없습니다.  
  
각 로그인에 대 한 리소스 클래스 설정 세션 아니라 개별 문 및 작업에 적용 됩니다.  
  
SQL Server PDW는 문이 실행 되기 전에 요청에 필요한 동시성 슬롯을 획득 하려고 시도 합니다. 충분 한 동시성 슬롯 획득할 수 없으므로, SQL Server PDW 요청 실행 대기 상태로 이동 합니다. 요청에 이미 할당 된 모든 관리 시스템은 시스템에 다시 반환 됩니다.  
  
대부분의 SQL 문 기본 리소스 할당에는 항상 필요 하 고 리소스 클래스에 의해 제어 되지 않습니다. 예를 들어 CREATE LOGIN만 적은 양의 리소스를 필요 하 고 CREATE LOGIN을 호출 하는 로그인의 멤버인 경우에 기본 리소스를 할당 되는 리소스 클래스입니다.  예를 들어 Anna가 largerc 리소스 클래스의 멤버인 그녀에서 CREATE LOGIN 문을 전송 하는 경우 CREATE LOGIN 문의 리소스의 기본 수도 실행 됩니다.  
  
SQL 문 및 리소스 클래스에 의해 제어 되는 작업의 경우:  
  
-   ALTER  INDEX  REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   ALTER 테이블 REBUILD  
  
-   클러스터형된 인덱스 만들기  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   TABLE AS SELECT 만들기  
  
-   원격 TABLE AS SELECT 만들기  
  
-   데이터를 로드할 **dwloader**합니다.  
  
-   INSERT SELECT  
  
-   UPDATE  
  
-   Delete  
  
-   RESTORE DATABASE 어플라이언스에 더 많은 계산 노드를 복원 하는 경우.  
  
-   DMV 전용 쿼리를 제외 하 고, 선택  
  
## <a name="Limits"></a>제한 사항  
리소스 클래스 메모리 할당과 동시성 할당을 제어합니다.  입/출력 작업은 적용 되지 않습니다.  
  
## <a name="Metadata"></a>메타 데이터  
리소스 클래스와 리소스 클래스 멤버에 대 한 정보를 포함 하는 Dmv  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
요청 및 필요한 리소스의 상태에 대 한 정보를 포함 하는 Dmv:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
계산 노드의 SQL Server Dmv를 통해 노출 되는 관련된 시스템 뷰. 참조 [SQL Server 동적 관리 뷰](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) msdn 이러한 Dmv에 대 한 링크입니다.  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodes_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodws_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_exec_sessions  
  
-   sys.dm_pdw_nodes_exec_requests  
  
-   sys.dm_pdw_nodes_exec_query_memory_grants  
  
-   sys.dm_pdw_nodes_exec_query_resource_semaphores  
  
-   sys.dm_pdw_nodes_os_memory_brokers  
  
-   sys.dm_pdw_nodes_os_memory_cache_entries  
  
-   sys.dm_pdw_nodes_exec_cached_plans  
  
## <a name="RelatedTasks"></a>관련된 태스크  
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
  
