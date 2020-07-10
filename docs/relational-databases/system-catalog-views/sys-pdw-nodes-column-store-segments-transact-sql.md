---
title: sys. pdw_nodes_column_store_segments (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 03/28/2018
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e2fdf8e9-1b74-4682-b2d4-c62aca053d7f
author: julieMSFT
ms.author: jrasnick
manager: jrj
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: fc1e04718ea9db16d3b0c2a1cc59b14f906c6f31
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197192"
---
# <a name="syspdw_nodes_column_store_segments-transact-sql"></a>sys. pdw_nodes_column_store_segments (Transact-sql)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

Columnstore 인덱스의 각 열에 대해 행을 하나씩 포함합니다.

| 열 이름                 | 데이터 형식  | Description                                                  |
| :-------------------------- | :--------- | :----------------------------------------------------------- |
| **partition_id**            | **bigint** | 파티션 ID를 나타냅니다. 데이터베이스 내에서 고유합니다.     |
| **hobt_id**                 | **bigint** | 이 Columnstore 인덱스를 가진 테이블의 B-트리 인덱스(hobt) 또는 힙의 ID입니다. |
| **column_id**               | **int**    | Columnstore 열의 ID입니다.                                |
| **segment_id**              | **int**    | 열 세그먼트의 ID입니다. 이전 버전과의 호환성을 위해 행 그룹 ID 인 경우에도 열 이름은 segment_id 계속 호출 됩니다. <hobt_id, partition_id, column_id> <segment_id>를 사용 하 여 세그먼트를 고유 하 게 식별할 수 있습니다. |
| **version**                 | **int**    | 열 세그먼트 형식의 버전입니다.                        |
| **encoding_type**           | **int**    | 해당 세그먼트에 사용 되는 인코딩 유형입니다.<br /><br /> 1 = VALUE_BASED-사전 없이 문자열이 아닌/이진 (일부 내부 변형이 있는 4와 유사)<br /><br /> 2 = VALUE_HASH_BASED-사전에 공통 값이 있는 문자열이 아닌/이진 열<br /><br /> 3 = STRING_HASH_BASED-사전에 공통 값이 있는 문자열/이진 열<br /><br /> 4 = STORE_BY_VALUE_BASED-사전이 없는 문자열/이진<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED-사전 없는 문자열/이진<br /><br /> 모든 인코딩은 가능 하면 비트 압축 및 실행 길이 인코딩을 활용 합니다. |
| **row_count**               | **int**    | 행 그룹의 행 수입니다.                             |
| **has_nulls**               | **int**    | 열 세그먼트에 Null 값이 있으면 1입니다.                     |
| **base_id**                 | **bigint** | 인코딩 유형 1을 사용 하는 경우 기준 값 ID입니다.  인코딩 유형 1을 사용 하지 않는 경우 base_id 1로 설정 됩니다. |
| **magnitude**               | **float**  | 인코딩 유형 1을 사용 하는 경우 크기입니다.  인코딩 유형 1을 사용 하지 않는 경우 크기는 1로 설정 됩니다. |
| **primary__dictionary_id**  | **int**    | 기본 사전의 ID입니다. 0이 아닌 값은 현재 세그먼트 (즉, 행 그룹)의이 열에 대 한 로컬 사전을 가리킵니다. 값-1은이 세그먼트에 대 한 로컬 사전이 없음을 나타냅니다. |
| **secondary_dictionary_id** | **int**    | 보조 사전의 ID입니다. 0이 아닌 값은 현재 세그먼트 (즉, 행 그룹)의이 열에 대 한 로컬 사전을 가리킵니다. 값-1은이 세그먼트에 대 한 로컬 사전이 없음을 나타냅니다. |
| **min_data_id**             | **bigint** | 열 세그먼트의 최소 데이터 ID입니다.                       |
| **max_data_id**             | **bigint** | 열 세그먼트의 최대 데이터 ID입니다.                       |
| **null_value**              | **bigint** | Null을 나타내는 데 사용되는 값입니다.                               |
| **on_disk_size**            | **bigint** | 세그먼트의 크기(바이트)입니다.                                    |
| **pdw_node_id**             | **int**    | 노드의 고유 식별자 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 입니다. |
| &nbsp; | &nbsp; | &nbsp; |

## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

다른 시스템 테이블과 pdw_nodes_column_store_segments를 조인 하 여 논리적 테이블당 columnstore 세그먼트 수를 확인 합니다.

```sql
SELECT  sm.name           as schema_nm
,       tb.name           as table_nm
,       nc.name           as col_nm
,       nc.column_id
,       COUNT(*)          as segment_count
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb                   ON  sm.[schema_id]          = tb.[schema_id]
JOIN    sys.[pdw_table_mappings] mp       ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt         ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[pdw_nodes_partitions] np     ON  np.[object_id]          = nt.[object_id]
                                          AND np.[pdw_node_id]        = nt.[pdw_node_id]
                                          AND np.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_nodes_columns] nc        ON  np.[object_id]          = nc.[object_id]
                                          AND np.[pdw_node_id]        = nc.[pdw_node_id]
                                          AND np.[distribution_id]    = nc.[distribution_id]
JOIN    sys.[pdw_nodes_column_store_segments] rg  ON  rg.[partition_id]         = np.[partition_id]
                                                      AND rg.[pdw_node_id]      = np.[pdw_node_id]
                                                      AND rg.[distribution_id]  = np.[distribution_id]
                                                      AND rg.[column_id]        = nc.[column_id]
GROUP BY    sm.name
,           tb.name
,           nc.name
,           nc.column_id  
ORDER BY    table_nm
,           nc.column_id
,           sm.name ;
```

## <a name="permissions"></a>권한

**VIEW SERVER STATE** 권한이 필요합니다.

## <a name="see-also"></a>참고 항목

[SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
[CREATE COLUMNSTORE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)  
[pdw_nodes_column_store_row_groups &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
[pdw_nodes_column_store_dictionaries &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)
