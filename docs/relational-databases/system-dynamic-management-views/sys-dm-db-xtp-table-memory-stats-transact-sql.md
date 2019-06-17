---
title: sys.dm_db_xtp_table_memory_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_table_memory_stats_TSQL
- dm_db_xtp_table_memory_stats
- sys.dm_db_xtp_table_memory_stats
- dm_db_xtp_table_memory_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_table_memory_stats
- dm_db_xtp_table_memory_stats
ms.assetid: ad0efc06-3d9c-4861-9dfa-a7a87822d0c8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ade5650c1c47f6d52602b04f14af3ad79dbe609
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63004086"
---
# <a name="sysdmdbxtptablememorystats-transact-sql"></a>sys.dm_db_xtp_table_memory_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스에서 각 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 테이블(사용자 및 시스템)에 대한 메모리 사용량 통계를 반환합니다. 시스템 테이블에는 음수 개체 ID가 있으며 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 엔진에 대한 런타임 정보가 저장됩니다. 사용자 개체와 달리 시스템 테이블은 내부에 있으며 메모리 내에만 존재하므로 카탈로그 뷰를 통해 보이지 않습니다. 시스템 테이블은 저장소의 모든 데이터/델타 파일에 대한 메타데이터, 병합 요청, 행 필터링을 위한 델타 파일의 워터마크, 삭제된 테이블, 복구 및 백업을 위한 관련 정보 등의 정보를 저장하는 데 사용됩니다. [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 엔진은 최대 8,192개의 데이터 및 델타 파일 쌍을 보유할 수 있으므로 큰 메모리 내 데이터베이스의 경우 시스템 테이블에서 사용하는 메모리가 몇 메가바이트일 수 있습니다.  
  
 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|테이블의 개체 ID입니다. 메모리 내 OLTP 시스템 테이블에 대해 NULL입니다.|  
|memory_allocated_for_table_kb|**bigint**|이 테이블에 할당된 메모리입니다.|  
|memory_used_by_table_kb|**bigint**|행 버전을 포함하여 테이블에 사용되는 메모리입니다.|  
|memory_allocated_for_indexes_kb|**bigint**|이 테이블의 인덱스에 할당된 메모리입니다.|  
|memory_used_by_indexes_kb|**bigint**|이 테이블의 인덱스에 소비된 메모리입니다.|  
  
## <a name="permissions"></a>사용 권한  
 현재 데이터베이스에 대해 VIEW DATABASE STATE 권한이 있으면 모든 행이 반환됩니다. 그렇지 않으면 빈 행 집합이 반환됩니다.  
  
 VIEW DATABASE 권한이 없으면 SELECT 권한이 있는 테이블의 행에 대해 모든 열이 반환됩니다.  
  
 시스템 테이블은 VIEW DATABASE STATE 권한이 있는 사용자의 경우에만 반환됩니다.  
  
## <a name="examples"></a>예  
 다음 DMV를 쿼리해서 데이터베이스 내의 테이블 및 인덱스에 대해 할당된 메모리를 가져올 수 있습니다.  
  
```  
-- finding memory for objects  
SELECT OBJECT_NAME(object_id), *   
FROM sys.dm_db_xtp_table_memory_stats;  
```  
  
 데이터베이스 내에서 모든 개체에 대한 메모리를 찾으려면:  
  
```  
SELECT SUM( memory_allocated_for_indexes_kb + memory_allocated_for_table_kb) AS  
 memoryallocated_objects_in_kb   
FROM sys.dm_db_xtp_table_memory_stats;  
```  
  
## <a name="user-scenario"></a>사용자 시나리오  
 먼저 HkDb1이라는 데이터베이스에 다음 테이블을 만듭니다.  
  
```  
-- set max server memory to 4 GB  
EXEC sp_configure 'max server memory (MB)', 4048  
go  
  
RECONFIGURE  
go  
  
-- create a resource pool for database with memory-optimized objects  
CREATE RESOURCE POOL PoolHkDb1 WITH (MAX_MEMORY_PERCENT = 50);  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
go  
  
--bind the pool to the database  
EXEC sp_xtp_bind_db_resource_pool 'HkDb1', 'PoolHkdb1'  
go  
  
-- take database offline/online to associate the pool  
use master  
go  
  
alter database HkDb1 set offline  
go  
alter database HkDb1 set online  
go  
  
USE HkDb1  
go  
  
CREATE TABLE dbo.t1 (  
       c1 int NOT NULL,  
       c2 char(40) NOT NULL,  
       c3 char(8000) NOT NULL,  
  
       CONSTRAINT [pk_t1_c1] PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 100000)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
CREATE TABLE dbo.t2 (  
       c1 int NOT NULL,  
       c2 char(40) NOT NULL,  
       c3 char(8000) NOT NULL,  
  
       CONSTRAINT [pk_t2_c1] PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 100000)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
CREATE TABLE dbo.t3 (  
       c1 int NOT NULL,  
       c2 char(40) NOT NULL,  
       c3 char(8000) NOT NULL,  
  
       CONSTRAINT [pk_t3_c1] PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 1000000)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
-- load 150K rows  
declare @i int = 0  
while (@i <= 150000)  
begin  
       insert t1 values (@i, 'a', replicate ('b', 8000))  
       set @i += 1;  
end  
go  
```  
  
 데이터가 테이블에 로드되면 사용자 정의 테이블과 이 테이블이 사용하고 있는 저장소 양을 볼 수 있습니다. 예를 들어, 테이블의 각 행은 약 8070바이트(할당 크기는 8K(8192바이트))일 수 있습니다. 테이블당 인덱스 수와 인덱스가 사용하는 저장소 양을 볼 수 있습니다. 예를 들어, 1MB는 100K개의 항목이며, 다음 2의 제곱(2**17) = 131072으로 반올림되고 각각 8바이트입니다. 테이블에 인덱스가 없을 수도 있으며 이 경우에는 인덱스에 대한 메모리 할당이 표시됩니다. 다른 행은 시스템 테이블을 나타낼 수 있습니다.  
  
```  
select convert(char(10), object_name(object_id)) as Name,*   
from sys.dm_db_xtp_table_memory_stats  
```  
  
 출력은 두 부분으로 다음과 같습니다.  
  
```  
Name       object_id   memory_allocated_for_table_kb memory_used_by_table_kb  
---------- ----------- ----------------------------- -----------------------  
t3         629577281   0                             0  
t1         565577053   1372928                       1202351  
t2         597577167   0                             0  
NULL       -6          0                             0  
NULL       -5          0                             0  
NULL       -4          0                             0  
NULL       -3          0                             0  
NULL       -2          192                           25  
  
memory_allocated_for_indexes_kb memory_used_by_indexes_kb  
------------------------------- -------------------------  
8192                            8192  
1024                            1024  
8192                            8192  
2                               2  
24                              24  
2                               2  
2                               2  
16                              16  
```  
  
 출력,  
  
```  
select  sum(allocated_bytes)/(1024*1024) as total_allocated_MB,   
       sum(used_bytes)/(1024*1024) as total_used_MB  
from sys.dm_db_xtp_memory_consumers  
```  
  
 ,  
  
```  
total_allocated_MB   total_used_MB  
-------------------- --------------------  
1357                 1191  
```  
  
 다음으로 리소스 풀의 출력을 살펴보겠습니다. 풀에서 사용된 메모리는 1356MB입니다.  
  
```  
select pool_id,convert(char(10), name) as Name, min_memory_percent, max_memory_percent,   
   max_memory_kb/1024 as max_memory_mb  
from sys.dm_resource_governor_resource_pools  
  
select used_memory_kb/1024 as used_memory_mb ,target_memory_kb/1024 as target_memory_mb  
from sys.dm_resource_governor_resource_pools  
```  
  
 출력은 다음과 같습니다.  
  
```  
pool_id     Name       min_memory_percent max_memory_percent max_memory_mb  
----------- ---------- ------------------ ------------------ --------------------  
1           internal   0                  100                3845  
2           default    0                  100                3845  
259         PoolHkDb1  0                  100                3845  
  
used_memory_mb       target_memory_mb  
-------------------- --------------------  
125                  3845  
32                   3845  
1356                 3845  
```  
  
## <a name="see-also"></a>관련 항목  
 [메모리 최적화 테이블 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
