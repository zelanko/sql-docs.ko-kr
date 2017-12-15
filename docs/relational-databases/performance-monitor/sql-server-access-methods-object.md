---
title: "SQL Server, Access Methods 개체 | Microsoft 문서"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access Methods object
- SQLServer:Access Methods
ms.assetid: 27558585-e780-48bb-a042-30d664662ebc
caps.latest.revision: "36"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 771047d7d21f79827c9ca073d22f2094f8603f0f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-access-methods-object"></a>SQL Server, Access Methods 개체
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 **Access Methods** 개체는 데이터베이스 내의 논리 페이지에 액세스하는 방법을 모니터링하는 카운터를 제공합니다. 디스크에 있는 데이터베이스 페이지에 대한 실제 액세스는 **Buffer Manager** 카운터를 사용하여 모니터링됩니다. 데이터베이스에 저장된 데이터에 액세스하는 방법을 모니터링하면 인덱스를 추가/수정하거나, 파티션을 추가/이동하거나, 파일 또는 파일 그룹을 추가하거나, 인덱스를 조각 모음하거나, 쿼리를 다시 작성하여 쿼리 성능을 향상시킬 수 있는지 확인하는 데 도움이 됩니다. 또한 **Access Methods** 카운터를 사용하면 데이터베이스에 있는 데이터, 인덱스, 여유 공간의 양을 모니터링하여 각 서버 인스턴스에 대한 데이터 볼륨 및 조각화 상태를 나타낼 수 있습니다. 과도한 인덱스 조각화는 성능을 저하시킬 수 있습니다.  
  
 데이터 볼륨, 조각화 및 사용법에 대한 자세한 내용을 보려면 다음 동적 관리 뷰를 사용합니다.  
  
-   [sys.dm_db_index_operational_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_db_partition_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)  
  
-   [sys.dm_db_index_usage_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)  
  
 파일, 태스크 및 세션 수준에서 **tempdb** 의 공간 소비를 보려면 다음 동적 관리 뷰를 사용합니다.  
  
-   [sys.dm_db_file_space_usage&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
-   [sys.dm_db_task_space_usage&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)  
  
-   [sys.dm_db_session_space_usage&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
  
 이 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Access Methods** 카운터에 대해 설명합니다.  
  
|SQL Server Access Methods 카운터|설명|  
|----------------------------------------|-----------------|  
|**AU cleanup batches/sec**|지연 및 삭제된 할당 단위를 정리하는 백그라운드 태스크에 의해 완료된 초당 일괄 처리 수입니다.|  
|**AU cleanups/sec**|지연 및 삭제된 할당 단위를 정리하는 백그라운드 태스크에 의해 삭제된 초당 할당 단위 수입니다. 할당 단위를 삭제할 때마다 다중 일괄 처리가 필요합니다.|  
|**By-reference Lob Create Count**|참조에 의해 전달된 LOB(Large Object) 수 값입니다. 값을 기준으로 LOB를 전달하는 비용을 피하기 위해 특정 대량 작업에 사용된 By-reference LOB입니다.|  
|**By-reference Lob Use Count**|사용된 참조에 의한 LOB 수 값입니다. 값을 기준으로 LOB를 전달하는 비용을 피하기 위해 특정 대량 작업에 사용된 참조에 의한 LOB입니다.|  
|**Count Lob Readahead**|미리 읽기가 실행된 LOB 페이지 수입니다.|  
|**Count Pull In Row**|행 외부에서 행 내부로 끌어온 열 수 값입니다.|  
|**Count Push Off Row**|행 내부에서 행 외부로 밀어넣은 열 값 개수입니다.|  
|**Deferred Dropped Aus**|지연 및 삭제된 할당 단위를 정리한 백그라운드 태스크에서 삭제 대기 중인 할당 단위 수입니다.|  
|**Deferred Dropped rowsets**|지연 및 삭제된 행 집합을 정리하는 백그라운드 태스크에 의한 삭제를 기다리고 있는, 온라인 인덱스 빌드 작업의 중단으로 인해 생성된 행 집합 수입니다.|  
|**Dropped rowset cleanups/sec**|지연 및 삭제된 행 집합을 정리하는 백그라운드 태스크에 의해 삭제된, 온라인 인덱스 빌드 작업의 중단으로 인해 생성된 초당 행 집합 수입니다.|  
|**Dropped rowsets skipped/sec**|생생된 행 집합 중 지연 및 삭제된 행 집합을 정리하는 백그라운드 태스크에서 건너뛴, 온라인 인덱스 빌드 작업의 중단으로 인해 생성된 초당 행 집합 수입니다.|  
|**Extent Deallocations/sec**|이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 데이터베이스에서 초당 할당 취소된 익스텐트 수입니다.|  
|**Extents Allocated/sec**|이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 데이터베이스에서 초당 할당된 익스텐트 수입니다.|  
|**Failed AU cleanup batches/sec**|지연 및 삭제된 할당 단위를 정리한 백그라운드 태스크가 실패해 다시 시도가 필요한 초당 일괄 처리 수입니다. 메모리 또는 디스크 공간 부족, 하드웨어 오류 및 기타 이유로 인해 실패할 수 있습니다.|  
|**Failed leaf page cookie**|리프 페이지에 변경 내용이 있으므로 인덱스 검색 중 리프 페이지 쿠키를 사용할 수 없는 횟수입니다. 쿠키는 인덱스 검색 속도를 높이는 데 사용됩니다.|  
|**Failed tree page cookie**|해당 트리 페이지의 부모 페이지에 변경 내용이 있으므로 인덱스 검색 중 트리 페이지 쿠키를 사용할 수 없는 횟수입니다. 쿠키는 인덱스 검색 속도를 높이는 데 사용됩니다.|  
|**Forwarded Records/sec**|전송된 레코드 포인터를 통해 인출된 초당 레코드 수입니다.|  
|**FreeSpace Page Fetches/sec**|사용 가능한 공간 검색에 의해 인출된 초당 페이지 수입니다. 사용 가능한 공간 검색은 레코드 조각 삽입 또는 수정에 대한 요청을 충족시키기 위해 할당 단위에 이미 할당된 페이지 내의 사용 가능한 공간을 검색합니다.|  
|**FreeSpace Scans/sec**|레코드 조각을 삽입 또는 수정하기 위해 할당 단위에 이미 할당된 페이지 내의 사용 가능한 공간 검색을 시작한 초당 검색 수입니다. 각 검색은 여러 페이지를 찾을 수 있습니다.|  
|**Full Scans/sec**|초당 제한되지 않은 전체 검색 수입니다. 기본 테이블이나 전체 인덱스 검색이 될 수 있습니다.|  
|**Index Searches/sec**|초당 인덱스 검색 수입니다. 초당 인덱스 검색은 범위 검색 시작, 범위 검색 위치 조정, 검색 지점 다시 검사, 단일 인덱스 레코드 인출, 새로운 행을 삽입할 장소를 찾기 위한 인덱스 검색 등에 사용됩니다.|  
|**InSysXact waits/sec**|InSysXact 비트가 설정되어 있어 판독기가 페이지를 기다려야 하는 횟수입니다.|  
|**LobHandle Create Count**|생성된 임시 LOB 수입니다.|  
|**LobHandle Destroy Count**|소멸된 임시 LOB 수입니다.|  
|**LobSS Provider Create Count**|생성된 LobSSP(LOB 저장소 서비스 공급자) 수입니다. LobSSP당 하나의 작업 테이블이 생성되었습니다.|  
|**LobSS Provider Destroy Count**|소멸된 LobSSP 수입니다.|  
|**LobSS Provider Truncation Count**|잘린 LobSSP 수입니다.|  
|**Mixed Page Allocations/sec**|혼합된 익스텐트에서 초당 할당된 페이지 수입니다. 할당 단위에 할당된 IAM 페이지와 첫 8페이지를 저장하기 위해 사용됩니다.|  
|**Page compression attempts/sec**|페이지 수준 압축에 대해 계산된 페이지 수입니다. 현저한 공간 절약 효과를 볼 수 있기 때문에 압축되지 않은 페이지도 포함됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 개체가 포함됩니다. 특정 개체에 대한 자세한 내용은 [sys.dm_db_index_operational_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)인스턴스의 모든 데이터베이스에서 초당 할당 취소된 익스텐트 수입니다.|  
|**Page Deallocations/sec**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 데이터베이스에서 초당 할당 취소된 페이지 수입니다. 여기에는 혼합 및 단일 익스텐트의 페이지가 포함됩니다.|  
|**Page Splits/sec**|인덱스 페이지 오버플로의 결과로 발생한 초당 페이지 분할 수입니다.|  
|**Pages Allocated/sec**|이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 데이터베이스에서 초당 할당된 페이지 수입니다. 여기에는 혼합 및 단일 익스텐트 모두의 페이지 할당이 포함됩니다.|  
|**Pages compressed/sec**|페이지 압축을 사용하여 압축된 데이터 페이지 수입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 개체가 포함됩니다. 특정 개체에 대한 자세한 내용은 [sys.dm_db_index_operational_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)인스턴스의 모든 데이터베이스에서 초당 할당 취소된 익스텐트 수입니다.|  
|**Probe Scans/sec**|인덱스나 기본 테이블에서 직접 정규화된 단일 행만 찾기 위해 사용된 초당 정밀 검색 수입니다.|  
|**Range Scans/sec**|인덱스를 통해 한정된 초당 범위 검색 수입니다.|  
|**Scan Point Revalidations/sec**|검색 지점이 검색을 계속하기 위해 유효성을 다시 검사해야 하는 초당 횟수입니다.|  
|**Skipped Ghosted Records/sec**|검색 중 건너뛴 초당 삭제할 레코드 수입니다.|  
|**Table Lock Escalations/sec**|테이블의 잠금이 TABLE 또는 HoBT 세분성으로 에스컬레이션된 횟수입니다.|  
|**Used leaf page cookie**|리프 페이지에 변경 내용이 없으므로 인덱스 검색 중 리프 페이지 쿠키가 사용된 횟수입니다. 쿠키는 인덱스 검색 속도를 높이는 데 사용됩니다.|  
|**Used tree page cookie**|트리 페이지의 부모 페이지에 변경 내용이 없으므로 인덱스 검색 중 트리 페이지 쿠키가 사용된 횟수입니다. 쿠키는 인덱스 검색 속도를 높이는 데 사용됩니다.|  
|**Workfiles Created/sec**|초당 만들어지는 작업 파일 수입니다. 예를 들어 작업 파일은 해시 조인 및 해시 집계에 대한 임시 결과를 저장하는 데 사용될 수 있습니다.|  
|**Worktables Created/sec**|초당 만들어지는 작업 테이블 수입니다. 예를 들어 작업 테이블은 쿼리 스풀, LOB 변수, XML 변수 및 커서에 대한 임시 결과를 저장하는 데 사용될 수 있습니다.|  
|**Worktables From Cache Base**|내부용으로만 사용할 수 있습니다.|  
|**Worktables From Cache Ratio**|작업 테이블의 첫 두 페이지가 할당되지 않았지만 작업 테이블 캐시에서 즉시 사용 가능한 곳에 생성된 작업 테이블의 비율입니다. 작업 테이블이 삭제되면 두 페이지는 할당된 상태를 유지할 수 있으며 작업 테이블 캐시로 반환됩니다. 이 경우 성능이 향상됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
