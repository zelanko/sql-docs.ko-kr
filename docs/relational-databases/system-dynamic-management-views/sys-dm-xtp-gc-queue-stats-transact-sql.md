---
title: sys.dm_xtp_gc_queue_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_xtp_gc_stats
- dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xtp_gc_stats dynamic management view
ms.assetid: addef774-318d-46a7-85df-f93168a800cb
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 39775b2a0b127a8a5fee8b700c0c93476628d222
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmxtpgcqueuestats-transact-sql"></a>sys.dm_xtp_gc_queue_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  서버에 있는 각 가비지 수집 작업자 큐에 대한 정보와 각 GC에 대한 다양한 통계를 출력합니다. 논리 CPU당 큐는 하나입니다.  
  
 기본 가비지 수집 스레드(유휴 스레드)는 기본 가비지 수집 스레드의 마지막 호출 이후 완료된 전체 트랜잭션에 대해 업데이트, 삭제 및 삽입된 행을 추적합니다. 가비지 수집 스레드를 실행하면 가장 오래된 활성 트랜잭션의 타임스탬프가 변경되었는지 여부를 결정합니다. 가장 오래된 활성 트랜잭션이 변경된 경우 유휴 스레드는 쓰기 집합이 더 이상 필요하지 않은 트랜잭션의 작업 항목(16개 행 단위)을 큐에 추가합니다. 예를 들어 1,024개 행을 삭제하는 경우 대기 중인 64개 가비지 수집 작업 항목이 궁극적으로 표시되고 각각에는 16개의 삭제된 행이 포함되어 있습니다.  사용자 트랜잭션은 커밋 후 스케줄러에서 큐에 추가된 모든 항목을 선택합니다. 스케줄러에 큐에 추가된 항목이 없는 경우 사용자 트랜잭션은 현재 NUMA 노드의 모든 큐를 검색합니다.  
  
 sys.dm_xtp_gc_queue_stats를 실행하여 큐에 추가된 작업이 처리 중인지 확인하여 가비지 수집이 삭제된 행에 대해 메모리를 해제할지 여부를 결정할 수 있습니다. current_queue_depth의 항목이 처리 되지 않는 경우 또는 새 작업 항목이 없는 current_queue_depth에 추가 되는 경우이 가비지 수집이 메모리를 해제 하지는 나타냅니다. 예를 들어 장기 실행 트랜잭션이 있으면 가비지 수집을 수행할 수 없습니다.  
  
 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  

|열 이름|유형|Description|  
|-----------------|----------|-----------------|  
|queue_id|**int**|큐의 고유 식별자입니다.|  
|total_enqueues|**bigint**|서버 시작 후 이 큐에 배치된 가비지 수집 작업 항목의 총 수입니다.|  
|total_dequeues|**bigint**|서버 시작 후 이 큐에서 제거된 가비지 수집 작업 항목의 총 수입니다.|  
|current_queue_depth|**bigint**|이 큐에 나타난 가비지 수집 작업 항목의 현재 수입니다. 이 항목은 하나 이상의 가비지 수집을 의미할 수 있습니다.|  
|maximum_queue_depth|**bigint**|이 큐의 최대 깊이입니다.|  
|last_service_ticks|**bigint**|큐가 마지막으로 서비스되었을 때의 CPU 틱입니다.|  
  
## <a name="permissions"></a>Permissions  
 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="user-scenario"></a>사용자 시나리오  
 이 출력은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 4개의 코어에서 실행되고 있거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 선호도가 4개의 코어로 설정되었음을 보여 줍니다.  
  
 이 출력은 큐에 처리할 작업 항목이 없음을 보여 줍니다. 큐 0의 경우 SQL 시작 후 큐에서 나온 총 작업 항목은 15625개이며 최대 큐 깊이는 215625였습니다.  
  
```  
queue_id total_enqueues total_dequeues current_queue_depth  maximum_queue_depth  last_service_ticks  
----------------------------------------------------------------------------------------------------  
0        15625                15625    0                    15625                1233573168347  
1        15625                15625    0                    15625                1234123295566  
2        15625                15625    0                    15625                1233569418146  
3        15625                15625    0                    15625                1233571605761  
```  
  
## <a name="see-also"></a>관련 항목:  
 [메모리 액세스에 최적화 된 테이블 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
