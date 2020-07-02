---
title: sys.debug (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 02/12/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.indexes
- indexes
- sys.indexes_TSQL
- indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes catalog view
ms.assetid: 066bd9ac-6554-4297-88fe-d740de1f94a8
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3fbd009d47d7019994359c480c55c251950d0940
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734847"
---
# <a name="sysindexes-transact-sql"></a>sys.indexes(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asdw-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  테이블, 뷰 또는 테이블 반환 함수와 같은 테이블 형식 개체의 인덱스 또는 힙당 하나의 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 인덱스가 속한 개체의 ID입니다.|  
|**name**|**sysname**|인덱스의 이름입니다. **이름은** 개체 내 에서만 고유 합니다.<br /><br /> NULL = 힙|  
|**index_id**|**int**|인덱스의 ID입니다. **index_id** 는 개체 내 에서만 고유 합니다.<br /><br /> 0 = 힙<br /><br /> 1 = 클러스터형 인덱스<br /><br /> > 1 = 비클러스터형 인덱스|  
|**type**|**tinyint**|인덱스의 유형입니다.<br /><br /> 0 = 힙<br /><br /> 1 = 클러스터형<br /><br /> 2 = 비클러스터형<br /><br /> 3 = XML<br /><br /> 4 = 공간<br /><br /> 5 = 클러스터형 columnstore 인덱스 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상<br /><br /> 6 = 비클러스터형 columnstore 인덱스입니다. **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 7 = 비클러스터형 해시 인덱스입니다. **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상|  
|**type_desc**|**nvarchar(60)**|인덱스 유형의 설명입니다.<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> XML<br /><br /> SPATIAL<br /><br /> 클러스터형 COLUMNSTORE-다음 **에 적용 됩니다. 이상에 적용**됩니다 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .<br /><br /> 비클러스터형 COLUMNSTORE- **이상에 적용 됩니다**. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]<br /><br /> 비클러스터형 해시: 비클러스터형 해시 인덱스는 메모리 최적화 테이블 에서만 지원 됩니다. sys.hash_indexes 뷰는 현재 해시 인덱스 및 해시 속성을 보여 줍니다. 자세한 내용은 [hash_indexes &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-hash-indexes-transact-sql.md)을 참조 하십시오. **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상|  
|**is_unique**|**bit**|1 = 인덱스가 고유합니다.<br /><br /> 0 = 인덱스가 고유하지 않습니다.<br /><br /> 클러스터형 columnstore 인덱스의 경우 항상 0입니다.|  
|**data_space_id**|**int**|이 인덱스에 대한 데이터 공간의 ID입니다. 데이터 공간은 파일 그룹 또는 파티션 구성표입니다.<br /><br /> 0 = **object_id** 테이블 반환 함수 또는 메모리 내 인덱스입니다.|  
|**ignore_dup_key**|**bit**|1 = IGNORE_DUP_KEY가 ON입니다.<br /><br /> 0 = IGNORE_DUP_KEY가 OFF입니다.|  
|**is_primary_key**|**bit**|1 = 인덱스가 PRIMARY KEY 제약 조건의 일부입니다.<br /><br /> 클러스터형 columnstore 인덱스의 경우 항상 0입니다.|  
|**is_unique_constraint**|**bit**|1 = 인덱스가 UNIQUE 제약 조건의 일부입니다.<br /><br /> 클러스터형 columnstore 인덱스의 경우 항상 0입니다.|  
|**fill_factor**|**tinyint**|> 0 = 인덱스를 만들거나 다시 작성할 때 사용 되는 FILLFACTOR 백분율입니다.<br /><br /> 0 = 기본값<br /><br /> 클러스터형 columnstore 인덱스의 경우 항상 0입니다.|  
|**is_padded**|**bit**|1 = PADINDEX가 ON입니다.<br /><br /> 0 = PADINDEX가 OFF입니다.<br /><br /> 클러스터형 columnstore 인덱스의 경우 항상 0입니다.|  
|**is_disabled**|**bit**|1 = 인덱스가 비활성화되었습니다.<br /><br /> 0 = 인덱스가 비활성화되지 않았습니다.|  
|**is_hypothetical**|**bit**|1 = 인덱스가 가상 인덱스이며 데이터 액세스 경로로 직접 사용할 수 없습니다. 가상 인덱스는 열 수준 통계를 보유합니다.<br /><br /> 0 = 인덱스가 가상 인덱스입니다.|  
|**allow_row_locks**|**bit**|1 = 인덱스에서 행 잠금을 허용합니다.<br /><br /> 0 = 인덱스에서 행 잠금을 허용하지 않습니다.<br /><br /> 클러스터형 columnstore 인덱스의 경우 항상 0입니다.|  
|**allow_page_locks**|**bit**|1 = 인덱스에서 페이지 잠금을 허용합니다.<br /><br /> 0 = 인덱스에서 페이지 잠금을 허용하지 않습니다.<br /><br /> 클러스터형 columnstore 인덱스의 경우 항상 0입니다.|  
|**has_filter**|**bit**|1 = 인덱스에 필터가 있고 포함된 모든 행이 필터 정의를 만족합니다.<br /><br /> 0 = 인덱스에 필터가 없습니다.|  
|**filter_definition**|**nvarchar(max)**|필터링된 인덱스에 포함된 행 하위 집합에 대한 식입니다.<br /><br /> 힙, 필터링 되지 않은 인덱스 또는 테이블에 대 한 권한이 부족 한 경우 NULL입니다.|  
|**auto_created**|**bit**|1 = 자동 조정으로 인덱스를 만들었습니다.<br /><br />0 = 사용자가 인덱스를 만들었습니다.
|**optimize_for_sequential_key**|**bit**|1 = 인덱스에서 마지막 페이지 삽입 최적화를 사용 하도록 설정 했습니다.<br><br>0 = 기본값 인덱스에서 마지막 페이지 삽입 최적화를 사용할 수 없습니다.|

> [!NOTE]
> **Optimize_for_sequential_key** 비트 SQL SERVER 2019 CTP 3.1 이상 버전 에서만 지원 됩니다.
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예제  
 다음 예에서는 데이터베이스의 테이블에 대 한 모든 인덱스를 반환 합니다 `Production.Product` [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
```  
  
SELECT i.name AS index_name  
    ,i.type_desc  
    ,is_unique  
    ,ds.type_desc AS filegroup_or_partition_scheme  
    ,ds.name AS filegroup_or_partition_scheme_name  
    ,ignore_dup_key  
    ,is_primary_key  
    ,is_unique_constraint  
    ,fill_factor  
    ,is_padded  
    ,is_disabled  
    ,allow_row_locks  
    ,allow_page_locks  
FROM sys.indexes AS i  
INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
WHERE is_hypothetical = 0 AND i.index_id <> 0   
AND i.object_id = OBJECT_ID('Production.Product');  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [index_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [Transact-sql&#41;sys.xml_indexes &#40;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [sys. 개체 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [key_constraints &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys. 파일 그룹 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [partition_schemes &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
