---
title: "SQL Server, Resource Pool Stats 개체 | Microsoft 문서"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Reosurce Pool Stats object
- 'SQLServer: Resource Pool Stats object'
ms.assetid: bb46e029-fcf9-4aeb-a066-be41e7668fb9
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1ccd649e92cd416ff086758005f3b5df728dfe1d
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-resource-pool-stats-object"></a>SQLServer, Resource Pool Stats 개체
  SQLServer:Resource Pool Stats 개체는 리소스 관리자 리소스 풀 통계에 대한 정보를 보고하는 성능 카운터를 포함합니다.  
  
 각 활성 리소스 풀은 리소스 관리자 리소스 풀 이름과 동일한 인스턴스 이름으로 SQLServer:Resource Pool Stats 성능 개체의 인스턴스를 생성합니다. 다음 표에서는 이 인스턴스에서 지원하는 카운터에 대해 설명합니다.  
  
|카운터 이름|Description|  
|------------------|-----------------|  
|**Active memory grant amount (KB)**|현재 부여된 메모리의 총 양(KB)입니다. 이 정보는 [sys.dm_exec_query_resource_semaphores](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)에 사용할 수도 있습니다.| 
|**Active memory grants count**|현재 총 메모리 부여 수입니다. 이 정보는 [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)에 사용할 수도 있습니다.|  
|**Avg Disk Read IO (ms)**|디스크에서 읽기 작업의 평균 시간(밀리초)입니다.|  
|**Avg Disk Read IO (ms) Base**|내부용으로만 사용할 수 있습니다.|
|**Avg Disk Write IO (ms)**|디스크에 쓰기 작업의 평균 시간(밀리초)입니다.|  
|**Avg Disk Write IO (ms) Base**|내부용으로만 사용할 수 있습니다.|
|**Cache memory target (KB)**|캐시를 위한 현재 메모리 브로커 대상(KB)입니다.|  
|**Compile memory target (KB)**|쿼리 컴파일을 위한 현재 메모리 브로커 대상(KB)입니다.|  
|**CPU control effect %**|리소스 관리자가 리소스 풀에 미치는 효과로, (CPU 사용량 %)/(리소스 관리자가 없을 경우의 CPU 사용량 %)로 계산합니다.|  
|**CPU delayed %**|지정된 성능 개체 인스턴스의 모든 요청에 대해 배포된 시스템 CPU이며 총 활성 시간 비율로 나타냅니다.|
|**CPU delayed % base**|내부용으로만 사용할 수 있습니다.|
|**CPU effective %**|지정된 성능 개체 인스턴스의 모든 요청에 사용된 시스템 CPU 사용량이며 총 활성 시간 비율로 나타냅니다.|
|**CPU effective % base**|내부용으로만 사용할 수 있습니다.|
|**CPU usage %**|이 풀에 속한 모든 작업 그룹의 모든 요청에 의한 CPU 대역폭 사용량으로, 컴퓨터를 기준으로 측정되고 시스템에 있는 모든 CPU를 기준으로 평균화됩니다. 이 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에 사용할 수 있는 CPU 양이 변경되면 그에 따라 변경됩니다. 이 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에 전달되는 CPU를 기준으로는 평균화되지 않습니다.|  
|**CPU usage % base**|내부용으로만 사용할 수 있습니다.|
|**CPU usage target %**|리소스 풀 구성 설정과 시스템 로드를 기반으로 한 리소스 풀에 대한 CPU 사용량 %의 대상 값입니다.|  
|**CPU violated %**|CPU 예약과 유효 일정 비율 간의 차이입니다.|
|**Disk Read Bytes/sec**|마지막 1초 동안 디스크에서 읽은 바이트 수입니다.|  
|**Disk Read IO Throttled/sec**|마지막 1초 동안 제한된 읽기 작업의 수입니다.|  
|**Disk Read IO/sec**|마지막 1초 동안 수행된 디스크에서 읽기 작업의 수입니다.| 
|**Disk Write Bytes/sec**|마지막 1초 동안 디스크에 쓴 바이트 수입니다.|  
|**Disk Write IO Throttled/sec**|마지막 1초 동안 제한된 쓰기 작업의 수입니다.| 
|**Disk Write IO/sec**|마지막 1초 동안 수행된 디스크에 쓰기 작업의 수입니다.|
|**Max memory (KB)**|리소스 풀이 리소스 풀 설정과 서버 상태를 기반으로 확보할 수 있는 최대 메모리 양(KB)입니다.| 
|**Memory grant timeouts/sec**|초당 메모리 부여 제한 시간 수입니다.|
|**Memory grants/sec**|현재 리소스 풀에서 초당 발생하는 메모리 부여의 수입니다.| 
|**Pending memory grant count**|큐에 대기 중인 메모리 부여에 대한 요청 수입니다. 이 정보는 [sys.dm_exec_query_resource_semaphores](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)에 사용할 수도 있습니다.|
|**Query exec memory target (KB)**|쿼리 실행 메모리 부여를 위한 현재 메모리 브로커 대상(KB)입니다. 이 정보는 [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)에 사용할 수도 있습니다.|  
|**Target memory (KB)**|리소스 풀이 리소스 풀 설정과 서버 상태를 기반으로 확보하려고 시도하는 대상 메모리 양(KB)입니다.|   
|**Used memory (KB)**|리소스 풀에 사용되는 최대 메모리 양((KB)입니다.|  

  
## <a name="see-also"></a>관련 항목:  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, Workload Group Stats 개체](../../relational-databases/performance-monitor/sql-server-workload-group-stats-object.md)   
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)  
  
  
