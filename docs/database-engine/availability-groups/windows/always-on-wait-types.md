---
title: 가용성 그룹과 연결된 대기 식별
description: T-SQL(Transact-SQL) 및 확장 이벤트를 사용하여 Always On 가용성 그룹과 연결된 대기를 식별합니다.
ms.custom: ag-guide, seodec18
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: afa8caff-f325-48d9-a8ef-a30beab60389
author: rothja
ms.author: jroth
ms.openlocfilehash: f16a93231cf8b3bc6f3ad224703e3902ff3cb9b7
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900926"
---
# <a name="identify-waits-associated-with-availability-groups"></a>가용성 그룹과 연결된 대기 식별
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Always On 가용성 그룹 대기 시간의 문제를 해결할 때 DMV(동적 관리 뷰) [sys.dm_os_wait_stats&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)에서 가용성 그룹 관련 대기 유형을 사용하여 누적에 대해 대기 통계를 모니터링할 수 있습니다.  
  
 대기 통계 사용에 대한 일반적인 정보는 [SQL Server 2005 대기 및 큐](https://technet.microsoft.com/library/cc966413.aspx)를 참조하세요. 해당 문서는 SQL Server 2005에 대해 작성되었지만 해당 정보는 SQL Server 이후 버전에 적용될 수 있습니다.  
  
## <a name="query-for-availability-groups-wait-types"></a>가용성 그룹 대기 유형에 대한 쿼리  
 다음 T-SQL 쿼리를 사용하여 가용성 그룹 대기 유형을 사용하여 모든 대기 통계를 검색할 수 있습니다.  
  
```sql  
SELECT * FROM sys.dm_os_wait_stats   
WHERE wait_type LIKE '%hadr%'  
ORDER BY wait_time_ms DESC  
```  
  
 확장 이벤트를 캡처하여 대기 통계를 모니터링하려면 다음 T-SQL 명령을 사용합니다.  
  
```sql
CREATE EVENT SESSION [alwayson] ON SERVER   
ADD EVENT sqlos.wait_info(  
    WHERE ([wait_type]=(758) OR [wait_type]=(776) OR [wait_type]=(853) OR [wait_type]=(833)))  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,  
MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)  
GO  
```  
  
 다음 쿼리를 실행하여 대기 유형의 키 값 매핑을 볼 수 있습니다.  
  
```sql
SELECT * FROM sys.dm_xe_map_values   
WHERE name='wait_types' AND map_value LIKE '%hadr%'   
ORDER BY map_key ASC  
```  
  
## <a name="next-steps"></a>다음 단계  
 [대기 유형](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md#WaitTypes)  
  
  
