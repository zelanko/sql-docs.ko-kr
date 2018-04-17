---
title: sys.pdw_nodes_column_store_segments (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2018
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e2fdf8e9-1b74-4682-b2d4-c62aca053d7f
caps.latest.revision: 9
author: hirokib
ms.author: elbutter;barbkess
manager: jrj
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6096185bec4378bd5d6b2f478796f8a2e34f5e1d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="syspdwnodescolumnstoresegments-transact-sql"></a>sys.pdw_nodes_column_store_segments (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Columnstore 인덱스의 각 열에 대해 행을 하나씩 포함합니다.  

| 열 이름                 | 데이터 형식  | Description                                                  |
| --------------------------- | ---------- | ------------------------------------------------------------ |
| **partition_id**            | **bigint** | 파티션 ID를 나타냅니다. 데이터베이스 내에서 고유합니다.     |
| **hobt_id**                 | **bigint** | 이 Columnstore 인덱스를 가진 테이블의 B-트리 인덱스(hobt) 또는 힙의 ID입니다. |
| **column_id**               | **int**    | Columnstore 열의 ID입니다.                                |
| **segment_id**              | **int**    | 열 세그먼트의 ID입니다. 이전 버전과 호환성에 대 한 열 이름을 계속 행 그룹 ID입니다. 있더라도 segment_id를 호출할 수 < Hobt_id, partition_id, column_id >를 사용 하 여 세그먼트를 고유 하 게 식별할 수 있습니다 < segment_id > 합니다. |
| **version**                 | **int**    | 열 세그먼트 형식의 버전입니다.                        |
| **encoding_type**           | **int**    | 해당 세그먼트에 대해 사용 되는 인코딩 유형:<br /><br /> 1 = VALUE_BASED-문자열/이진이 아님으로 사용 가능한 사전 (일부 내부 변형이 4와 유사)<br /><br /> 2 = VALUE_HASH_BASED-사전에 공통 값과 문자열/이진이 아닌 열<br /><br /> 3 = STRING_HASH_BASED-사전에 공통 값과 문자열/이진 열<br /><br /> 4 = STORE_BY_VALUE_BASED-문자열/이진이 아님으로 없는 사전 사용 하 여<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED-문자열/이항 없는 사전 사용 하 여<br /><br /> 모든 인코딩을 활용 가능한 경우 비트 압축 및 실행 길이 인코딩. |
| **row_count**               | **int**    | 행 그룹의 행 수입니다.                             |
| **has_nulls**               | **int**    | 열 세그먼트에 Null 값이 있으면 1입니다.                     |
| **base_id**                 | **bigint** | 인코딩 유형 1 기준 값 ID는 사용 중입니다.  인코딩 유형 1은 사용 되지 않으면 base_id가 1로 설정 됩니다. |
| **magnitude**               | **float**  | 인코딩 유형 1 경우 magnitude는 사용 중입니다.  인코딩 유형 1은 사용 되지 크기가 1로 설정 됩니다. |
| **primary__dictionary_id**  | **int**    | 기본 사전의 ID입니다. 0이 아닌 값이이 열에 현재 세그먼트 (즉, 행)에 대 한 로컬 사전을를 가리킵니다. -1 값이이 세그먼트에 대 한 사전이 없습니다 로컬 임을 나타냅니다. |
| **secondary_dictionary_id** | **int**    | 보조 사전의 ID입니다. 0이 아닌 값이이 열에 현재 세그먼트 (즉, 행)에 대 한 로컬 사전을를 가리킵니다. -1 값이이 세그먼트에 대 한 사전이 없습니다 로컬 임을 나타냅니다. |
| **min_data_id**             | **bigint** | 열 세그먼트의 최소 데이터 ID입니다.                       |
| **max_data_id**             | **bigint** | 열 세그먼트의 최대 데이터 ID입니다.                       |
| **null_value**              | **bigint** | Null을 나타내는 데 사용되는 값입니다.                               |
| **on_disk_size**            | **bigint** | 세그먼트의 크기(바이트)입니다.                                    |
| **pdw_node_id**             | **int**    | 고유 식별자는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 노드. |

## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  

Sys.pdw_nodes_column_store_segments 논리 테이블당 columnstore 세그먼트의 수를 확인 하려면 다른 시스템 테이블을 조인 합니다. 

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
,           sm.name
```

## <a name="permissions"></a>Permissions  
 **VIEW SERVER STATE** 권한이 필요합니다.  

## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [COLUMNSTORE 인덱스를 만들 &#40;Transact SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_row_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)   
 [sys.pdw_nodes_column_store_dictionaries &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  

  

