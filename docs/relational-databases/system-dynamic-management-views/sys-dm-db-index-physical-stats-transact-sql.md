---
description: sys.dm_db_index_physical_stats(Transact-SQL)
title: sys. dm_db_index_physical_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_index_physical_stats
- sys.dm_db_index_physical_stats_TSQL
- sys.dm_db_index_physical_stats
- dm_db_index_physical_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_physical_stats dynamic management function
- fragmentation [SQL Server]
ms.assetid: d294dd8e-82d5-4628-aa2d-e57702230613
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 23fa1d8b5dc2f6e9caa1dccaf73ea788dac8bc1f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447765"
---
# <a name="sysdm_db_index_physical_stats-transact-sql"></a>sys.dm_db_index_physical_stats(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지정한 테이블 또는 뷰의 데이터 및 인덱스에 대한 크기 및 조각화 정보를 반환합니다. 인덱스의 경우 각 파티션에 있는 B-트리의 각 수준에 대해 행이 반환됩니다. 힙의 경우 각 파티션의 IN_ROW_DATA 할당 단위에 대해 행이 반환됩니다. LOB(Large Object) 데이터의 경우 각 파티션의 LOB_DATA 할당 단위에 대해 행이 반환됩니다. 테이블에 행-오버플로 데이터가 있는 경우 각 파티션의 ROW_OVERFLOW_DATA 할당 단위에 대해 행이 반환됩니다. xVelocity  메모리 액세스에 최적화된 columnstore  인덱스에 대한 정보를 반환하지 않습니다.  
  
> [!IMPORTANT]
> Always On [읽을 수 있는 보조 복제본](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)을 호스팅하는 서버 인스턴스에서 **dm_db_index_physical_stats** 를 쿼리하면 다시 실행 차단 문제가 발생할 수 있습니다. 이는 이 동적 관리 뷰가 지정된 사용자 테이블 또는 뷰에 대한 IS 잠금을 획득하여 REDO 스레드에서의 해당 사용자 테이블 또는 뷰에 대한 X 잠금 요청이 차단되기 때문입니다.  
  
 **dm_db_index_physical_stats** 는 메모리 최적화 인덱스에 대 한 정보를 반환 하지 않습니다. 메모리 최적화 인덱스 사용에 대 한 자세한 내용은 [dm_db_xtp_index_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)을 참조 하십시오.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.dm_db_index_physical_stats (   
    { database_id | NULL | 0 | DEFAULT }  
  , { object_id | NULL | 0 | DEFAULT }  
  , { index_id | NULL | 0 | -1 | DEFAULT }  
  , { partition_number | NULL | 0 | DEFAULT }  
  , { mode | NULL | DEFAULT }  
)  
```  
  
## <a name="arguments"></a>인수  
 *database_id* \| NULL \| 0 \| 기본값  
 데이터베이스의 ID입니다. *database_id* 은 **smallint**입니다. 올바른 입력은 데이터베이스의 ID 번호, NULL, 0 또는 DEFAULT입니다. 기본값은 0입니다. 이 컨텍스트에서 NULL, 0 및 DEFAULT는 동등한 값입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 데이터베이스에 대한 정보를 반환하려면 NULL을 지정합니다. *Database_id*에 대해 null을 지정 하는 경우 *object_id*, *index_id*및 *partition_number*에 대해서도 null을 지정 해야 합니다.  
  
 [DB_ID](../../t-sql/functions/db-id-transact-sql.md) 기본 제공 함수를 지정할 수 있습니다. 데이터베이스 이름을 지정하지 않고 DB_ID를 사용하는 경우 현재 데이터베이스의 호환성 수준은 90 이상이어야 합니다.  
  
 *object_id* \| NULL \| 0 \| 기본값  
 인덱스가 있는 테이블 또는 뷰의 개체 ID입니다. *object_id* 는 **int**입니다.  
  
 올바른 입력은 테이블 및 뷰의 ID 번호, NULL, 0 또는 DEFAULT입니다. 기본값은 0입니다. 이 컨텍스트에서 NULL, 0 및 DEFAULT는 동등한 값입니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 유효한 입력은 service broker 큐 이름 또는 큐 내부 테이블 이름을 포함 합니다. 모든 개체, 모든 인덱스 등의 기본 매개 변수를 적용 하는 경우 모든 큐에 대 한 조각화 정보는 결과 집합에 포함 됩니다.  
  
 지정된 데이터베이스에 있는 모든 테이블 및 뷰에 대한 정보를 반환하려면 NULL을 지정합니다. *Object_id*에 대해 null을 지정 하는 경우 *index_id* 및 *partition_number*에 대해서도 null을 지정 해야 합니다.  
  
 *index_id* \| 0 \| NULL \| -1 \| 기본값  
 인덱스의 ID입니다. *index_id* 은 **int**입니다. 유효한 입력은 인덱스의 ID 번호, *object_id* 가 힙, NULL,-1 또는 DEFAULT 인 경우 0입니다. 기본값은 -1입니다. 이 컨텍스트에서 NULL,-1 및 DEFAULT는 동일한 값입니다.  
  
 기본 테이블 또는 뷰에 대한 모든 인덱스 정보를 반환하려면 NULL을 지정합니다. *Index_id*에 대해 null을 지정 하는 경우 *partition_number*에 대해서도 null을 지정 해야 합니다.  
  
 *partition_number* \| NULL \| 0 \| 기본값  
 개체의 파티션 번호입니다. *partition_number* 은 **int**입니다. 유효한 입력은 인덱스 또는 힙의 *partion_number* , NULL, 0 또는 DEFAULT입니다. 기본값은 0입니다. 이 컨텍스트에서 NULL, 0 및 DEFAULT는 동등한 값입니다.  
  
 소유하는 개체의 모든 파티션에 대한 정보를 반환하려면 NULL을 지정합니다.  
  
 *partition_number* 은 1부터 사용 됩니다. 분할 되지 않은 인덱스 또는 힙의 *partition_number* 1로 설정 되어 있습니다.  
  
 *모드* \| NULL \| 기본값  
 모드 이름입니다. *모드* 통계를 얻는 데 사용 되는 검색 수준을 지정 합니다. *모드* 는 **sysname**입니다. 유효한 입력은 DEFAULT, NULL, LIMITED, SAMPLED 또는 DETAILED입니다. 기본값(NULL)은 LIMITED입니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|테이블 또는 뷰의 데이터베이스 ID입니다.|  
|object_id|**int**|인덱스가 있는 테이블 또는 뷰의 개체 ID입니다.|  
|index_id|**int**|인덱스의 인덱스 ID입니다.<br /><br /> 0 = 힙|  
|partition_number|**int**|테이블, 뷰 또는 인덱스 등의 소유하는 개체 내의 1부터 시작하는 파티션 번호입니다.<br /><br /> 1 = 분할되지 않은 인덱스 또는 힙|  
|index_type_desc|**nvarchar(60)**|인덱스 유형에 대한 설명입니다.<br /><br /> HEAP<br /><br /> CLUSTERED  INDEX<br /><br /> NONCLUSTERED  INDEX<br /><br /> PRIMARY  XML  INDEX<br /><br /> 확장 인덱스<br /><br /> XML INDEX<br /><br /> COLUMNSTORE 매핑 인덱스 (내부)<br /><br /> COLUMNSTORE DELETEBUFFER 인덱스 (내부)<br /><br /> COLUMNSTORE DELETEBITMAP 인덱스 (내부)|  
|hobt_id|**bigint**|힙 또는 B-인덱스 또는 파티션의 ID입니다.<br /><br /> 사용자 정의 인덱스의 hobt_id 반환 하는 것 외에도 내부 columnstore 인덱스의 hobt_id 반환 합니다.|  
|alloc_unit_type_desc|**nvarchar(60)**|할당 단위 유형에 대한 설명입니다.<br /><br /> IN_ROW_DATA<br /><br /> LOB_DATA<br /><br /> ROW_OVERFLOW_DATA<br /><br /> LOB_DATA 할당 단위에는 **text**, **ntext**, **image**, **varchar (max)**, **nvarchar (max**), **varbinary (max)** 및 **xml**형식의 열에 저장 되는 데이터가 포함 됩니다. 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.<br /><br /> ROW_OVERFLOW_DATA 할당 단위에는 **varchar (n)**, **nvarchar (n)**, **varbinary (n)** 및 **sql_variant** 행 외부로 푸시된 데이터 형식의 열에 저장 된 데이터가 포함 됩니다.|  
|index_depth|**tinyint**|인덱스 수준의 수입니다.<br /><br /> 1 = 힙 또는 LOB_DATA나 ROW_OVERFLOW_DATA 할당 단위|  
|index_level|**tinyint**|인덱스의 현재 수준입니다.<br /><br /> 인덱스 리프 수준, 힙 및 LOB_DATA 또는 ROW_OVERFLOW_DATA 할당 단위에 대해 0입니다.<br /><br /> 리프가 아닌 인덱스 수준의 경우 0보다 큽니다. *index_level* 은 인덱스의 루트 수준에서 가장 높습니다.<br /><br /> 리프가 아닌 인덱스 수준은 *mode* = DETAILED 인 경우에만 처리 됩니다.|  
|avg_fragmentation_in_percent|**float**|인덱스의 논리적 조각화 또는 IN_ROW_DATA 할당 단위에서 힙의 익스텐트 조각화입니다.<br /><br /> 값은 여러 파일을 고려하여 백분율로 측정됩니다. 논리적 조각화 및 익스텐트 조각화에 대한 정의는 주의를 참조하세요.<br /><br /> LOB_DATA 및 ROW_OVERFLOW_DATA 할당 단위에 대해 0입니다.<br /><br /> *Mode* = 샘플링 된 경우 힙의 경우 NULL입니다.|  
|fragment_count|**bigint**|IN_ROW_DATA 할당 단위의 리프 수준에 있는 조각 수입니다. 조각에 대한 자세한 내용은 주의를 참조하세요.<br /><br /> 리프가 아닌 인덱스 수준과 LOB_DATA 또는 ROW_OVERFLOW_DATA 할당 단위에 대해 NULL입니다.<br /><br /> *Mode* = 샘플링 된 경우 힙의 경우 NULL입니다.|  
|avg_fragment_size_in_pages|**float**|IN_ROW_DATA 할당 단위의 리프 수준에 있는 조각 하나의 평균 페이지 수입니다.<br /><br /> 리프가 아닌 인덱스 수준과 LOB_DATA 또는 ROW_OVERFLOW_DATA 할당 단위에 대해 NULL입니다.<br /><br /> *Mode* = 샘플링 된 경우 힙의 경우 NULL입니다.|  
|page_count|**bigint**|전체 인덱스 또는 데이터 페이지 수입니다.<br /><br /> 인덱스의 경우 IN_ROW_DATA 할당 단위에서 B-트리의 현재 수준에 있는 총 인덱스 페이지 수입니다.<br /><br /> 힙의 경우 IN_ROW_DATA 할당 단위에서 총 데이터 페이지 수입니다.<br /><br /> LOB_DATA 또는 ROW_OVERFLOW_DATA 할당 단위의 경우 할당 단위에서 총 페이지 수입니다.|  
|avg_page_space_used_in_percent|**float**|모든 페이지에서 사용되는 사용 가능한 데이터 스토리지 공간의 평균 백분율입니다.<br /><br /> 인덱스의 경우 IN_ROW_DATA 할당 단위에서 B-트리의 현재 수준에 평균이 적용됩니다.<br /><br /> 힙의 경우 IN_ROW_DATA 할당 단위에서 모든 데이터 페이지의 평균입니다.<br /><br /> LOB_DATA 또는 ROW_OVERFLOW DATA 할당 단위의 경우 할당 단위에서 모든 페이지의 평균입니다.<br /><br /> *Mode* =가 제한 된 경우 NULL입니다.|  
|record_count|**bigint**|총 레코드 수입니다.<br /><br /> 인덱스의 경우 IN_ROW_DATA 할당 단위에서 B-트리의 현재 수준에 총 레코드 수가 적용됩니다.<br /><br /> 힙의 경우 IN_ROW_DATA 할당 단위에서 총 레코드 수입니다.<br /><br /> **참고:** 힙의 경우이 함수에서 반환 된 레코드 수는 힙에 대해 SELECT COUNT ()를 실행 하 여 반환 되는 행 수와 일치 하지 않을 수 있습니다 \* . 이것은 한 행에 여러 레코드가 있기 때문입니다. 예를 들어 특정 업데이트 상황에서 업데이트 작업으로 인해 단일 힙 행에 한 개의 전달되고 있는 레코드와 한 개의 전달된 레코드가 있을 수 있습니다. 또한 가장 큰 LOB 행이 LOB_DATA 스토리지에서 여러 레코드로 분할됩니다.<br /><br /> LOB_DATA 또는 ROW_OVERFLOW_DATA 할당 단위의 경우 전체 할당 단위에서 총 레코드 수입니다.<br /><br /> *Mode* =가 제한 된 경우 NULL입니다.|  
|ghost_record_count|**bigint**|할당 단위에서 삭제할 레코드 정리 태스크에 의해 제거될 삭제할 레코드 수입니다.<br /><br /> IN_ROW_DATA 할당 단위에서 리프가 아닌 인덱스 수준에 대해 0입니다.<br /><br /> *Mode* =가 제한 된 경우 NULL입니다.|  
|version_ghost_record_count|**bigint**|할당 단위에서 처리 중인 스냅샷 격리 트랜잭션이 보유하고 있는 삭제할 레코드 수입니다.<br /><br /> IN_ROW_DATA 할당 단위에서 리프가 아닌 인덱스 수준에 대해 0입니다.<br /><br /> *Mode* =가 제한 된 경우 NULL입니다.|  
|min_record_size_in_bytes|**int**|최소 레코드 크기(바이트)입니다.<br /><br /> 인덱스의 경우 IN_ROW_DATA 할당 단위에서 B-트리의 현재 수준에 최소 레코드 크기가 적용됩니다.<br /><br /> 힙의 경우 IN_ROW_DATA 할당 단위에서 최소 레코드 크기입니다.<br /><br /> LOB_DATA 또는 ROW_OVERFLOW_DATA 할당 단위의 경우 전체 할당 단위에서 최소 레코드 크기입니다.<br /><br /> *Mode* =가 제한 된 경우 NULL입니다.|  
|max_record_size_in_bytes|**int**|최대 레코드 크기(바이트)입니다.<br /><br /> 인덱스의 경우 IN_ROW_DATA 할당 단위에서 B-트리의 현재 수준에 최대 레코드 크기가 적용됩니다.<br /><br /> 힙의 경우 IN_ROW_DATA 할당 단위에서 최대 레코드 크기입니다.<br /><br /> LOB_DATA 또는 ROW_OVERFLOW_DATA 할당 단위의 경우 전체 할당 단위에서 최대 레코드 크기입니다.<br /><br /> *Mode* =가 제한 된 경우 NULL입니다.|  
|avg_record_size_in_bytes|**float**|평균 레코드 크기(바이트)입니다.<br /><br /> 인덱스의 경우 IN_ROW_DATA 할당 단위에서 B-트리의 현재 수준에 평균 레코드 크기가 적용됩니다.<br /><br /> 힙의 경우 IN_ROW_DATA 할당 단위에서 평균 레코드 크기입니다.<br /><br /> LOB_DATA 또는 ROW_OVERFLOW_DATA 할당 단위의 경우 전체 할당 단위에서 평균 레코드 크기입니다.<br /><br /> *Mode* =가 제한 된 경우 NULL입니다.|  
|forwarded_record_count|**bigint**|다른 데이터 위치로의 전달 포인터가 있는 힙의 레코드 수입니다. 이 상태는 업데이트하는 동안 원본 위치에 새 행을 저장할 공간이 충분하지 않은 경우에 발생합니다.<br /><br /> 힙의 IN_ROW_DATA 할당 단위 이외의 모든 할당 단위에 대해 NULL입니다.<br /><br /> *Mode* = 제한 된 경우 힙의 경우 NULL입니다.|  
|compressed_page_count|**bigint**|압축된 페이지 수입니다.<br /><br /> 힙의 경우 새로 할당된 페이지는 PAGE 압축되지 않습니다. 힙은 데이터를 대량으로 가져오거나 힙을 다시 작성하는 경우의 두 가지 특별한 조건에서 PAGE 압축됩니다. 일반적으로 페이지 할당을 발생시키는 DML 작업은 PAGE 압축되지 않습니다. compressed_page_count 값이 원하는 임계값보다 커지면 힙을 다시 작성하십시오.<br /><br /> 클러스터형 인덱스가 있는 테이블의 경우 compressed_page_count 값은 PAGE 압축의 효율성을 나타냅니다.|  
|hobt_id|bigint|Columnstore 인덱스의 경우에는 파티션에 대 한 내부 columnstore 데이터를 추적 하는 행 집합의 ID입니다. 행 집합은 데이터 힙 또는 이진 트리로 저장 됩니다. 부모 columnstore 인덱스와 동일한 인덱스 ID를 가집니다. 자세한 내용은 [internal_partitions &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)을 참조 하십시오.<br /><br /> If 인 경우 NULL <br /><br /> **적용 대상**: SQL Server 2016 이상, Azure SQL Database, Azure SQL Managed Instance|  
|column_store_delete_buffer_state|tinyint| 0 = NOT_APPLICABLE<br /><br /> 1 = OPEN<br /><br /> 2 = 드레이닝<br /><br /> 3 = 플러시<br /><br /> 4 = 사용 중지<br /><br /> 5 = 준비<br /><br />**적용 대상**: SQL Server 2016 이상, Azure SQL Database, Azure SQL Managed Instance|  
|column_store_delete_buff_state_desc|| 유효 하지 않음-부모 인덱스가 columnstore 인덱스가 아닙니다.<br /><br /> 열기-deleters 및 스캐너가이를 사용 합니다.<br /><br /> 드레이닝이 드레이닝 중입니다. 하지만 스캐너는이를 계속 사용 합니다.<br /><br /> 플러시-버퍼가 닫히고 버퍼의 행이 삭제 비트맵에 기록 됩니다.<br /><br /> 사용 중지-닫힌 삭제 버퍼의 행이 삭제 비트맵에 기록 되었지만 스캐너가 아직 사용 하 고 있기 때문에 버퍼가 잘렸습니다. 새 스캐너는 오픈 버퍼가 충분 하므로 사용 중지 버퍼를 사용할 필요가 없습니다.<br /><br /> 준비-이 삭제 버퍼를 사용할 준비가 되었습니다. <br /><br /> **적용 대상**: SQL Server 2016 이상, Azure SQL Database, Azure SQL Managed Instance|  
|version_record_count|**bigint**|이 인덱스에서 유지 관리 되는 행 버전 레코드의 수입니다.  이러한 행 버전은 [가속화 된 데이터베이스 복구](../../relational-databases/accelerated-database-recovery-concepts.md) 기능을 통해 유지 관리 됩니다. <br /><br /> [!INCLUDE[SQL2019](../../includes/applies-to-version/sqlserver2019.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] |  
|inrow_version_record_count|**bigint**|빠른 검색을 위해 데이터 행에 보관 된 ADR 버전 레코드 수입니다. <br /><br />  [!INCLUDE[SQL2019](../../includes/applies-to-version/sqlserver2019.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e|  
|inrow_diff_version_record_count|**bigint**| 기본 버전의 차이 형식으로 유지 된 ADR 버전 레코드의 수입니다. <br /><br /> [!INCLUDE[SQL2019](../../includes/applies-to-version/sqlserver2019.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|total_inrow_version_payload_size_in_bytes|**bigint**|이 인덱스에 대 한 행 내부 버전 레코드의 총 크기 (바이트)입니다. <br /><br /> [!INCLUDE[SQL2019](../../includes/applies-to-version/sqlserver2019.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|offrow_regular_version_record_count|**bigint**|원본 데이터 행 외부에 유지 되는 버전 레코드의 수입니다. <br /><br /> [!INCLUDE[SQL2019](../../includes/applies-to-version/sqlserver2019.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|offrow_long_term_version_record_count|**bigint**|장기 간주 되는 버전 레코드 수입니다. <br /><br /> [!INCLUDE[SQL2019](../../includes/applies-to-version/sqlserver2019.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] |  

## <a name="remarks"></a>설명  
 sys.dm_db_index_physical_stats 동적 관리 함수는 DBCC SHOWCONTIG 문을 대체합니다.  
  
## <a name="scanning-modes"></a>검색 모드  
 함수가 실행되는 모드에 따라 함수에 사용되는 통계 데이터를 가져오기 위해 수행하는 검색 수준이 결정됩니다. *모드* 는 제한 됨, 샘플링 됨 또는 자세히로 지정 됩니다. 함수는 테이블이나 인덱스의 지정한 파티션을 구성하는 할당 단위에 대해 페이지 체인을 탐색합니다. dm_db_index_physical_stats는 실행 되는 모드에 관계 없이 의도 공유 (IS) 테이블 잠금만 필요 합니다.  
  
 LIMITED 모드는 가장 빠른 모드이며 가장 적은 수의 페이지를 검색합니다. 인덱스의 경우 B-트리의 부모 수준 페이지만(즉, 리프 수준 이상의 페이지) 검색합니다. 힙의 경우 연결된 PFS 및 IAM 페이지가 검사되고 힙의 데이터 페이지는 LIMITED 모드로 검색됩니다.  
  
 LIMITED 모드를 사용하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 B-트리의 비-리프 페이지와 힙의 IAM 및 PFS 페이지만 검색하므로 compressed_page_count가 NULL입니다. 샘플링 모드를 사용 하 여 compressed_page_count에 대 한 예상 값을 가져오고 DETAILED 모드를 사용 하 여 compressed_page_count에 대 한 실제 값을 가져옵니다. SAMPLED 모드는 인덱스 또는 힙에서 모든 페이지의 1퍼센트 샘플을 기반으로 통계를 반환합니다. SAMPLED 모드의 결과는 대략적인 값으로 간주되어야 합니다. 인덱스나 힙의 페이지 수가 10,000개 미만이면 SAMPLED 대신 DETAILED 모드가 사용됩니다.  
  
 DETAILED 모드는 모든 페이지를 검색하여 전체 통계를 반환합니다.  
  
 LIMITED에서 DETAILED 모드의 순서로 각 모드에서 수행되는 작업이 더 많아지기 때문에 속도는 점점 더 느려집니다. 테이블 또는 인덱스의 크기나 조각화 수준을 빠르게 측정하려면 LIMITED 모드를 사용합니다. 이 모드가 가장 빠르게 실행되며 인덱스의 IN_ROW_DATA 할당 단위에서 리프가 아닌 각 수준에 대해서는 행을 반환하지 않습니다.  
  
## <a name="using-system-functions-to-specify-parameter-values"></a>시스템 함수를 사용하여 매개 변수 값 지정  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] [DB_ID](../../t-sql/functions/db-id-transact-sql.md) 및 [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md) 함수를 사용 하 여 *database_id* 및 *object_id* 매개 변수에 대 한 값을 지정할 수 있습니다. 그러나 이러한 함수에 유효하지 않은 값을 전달하면 의도하지 않은 결과가 발생할 수 있습니다. 존재하지 않거나 철자가 틀린 경우와 같이 데이터베이스 또는 개체 이름을 찾을 수 없는 경우에는 두 함수 모두 NULL을 반환합니다. sys.dm_db_index_physical_stats 함수는 NULL을 모든 데이터베이스나 모든 개체를 지정하는 와일드카드 값으로 해석합니다.  
  
 또한 OBJECT_ID 함수는 dm_db_index_physical_stats 함수가 호출 되기 전에 처리 되므로 *database_id*에 지정 된 데이터베이스가 아니라 현재 데이터베이스의 컨텍스트에서 평가 됩니다. 이 동작으로 인해 OBJECT_ID 함수에서 NULL 값이 반환될 수 있습니다. 또는 개체 이름이 현재 데이터베이스 컨텍스트와 지정된 데이터베이스 둘 다에 있는 경우에는 오류 메시지가 반환될 수도 있습니다. 다음 예에서는 의도되지 않은 이러한 결과를 보여 줍니다.  
  
```  
USE master;  
GO  
-- In this example, OBJECT_ID is evaluated in the context of the master database.   
-- Because Person.Address does not exist in master, the function returns NULL.  
-- When NULL is specified as an object_id, all objects in the database are returned.  
-- The same results are returned when an object that is not valid is specified.  
SELECT * FROM sys.dm_db_index_physical_stats  
    (DB_ID(N'AdventureWorks'), OBJECT_ID(N'Person.Address'), NULL, NULL , 'DETAILED');  
GO  
-- This example demonstrates the results of specifying a valid object name  
-- that exists in both the current database context and  
-- in the database specified in the database_id parameter of the   
-- sys.dm_db_index_physical_stats function.  
-- An error is returned because the ID value returned by OBJECT_ID does not  
-- match the ID value of the object in the specified database.  
CREATE DATABASE Test;  
GO  
USE Test;  
GO  
CREATE SCHEMA Person;  
GO  
CREATE Table Person.Address(c1 int);  
GO  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_index_physical_stats  
    (DB_ID(N'Test'), OBJECT_ID(N'Person.Address'), NULL, NULL , 'DETAILED');  
GO  
-- Clean up temporary database.  
DROP DATABASE Test;  
GO  
```  
  
### <a name="best-practice"></a>모범 사례  
 DB_ID 또는 OBJECT_ID를 사용할 때는 항상 유효한 ID가 반환되는지 확인합니다. 예를 들어 OBJECT_ID를 사용 하는 경우와 같은 세 부분으로 구성 된 이름을 지정 `OBJECT_ID(N'AdventureWorks2012.Person.Address')` 하거나 함수에서 반환 된 값을 테스트 하 여 dm_db_index_physical_stats 함수에서 사용 합니다. 뒤에 나오는 예 1과 2에서는 데이터베이스와 개체 ID를 안전하게 지정하는 방법을 보여 줍니다.  
  
## <a name="detecting-fragmentation"></a>조각화 검색  
 조각화는 테이블, 즉 테이블에 정의된 인덱스에 대한 데이터 수정 작업(INSERT, UPDATE 및 DELETE 문)을 처리할 때 발생합니다. 이러한 수정 사항은 테이블 및 인덱스의 행에서 균등하게 분산되지 않으므로 각 페이지의 사용률이 시간에 따라 달라지게 됩니다. 테이블의 인덱스 일부 또는 전부를 검색하는 쿼리의 경우 이런 테이블 조각화로 인해 읽어야 하는 페이지의 수가 늘어날 수 있으며 이는 데이터의 병렬 검색에 방해가 됩니다.  
  
 인덱스 또는 힙의 조각화 수준은 avg_fragmentation_in_percent 열에 표시됩니다. 힙의 경우 이 값은 힙의 익스텐트 조각화를 나타냅니다. 인덱스의 경우 이 값은 인덱스의 논리적 조각화를 나타냅니다. DBCC SHOWCONTIG와는 달리 두 경우 모두 조각화 계산 알고리즘에 따라 여러 파일에 걸쳐 있는 스토리지가 고려되므로 결과가 정확합니다.  
  
 **논리적 조각화**  
  
 인덱스의 리프 페이지에서 순서가 잘못된 페이지의 비율입니다. 순서가 잘못된 페이지란 인덱스에 할당된 다음 물리적 페이지가 현재 리프 페이지의 다음 페이지  포인터가 가리키는 페이지와 다른 경우를 나타냅니다.  
  
 **익스텐트 조각화**  
  
 힙의 리프 페이지에서 순서가 잘못된 익스텐트의 비율입니다. 순서가 잘못된 익스텐트란 힙의 현재 페이지가 들어 있는 익스텐트가 실제로 이전 페이지가 들어 있는 익스텐트의 다음 익스텐트가 아닌 경우입니다.  
  
 최상의 성능을 얻기 위해서는 avg_fragmentation_in_percent 값이 0에 가까워야 하지만 대개 0~10%의 값이면 적당합니다. 다시 작성, 다시 구성 또는 다시 만들기 등 조각화를 줄이기 위한 모든 방법을 통해 이 값을 줄일 수 있습니다. 인덱스의 조각화 수준을 분석 하는 방법에 대 한 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)을 참조 하세요.  
  
## <a name="reducing-fragmentation-in-an-index"></a>인덱스의 조각화 줄이기  
 인덱스의 조각화가 쿼리 성능에 영향을 미치는 경우 다음 세 방법 중 하나를 사용하여 조각화를 줄일 수 있습니다.  
  
-   클러스터형 인덱스를 삭제한 다음 다시 만듭니다.  
  
     클러스터형 인덱스를 다시 만들면 데이터가 재구성되어 완전한 데이터 페이지가 만들어집니다. 사용률 수준은 CREATE INDEX의 FILLFACTOR 옵션으로 구성할 수 있습니다. 이 방법의 단점은 삭제하거나 다시 만드는 동안 인덱스가 오프라인 상태라는 것과 작업의 원자성에 있습니다. 인덱스 생성이 중단되면 그 인덱스는 다시 생성되지 않습니다. 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
-   DBCC INDEXDEFRAG 대신 ALTER INDEX REORGANIZE를 사용하여 인덱스의 리프 수준 페이지를 논리적 순서로 다시 정렬합니다. 이 작업은 온라인 작업이므로 문이 실행 중일 때 인덱스를 사용할 수 있습니다. 또한 작업이 중단되더라도 이미 완료된 작업은 손실되지 않습니다. 이 방법의 단점은 데이터를 다시 구성하는 작업이 인덱스를 다시 작성하는 작업만큼 효과적이지 않다는 것과 통계가 업데이트되지 않는다는 것입니다.  
  
-   DBCC DBREINDEX 대신 ALTER INDEX REBUILD를 사용하여 인덱스를 온라인이나 오프라인 상태로 다시 작성합니다. 자세한 내용은 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요.  
  
 인덱스를 다시 구성하거나 작성하는 이유가 전적으로 조각화 때문만은 아닙니다. 조각화는 주로 인덱스 검색 중 페이지 미리 읽기 성능을 저하시킵니다. 이로 인해 응답 시간이 느려집니다. 조각화된 테이블이나 인덱스에 대한 쿼리 작업은 기본적으로 단일 조회이기 때문에 검색과 관련이 없는 경우에는 조각화를 제거하더라도 효과를 기대하기 어려울 수 있습니다.
  
> [!NOTE]  
>  축소 작업 중에 인덱스 일부나 전부가 이동한 경우 DBCC SHRINKFILE 또는 DBCC SHRINKDATABASE를 실행하면 조각화가 발생할 수 있습니다. 따라서 조각화를 제거하기 전에 축소 작업을 수행하세요.  
  
## <a name="reducing-fragmentation-in-a-heap"></a>힙의 조각화 줄이기  
 힙의 익스텐트 조각화를 줄이려면 테이블에 클러스터형 인덱스를 만든 다음 해당 인덱스를 삭제합니다. 이렇게 하면 클러스터형 인덱스를 만드는 동안 데이터가 다시 구성되고 데이터베이스에서 사용할 수 있는 공간의 분포를 고려하여 최적화됩니다. 그런 다음 클러스터형 인덱스를 삭제하여 힙을 다시 만들면 데이터가 이동하지 않고 최적의 분포를 유지합니다. 이러한 작업을 수행하는 방법은 [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) 및 [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)를 참조하십시오.  
  
> [!CAUTION]  
>  테이블에서 클러스터형 인덱스를 만들고 삭제 하면 해당 테이블의 모든 비클러스터형 인덱스가 두 번 다시 작성 됩니다.  
  
## <a name="compacting-large-object-data"></a>LOB 데이터 압축  
 기본적으로 ALTER INDEX REORGANIZE 문은 LOB(Large Object) 데이터가 들어 있는 페이지를 압축합니다. LOB 페이지는 비어 있는 경우에도 할당이 취소되지 않으므로 대량의 LOB 데이터를 삭제했거나 LOB 열을 제거한 경우 이 데이터를 압축하면 사용할 수 있는 디스크 공간이 늘어납니다.  
  
 지정한 클러스터형 인덱스를 다시 구성하면 클러스터형 인덱스에 포함된 모든 LOB 열이 압축됩니다. 비클러스터형 인덱스를 다시 구성하면 인덱스에서 키가 아닌(포괄) 열인 LOB 열이 모두 압축됩니다. 문에 ALL을 지정하면 지정한 테이블이나 뷰에 연결된 모든 인덱스가 다시 구성됩니다. 또한 클러스터형 인덱스, 기본 테이블 또는 포괄 열이 있는 비클러스터형 인덱스에 연결된 모든 LOB 열이 압축됩니다.  
  
## <a name="evaluating-disk-space-use"></a>디스크 공간 사용률 평가  
 avg_page_space_used_in_percent 열은 페이지 사용률을 나타냅니다. 디스크 공간 사용을 최적화하려면 이 값이 임의로 삽입된 항목이 많지 않은 인덱스에 대해 100%에 가까워야 합니다. 그러나 임의 삽입이 많고 페이지 사용률이 매우 높은 인덱스에서는 페이지 분할의 횟수가 증가하므로 더 많은 조각이 생깁니다. 따라서 페이지 분할을 줄이려면 값이 100%보다 작아야 합니다. FILLFACTOR 옵션을 지정하여 인덱스를 다시 작성하면 인덱스에 대한 쿼리 패턴에 맞게 페이지 사용률을 변경할 수 있습니다. 채우기 비율에 대 한 자세한 내용은 [인덱스의 채우기 비율 지정](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)을 참조 하세요. 또한 ALTER INDEX REORGANIZE는 마지막으로 지정한 FILLFACTOR에 따라 페이지 채우기를 시도하여 인덱스를 압축하므로 avg_space_used_in_percent 값이 증가합니다. ALTER INDEX REORGANIZE는 페이지 사용률을 줄이지 않습니다. 페이지 사용률을 줄이려면 인덱스를 다시 작성해야 합니다.  
  
## <a name="evaluating-index-fragments"></a>인덱스 조각 평가  
 조각은 할당 단위에 대해 동일한 파일에서 물리적으로 연속되는 리프 페이지로 구성됩니다. 인덱스에는 적어도 하나의 조각이 있습니다. 인덱스에 포함할 수 있는 최대 조각 수는 인덱스의 리프 수준에 있는 페이지 수와 동일합니다. 동일한 수의 페이지의 경우 조각이 클수록 읽는 데 필요한 디스크 I/O는 줄어듭니다. 따라서 avg_fragment_size_in_pages 값이 클수록 범위 검색 성능이 좋아집니다. avg_fragment_size_in_pages 및 avg_fragmentation_in_percent 값은 서로 반비례합니다. 따라서 인덱스를 다시 작성하거나 다시 구성하면 조각화의 양은 줄어들고 조각 크기는 커집니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 클러스터형 columnstore 인덱스에 데이터를 반환하지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 다음 사용 권한이 필요합니다.  
  
-   데이터베이스 내의 지정된 개체에 대한 CONTROL 권한  
  
-   개체 와일드 카드 @*object_id*= NULL을 사용 하 여 지정 된 데이터베이스 내의 모든 개체에 대 한 정보를 반환 하는 VIEW DATABASE STATE 권한입니다.  
  
-   데이터베이스 와일드 카드 @*database_id* = NULL을 사용 하 여 모든 데이터베이스에 대 한 정보를 반환 하는 VIEW SERVER STATE 권한  
  
 VIEW DATABASE STATE를 허용하면 특정 개체에 대해 거부된 CONTROL 권한에 관계없이 데이터베이스의 모든 개체가 반환됩니다.  
  
 VIEW DATABASE STATE를 거부하면 특정 개체에 대해 허용된 CONTROL 권한에 관계없이 데이터베이스의 모든 개체가 반환되지 않습니다. 또한 데이터베이스 와일드 카드 @*database_id*= NULL을 지정 하면 데이터베이스가 생략 됩니다.  
  
 자세한 내용은 [동적 관리 뷰 및 함수 &#40;transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)를 참조 하세요.  
  
## <a name="examples"></a>예제  
  
### <a name="a-returning-information-about-a-specified-table"></a>A. 지정한 테이블에 대한 정보 반환  
 다음 예에서는 `Person.Address` 테이블의 모든 인덱스와 파티션에 대한 크기 및 조각화 통계를 반환합니다. 최대한의 성능을 발휘하고 반환되는 통계를 제한하기 위해 검색 모드를 `'LIMITED'`로 설정합니다. 이 쿼리를 실행하려면 최소한 `Person.Address` 테이블에 대한 CONTROL  권한이 필요합니다.  
  
```  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
  
IF @db_id IS NULL  
BEGIN;  
    PRINT N'Invalid database';  
END;  
ELSE IF @object_id IS NULL  
BEGIN;  
    PRINT N'Invalid object';  
END;  
ELSE  
BEGIN;  
    SELECT * FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'LIMITED');  
END;  
GO  
  
```  
  
### <a name="b-returning-information-about-a-heap"></a>B. 힙에 대한 정보 반환  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `dbo.DatabaseLog` 힙에 대한 모든 통계를 반환합니다. 테이블에 LOB  데이터가 들어 있으므로 `LOB_DATA` 할당 단위에 대한 행이 반환되고 힙의 데이터 페이지를 저장하는 `IN_ROW_ALLOCATION_UNIT`에 대한 행도 반환됩니다. 이 쿼리를 실행하려면 최소한 `dbo.DatabaseLog` 테이블에 대한 CONTROL  권한이 필요합니다.  
  
```  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.DatabaseLog');  
IF @object_id IS NULL   
BEGIN;  
    PRINT N'Invalid object';  
END;  
ELSE  
BEGIN;  
    SELECT * FROM sys.dm_db_index_physical_stats(@db_id, @object_id, 0, NULL , 'DETAILED');  
END;  
GO  
  
```  
  
### <a name="c-returning-information-for-all-databases"></a>C. 모든 데이터베이스에 대한 정보 반환  
 다음 예에서는 모든 매개 변수에 와일드카드인 `NULL`을 지정하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내의 모든 테이블과 인덱스에 대한 모든 통계를 반환합니다. 이 쿼리를 실행하려면 VIEW SERVER STATE 권한이 필요합니다.  
  
```  
SELECT * FROM sys.dm_db_index_physical_stats (NULL, NULL, NULL, NULL, NULL);  
GO  
  
```  
  
### <a name="d-using-sysdm_db_index_physical_stats-in-a-script-to-rebuild-or-reorganize-indexes"></a>D. 스크립트에 sys.dm_db_index_physical_stats를 사용하여 인덱스를 다시 작성하거나 다시 구성  
 다음 예에서는 데이터베이스에서 평균 조각화가 10%를 넘는 모든 파티션을 자동으로 다시 구성하거나 다시 작성합니다. 이 쿼리를 실행하려면 VIEW DATABASE STATE 권한이 필요합니다. 이 예에서는 데이터베이스 이름을 지정하지 않고 `DB_ID`를 첫 번째 매개 변수로 지정합니다. 현재 데이터베이스의 호환성 수준이 80 이하이면 오류가 발생합니다. 오류를 해결하려면 `DB_ID()`를 올바른 데이터베이스 이름으로 대체합니다. 데이터베이스 호환성 수준에 대 한 자세한 내용은 [ALTER Database Compatibility Level &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)를 참조 하세요.  
  
```  
-- Ensure a USE <databasename> statement has been executed first.  
SET NOCOUNT ON;  
DECLARE @objectid int;  
DECLARE @indexid int;  
DECLARE @partitioncount bigint;  
DECLARE @schemaname nvarchar(130);   
DECLARE @objectname nvarchar(130);   
DECLARE @indexname nvarchar(130);   
DECLARE @partitionnum bigint;  
DECLARE @partitions bigint;  
DECLARE @frag float;  
DECLARE @command nvarchar(4000);   
-- Conditionally select tables and indexes from the sys.dm_db_index_physical_stats function   
-- and convert object and index IDs to names.  
SELECT  
    object_id AS objectid,  
    index_id AS indexid,  
    partition_number AS partitionnum,  
    avg_fragmentation_in_percent AS frag  
INTO #work_to_do  
FROM sys.dm_db_index_physical_stats (DB_ID(), NULL, NULL , NULL, 'LIMITED')  
WHERE avg_fragmentation_in_percent > 10.0 AND index_id > 0;  
  
-- Declare the cursor for the list of partitions to be processed.  
DECLARE partitions CURSOR FOR SELECT * FROM #work_to_do;  
  
-- Open the cursor.  
OPEN partitions;  
  
-- Loop through the partitions.  
WHILE (1=1)  
    BEGIN;  
        FETCH NEXT  
           FROM partitions  
           INTO @objectid, @indexid, @partitionnum, @frag;  
        IF @@FETCH_STATUS < 0 BREAK;  
        SELECT @objectname = QUOTENAME(o.name), @schemaname = QUOTENAME(s.name)  
        FROM sys.objects AS o  
        JOIN sys.schemas as s ON s.schema_id = o.schema_id  
        WHERE o.object_id = @objectid;  
        SELECT @indexname = QUOTENAME(name)  
        FROM sys.indexes  
        WHERE  object_id = @objectid AND index_id = @indexid;  
        SELECT @partitioncount = count (*)  
        FROM sys.partitions  
        WHERE object_id = @objectid AND index_id = @indexid;  
  
-- 30 is an arbitrary decision point at which to switch between reorganizing and rebuilding.  
        IF @frag < 30.0  
            SET @command = N'ALTER INDEX ' + @indexname + N' ON ' + @schemaname + N'.' + @objectname + N' REORGANIZE';  
        IF @frag >= 30.0  
            SET @command = N'ALTER INDEX ' + @indexname + N' ON ' + @schemaname + N'.' + @objectname + N' REBUILD';  
        IF @partitioncount > 1  
            SET @command = @command + N' PARTITION=' + CAST(@partitionnum AS nvarchar(10));  
        EXEC (@command);  
        PRINT N'Executed: ' + @command;  
    END;  
  
-- Close and deallocate the cursor.  
CLOSE partitions;  
DEALLOCATE partitions;  
  
-- Drop the temporary table.  
DROP TABLE #work_to_do;  
GO  
  
```  
  
### <a name="e-using-sysdm_db_index_physical_stats-to-show-the-number-of-page-compressed-pages"></a>E. sys.dm_db_index_physical_stats를 사용하여 페이지 대 압축된 페이지 수 표시  
 다음 예에서는 행 및 페이지가 압축된 페이지에 대한 총 페이지 수를 표시하고 비교하는 방법을 보여 줍니다. 이 정보는 인덱스 또는 테이블 압축의 효과를 확인할 때 사용할 수 있습니다.  
  
```  
SELECT o.name,  
    ips.partition_number,  
    ips.index_type_desc,  
    ips.record_count, ips.avg_record_size_in_bytes,  
    ips.min_record_size_in_bytes,  
    ips.max_record_size_in_bytes,  
    ips.page_count, ips.compressed_page_count  
FROM sys.dm_db_index_physical_stats ( DB_ID(), NULL, NULL, NULL, 'DETAILED') ips  
JOIN sys.objects o on o.object_id = ips.object_id  
ORDER BY record_count DESC;  
```  
  
### <a name="f-using-sysdm_db_index_physical_stats-in-sampled-mode"></a>F. SAMPLED 모드에서 sys.dm_db_index_physical_stats 사용  
 다음 예에서는 SAMPLED 모드가 DETAILED 모드 결과와 다른 대략적인 값을 어떻게 반환하는지를 보여 줍니다.  
  
```  
CREATE TABLE t3 (col1 int PRIMARY KEY, col2 varchar(500)) WITH(DATA_COMPRESSION = PAGE);  
GO  
BEGIN TRAN  
DECLARE @idx int = 0;  
WHILE @idx < 1000000  
BEGIN  
    INSERT INTO t3 (col1, col2)   
    VALUES (@idx,   
    REPLICATE ('a', 100) + CAST (@idx as varchar(10)) + REPLICATE ('a', 380))  
    SET @idx = @idx + 1  
END  
COMMIT;  
GO  
SELECT page_count, compressed_page_count, forwarded_record_count, *   
FROM sys.dm_db_index_physical_stats (db_id(),   
    object_id ('t3'), null, null, 'SAMPLED');  
SELECT page_count, compressed_page_count, forwarded_record_count, *   
FROM sys.dm_db_index_physical_stats (db_id(),   
    object_id ('t3'), null, null, 'DETAILED');  
```  
  
### <a name="g-querying-service-broker-queues-for-index-fragmentation"></a>G. 인덱스 조각화를 위해 service broker 큐 쿼리  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]까지|  
  
 다음 예에서는 서버 broker 큐의 조각화를 쿼리 하는 방법을 보여 줍니다.  
  
```  
--Using queue internal table name   
select * from sys.dm_db_index_physical_stats (db_id(), object_id ('sys.queue_messages_549576996'), default, default, default)   
  
--Using queue name directly  
select * from sys.dm_db_index_physical_stats (db_id(), object_id ('ExpenseQueue'), default, default, default)  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [인덱스 관련 동적 관리 뷰 및 함수 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [dm_db_index_operational_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [dm_db_index_usage_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [dm_db_partition_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 뷰 ](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  

