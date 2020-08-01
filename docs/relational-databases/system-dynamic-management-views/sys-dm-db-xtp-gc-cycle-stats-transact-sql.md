---
title: sys. dm_db_xtp_gc_cycle_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_gc_cycle_stats_TSQL
- dm_db_xtp_gc_cycle_stats
- sys.dm_db_xtp_gc_cycle_stats_TSQL
- sys.dm_db_xtp_gc_cycle_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_gc_cycle_stats dynamic management view
ms.assetid: bbc9704e-158e-4d32-b693-f00dce31cd2f
author: CarlRabeler
ms.author: carlrab
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8e0edb4d46ae47b4c45dc01f7d2e33f856424352
ms.sourcegitcommit: 039fb38c583019b3fd06894160568387a19ba04e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87442574"
---
# <a name="sysdm_db_xtp_gc_cycle_stats-transact-sql"></a>sys.dm_db_xtp_gc_cycle_stats(Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  하나 이상의 행을 삭제한 커밋된 트랜잭션의 현재 상태를 출력합니다. 마지막 가비지 수집 주기 이후 유휴 가비지 수집 스레드는 매분 또는 커밋된 DML 트랜잭션 수가 내부 임계값을 초과할 때 실행됩니다. 가비지 수집 주기의 일부로 세대와 관련된 하나 이상의 큐에 커밋된 트랜잭션을 이동합니다. 유효하지 않은 버전을 만든 트랜잭션은 다음과 같이 16개 세대 간에 16개 트랜잭션 단위로 그룹화됩니다.  
  
-   0 세대: 가장 오래 된 활성 트랜잭션 보다 이전에 커밋된 모든 트랜잭션을 저장 합니다. 이러한 트랜잭션으로 생성된 행 버전은 가비지 수집에 즉시 사용할 수 있습니다.  
  
-   세대 1-14: 타임 스탬프가 가장 오래 된 활성 트랜잭션 보다 큰 트랜잭션을 저장 합니다. 행 버전은 가비지 수집될 수 없습니다. 각 세대는 최대 16개의 트랜잭션을 보유할 수 있습니다. 총 224(14*16)개 트랜잭션이 이 세대에 존재할 수 있습니다.  
  
-   5 세대: 타임 스탬프가 가장 오래 된 활성 트랜잭션 보다 긴 남은 트랜잭션은 세대 15로 이동 합니다. 세대-0과 유하사게 세대-15에는 트랜잭션 수 제한이 없습니다.  
  
 메모리 가중이 있는 경우 가비지 수집기 스레드가 가장 오래된 활성 트랜잭션 힌트를 적극적으로 업데이트하고, 이는 가비지 수집을 강제로 수행합니다.  
  
 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
  
|열 이름|Type|Description|  
|-----------------|----------|-----------------|  
|cycle_id|**bigint**|가비지 수집 주기에 대한 고유 식별자입니다.|  
|ticks_at_cycle_start|**bigint**|주기가 시작된 시간의 틱입니다.|  
|ticks_at_cycle_end|**bigint**|주기가 종료된 시간의 틱입니다.|  
|base_generation|**bigint**|데이터베이스의 현재 기본 생성 값입니다. 이는 가비지 수집에 대한 트랜잭션을 식별하는 데 사용되는 가장 오래된 활성 트랜잭션의 타임스탬프를 나타냅니다. 가장 오래된 활성 트랜잭션 ID는 16의 증분으로 업데이트됩니다. 예를 들어 트랜잭션 id가 124, 125, 126 ... 인 경우 139, 값은 124이 됩니다. 예를 들어 140이라는 다른 트랜잭션을 추가하는 경우 값은 140이 됩니다.|  
|xacts_copied_to_local|**bigint**|트랜잭션 파이프라인에서 데이터베이스의 생성 배열로 복사하는 트랜잭션 수입니다.|  
|xacts_in_gen_0- xacts_in_gen_15|**bigint**|각 세대의 트랜잭션 수입니다.|  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="usage-scenario"></a>사용 시나리오  
 27세대를 보여 주는 열 하위 집합의 예제 출력은 다음과 같습니다.  
  
```  
cycle_id   ticks_at_cycle_start ticks_at_cycle_end   base_generation  xacts_in_gen_0    xacts_in_gen_1  
  
1          123160509            123160509            1                    0                    0  
2          123176822            123176822            1                    0                    1  
3          123236826            123236826            1                    0                    1  
4          123296829            123296829            1                    0                    1  
5          123356832            123356941            129                  0                    0  
6          123357473            123357473            129                  0                    0  
7          123417486            123417486            129                  0                    0  
8          123477489            123477489            129                  0                    0  
9          123537492            123537492            129                  0                    0  
10         123597500            123597500            129                  0                    0  
11         123657504            123657504            129                  0                    0  
12         123717507            123717507            129                  0                    0  
13         123777510            123777510            129                  0                    0  
14         123837513            123837513            129                  0                    0  
15         123897516            123897516            129                  0                    0  
16         123957516            123957516            129                  0                    0  
17         124017516            124017516            129                  0                    0  
18         124077517            124077517            129                  0                    0  
19         124137517            124137517            129                  0                    0  
20         124197518            124197518            129                  0                    0  
21         124257518            124257518            129                  0                    0  
22         124317523            124317523            129                  0                    0  
23         124377526            124377526            129                  0                    0  
24         124437529            124437529            129                  0                    0  
25         124497533            124497533            129                  0                    0  
26         124557536            124557536            129                  0                    0  
27         124617539            124617539            129                  0                    0  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [메모리 최적화 테이블 동적 관리 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
