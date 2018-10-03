---
title: sys.dm_fts_index_population (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_population
- dm_fts_index_population
- sys.dm_fts_index_population_TSQL
- dm_fts_index_population_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_population dynamic management view
ms.assetid: 82d1c102-efcc-4b60-9a5e-3eee299bcb2b
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8119326d4e310eafbc82361594a65d35accb7fce
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618221"
---
# <a name="sysdmftsindexpopulation-transact-sql"></a>sys.dm_fts_index_population(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 현재 진행 중인 전체 텍스트 인덱스 및 의미 키 구 채우기에 대한 정보를 반환합니다.  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|채우기가 진행되고 있는 전체 텍스트 인덱스를 포함하는 데이터베이스의 ID입니다.|  
|**catalog_id**|**int**|이 전체 텍스트 인덱스를 포함하는 전체 텍스트 카탈로그의 ID입니다.|  
|**table_id**|**int**|전체 텍스트 인덱스가 채워지고 있는 테이블의 ID입니다.|  
|**memory_address**|**varbinary(8)**|활성 채우기를 나타내는 데 사용되는 내부 데이터 구조의 메모리 주소입니다.|  
|**population_type**|**int**|채우기 유형으로, 다음 중 하나일 수 있습니다.<br /><br /> 1 = 전체 채우기<br /><br /> 2 = 증분 타임스탬프 기반 채우기<br /><br /> 3 = 추적된 변경 내용의 수동 업데이트<br /><br /> 4 = 추적된 변경 내용의 백그라운드 업데이트|  
|**population_type_description**|**nvarchar(120)**|채우기 유형에 대한 설명입니다.|  
|**is_clustered_index_scan**|**bit**|채우기에 클러스터형 인덱스에 대한 스캔이 수반되는지 여부를 나타냅니다.|  
|**range_count**|**int**|이 채우기가 병렬 처리된 하위 범위 수입니다.|  
|**completed_range_count**|**int**|처리가 완료된 범위 수입니다.|  
|**outstanding_batch_count**|**int**|이 채우기에 대해 현재 처리 중인 일괄 처리 수입니다. 자세한 내용은 [sys.dm_fts_outstanding_batches &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)합니다.|  
|**상태**|**int**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 이 채우기의 상태입니다. 참고: 일부 상태는 일시적입니다. 다음 중 하나일 수 있습니다.<br /><br /> 3 = 시작 중<br /><br /> 5 = 정상적으로 처리 중<br /><br /> 7 = 처리가 중지됨<br /><br /> 예를 들어 자동 병합이 진행 중일 때 이 상태가 될 수 있습니다.<br /><br /> 11 = 채우기 중단됨<br /><br /> 12 = 의미 유사 추출 처리|  
|**status_description**|**nvarchar(120)**|채우기 상태에 대한 설명입니다.|  
|**completion_type**|**int**|이 채우기의 완료 상태입니다.|  
|**completion_type_description**|**nvarchar(120)**|완료 유형에 대한 설명입니다.|  
|**worker_count**|**int**|이 값은 항상 0입니다.|  
|**queued_population_type**|**int**|현재 채우기 다음에 실행될 채우기 유형으로, 추적된 변경 내용에 기반합니다(있는 경우).|  
|**queued_population_type_description**|**nvarchar(120)**|다음에 실행될 채우기에 대한 설명입니다(있는 경우). 예를 들어 CHANGE TRACKING = AUTO이고 초기 전체 채우기가 진행 중이면 이 열에 "자동 채우기"라고 표시됩니다.|  
|**start_time**|**datetime**|채우기가 시작된 시간입니다.|  
|**incremental_timestamp**|**timestamp**|전체 채우기의 시작 타임스탬프를 나타냅니다. 다른 모든 채우기 유형의 경우 이 값은 마지막으로 커밋된 검사점으로, 채우기의 진행 상태를 나타냅니다.|  
  
## <a name="remarks"></a>Remarks  
 전체 텍스트 인덱싱뿐 아니라 통계 의미 인덱싱을 사용하도록 설정하면 전체 텍스트 인덱싱에서 키 구의 의미 추출 및 채우기와 문서 유사 데이터의 추출이 동시에 발생합니다. 문서 유사 인덱스의 채우기는 나중에 두 번째 단계에서 발생합니다. 자세한 내용은 [관리 및 모니터링 의미 체계 검색](../../relational-databases/search/manage-and-monitor-semantic-search.md)합니다.  
  
## <a name="permissions"></a>사용 권한  

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   
  
## <a name="physical-joins"></a>물리적 조인  
 ![이 동적 관리 뷰의 유효 조인](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-index-population-1.gif "이 동적 관리 뷰의 유효 조인")  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|보낸 사람|수행할 작업|관계|  
|----------|--------|------------------|  
|dm_fts_active_catalogs.database_id|dm_fts_index_population.database_id|일 대 일|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|일 대 일|  
|dm_fts_population_ranges.parent_memory_address|dm_fts_index_population.memory_address|다 대 일|  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [전체 텍스트 검색 및 의미 체계 검색 동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

