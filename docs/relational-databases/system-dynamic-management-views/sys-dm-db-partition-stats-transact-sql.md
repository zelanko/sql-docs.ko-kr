---
title: sys.dm_db_partition_stats (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_partition_stats
- dm_db_partition_stats_TSQL
- sys.dm_db_partition_stats_TSQL
- sys.dm_db_partition_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_partition_stats dynamic management view
ms.assetid: 9db9d184-b3a2-421e-a804-b18ebcb099b7
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 668a7e12b4159aa5d3cc69fdc3937d817941cdd1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbpartitionstats-transact-sql"></a>sys.dm_db_partition_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스의 모든 파티션에 대해 페이지 및 행 수 정보를 반환합니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_db_partition_stats**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|파티션의 ID입니다. 데이터베이스 내에서 고유합니다. 이 동일한 값으로는 **partition_id** 에 **sys.partitions** 카탈로그 뷰|  
|**object_id**|**int**|파티션이 속한 테이블 또는 인덱싱된 뷰의 개체 ID입니다.|  
|**index_id**|**int**|파티션이 속한 힙 또는 인덱스의 ID입니다.<br /><br /> 0 = 힙<br /><br /> 1 = 클러스터형 인덱스<br /><br /> > 1 = 비클러스터형 인덱스|  
|**partition_number**|**int**|인덱스 또는 힙 내의 1부터 시작하는 파티션 번호입니다.|  
|**in_row_data_page_count**|**bigint**|이 파티션의 행 내부 데이터를 저장하는 데 사용되는 페이지 수입니다. 파티션이 힙의 일부인 경우 이 값은 힙의 데이터 페이지 수입니다. 파티션이 인덱스의 일부인 경우 이 값은 리프 수준의 페이지 수입니다. B-트리의 리프가 아닌 페이지는 이 수에 포함되지 않습니다. 어느 경우에도 IAM(Index Allocation Map) 페이지는 포함되지 않습니다. xVelocity 메모리 최적화 columnstore 인덱스의 경우 항상 0입니다.|  
|**in_row_used_page_count**|**bigint**|이 파티션의 행 내부 데이터를 저장하고 관리하는 데 사용되는 페이지의 총 수입니다. 리프가 아닌 B-트리 페이지, IAM 페이지 및에 포함 된 모든 페이지를 포함 하는이 개수는 **in_row_data_page_count** 열입니다. columnstore 인덱스의 경우 항상 0입니다.|  
|**in_row_reserved_page_count**|**bigint**|페이지 사용 여부에 관계없이 이 파티션의 행 내부 데이터를 저장하고 관리하는 데 사용하도록 예약된 페이지의 총 수입니다. columnstore 인덱스의 경우 항상 0입니다.|  
|**lob_used_page_count**|**bigint**|저장 하 고 행 아웃 관리에 사용 중인 페이지 수 **텍스트**, **ntext**, **이미지**, **varchar (max)**, **nvarchar (max)** , **varbinary (max)**, 및 **xml** 파티션 내에서 열. IAM 페이지가 포함됩니다.<br /><br /> 파티션의 columnstore 인덱스를 저장하고 관리하는 데 사용되는 LOB의 총 수입니다.|  
|**lob_reserved_page_count**|**bigint**|저장 하 고 행 아웃 관리 하도록 예약 된 페이지의 총 **텍스트**, **ntext**, **이미지**, **varchar (max)**,  **nvarchar (max)**, **varbinary (max)**, 및 **xml** 여부에서 페이지를 사용 하 여 여부에 관계 없이 파티션 내에서 열. IAM 페이지가 포함됩니다.<br /><br /> 파티션의 columnstore 인덱스를 저장하고 관리하는 데 사용하도록 예약된 LOB의 총 수입니다.|  
|**row_overflow_used_page_count**|**bigint**|페이지를 저장 및 행 오버플로 관리에 대 한 사용 수가 **varchar**, **nvarchar**, **varbinary**, 및 **sql_variant** 열 파티션 내에서. IAM 페이지가 포함됩니다.<br /><br /> columnstore 인덱스의 경우 항상 0입니다.|  
|**row_overflow_reserved_page_count**|**bigint**|저장 하 고 행-오버플로 관리 하도록 예약 된 페이지의 총 **varchar**, **nvarchar**, **varbinary**, 및 **sql_variant** 여부에서 페이지를 사용 하 여 여부에 관계 없이 파티션 내에서 열입니다. IAM 페이지가 포함됩니다.<br /><br /> columnstore 인덱스의 경우 항상 0입니다.|  
|**used_page_count**|**bigint**|파티션에 사용되는 페이지의 총 수입니다. 다음과 같이 계산 **in_row_used_page_count** + **lob_used_page_count** + **row_overflow_used_page_count**합니다.|  
|**reserved_page_count**|**bigint**|파티션에 사용하도록 예약된 페이지의 총 수입니다. 다음과 같이 계산 **in_row_reserved_page_count** + **lob_reserved_page_count** + **row_overflow_reserved_page_count**합니다.|  
|**row_count**|**bigint**|파티션에 있는 행의 대략적인 수입니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
|**distribution_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 분포에 관련 된 고유 숫자 id입니다.|  
  
## <a name="remarks"></a>주의  
 **sys.dm_db_partition_stats** 저장 하 고 행 내부, LOB 데이터 및 데이터베이스의 모든 파티션에 대 한 행 오버플로 데이터를 관리 하는 데 사용 되는 공간에 대 한 정보를 표시 합니다. 파티션마다 행 하나가 표시됩니다.  
  
 출력의 기준이 되는 이 개수는 메모리에 캐시되거나 디스크에서 다양한 시스템 테이블에 저장됩니다.  
  
 행 내부 데이터, LOB 데이터 및 행 오버플로 데이터는 파티션을 구성하는 세 개의 할당 단위를 나타냅니다. [sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md) 데이터베이스의 각 할당 단위에 대 한 메타 데이터에 대 한 카탈로그 뷰를 쿼리할 수 있습니다.  
  
 힙이나 인덱스가 분할되지 않은 경우에는 하나의 파티션으로 구성되므로(파티션 번호 = 1) 힙이나 인덱스에 대해 하나의 행만 반환됩니다. [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) 모든 테이블 및 데이터베이스에서 인덱스의 각 파티션에 대 한 메타 데이터에 대 한 카탈로그 뷰를 쿼리할 수 있습니다.  
  
 개별 테이블이나 인덱스에 대한 총 수는 관련된 모든 파티션에 대한 수를 더하여 얻을 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 쿼리하려면 VIEW DATABASE STATE 권한이 필요는 **sys.dm_db_partition_stats** 동적 관리 뷰. 동적 관리 뷰 사용 권한에 대 한 자세한 내용은 참조 [동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-all-counts-for-all-partitions-of-all-indexes-and-heaps-in-a-database"></a>1. 데이터베이스에 있는 모든 인덱스와 힙의 모든 파티션에 대한 모든 개수 반환  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 모든 인덱스와 힙의 모든 파티션에 대한 모든 개수를 표시합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_partition_stats;  
GO  
```  
  
### <a name="b-returning-all-counts-for-all-partitions-of-a-table-and-its-indexes"></a>2. 테이블과 테이블 인덱스의 모든 파티션에 대한 모든 개수 반환  
 다음 예에서는 `HumanResources.Employee` 테이블과 해당 인덱스의 모든 파티션에 대한 모든 개수를 표시합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_partition_stats   
WHERE object_id = OBJECT_ID('HumanResources.Employee');  
GO  
```  
  
### <a name="c-returning-total-used-pages-and-total-number-of-rows-for-a-heap-or-clustered-index"></a>3. 힙 또는 클러스터형 인덱스에 대해 사용된 총 페이지 및 총 행 수 반환  
 다음 예에서는 `HumanResources.Employee` 테이블의 힙이나 클러스터형 인덱스에 대해 사용된 총 페이지와 총 행 수를 반환합니다. `Employee` 테이블은 기본적으로 분할되지 않기 때문에 합계에는 하나의 파티션만 포함됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT SUM(used_page_count) AS total_number_of_used_pages,   
    SUM (row_count) AS total_number_of_rows   
FROM sys.dm_db_partition_stats  
WHERE object_id=OBJECT_ID('HumanResources.Employee')    AND (index_id=0 or index_id=1);  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  


