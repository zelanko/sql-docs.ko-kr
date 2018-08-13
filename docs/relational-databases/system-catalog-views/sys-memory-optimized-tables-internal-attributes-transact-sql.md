---
title: sys.memory_optimized_tables_internal_attributes (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.memory_optimized_tables_internal_attributes
- sys.memory_optimized_tables_internal_attributes_TSQL
- memory_optimized_tables_internal_attributes
- memory_optimized_tables_internal_attributes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.memory_optimized_tables_internal_attributes catalog view
ms.assetid: 78ef5807-0504-4de8-9a01-ede6c03c7ff1
caps.latest.revision: 13
author: jodebrui
ms.author: jodebrui
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 51cd7c4fa45c6a09a0885bb69b11b916fa4caa51
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39535093"
---
# <a name="sysmemoryoptimizedtablesinternalattributes-transact-sql"></a>sys.memory_optimized_tables_internal_attributes(TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

사용자 메모리 최적화 테이블을 저장하는 데 사용되는 각 내부 메모리 최적화 테이블에 대한 행을 포함합니다. 사용자 테이블 각각은 하나 이상의 내부 테이블에 해당합니다. 단일 테이블은 핵심 데이터 저장소에 사용됩니다. 추가 내부 테이블은 메모리 최적화 테이블의 temporal, columnstore 인덱스 및 행 외부(LOB) 저장소와 같은 기능을 지원하는 데 사용됩니다.
 
| 열 이름  | 데이터 형식  | Description |
| :------ |:----------| :-----|
|object_id  |**int**|       사용자 테이블의 ID입니다. 사용자 테이블을 지원하는 데 필요한 내부 메모리 최적화 테이블(예: Hk/Columnstore 조합의 경우 행 외부 저장소 또는 삭제된 행)에는 부모와 동일한 object_id가 있습니다. |
|xtp_object_id  |**bigint**|    사용자 테이블을 지원하는 데 사용되는 내부 메모리 최적화 테이블에 해당되는 메모리 내 OLTP의 개체 ID입니다. 데이터베이스 내에서 고유하며 개체의 수명 주기 동안 변경할 수 있습니다. 
|유형|  **int** |   내부 테이블의 형식입니다.<br/><br/> 0 => DELETED_ROWS_TABLE <br/> 1 => USER_TABLE <br/> 2 => DICTIONARIES_TABLE<br/>3 => SEGMENTS_TABLE<br/>4 => ROW_GROUPS_INFO_TABLE<br/>5 => INTERNAL OFF-ROW DATA TABLE<br/>252 => INTERNAL_TEMPORAL_HISTORY_TABLE | 
|type_desc| **nvarchar(60)**|   유형에 대한 설명<br/><br/>DELETED_ROWS_TABLE -> columnstore 인덱스에 대해 삭제된 행을 추적하는 내부 테이블<br/>USER_TABLE-> 행 내부 사용자 데이터를 포함한 테이블<br/>DICTIONARIES_TABLE -> columnstore 인덱스에 대한 사전<br/>SEGMENTS_TABLE -> columnstore 인덱스에 대해 압축된 세그먼트<br/>ROW_GROUPS_INFO_TABLE -> columnstore 인덱스의 압축된 행 그룹에 대한 메타데이터<br/>INTERNAL OFF-ROW DATA TABLE -> 행 외부 열 저장소에 사용되는 내부 테이블. 이 경우 minor_id는 column_id를 반영합니다.<br/>INTERNAL_TEMPORAL_HISTORY_TABLE -> 디스크 기반 이력 테이블의 핫 테일(Hot tail) 기록에 삽입할 행이 먼저 이 내부 메모리 최적화 테이블에 삽입됩니다. 내부 테이블의 행이 디스크 기반 기록 테이블로 비동기적으로 이동하는 백그라운드 작업이 있습니다. |
|minor_id|  **int**|    0은 사용자 또는 내부 테이블을 나타냅니다.<br/><br/>0이 아니면 행 외부에 저장된 열 ID를 나타냅니다. sys.columns의 column_id와 조인합니다.<br/><br/>행 외부에서 저장된 각 열에는 이 시스템 보기에 해당하는 열이 있습니다.|

## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-all-columns-that-are-stored-off-row"></a>1. 행 외부에서 저장된 모든 열 반환

다음 T-SQL 스크립트에서는 여러 큰 비-LOB 열과 단일 LOB 열이 있는 테이블을 보여 줍니다.

```Transact-SQL
CREATE TABLE dbo.LargeTableSample
(
      Id   int IDENTITY PRIMARY KEY NONCLUSTERED,
      C1   nvarchar(4000),
      C2   nvarchar(4000),
      C3   nvarchar(4000),
      C4   nvarchar(4000),
      Misc nvarchar(max)
) WITH (MEMORY_OPTIMIZED = ON);
GO
```

다음 쿼리는 행 외부에 저장되는 모든 열을 해당 크기와 함께 표시합니다. -1 크기는 LOB 열을 나타냅니다. 모든 LOB 열은 행 외부에 저장됩니다.

```Transact-SQL
SELECT 
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table', 
  c.name AS 'column', 
  c.max_length
FROM sys.memory_optimized_tables_internal_attributes moa
     JOIN sys.columns c ON moa.object_id = c.object_id AND moa.minor_id=c.column_id
     JOIN sys.objects o on moa.object_id=o.object_id 
WHERE moa.type=5;
```

### <a name="b-returning-memory-consumption-of-all-columns-that-are-stored-off-row"></a>2. 행 외부에서 저장된 모든 열의 메모리 사용량 반환

행 외부 열의 메모리 사용에 대한 자세한 정보를 얻으려면 행 외부 열을 저장하는 데 사용되는 모든 내부 테이블 및 인덱스의 메모리 사용량을 보여 주는 다음 쿼리를 사용할 수 있습니다.

```Transact-SQL
SELECT
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table',
  c.name AS 'column',
  c.max_length,
  mc.memory_consumer_desc,
  mc.index_id,
  mc.allocated_bytes,
  mc.used_bytes
FROM sys.memory_optimized_tables_internal_attributes moa
   JOIN sys.columns c ON moa.object_id = c.object_id AND moa.minor_id=c.column_id
   JOIN sys.dm_db_xtp_memory_consumers mc ON moa.xtp_object_id=mc.xtp_object_id
   JOIN sys.objects o on moa.object_id=o.object_id 
WHERE moa.type=5;
```

### <a name="c-returning-memory-consumption-of-columnstore-indexes-on-memory-optimized-tables"></a>3. 메모리 최적화 테이블에서 columnstore 인덱스의 메모리 사용량 반환

다음 쿼리를 사용 하 여 메모리 최적화 테이블에서 columnstore 인덱스의 메모리 사용량을 보여 줍니다.

```Transact-SQL
SELECT
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table',
  i.name AS 'columnstore index',
  SUM(mc.allocated_bytes) / 1024 as [allocated_kb],
  SUM(mc.used_bytes) / 1024 as [used_kb]
FROM sys.memory_optimized_tables_internal_attributes moa
   JOIN sys.indexes i ON moa.object_id = i.object_id AND i.type in (5,6)
   JOIN sys.dm_db_xtp_memory_consumers mc ON moa.xtp_object_id=mc.xtp_object_id
   JOIN sys.objects o on moa.object_id=o.object_id
WHERE moa.type IN (0, 2, 3, 4)
GROUP BY o.schema_id, moa.object_id, i.name;
```

메모리 최적화 테이블에서 columnstore 인덱스에 사용 되는 내부 구조에서 다음 쿼리 되면서 메모리 소비를 사용 합니다.

```Transact-SQL
SELECT
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table',
  i.name AS 'columnstore index',
  moa.type_desc AS 'internal table',
  mc.index_id AS 'index',
  mc.memory_consumer_desc,
  mc.allocated_bytes / 1024 as [allocated_kb],
  mc.used_bytes / 1024 as [used_kb]
FROM sys.memory_optimized_tables_internal_attributes moa
   JOIN sys.indexes i ON moa.object_id = i.object_id AND i.type in (5,6)
   JOIN sys.dm_db_xtp_memory_consumers mc ON moa.xtp_object_id=mc.xtp_object_id
   JOIN sys.objects o on moa.object_id=o.object_id
WHERE moa.type IN (0, 2, 3, 4)
```


