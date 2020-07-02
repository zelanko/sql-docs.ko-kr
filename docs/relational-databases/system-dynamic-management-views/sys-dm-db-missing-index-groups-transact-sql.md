---
title: sys. dm_db_missing_index_groups (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_groups
- sys.dm_db_missing_index_groups_TSQL
- dm_db_missing_index_groups
- dm_db_missing_index_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_groups dynamic management view
- missing indexes feature [SQL Server], sys.dm_db_missing_index_groups dynamic management view
ms.assetid: 9cc00acd-d83d-49f8-be72-5b2aebed246b
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a5ca04c0774e639edb06edac4762ed6beeb7af58
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718810"
---
# <a name="sysdm_db_missing_index_groups-transact-sql"></a>sys.dm_db_missing_index_groups(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  이 DMV는 공간 인덱스를 제외 하 고 특정 인덱스 그룹에 누락 된 인덱스에 대 한 정보를 반환 합니다. 
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이 정보를 노출 하지 않도록 하기 위해 연결 된 테 넌 트에 속하지 않는 데이터를 포함 하는 모든 행이 필터링 됩니다.  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**index_group_handle**|**int**|누락된 인덱스 그룹을 식별합니다.|  
|**index_handle**|**int**|**index_group_handle**로 지정된 그룹에 속하는 누락된 인덱스를 식별합니다.<br /><br /> 인덱스 그룹에는 인덱스가 하나만 포함되어 있습니다.|  
  
## <a name="remarks"></a>설명  
 **sys.dm_db_missing_index_groups**에서 반환된 정보는 쿼리 최적화 프로그램이 쿼리를 최적화할 때 업데이트되며 지속되지 않습니다. 누락된 인덱스 정보는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작할 때까지만 유지됩니다. 서버 재활용 후에도 누락된 인덱스 정보를 유지하려면 데이터베이스 관리자가 정기적으로 누락된 인덱스 정보의 백업 복사본을 만들어야 합니다.  
  
 출력 결과 집합의 두 열은 키가 아니지만 함께 결합되어 인덱스 키를 형성합니다.  

  >[!NOTE]
  >이 DMV의 결과 집합은 600 개 행으로 제한 됩니다. 각 행에는 누락 된 인덱스가 하나 있습니다. 인덱스가 600 개를 초과 하는 경우 기존 누락 된 인덱스를 처리 하 여 최신 인덱스를 볼 수 있도록 해야 합니다.
  
## <a name="permissions"></a>사용 권한  
 이 동적 관리 뷰를 쿼리하려면 사용자에게 VIEW SERVER STATE 권한이나 VIEW SERVER STATE 권한을 나타내는 사용 권한을 부여해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [dm_db_missing_index_columns &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [dm_db_missing_index_details &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [dm_db_missing_index_group_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
