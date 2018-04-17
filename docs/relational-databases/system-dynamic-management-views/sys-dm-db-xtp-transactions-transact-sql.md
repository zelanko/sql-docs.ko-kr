---
title: sys.dm_db_xtp_transactions (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_transactions
- sys.dm_db_xtp_transactions_TSQL
- dm_db_xtp_transactions
- dm_db_xtp_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_transactions dynamic management view
ms.assetid: 5c1a0a7a-e851-4b6f-8dfd-c9655fbf5a51
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7340cef4cd99e1645c9be6c8a09721c4f077d0fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbxtptransactions-transact-sql"></a>sys.dm_db_xtp_transactions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  메모리 OLTP 데이터베이스 엔진의 활성 트랜잭션을 보고합니다.  
  
 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
    
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|xtp_transaction_id|**bigint**|XTP 트랜잭션 관리자에서 이 트랜잭션의 내부 ID입니다.|  
|transaction_id|**bigint**|트랜잭션 ID입니다. sys.dm_tran_active_transactions 등의 다른 트랜잭션 관련 DMV에 있는 트랜잭션 ID와 조인합니다.<br /><br /> 고유하게 컴파일된 저장 프로시저에 의해 시작된 트랜잭션과 같은 XTP 전용 트랜잭션의 경우 0입니다.|  
|session_id|**smallint**|이 트랜잭션을 실행 중인 세션의 세션 식별자입니다. sys.dm_exec_sessions와 조인합니다.|  
|begin_tsn|**bigint**|트랜잭션의 트랜잭션 일련 번호를 시작합니다.|  
|end_tsn|**bigint**|트랜잭션의 트랜잭션 일련 번호를 종료합니다.|  
|state|**int**|트랜잭션의 상태입니다.<br /><br /> 0=ACTIVE<br /><br /> 1=COMMITTED<br /><br /> 2=ABORTED<br /><br /> 3=VALIDATING|  
|state_desc|**nvarchar**|트랜잭션 상태에 대한 설명입니다.|  
|result|**int**|이 트랜잭션의 결과입니다. 가능한 값은 다음과 같습니다.<br /><br /> 0 - IN PROGRESS<br /><br /> 1 - SUCCESS<br /><br /> 2 - ERROR<br /><br /> 3 - COMMIT DEPENDENCY<br /><br /> 4 - VALIDATION FAILED (RR)<br /><br /> 5 - VALIDATION FAILED (SR)<br /><br /> 6 - ROLLBACK|  
|result_desc|**nvarchar**|이 트랜잭션의 결과입니다. 가능한 값은 다음과 같습니다.<br /><br /> IN PROGRESS<br /><br /> SUCCESS<br /><br /> ERROR<br /><br /> COMMIT DEPENDENCY<br /><br /> VALIDATION FAILED (RR)<br /><br /> VALIDATION FAILED (SR)<br /><br /> ROLLBACK|  
|last_error|**int**|내부적으로만 사용됩니다.|  
|is_speculative|**bit**|내부적으로만 사용됩니다.|  
|is_prepared|**bit**|내부적으로만 사용됩니다.|  
|is_delayed_durability|**bit**|내부적으로만 사용됩니다.|  
|memory_address|**varbinary**|내부적으로만 사용됩니다.|  
|database_address|**varbinary**|내부적으로만 사용됩니다.|  
|thread_id|**int**|내부적으로만 사용됩니다.|  
|read_set_row_count|**int**|내부적으로만 사용됩니다.|  
|write_set_row_count|**int**|내부적으로만 사용됩니다.|  
|scan_set_count|**int**|내부적으로만 사용됩니다.|  
|savepoint_garbage_count|**int**|내부적으로만 사용됩니다.|  
|log_bytes_required|**bigint**|내부적으로만 사용됩니다.|  
|count_of_allocations|**int**|내부적으로만 사용됩니다.|  
|allocated_bytes|**int**|내부적으로만 사용됩니다.|  
|reserved_bytes|**int**|내부적으로만 사용됩니다.|  
|commit_dependency_count|**int**|내부적으로만 사용됩니다.|  
|commit_dependency_total_attempt_count|**int**|내부적으로만 사용됩니다.|  
|scan_area|**int**|내부적으로만 사용됩니다.|  
|scan_area_desc|**nvarchar**|내부적으로만 사용됩니다.|  
|scan_location|**int**|내부적으로만 사용됩니다.|  
|dependent_1_address|**varbinary(8)**|내부적으로만 사용됩니다.|  
|dependent_2_address|**varbinary(8)**|내부적으로만 사용됩니다.|  
|dependent_3_address|**varbinary(8)**|내부적으로만 사용됩니다.|  
|dependent_4_address|**varbinary(8)**|내부적으로만 사용됩니다.|  
|dependent_5_address|**varbinary(8)**|내부적으로만 사용됩니다.|  
|dependent_6_address|**varbinary(8)**|내부적으로만 사용됩니다.|  
|dependent_7_address|**varbinary(8)**|내부적으로만 사용됩니다.|  
|dependent_8_address|**varbinary(8)**|내부적으로만 사용됩니다.|  
  
## <a name="permissions"></a>Permissions  
 서버에 대한 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [메모리 액세스에 최적화 된 테이블 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
