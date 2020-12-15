---
description: sys.dm_fts_active_catalogs(Transact-SQL)
title: sys.dm_fts_active_catalogs (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_active_catalogs_TSQL
- dm_fts_active_catalogs
- dm_fts_active_catalogs_TSQL
- sys.dm_fts_active_catalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_active_catalogs dynamic management view
ms.assetid: 40ab5453-040c-4d2e-bb49-e340cf90c3ee
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6b557073c7ad5d9aaef7f90380bf80f6ba382901
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482734"
---
# <a name="sysdm_fts_active_catalogs-transact-sql"></a>sys.dm_fts_active_catalogs(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  서버에서 일부 채우기 작업이 진행 중인 전체 텍스트 카탈로그에 대한 정보를 반환합니다.  
  
> [!NOTE]
>  다음 열은의 이후 버전에서 제거 될 예정입니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . is_paused, previous_status, previous_status_description, row_count_in_thousands, 상태, status_description 및 worker_count. 향후 개발 작업에서는 이러한 열을 사용하지 않도록 하고 현재 이러한 열을 사용하는 애플리케이션은 수정하십시오.  
  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|활성 전체 텍스트 카탈로그를 포함하는 데이터베이스의 ID입니다.|  
|**catalog_id**|**int**|활성 전체 텍스트 카탈로그의 ID입니다.|  
|**memory_address**|**varbinary(8)**|이 전체 텍스트 카탈로그와 관련된 채우기 작업에 할당된 메모리 버퍼의 주소입니다.|  
|**name**|**nvarchar(128)**|활성 전체 텍스트 카탈로그의 이름입니다.|  
|**is_paused**|**bit**|활성 전체 텍스트 카탈로그 채우기가 일시 중지되었는지 나타냅니다.|  
|**status**|**int**|전체 텍스트 카탈로그의 현재 상태입니다. 다음 중 하나<br /><br /> 0 = 초기화하는 중입니다.<br /><br /> 1 = 준비되었습니다.<br /><br /> 2 = 일시 중지됨<br /><br /> 3 = 임시 오류입니다.<br /><br /> 4 = 다시 탑재해야 합니다.<br /><br /> 5 = 종료<br /><br /> 6 = 백업을 위해 정지되었습니다.<br /><br /> 7 = 카탈로그를 통해 백업이 완료되었습니다.<br /><br /> 8 = 카탈로그가 손상되었습니다.|  
|**status_description**|**nvarchar(120)**|활성 전체 텍스트 카탈로그의 현재 상태에 대한 설명입니다.|  
|**previous_status**|**int**|전체 텍스트 카탈로그의 이전 상태입니다. 다음 중 하나<br /><br /> 0 = 초기화하는 중입니다.<br /><br /> 1 = 준비되었습니다.<br /><br /> 2 = 일시 중지됨<br /><br /> 3 = 임시 오류입니다.<br /><br /> 4 = 다시 탑재해야 합니다.<br /><br /> 5 = 종료<br /><br /> 6 = 백업을 위해 정지되었습니다.<br /><br /> 7 = 카탈로그를 통해 백업이 완료되었습니다.<br /><br /> 8 = 카탈로그가 손상되었습니다.|  
|**previous_status_description**|**nvarchar(120)**|활성 전체 텍스트 카탈로그의 이전 상태에 대한 설명입니다.|  
|**worker_count**|**int**|이 전체 텍스트 카탈로그에서 현재 작동 중인 스레드 수입니다.|  
|**active_fts_index_count**|**int**|채울 전체 텍스트 인덱스 수입니다.|  
|**auto_population_count**|**int**|이 전체 텍스트 카탈로그에 대해 자동 채우기가 진행 중인 테이블 수입니다.|  
|**manual_population_count**|**int**|이 전체 텍스트 카탈로그에 대해 수동 채우기가 진행 중인 테이블 수입니다.|  
|**full_incremental_population_count**|**int**|이 전체 텍스트 카탈로그에 대해 전체 또는 증분 채우기가 진행 중인 테이블 수입니다.|  
|**row_count_in_thousands**|**int**|이 전체 텍스트 카탈로그의 모든 전체 텍스트 인덱스에 있을 것으로 예상된 행 수(천 단위)입니다.|  
|**is_importing**|**bit**|전체 텍스트 카탈로그를 가져올 것인지 여부를 나타냅니다.<br /><br /> 1 = 카탈로그를 가져옵니다.<br /><br /> 2 = 카탈로그를 가져오지 않습니다.|  
  
## <a name="remarks"></a>설명  
 Is_importing 열은의 새 열 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 입니다.  
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   
   
## <a name="physical-joins"></a>물리적 조인  
 ![이 동적 관리 뷰의 유효 조인](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-active-catalogs-1.gif "이 동적 관리 뷰의 유효 조인")  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|From|대상|관계|  
|----------|--------|------------------|  
|dm_fts_active_catalogs.database_id|dm_fts_index_population.database_id|일대일|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|일대일|  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 데이터베이스의 활성 전체 텍스트 카탈로그에 대한 정보를 반환합니다.  
  
```  
SELECT catalog.name, catalog.is_importing, catalog.auto_population_count,  
  OBJECT_NAME(population.table_id) AS table_name,  
  population.population_type_description, population.is_clustered_index_scan,  
  population.status_description, population.completion_type_description,  
  population.queued_population_type_description, population.start_time,  
  population.range_count   
FROM sys.dm_fts_active_catalogs catalog   
CROSS JOIN sys.dm_fts_index_population population   
WHERE catalog.database_id = population.database_id   
AND catalog.catalog_id = population.catalog_id   
AND catalog.database_id = (SELECT dbid FROM sys.sysdatabases WHERE name = DB_NAME());  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 
 [Transact-sql&#41;전체 텍스트 검색 및 의미 체계 검색 동적 관리 뷰 및 함수 &#40;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
