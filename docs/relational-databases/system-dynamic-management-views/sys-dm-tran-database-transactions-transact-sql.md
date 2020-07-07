---
title: sys. dm_tran_database_transactions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_database_transactions
- sys.dm_tran_database_transactions_TSQL
- dm_tran_database_transactions_TSQL
- sys.dm_tran_database_transactions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_database_transactions dynamic management view
ms.assetid: 82a44295-4cbc-4a5b-891a-8ebaf307b8f5
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1e7e0f6716eeabaead05a8d980034474033b3e9b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86005212"
---
# <a name="sysdm_tran_database_transactions-transact-sql"></a>sys.dm_tran_database_transactions(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  데이터베이스 수준에서 트랜잭션에 대한 정보를 반환합니다.  
  
> [!NOTE]  
>  또는에서이 DMV를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_tran_database_transactions**를 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|transaction_id|**bigint**|데이터베이스 수준이 아닌 인스턴스 수준의 트랜잭션 ID입니다. 이 ID는 한 인스턴스 내의 모든 데이터베이스에서 고유하지만 모든 서버 인스턴스에서 고유하지는 않습니다.|  
|database_id|**int**|트랜잭션과 관련된 데이터베이스의 ID입니다.|  
|database_transaction_begin_time|**datetime**|트랜잭션에 데이터베이스가 관련된 시간입니다. 특히 트랜잭션에 대한 데이터베이스의 첫 번째 로그 레코드 시간입니다.|  
|database_transaction_type|**int**|1 = 읽기/쓰기 트랜잭션<br /><br /> 2 = 읽기 전용 트랜잭션<br /><br /> 3 = 시스템 트랜잭션|  
|database_transaction_state|**int**|1 = 트랜잭션이 초기화되지 않았습니다.<br /><br /> 3 = 트랜잭션이 초기화되었지만 로그 레코드를 생성하지 않았습니다.<br /><br /> 4 = 트랜잭션이 로그 레코드를 생성했습니다.<br /><br /> 5 = 트랜잭션이 준비되었습니다.<br /><br /> 10 = 트랜잭션을 커밋했습니다.<br /><br /> 11 = 트랜잭션을 롤백했습니다.<br /><br /> 12 = 트랜잭션을 커밋하고 있습니다. (로그 레코드가 생성 되 고 있지만 구체화 되거나 지속 되지 않았습니다.)|  
|database_transaction_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_status2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_log_record_count|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 데이터베이스에 생성된 트랜잭션의 로그 레코드 수입니다.|  
|database_transaction_replicate_record_count|**int**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 복제 된 트랜잭션에 대해 데이터베이스에 생성 된 로그 레코드 수입니다.|  
|database_transaction_log_bytes_used|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 지금까지 트랜잭션의 데이터베이스 로그에 사용된 바이트 수입니다.|  
|database_transaction_log_bytes_reserved|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 트랜잭션의 데이터베이스 로그에 사용하도록 예약된 바이트 수입니다.|  
|database_transaction_log_bytes_used_system|**int**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 지금까지 트랜잭션 대신 시스템 트랜잭션의 데이터베이스 로그에 사용된 바이트 수입니다.|  
|database_transaction_log_bytes_reserved_system|**int**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 트랜잭션 대신 시스템 트랜잭션의 데이터베이스 로그에 사용하도록 예약된 바이트 수입니다.|  
|database_transaction_begin_lsn|**numeric(25,0)**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 데이터베이스 로그에서 트랜잭션 시작 레코드의 LSN(로그 시퀀스 번호)입니다.|  
|database_transaction_last_lsn|**numeric(25,0)**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 데이터베이스 로그에서 가장 최근에 기록된 트랜잭션 레코드의 LSN입니다.|  
|database_transaction_most_recent_savepoint_lsn|**numeric(25,0)**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 데이터베이스 로그에서 가장 최근 트랜잭션 저장점의 LSN입니다.|  
|database_transaction_commit_lsn|**numeric(25,0)**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 데이터베이스 로그에서 트랜잭션 커밋 로그 레코드의 LSN입니다.|  
|database_transaction_last_rollback_lsn|**numeric(25,0)**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 가장 최근에 롤백된 LSN입니다. 롤백이 수행 되지 않은 경우 값은 MaxLSN입니다.|  
|database_transaction_next_undo_lsn|**numeric(25,0)**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 실행 취소할 다음 레코드의 LSN입니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   

## <a name="see-also"></a>참고 항목  
 [dm_tran_active_transactions &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-transactions-transact-sql.md)   
 [dm_tran_session_transactions &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)   
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [트랜잭션 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


