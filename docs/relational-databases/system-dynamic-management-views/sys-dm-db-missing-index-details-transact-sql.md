---
description: sys.dm_db_missing_index_details(Transact-SQL)
title: sys. dm_db_missing_index_details (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f88249c10b9e6c58e1ae68b598cfb92a876bf56a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89518883"
---
# <a name="sysdm_db_missing_index_details-transact-sql"></a>sys.dm_db_missing_index_details(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  공간 인덱스를 제외하고 누락된 인덱스에 대한 자세한 정보를 반환합니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이 정보를 노출 하지 않도록 하기 위해 연결 된 테 넌 트에 속하지 않는 데이터를 포함 하는 모든 행이 필터링 됩니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**index_handle**|**int**|특정 누락된 인덱스를 식별합니다. 이 식별자는 서버에서 고유합니다. **index_handle** 은이 테이블의 키입니다.|  
|**database_id**|**smallint**|누락된 인덱스가 있는 테이블이 위치한 데이터베이스를 식별합니다.|  
|**object_id**|**int**|인덱스가 없는 테이블을 식별합니다.|  
|**equality_columns**|**nvarchar(4000)**|다음 형식의 같음 조건자에 적용되는 쉼표로 구분된 열 목록입니다.<br /><br /> *table. 열*  = *constant_value*|  
|**inequality_columns**|**nvarchar(4000)**|다음 형식의 같지 않음 조건자에 적용되는 쉼표로 구분된 열 목록입니다.<br /><br /> *table. 열*  >  *constant_value*<br /><br /> "="가 아닌 모든 비교 연산자는 같지 않음을 표시합니다.|  
|**included_columns**|**nvarchar(4000)**|쿼리에 대한 포함 열로서 필요한 쉼표로 구분된 열 목록입니다. 포괄 열 또는 포괄 열에 대 한 자세한 내용은 [포괄 열을 사용 하 여 인덱스 만들기](../../relational-databases/indexes/create-indexes-with-included-columns.md)를 참조 하세요.<br /><br /> 메모리 최적화 인덱스 (해시 및 메모리 최적화 비클러스터형)의 경우 **included_columns**를 무시 합니다. 테이블의 모든 열은 모든 메모리 최적화 인덱스에 포함됩니다.|  
|**statement**|**nvarchar(4000)**|인덱스가 없는 테이블의 이름입니다.|  
  
## <a name="remarks"></a>설명  
 **sys.dm_db_missing_index_details**에서 반환된 정보는 쿼리 최적화 프로그램이 쿼리를 최적화할 때 업데이트되며 지속되지 않습니다. 누락된 인덱스 정보는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작할 때까지만 유지됩니다. 서버 재활용 후에도 누락된 인덱스 정보를 유지하려면 데이터베이스 관리자가 정기적으로 누락된 인덱스 정보의 백업 복사본을 만들어야 합니다.  
  
 특정 누락된 인덱스가 속해 있는 누락된 인덱스 그룹을 확인하려면 **index_handle** 열을 기준으로 **sys.dm_db_missing_index_details**와 동등 조인하여 **sys.dm_db_missing_index_groups** 동적 관리 뷰를 쿼리할 수 있습니다.  

  >[!NOTE]
  >이 DMV의 결과 집합은 600 개 행으로 제한 됩니다. 각 행에는 누락 된 인덱스가 하나 있습니다. 인덱스가 600 개를 초과 하는 경우 기존 누락 된 인덱스를 처리 하 여 최신 인덱스를 볼 수 있도록 해야 합니다. 
  
## <a name="using-missing-index-information-in-create-index-statements"></a>CREATE INDEX 문에서 누락된 인덱스 정보 사용  
 **Dm_db_missing_index_details** 에서 반환 되는 정보를 메모리 최적화 및 디스크 기반 인덱스 모두에 대 한 CREATE index 문으로 변환 하려면 같음 열 앞에 같음 열을 삽입 하 고이를 함께 사용 하 여 인덱스의 키를 만들어야 합니다. 또한 INCLUDE 절을 사용하여 CREATE INDEX 문에 포괄 열을 추가해야 합니다. 같음 열에 효율적인 순서를 결정하려면 선택도를 기준으로 열을 정렬합니다. 즉, 가장 많이 선택되는 열을 먼저 나열합니다(열 목록에서 맨 왼쪽).  
  
 메모리 최적화 인덱스에 대 한 자세한 내용은 메모리 액세스 [에 최적화 된 테이블에 대 한 인덱스](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)를 참조 하세요.  
  
## <a name="transaction-consistency"></a>트랜잭션 일관성  
 트랜잭션이 테이블을 만들거나 삭제하면 삭제된 개체에 대한 누락된 인덱스 정보가 포함된 행이 이 동적 관리 개체에서 제거되어 트랜잭션 일관성이 유지됩니다.  
  
## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   

## <a name="see-also"></a>참고 항목  
 [dm_db_missing_index_columns &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [dm_db_missing_index_groups &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [dm_db_missing_index_group_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
