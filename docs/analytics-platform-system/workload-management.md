---
title: Analytics Platform System의 워크 로드 관리 | Microsoft Docs
description: Analytics Platform System의 워크 로드 관리 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2281262c086f4d8dcab27debc8bb735ea5e8e1ba
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52419884"
---
# <a name="workload-management-in-analytics-platform-system"></a>Analytics Platform System의 워크 로드 관리

SQL Server PDW 워크 로드 관리 기능에는 사용자 및 관리자 메모리 및 동시성의 구성을 미리 설정에 대 한 요청을 할당할 수 있습니다. 적절 한 리소스 요청을 영구적으로 서비스가 없는 것을 요청 함으로써 워크 로드에 일관 된 또는 혼합의 성능을 향상 시키려면 워크 로드 관리를 사용 합니다.  
  
예를 들어, SQL Server PDW에서 워크 로드 관리 기법을 사용 하 여 할 수 있습니다.  
  
-   많은 수의 로드 작업에 리소스를 할당 합니다.  
  
-   Columnstore 인덱스 구축을 위한 더 많은 리소스를 지정 합니다.  
  
-   느리게 해시 조인이 더 많은 메모리를 해야 하는 경우를 확인 하려면 문제를 해결 하 고 더 많은 메모리 부여 합니다.  
  
## <a name="Basics"></a>워크 로드 관리 기본 사항  
  
### <a name="key-terms"></a>주요 용어  
워크 로드 관리  
*워크 로드 관리* 이해 및 동시 요청에 대 한 최상의 성능을 얻기 위해 시스템 리소스 사용률을 조정 하는 기능입니다.  
  
리소스 클래스  
SQL Server PDW에는 *리소스 클래스* 는 기본 제공 서버 역할에 미리 할당 된 메모리 및 동시성 제한입니다. SQL Server PDW는 요청을 제출 하는 로그인의 리소스 클래스 서버 역할 멤버 자격에 따라 요청에는 리소스를 할당 합니다.  
  
계산 노드에서 리소스 클래스의 구현을 SQL Server에서 리소스 관리자 기능을 사용합니다. 리소스 관리자에 대 한 자세한 내용은 참조 하세요. [Resource Governor](../relational-databases/resource-governor/resource-governor.md) MSDN에 있습니다.  
  
### <a name="understand-current-resource-utilization"></a>현재 리소스 사용률을 이해  
현재 실행 중인 요청에 대 한 시스템 리소스 사용률을 이해 하려면 SQL Server PDW 동적 관리 뷰를 사용 합니다. 예를 들어, 실행 속도가 느린 큰 해시 조인이 더 많은 메모리를 함으로써 이점을 얻을 수는 경우를 이해 하려면 Dmv를 사용할 수 있습니다.  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>리소스 할당을 조정 합니다.  
리소스 사용률을 조정 하려면 요청을 제출 하는 로그인의 리소스 클래스 멤버 자격을 변경 합니다. 리소스 클래스 서버 역할 이름은 **mediumrc**를 **largerc**, 및 **xlargerc**합니다. 중형, 대형 및 초대형 리소스 할당을 각각 나타냅니다.  
  
예를 들어, 많은 양의 요청에 대 한 시스템 리소스를 할당 하려면 요청을 제출 하는 로그인을 추가 합니다 **largerc** 서버 역할입니다. 다음 ALTER SERVER ROLE 문을 largerc 서버 역할에 Anna 로그인을 추가합니다.  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>리소스 클래스 설명  
다음 표에서 리소스 클래스 및 해당 시스템 리소스 할당에 설명합니다.  
  
|리소스 클래스|중요도 요청 합니다.|최대 메모리 사용 *|동시성 슬롯 수 (최대 32 =)|Description|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|기본|보통|400MB|1|기본적으로 각 로그인에는 적은 양의 메모리 및 동시성 리소스의 요청에 대 한 허용 됩니다.<br /><br />로그인은 리소스 클래스에 추가 되 면 새 클래스는 우선 합니다. 모든 리소스 클래스에서 로그인을 삭제 하면 기본 리소스 할당에 다시 로그인이 되돌립니다.|  
|MediumRC|보통|1200 MB|3|중간 리소스 클래스를 필요로 할 수 있는 요청 예제:<br /><br />크게는 CTAS 작업 해시 조인 합니다.<br /><br />더 많은 메모리를 디스크에 캐시 하지 않도록 해야 하는 작업을 선택 합니다.<br /><br />클러스터형된 columnstore 인덱스에 데이터를 로드 합니다.<br /><br />빌드, 다시 작성 및 10 ~ 15 개 열이 있는 작은 테이블에 클러스터형된 columnstore 인덱스 다시 구성 합니다.|  
|Largerc|높음|2.8 GB|7|큰 리소스 클래스를 필요로 할 수 있는 요청 예제:<br /><br />큰 해시 조인 또는 큰 ORDER BY 또는 GROUP BY 절 등 많은 집계를 포함 하는 매우 큰 CTAS 작업입니다.<br /><br />해시 조인 등의 작업 또는 ORDER BY 또는 GROUP BY 절 등 집계에 대 한 매우 많은 양의 메모리를 필요로 하는 작업을 선택 합니다.<br /><br />클러스터형된 columnstore 인덱스에 데이터를 로드 합니다.<br /><br />빌드, 다시 작성 및 10 ~ 15 개 열이 있는 작은 테이블에 클러스터형된 columnstore 인덱스 다시 구성 합니다.|  
|xlargerc|높음|8.4 GB|22|초대형 리소스 클래스는 런타임에 초대형 리소스 소비를 필요할 수 있는 요청입니다.|  
  
<sup>*</sup>최대 메모리 사용량은 근사치입니다.  
  
### <a name="request-importance"></a>중요도 요청 합니다.  
요청 중요도 계산 노드에서 실행 중인 SQL Server에서 요청에 제공 하는 CPU 시간에 매핑됩니다.  요청 우선 순위가 높은 CPU 시간이 더 많이 받습니다.  
  
### <a name="maximum-memory-usage"></a>최대 메모리 사용량  
최대 메모리 사용량이 최대 사용 가능한 메모리 요청이 각 처리 공간 내에서 사용할 수 있습니다. 예를 들어 mediumrc 요청이 각 배포 내에서 처리를 위해 1200MB를 사용할 수 있습니다. 대부분의 작업을 수행 하는 몇 가지 배포 되지 않도록 하기 위해 하지 기울어진 데이터 인 되도록 여전히이 반드시 합니다.  
  
### <a name="concurrency-slots"></a>동시성 슬롯 수  
1, 3, 7 및 22 동시성 슬롯을 할당 하는 목적은 크건 작건 프로세스를 큰 프로세스가 실행 중일 때 작은 프로세스를 차단 하지 않고 동시에 실행할 수 있도록 하는 것입니다.  예를 들어, SQL Server PDW는 최대 동시 1 초대형 요청 (22 슬롯), 1 큰 요청 (7 슬롯) 및 1 중간 요청 (3 개의 슬롯)을 실행 하려면 32 개의 동시성 슬롯을 할당할 수 있습니다.  
  
동시 요청 수를 최대 32 개의 동시성 슬롯을 할당 하는 예제:  
  
-   28 슬롯 = 큰 4  
  
-   30 슬롯 = 보통 10  
  
-   32 개의 슬롯 = 32 기본값  
  
-   32 개의 슬롯 = 초대형 1 + 1 큰 + 1-보통  
  
-   32 개의 슬롯 = 2 큰 + 4 중간 + 6 기본  
  
SQL Server PDW에 제출 되는 6 큰 요청 및 10 개의 기본 요청을 제출 하는 고 가정 합니다. SQL Server PDW 우선 순위에 따라 요청을 다음과 같이 처리 됩니다.  
  
-   메모리를 사용할 수 있게 하는 대로 4 큰 요청을 처리 하려면 28 동시성 슬롯을 할당 하 고 큐에서 큰 요청이 2 개를 유지 합니다.  
  
-   4 개의 기본 요청을 처리 하려면 4 개의 동시성 슬롯을 할당 하 고 대기 큐에 있는 6 기본 요청을 계속 합니다.  
  
요청이 완료와 동시성 슬롯을 사용할 수 있게 SQL Server PDW는 사용 가능한 리소스 및 우선 순위에 따라 나머지 요청을 할당 합니다. 예를 들어 7 동시성 슬롯을 열 경우 큰 요청을 대기 해야 보다 우선 순위가 7 슬롯에 대해 대기 중인 중간 요청 합니다.  6 개의 슬롯을 여는 경우 6 개 더 많은 기본 크기의 요청이 SQL Server PDW에 할당 됩니다. 그러나 메모리 및 동시성 슬롯 모두 사용할 수 있어야 SQL Server PDW 실행 하 라는 요청을 허용 합니다.  
  
각 리소스 클래스 내에서 FIFO (선입 선출) 순서에서 첫 번째에서 요청을 실행합니다.  
  
## <a name="GeneralRemarks"></a>일반적인 주의 사항  
둘 이상의 리소스 클래스의 멤버인 로그인을 사용 하는 경우 대부분의 리소스를 사용 하 여 클래스 우선 합니다.  
  
변경 내용이 모든 향후 요청에 대해 즉시 적용 로그인을 추가 하거나 리소스 클래스에서 삭제 대기 중이거나 실행은 현재 요청을 받지 않습니다. 로그인 연결을 끊고 되려면 변경을 위해 다시 연결할 필요가 없습니다.  
  
각 로그인에 대 한 리소스 클래스 설정은 세션이 아닌 개별 문 및 작업에 적용 됩니다.  
  
SQL Server PDW 문이 실행 되기 전에 요청에 필요한 동시성 슬롯을 가져오려고 시도 합니다. 충분 한 동시성 슬롯을 획득할 수 없으면 SQL Server PDW 요청의 실행 대기 상태로 이동 합니다. 요청에 이미 할당 된 모든 리소스 시스템은 시스템에 다시 반환 됩니다.  
  
대부분의 SQL 문에 항상 기본 리소스 할당을 사용 해야 하 고 리소스 클래스에 의해 제어 되지 않습니다. 예를 들어 CREATE LOGIN만 적은 양의 리소스를 하며 CREATE LOGIN을 호출 하는 로그인을 사용 하면 리소스 클래스의 멤버인 경우에 기본 리소스를 할당 됩니다.  예를 들어 Anna가 largerc 리소스 클래스의 멤버인 경우 CREATE LOGIN 문의 제출 그녀는 CREATE LOGIN 문에 리소스의 기본 수를 사용 하 여 실행 됩니다.  
  
SQL 문 및 리소스 클래스에 의해 제어 되는 작업:  
  
-   ALTER  INDEX  REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   ALTER TABLE REBUILD  
  
-   클러스터형된 인덱스 만들기  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   CREATE TABLE AS SELECT  
  
-   CREATE REMOTE TABLE AS SELECT  
  
-   사용 하 여 데이터 로드 **dwloader**합니다.  
  
-   INSERT SELECT  
  
-   UPDATE  
  
-   Delete  
  
-   RESTORE DATABASE 더 많은 계산 노드를 사용 하 여 어플라이언스로 복원 하는 경우.  
  
-   선택, DMV 전용 쿼리를 제외 합니다.  
  
## <a name="Limits"></a>제한 사항  
리소스 클래스 할당 메모리 및 동시성을 제어합니다.  입/출력 작업을 제어 하지 않는다는 점에서 합니다.  
  
## <a name="Metadata"></a>메타 데이터  
리소스 클래스 및 리소스 클래스 멤버에 대 한 정보를 포함 하는 Dmv 합니다.  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
요청 및 필요한 리소스의 상태에 대 한 정보를 포함 하는 Dmv:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
관련된 시스템 보기에서 계산 노드의 SQL Server Dmv를 통해 노출 합니다. 참조 [SQL Server 동적 관리 뷰](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) MSDN에서 이러한 Dmv에 대 한 링크입니다.  
  
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
[워크 로드 관리 작업](workload-management-tasks.md)  
  
<!-- MISSING LINKS
See the Workload Management section of [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md) for the following tasks:  
  
1.  Find the number of active requests for each resource group.  
  
2.  Determine if my requests need more memory  
  
3.  Determine if there are a high number of query optimizations or suboptimal plan generations.  
  
4.  Determine Average CPU time per request in each resource pool to date  
  
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
