---
title: sys.dm_db_missing_index_columns (Transact SQL) | Microsoft Docs
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
- dm_db_missing_index_columns_TSQL
- sys.dm_db_missing_index_columns_TSQL
- sys.dm_db_missing_index_columns
- dm_db_missing_index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_columns dynamic management function
- missing indexes feature [SQL Server], sys.dm_db_missing_index_columns dynamic management function
ms.assetid: 3b24e5ed-0c79-47e5-805c-a0902d0aeb86
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 568d909d993f3978c9b5f754b063d6357d51af8c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmdbmissingindexcolumns-transact-sql"></a>sys.dm_db_missing_index_columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  공간 인덱스를 제외하고 인덱스가 없는 데이터베이스 테이블 열에 대한 정보를 반환합니다. **sys.dm_db_missing_index_columns** 는 동적 관리 함수입니다.  

## <a name="syntax"></a>구문  
  
```  
  
sys.dm_db_missing_index_columns(index_handle)  
```  
  
## <a name="arguments"></a>인수  
 *index_handle*  
 누락된 인덱스를 고유하게 식별하는 정수로, 다음 동적 관리 개체로부터 얻을 수 있습니다.  
  
 [sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)  
  
 [sys.dm_db_missing_index_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|열의 ID입니다.|  
|**column_name**|**sysname**|테이블 열의 이름입니다.|  
|**column_usage**|**varchar(20)**|열이 쿼리에 사용되는 방법입니다. 가능한 값 및 해당 설명을 보려면은 합니다.<br /><br /> 동등 열 형식으로 같음을 표시 하는 조건자에 적용 됩니다.: <br />                        *table.column* = *constant_value*<br /><br /> 같지 않음: 열에 기여 같지 않음, 예를 들어 표시 하는 조건자 폼의 조건자: *열* > *상수 _ 값*합니다. "="가 아닌 모든 비교 연산자는 같지 않음을 표시합니다.<br /><br /> INCLUDE: 열을 사용 하지 않고 조건자를 계산 않고 쿼리를 포함 하 예를 들어 또 다른 이유로 사용 됩니다.|  
  
## <a name="remarks"></a>주의  
 반환 된 정보 **sys.dm_db_missing_index_columns** 쿼리는 쿼리 최적화 프로그램이 쿼리 최적화 되 고 지속 되지 않는 때 업데이트 됩니다. 누락된 인덱스 정보는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작할 때까지만 유지됩니다. 서버 재활용 후에도 누락된 인덱스 정보를 유지하려면 데이터베이스 관리자가 정기적으로 누락된 인덱스 정보의 백업 복사본을 만들어야 합니다.  
  
## <a name="transaction-consistency"></a>트랜잭션 일관성  
 트랜잭션이 테이블을 만들거나 삭제하면 삭제된 개체에 대한 누락된 인덱스 정보가 포함된 행이 이 동적 관리 개체에서 제거되어 트랜잭션 일관성이 유지됩니다.  
  
## <a name="permissions"></a>Permissions  
 이 동적 관리 함수를 쿼리하려면 사용자에게 VIEW SERVER STATE 권한이나 VIEW SERVER STATE 권한을 나타내는 사용 권한을 부여해야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Address` 테이블에 대한 쿼리를 실행한 다음 인덱스가 없는 테이블 열을 반환하도록 `sys.dm_db_missing_index_columns` 동적 관리 뷰를 사용하여 쿼리를 실행합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE StateProvinceID = 9;  
GO  
SELECT mig.*, statement AS table_name,  
    column_id, column_name, column_usage  
FROM sys.dm_db_missing_index_details AS mid  
CROSS APPLY sys.dm_db_missing_index_columns (mid.index_handle)  
INNER JOIN sys.dm_db_missing_index_groups AS mig ON mig.index_handle = mid.index_handle  
ORDER BY mig.index_group_handle, mig.index_handle, column_id;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
