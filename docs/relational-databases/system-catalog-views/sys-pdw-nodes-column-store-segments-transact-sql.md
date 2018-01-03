---
title: sys.pdw_nodes_column_store_segments (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: e2fdf8e9-1b74-4682-b2d4-c62aca053d7f
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b10564c7736dce2ab21cc83bed819606230e7b9
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="syspdwnodescolumnstoresegments-transact-sql"></a>sys.pdw_nodes_column_store_segments (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Columnstore 인덱스의 각 열에 대해 행을 하나씩 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|파티션 ID를 나타냅니다. 데이터베이스 내에서 고유합니다.|  
|**hobt_id**|**bigint**|이 Columnstore 인덱스를 가진 테이블의 B-트리 인덱스(hobt) 또는 힙의 ID입니다.|  
|**column_id**|**int**|Columnstore 열의 ID입니다.|  
|**segment_id**|**int**|열 세그먼트의 ID입니다.|  
|**version**|**int**|열 세그먼트 형식의 버전입니다.|  
|**encoding_type**|**int**|세그먼트에 사용되는 인코딩 형식입니다.|  
|**row_count**|**int**|행 그룹의 행 수입니다.|  
|**has_nulls**|**int**|열 세그먼트에 Null 값이 있으면 1입니다.|  
|**않으면 base_id**|**bigint**|인코딩 유형 1 기준 값 id는 사용 중입니다.  인코딩 유형 1은 사용 되지 않으면 base_id가 1로 설정 됩니다.|  
|**크기**|**float**|인코딩 유형 1 경우 magnitude는 사용 중입니다.  인코딩 유형 1은 사용 되지 크기가 1로 설정 됩니다.|  
|**primary__dictionary_id**|**int**|기본 사전의 ID입니다.|  
|**secondary_dictionary_id**|**int**|보조 사전의 ID입니다. 보조 사전이 없는 경우 -1을 반환합니다.|  
|**min_data_id**|**bigint**|열 세그먼트의 최소 데이터 ID입니다.|  
|**max_data_id**|**bigint**|열 세그먼트의 최대 데이터 ID입니다.|  
|**반환**|**bigint**|Null을 나타내는 데 사용되는 값입니다.|  
|**on_disk_size**|**bigint**|세그먼트의 크기(바이트)입니다.|  
|**pdw_node_id**|**int**|고유 식별자는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 참고 합니다.|  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 쿼리는 columnstore 인덱스의 세그먼트에 대한 정보를 반환합니다.  
  
```sql  
SELECT i.name, p.object_id, p.index_id, i.type_desc,   
    COUNT(*) AS number_of_segments  
FROM sys.column_store_segments AS s   
INNER JOIN sys.partitions AS p   
    ON s.hobt_id = p.hobt_id   
INNER JOIN sys.indexes AS i   
    ON p.object_id = i.object_id  
WHERE i.type = 6  
GROUP BY i.name, p.object_id, p.index_id, i.type_desc ;  
```  
  
 행 개수를 결정 하 고 디스크에 있는 세그먼트의 크기를 다른 시스템 테이블이 있는 sys.pdw_nodes_column_store_segments를 조인 합니다.  
  
```  
SELECT o.name, css.hobt_id, css. column_id, css.pdw_node_id, css.row_count, css.on_disk_size  
FROM sys.pdw_nodes_column_store_segments AS css  
JOIN sys.pdw_nodes_partitions AS pnp  
    ON css.partition_id = pnp.partition_id  
JOIN sys.pdw_nodes_tables AS part  
    ON pnp.object_id = part.object_id   
    AND pnp.pdw_node_id = part.pdw_node_id  
JOIN sys.pdw_table_mappings AS TMap  
    ON part.name = TMap.physical_name  
JOIN sys.objects AS o  
    ON TMap.object_id = o.object_id  
ORDER BY css.hobt_id, css.column_id;  
```  
  
## <a name="permissions"></a>Permissions  
 필요한 **VIEW SERVER STATE** 권한.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [COLUMNSTORE index&#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_row_groups &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)   
 [sys.pdw_nodes_column_store_dictionaries &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
  

