---
description: sys.dm_db_xtp_memory_consumers(Transact-SQL)
title: sys. dm_db_xtp_memory_consumers (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_memory_consumers
- dm_db_xtp_memory_consumers
- dm_db_xtp_memory_consumers_TSQL
- sys.dm_db_xtp_memory_consumers_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_memory_consumers dynamic management view
ms.assetid: f7ab2eaf-e627-464d-91fe-0e170b3f37bc
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 321297a2590a18ed7e51364b3f532076f90ce740
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542241"
---
# <a name="sysdm_db_xtp_memory_consumers-transact-sql"></a>sys.dm_db_xtp_memory_consumers(Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 데이터베이스 엔진에서 데이터베이스 수준 메모리 소비자를 보고합니다. 뷰는 데이터베이스 엔진에 사용되는 각 메모리 소비자에 대한 행을 반환합니다. 이 DMV를 사용 하 여 여러 내부 개체에서 메모리를 분산 하는 방법을 확인 합니다.  
  
 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|memory_consumer_id|**bigint**|메모리 소비자의 ID(내부)입니다.|  
|memory_consumer_type|**int**|메모리 소비자 유형입니다.<br /><br /> 0=Aggregation. (둘 이상 소비자의 메모리 사용량을 집계합니다. 표시되어서는 안 됩니다.)<br /><br /> 2=VARHEAP(가변 길이 힙에 대한 메모리 소비량을 추적합니다.)<br /><br /> 3=HASH(인덱스에 대한 메모리 소비를 추적합니다.)<br /><br /> 5=DB 페이지 풀(런타임 작업에 사용되는 데이터베이스 페이지 풀에 대한 메모리 소비량을 추적합니다. 예를 들어 테이블 변수 및 일부 순차 가능 검색입니다. 데이터베이스당 이 유형의 메모리 소비자는 하나뿐입니다.)|  
|memory_consumer_type_desc|**nvarchar (64)**|메모리 소비자 유형: VARHEAP, HASH 또는 PGPOOL.<br /><br /> 0-(표시 되지 않아야 함)<br /><br /> 2 - VARHEAP<br /><br /> 3 - HASH<br /><br /> 5 - PGPOOL|  
|memory_consumer_desc|**nvarchar (64)**|메모리 소비자 인스턴스에 대한 설명입니다.<br /><br /> VARHEAP <br />데이터베이스 힙입니다. 데이터베이스에 대한 사용자 데이터(행)를 할당하는 데 사용됩니다.<br />데이터베이스 시스템 힙입니다. 메모리 덤프에 포함되고 사용자 데이터를 포함하지 않는 데이터베이스 데이터를 할당하는 데 사용됩니다.<br />범위 인덱스 힙입니다. BW 페이지를 할당하기 위해 범위 인덱스에서 사용되는 프라이빗 힙입니다.<br /><br /> HASH: object_id는 테이블 및 index_id 해시 인덱스 자체를 나타내므로 설명이 없습니다.<br /><br /> PGPOOL: 데이터베이스에는 페이지 풀 데이터베이스 64K 페이지 풀이 하나만 있습니다.|  
|object_id|**bigint**|할당된 메모리가 속하는 개체 ID입니다. 시스템 개체에 대한 음수 값입니다.|  
|xtp_object_id|**bigint**|메모리 최적화 테이블의 개체 ID입니다.|  
|index_id|**int**|소비자의 인덱스 ID입니다(해당하는 경우). 기본 테이블의 경우 NULL입니다.|  
|allocated_bytes|**bigint**|이 소비자에 대해 예약된 바이트 수입니다.|  
|used_bytes|**bigint**|이 소비자가 사용하는 바이트입니다. varheap에만 적용됩니다.|  
|allocation_count|**int**|할당 수입니다.|  
|partition_count|**int**|내부적으로만 사용됩니다.|  
|sizeclass_count|**int**|내부적으로만 사용됩니다.|  
|min_sizeclass|**int**|내부적으로만 사용됩니다.|  
|max_sizeclass|**int**|내부적으로만 사용됩니다.|  
|memory_consumer_address|**varbinary**|소비자의 내부 주소입니다. 내부 전용입니다.|  
|xtp_object_id|**bigint**|메모리 액세스에 최적화 된 테이블에 해당 하는 메모리 내 OLTP 개체 ID입니다.|  
  
## <a name="remarks"></a>설명  
 출력에서 데이터베이스 수준의 할당자는 사용자 테이블, 인덱스 및 시스템 테이블을 나타냅니다. object_id = NULL인 VARHEAP는 가변 길이 열을 포함하는 테이블에 할당된 메모리를 나타냅니다.  
  
## <a name="permissions"></a>사용 권한  
 현재 데이터베이스에 대해 VIEW DATABASE STATE 권한이 있으면 모든 행이 반환됩니다. 그렇지 않으면 빈 행 집합이 반환됩니다.  
  
 VIEW DATABASE 권한이 없으면 SELECT 권한이 있는 테이블의 행에 대해 모든 열이 반환됩니다.  
  
 시스템 테이블은 VIEW DATABASE STATE 권한이 있는 사용자의 경우에만 반환됩니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 메모리 최적화 테이블에 columnstore 인덱스가 있는 경우 시스템은 일부 메모리를 사용 하는 일부 내부 테이블을 사용 하 여 columnstore 인덱스에 대 한 데이터를 추적 합니다. 이러한 내부 테이블 및 메모리 사용을 보여 주는 예제 쿼리에 대 한 자세한 내용은 [memory_optimized_tables_internal_attributes (transact-sql)](../../relational-databases/system-catalog-views/sys-memory-optimized-tables-internal-attributes-transact-sql.md)를 참조 하세요.
 
  
## <a name="examples"></a>예제  
  
```  
-- memory consumers (database level)  
SELECT OBJECT_NAME(object_id), *   
FROM sys.dm_db_xtp_memory_consumers;  
```  
  
## <a name="user-scenario"></a>사용자 시나리오  
  
```  
-- memory consumers (database level)  
  
select  convert(char(10), object_name(object_id)) as Name,   
convert(char(10),memory_consumer_type_desc ) as memory_consumer_type_desc, object_id,index_id, allocated_bytes,  used_bytes   
from sys.dm_db_xtp_memory_consumers  
```  
  
 열의 하위 집합을 사용한 출력은 다음과 같습니다. 데이터베이스 수준의 할당자는 사용자 테이블, 인덱스 및 시스템 테이블을 나타냅니다. object_id = NULL(마지막 행)인 VARHEAP는 테이블의 데이터 행에 할당된 메모리를 나타냅니다(이 예에서는 t1). 할당된 바이트를 MB로 환산하면 1340MB입니다.  
  
```  
Name       memory_consumer_type_desc object_id   index_id    allocated_bytes      used_bytes  
---------- ------------------------- ----------- ----------- -------------------- --------------------  
t3         HASH                      629577281   2           8388608              8388608  
t2         HASH                      597577167   2           8388608              8388608  
t1         HASH                      565577053   2           1048576              1048576  
NULL       HASH                      -6          1           2048                 2048  
NULL       VARHEAP                   -6          NULL        0                    0  
NULL       HASH                      -5          3           8192                 8192  
NULL       HASH                      -5          2           8192                 8192  
NULL       HASH                      -5          1           8192                 8192  
NULL       HASH                      -4          1           2048                 2048  
NULL       VARHEAP                   -4          NULL        0                    0  
NULL       HASH                      -3          1           2048                 2048  
NULL       HASH                      -2          2           8192                 8192  
NULL       HASH                      -2          1           8192                 8192  
NULL       VARHEAP                   -2          NULL        196608               26496  
NULL       HASH                      0           1           2048                 2048  
NULL       PGPOOL                    0           NULL        0                    0  
NULL       VARHEAP                   NULL        NULL        1405943808           1231220560  
  
(17 row(s) affected)  
```  
  
 이 DMV에서 할당 되 고 사용 되는 총 메모리는 [dm_db_xtp_table_memory_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md)의 개체 수준과 동일 합니다.  
  
```  
select  sum(allocated_bytes)/(1024*1024) as total_allocated_MB,   
        sum(used_bytes)/(1024*1024) as total_used_MB  
from sys.dm_db_xtp_memory_consumers  
  
total_allocated_MB   total_used_MB  
-------------------- --------------------  
1358                 1191  
```  
  
## <a name="see-also"></a>참고 항목  
 [메모리 최적화 테이블 동적 관리 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
