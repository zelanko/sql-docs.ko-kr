---
title: sys.dm_db_missing_index_group_stats (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_group_stats_TSQL
- sys.dm_db_missing_index_group_stats
- dm_db_missing_index_group_stats_TSQL
- dm_db_missing_index_group_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_group_stats dynamic management view
- missing indexes feature [SQL Server], sys.dm_db_missing_index_group_stats dynamic management view
ms.assetid: c2886986-9e07-44ea-a350-feeac05ee4f4
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4084fc2debabe8f8db90d350dc59f43995a58593
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmdbmissingindexgroupstats-transact-sql"></a>sys.dm_db_missing_index_group_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  공간 인덱스를 제외한 누락된 인덱스 그룹에 대한 요약 정보를 반환합니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이러한 정보 노출을 방지하기 위해 연결된 테넌트에 속하지 않는 데이터가 포함된 행은 모두 필터링됩니다.  
    
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**group_handle**|**int**|누락된 인덱스 그룹을 식별합니다. 이 식별자는 서버에서 고유합니다.<br /><br /> 다른 열은 그룹의 인덱스가 누락된 것으로 간주되는 모든 쿼리에 대한 정보를 제공합니다.<br /><br /> 인덱스 그룹에는 인덱스가 하나만 포함되어 있습니다.|  
|**unique_compiles**|**bigint**|이 누락된 인덱스 그룹에 적합한 컴파일 및 다시 컴파일 수입니다. 서로 다른 많은 쿼리의 컴파일 및 다시 컴파일이 이 열 값에 영향을 줄 수 있습니다.|  
|**user_seeks**|**bigint**|그룹의 권장 인덱스가 사용되었을 수 있는 사용자 쿼리에 의해 수행된 검색(Seek) 수입니다.|  
|**user_scans**|**bigint**|그룹의 권장 인덱스가 사용되었을 수 있는 사용자 쿼리에 의해 수행된 검색(Scan) 수입니다.|  
|**last_user_seek**|**datetime**|그룹의 권장 인덱스가 사용되었을 수 있는 사용자 쿼리에 의해 수행된 마지막 검색(Seek)의 날짜와 시간입니다.|  
|**last_user_scan**|**datetime**|날짜 및에 대 한 그룹의 권장된 인덱스가 사용 되었을 수 있는 사용자 쿼리에 의해 수행 된 마지막 검사 시간입니다.|  
|**avg_total_user_cost**|**float**|그룹의 인덱스로 줄일 수 있는 사용자 쿼리의 평균 비용입니다.|  
|**avg_user_impact**|**float**|누락된 인덱스 그룹을 구현할 경우 사용자 쿼리에서 얻을 수 있는 적합한 평균 백분율입니다. 즉, 이 누락된 인덱스 그룹을 구현할 경우 쿼리 비용이 평균적으로 이 백분율만큼 감소합니다.|  
|**system_seeks**|**bigint**|그룹의 권장 인덱스가 사용되었을 수 있는 auto stats 쿼리와 같은 시스템 쿼리에 의해 수행된 검색(Seek) 수입니다. 자세한 내용은 참조 [Auto Stats 이벤트 클래스](../../relational-databases/event-classes/auto-stats-event-class.md)합니다.|  
|**system_scans**|**bigint**|그룹의 권장 인덱스가 사용되었을 수 있는 시스템 쿼리에 의해 수행된 검색(Scan) 수입니다.|  
|**last_system_seek**|**datetime**|그룹의 권장 인덱스가 사용되었을 수 있는 시스템 쿼리에 의해 수행된 마지막 시스템 검색(Seek)의 날짜와 시간입니다.|  
|**last_system_scan**|**datetime**|그룹의 권장 인덱스가 사용되었을 수 있는 시스템 쿼리에 의해 수행된 마지막 시스템 검색(Scan)의 날짜와 시간입니다.|  
|**avg_total_system_cost**|**float**|그룹의 인덱스로 줄일 수 있는 시스템 쿼리의 평균 비용입니다.|  
|**avg_system_impact**|**float**|누락된 인덱스 그룹을 구현할 경우 시스템 쿼리에서 얻을 수 있는 적합한 평균 백분율입니다. 즉, 이 누락된 인덱스 그룹을 구현할 경우 쿼리 비용이 평균적으로 이 백분율만큼 감소합니다.|  
  
## <a name="remarks"></a>주의  
 반환 된 정보 **sys.dm_db_missing_index_group_stats** 모든 쿼리 실행에 의해 모든 쿼리 컴파일 또는 다시 업데이트 됩니다. 사용 통계는 지속되지 않으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작할 때까지만 유지됩니다. 서버 재활용 후에도 사용 통계를 유지하려면 데이터베이스 관리자가 정기적으로 누락된 인덱스 정보의 백업 복사본을 만들어야 합니다.  
  
## <a name="permissions"></a>Permissions  
 이 동적 관리 뷰를 쿼리하려면 사용자에게 VIEW SERVER STATE 권한이나 VIEW SERVER STATE 권한을 나타내는 사용 권한을 부여해야 합니다.  
  
## <a name="examples"></a>예  
 다음 예제는 사용 하는 방법을 설명 합니다.는 **sys.dm_db_missing_index_group_stats** 동적 관리 뷰.  
  
### <a name="a-find-the-10-missing-indexes-with-the-highest-anticipated-improvement-for-user-queries"></a>1. 사용자 쿼리 성능이 가장 많이 향상될 것으로 예상되는 누락된 인덱스 10개 찾기  
 다음 쿼리에서는 사용자 쿼리의 누적 성능이 가장 많이 향상될 것으로 예상되는 누락된 인덱스 10개를 내림차순으로 확인합니다.  
  
```  
SELECT TOP 10 *  
FROM sys.dm_db_missing_index_group_stats  
ORDER BY avg_total_user_cost * avg_user_impact * (user_seeks + user_scans)DESC;  
```  
  
### <a name="b-find-the-individual-missing-indexes-and-their-column-details-for-a-particular-missing-index-group"></a>2. 특정 누락된 인덱스 그룹의 개별 누락된 인덱스 및 해당 열 정보 찾기  
 다음 쿼리에서는 특정 누락된 인덱스 그룹을 구성하는 누락된 인덱스를 확인하고 해당 열 정보를 표시합니다. 이 예에서 누락된 인덱스 그룹 핸들은 24입니다.  
  
```  
SELECT migs.group_handle, mid.*  
FROM sys.dm_db_missing_index_group_stats AS migs  
INNER JOIN sys.dm_db_missing_index_groups AS mig  
    ON (migs.group_handle = mig.index_group_handle)  
INNER JOIN sys.dm_db_missing_index_details AS mid  
    ON (mig.index_handle = mid.index_handle)  
WHERE migs.group_handle = 24;  
```  
  
 이 쿼리는 인덱스가 누락된 데이터베이스, 스키마 및 테이블의 이름을 제공합니다. 또한 인덱스 키로 사용해야 하는 열의 이름을 제공합니다. CREATE INDEX DDL 문을 작성 누락 된 인덱스를 구현 하려면 같음 열을 먼저 나열 후 같지 않음 열 on에서 \< *table_name*> CREATE INDEX 문의 절. 포괄 열은 CREATE INDEX 문의 INCLUDE 절에 나열해야 합니다. 같음 열에 효율적인 순서를 결정하려면 선택도를 기준으로 열을 정렬합니다. 즉, 가장 많이 선택되는 열을 먼저 나열합니다(열 목록에서 맨 왼쪽).  
  
## <a name="see-also"></a>관련 항목:  
 [sys.dm_db_missing_index_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
  
