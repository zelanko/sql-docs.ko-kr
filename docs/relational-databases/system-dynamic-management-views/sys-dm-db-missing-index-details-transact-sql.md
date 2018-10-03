---
title: sys.dm_db_missing_index_details (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_details
- dm_db_missing_index_details
- sys.dm_db_missing_index_details_TSQL
- dm_db_missing_index_details_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- missing indexes feature [SQL Server], sys.dm_db_missing_index_details dynamic management view
- sys.dm_db_missing_index_details dynamic management view
ms.assetid: ced484ae-7c17-4613-a3f9-6d8aba65a110
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 35058af357c7ab702a39e07baac96fa1ee9a38f8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649011"
---
# <a name="sysdmdbmissingindexdetails-transact-sql"></a>sys.dm_db_missing_index_details(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  공간 인덱스를 제외하고 누락된 인덱스에 대한 자세한 정보를 반환합니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이러한 정보 노출을 방지하기 위해 연결된 테넌트에 속하지 않는 데이터가 포함된 행은 모두 필터링됩니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**index_handle**|**int**|특정 누락된 인덱스를 식별합니다. 이 식별자는 서버에서 고유합니다. **index_handle** 은이 테이블의 키입니다.|  
|**database_id**|**smallint**|누락된 인덱스가 있는 테이블이 위치한 데이터베이스를 식별합니다.|  
|**object_id**|**int**|인덱스가 없는 테이블을 식별합니다.|  
|**equality_columns**|**nvarchar(4000)**|다음 형식의 같음 조건자에 적용되는 쉼표로 구분된 열 목록입니다.<br /><br /> *table.column* =*constant_value*|  
|**inequality_columns**|**nvarchar(4000)**|다음 형식의 같지 않음 조건자에 적용되는 쉼표로 구분된 열 목록입니다.<br /><br /> *table.column* > *constant_value*<br /><br /> "="가 아닌 모든 비교 연산자는 같지 않음을 표시합니다.|  
|**included_columns**|**nvarchar(4000)**|쿼리에 대한 포함 열로서 필요한 쉼표로 구분된 열 목록입니다. 포함에 대 한 자세한 내용은 포함 된 열 참조 또는 [Create Indexes with Included](../../relational-databases/indexes/create-indexes-with-included-columns.md)합니다.<br /><br /> 메모리 최적화 인덱스에 대 한 (모두 해시 및 메모리 최적화 비클러스터형)를 무시 **included_columns**합니다. 테이블의 모든 열은 모든 메모리 최적화 인덱스에 포함됩니다.|  
|**statement**|**nvarchar(4000)**|인덱스가 없는 테이블의 이름입니다.|  
  
## <a name="remarks"></a>Remarks  
 반환 된 정보 **sys.dm_db_missing_index_details** 쿼리는 쿼리 최적화 프로그램이 쿼리 최적화 되 고 지속 되지 않습니다 때 업데이트 됩니다. 누락된 인덱스 정보는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작할 때까지만 유지됩니다. 서버 재활용 후에도 누락된 인덱스 정보를 유지하려면 데이터베이스 관리자가 정기적으로 누락된 인덱스 정보의 백업 복사본을 만들어야 합니다.  
  
 일부를 쿼리할 수는 누락 된 인덱스는 특정 누락 된 인덱스 그룹을 결정 하는 **sys.dm_db_missing_index_groups** 동등 조인 하 여 동적 관리 뷰 사용 하 여 **sys.dm_db_missing_index_details**  기준으로 합니다 **index_handle** 열입니다.  

  >[!NOTE]
  >이 DMV에 대 한 설정 하면 600 행으로 제한 됩니다. 각 행에 하나의 누락 된 인덱스를 포함 합니다. 누락 된 인덱스는 600 개 이상의 경우 새로운 기술을 볼 수 있도록 기존 누락 된 인덱스를 처리 해야 합니다. 
  
## <a name="using-missing-index-information-in-create-index-statements"></a>CREATE INDEX 문에서 누락된 인덱스 정보 사용  
 반환 된 정보를 변환할 **sys.dm_db_missing_index_details** 모두 메모리 최적화 테이블과 디스크 기반 인덱스에 대 한 CREATE INDEX 문으로, 같음 열 넣어야 같지 않음 열 앞과 함께 인덱스의 키를 구성 해야 합니다. 또한 INCLUDE 절을 사용하여 CREATE INDEX 문에 포괄 열을 추가해야 합니다. 같음 열에 효율적인 순서를 결정하려면 선택도를 기준으로 열을 정렬합니다. 즉, 가장 많이 선택되는 열을 먼저 나열합니다(열 목록에서 맨 왼쪽).  
  
 메모리 최적화 인덱스에 대 한 자세한 내용은 참조 하세요. [메모리 최적화 테이블에 대 한 인덱스](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)합니다.  
  
## <a name="transaction-consistency"></a>트랜잭션 일관성  
 트랜잭션이 테이블을 만들거나 삭제하면 삭제된 개체에 대한 누락된 인덱스 정보가 포함된 행이 이 동적 관리 개체에서 제거되어 트랜잭션 일관성이 유지됩니다.  
  
## <a name="permissions"></a>사용 권한

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   

## <a name="see-also"></a>관련 항목  
 [sys.dm_db_missing_index_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
