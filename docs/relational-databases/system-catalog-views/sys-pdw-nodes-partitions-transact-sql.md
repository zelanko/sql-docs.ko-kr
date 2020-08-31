---
description: sys. pdw_nodes_partitions (Transact-sql)
title: sys. pdw_nodes_partitions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: b4216752-4813-4b2c-b259-7d8ffc6cc190
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 82903661be207c73b1b848e8273b594ff49d1642
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89062272"
---
# <a name="syspdw_nodes_partitions-transact-sql"></a>sys. pdw_nodes_partitions (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  모든 테이블의 각 파티션에 대 한 행과 데이터베이스의 대부분의 인덱스 유형을 포함 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 합니다. 모든 테이블 및 인덱스는 명시적으로 분할 되었는지 여부에 관계 없이 하나 이상의 파티션을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|파티션의 ID입니다. 데이터베이스 내에서 고유합니다.|  
|object_id|**int**|이 파티션이 속한 개체의 ID입니다. 모든 테이블 또는 뷰는 최소한 하나 이상의 파티션으로 구성됩니다.|  
|index_id|**int**|이 파티션이 속한 개체 내부의 인덱스 ID입니다.|  
|partition_number|**int**|소유하는 인덱스나 힙 내의 1부터 시작하는 파티션 번호입니다. 의 경우 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 이 열의 값은 1입니다.|  
|hobt_id|**bigint**|이 파티션에 대 한 행을 포함 하는 데이터 힙 또는 B-트리 (HoBT)의 ID입니다.|  
|rows|**bigint**|이 파티션에 있는 행의 대략적인 수입니다. |  
|data_compression|**int**|각 파티션의 압축 상태를 나타냅니다.<br /><br /> 0 = 없음<br /><br /> 1 = ROW<br /><br /> 2 = PAGE<br /><br /> 3 = COLUMNSTORE|  
|data_compression_desc|**nvarchar(60)**|각 파티션의 압축 상태를 나타냅니다. 가능한 값은 NONE, ROW 및 PAGE입니다.|  
|pdw_node_id|**int**|노드의 고유 식별자 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 입니다.|  
  
## <a name="permissions"></a>사용 권한  
 `CONTROL SERVER` 권한이 필요합니다.  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  

### <a name="example-a-display-rows-in-each-partition-within-each-distribution"></a>예 A: 각 배포 내의 각 파티션에 행 표시 

**적용 대상:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]
 
각 배포 내의 각 파티션에 있는 행 수를 표시 하려면 [DBCC PDW_SHOWPARTITIONSTATS (SQL Server PDW)](../../t-sql/database-console-commands/dbcc-pdw-showpartitionstats-transact-sql.md) 를 사용 합니다.

### <a name="example-b-uses-system-views-to-view-rows-in-each-partition-of-each-distribution-of-a-table"></a>예 2: 시스템 뷰를 사용 하 여 테이블의 각 배포에 대 한 각 파티션의 행을 볼 수 있습니다.

**적용 대상:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
 
이 쿼리는 테이블의 각 배포에 대 한 각 파티션에 있는 행 수를 반환 합니다 `myTable` .  
 
```sql  
SELECT o.name, pnp.index_id, pnp.partition_id, pnp.rows,   
    pnp.data_compression_desc, pnp.pdw_node_id  
FROM sys.pdw_nodes_partitions AS pnp  
JOIN sys.pdw_nodes_tables AS NTables  
    ON pnp.object_id = NTables.object_id  
AND pnp.pdw_node_id = NTables.pdw_node_id  
JOIN sys.pdw_table_mappings AS TMap  
    ON NTables.name = TMap.physical_name 
    AND substring(TMap.physical_name,40, 10) = pnp.distribution_id 
JOIN sys.objects AS o  
    ON TMap.object_id = o.object_id  
WHERE o.name = 'myTable'  
ORDER BY o.name, pnp.index_id, pnp.partition_id;  
```    
  
## <a name="see-also"></a>참고 항목  
 [SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

