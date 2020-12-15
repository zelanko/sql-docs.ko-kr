---
description: sys.dm_db_log_stats(Transact-SQL)
title: sys.dm_db_log_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_log_stats_TSQL
- sys.dm_db_log_stats
- sys.dm_db_log_stats_TSQL
- dm_db_log_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_stats dynamic management function
ms.assetid: ''
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5a5ea85a212e33a3e26ef295cc4d38c84967560a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472834"
---
# <a name="sysdm_db_log_stats-transact-sql"></a>sys.dm_db_log_stats(Transact-SQL)   
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

데이터베이스의 트랜잭션 로그 파일에 대 한 요약 수준 특성 및 정보를 반환 합니다. 이 정보를 사용 하 여 트랜잭션 로그 상태를 모니터링 하 고 진단 합니다.   
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>인수  

*database_id* | NULL | **기본값**

데이터베이스의 ID입니다. `database_id`이(가) `int`인 경우 유효한 입력은 데이터베이스의 ID 번호, `NULL` 또는 `DEFAULT` 입니다. 기본값은 `NULL`입니다. `NULL` 및 `DEFAULT` 는 현재 데이터베이스의 컨텍스트에서 동일한 값입니다.  
[DB_ID](../../t-sql/functions/db-id-transact-sql.md) 기본 제공 함수를 지정할 수 있습니다. `DB_ID`데이터베이스 이름을 지정 하지 않고를 사용 하는 경우 현재 데이터베이스의 호환성 수준은 90 이상 이어야 합니다.

  
## <a name="tables-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |데이터베이스 ID |  
|recovery_model |**nvarchar(60)**   |   데이터베이스의 복구 모델입니다. 가능한 값은 다음과 같습니다. <br /> SIMPLE<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar(24)**   |   트랜잭션 로그의 현재 시작 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 입니다.|  
|log_end_lsn    |**nvarchar(24)**   |   트랜잭션 로그에 있는 마지막 로그 레코드의 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 입니다.|  
|current_vlf_sequence_number    |**bigint** |   실행 시의 현재 [가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 시퀀스 번호입니다.|  
|current_vlf_size_mb    |**float**  |   현재 [가상 로그 파일 (VLF) 크기 (MB)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 입니다.|   
|total_vlf_count    |**bigint** |   트랜잭션 로그에서 [vlf (가상 로그 파일)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 의 총 수입니다. |  
|total_log_size_mb  |**float**  |   총 트랜잭션 로그 크기 (MB)입니다. |  
|active_vlf_count   |**bigint** |   트랜잭션 로그에서 활성 [가상 로그 파일 (vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 의 총 수입니다.|  
|active_log_size_mb |**float**  |   총 활성 트랜잭션 로그 크기 (MB)입니다.|  
|log_truncation_holdup_reason   |**nvarchar(60)**   |   로그 잘림 고정 이유. 값은  `log_reuse_wait_desc` 의 열과 같습니다 `sys.databases` .  이러한 값에 대 한 자세한 설명은 [트랜잭션 로그](../../relational-databases/logs/the-transaction-log-sql-server.md)를 참조 하세요. <br />가능한 값은 다음과 같습니다. <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />복제<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />기타 임시 |  
|log_backup_time    |**datetime**   |   마지막 트랜잭션 로그 백업 시간입니다.|   
|log_backup_lsn |**nvarchar(24)**   |   마지막 트랜잭션 로그 백업 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)입니다.|   
|log_since_last_log_backup_mb   |**float**  |   마지막 트랜잭션 로그 백업 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)이후 로그 크기 (MB)입니다.|  
|log_checkpoint_lsn |**nvarchar(24)**   |   마지막 검사점 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)입니다.|  
|log_since_last_checkpoint_mb   |**float**  |   마지막 검사점 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)이후 로그 크기 (MB)입니다.|  
|log_recovery_lsn   |**nvarchar(24)**   |   데이터베이스의 복구 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 입니다. `log_recovery_lsn`가 검사점 lsn 이전에 발생 하는 경우 `log_recovery_lsn` 은 가장 오래 된 활성 트랜잭션 LSN이 고, 그렇지 않으면 `log_recovery_lsn` 검사점 lsn입니다.|  
|log_recovery_size_mb   |**float**  |   로그 복구 [로그 시퀀스 번호 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)이후의 로그 크기 (MB)입니다.|  
|recovery_vlf_count |**bigint** |   장애 조치 (failover) 또는 서버를 다시 시작 하는 경우 복구할 [vlf (가상 로그 파일)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 의 총 수입니다. |  


## <a name="remarks"></a>설명
`sys.dm_db_log_stats`가용성 그룹에 보조 복제본으로 참여 하는 데이터베이스에 대해 실행 하는 경우 위에 설명 된 필드의 하위 집합만 반환 됩니다.  현재 `database_id` `recovery_model` `log_backup_time` 보조 데이터베이스에 대해 실행 되는 경우, 및만 반환 됩니다.   

## <a name="permissions"></a>사용 권한  
데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` .   
  
## <a name="examples"></a>예  

### <a name="a-determining-databases-in-a-ssnoversion-instance-with-high-number-of-vlfs"></a>A. Vlf 수가 많은 인스턴스에서 데이터베이스 확인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]   
다음 쿼리는 로그 파일에 100 개를 초과 하는 Vlf 데이터베이스를 반환 합니다. Vlf이 많으면 데이터베이스 시작, 복원 및 복구 시간에 영향을 줄 수 있습니다.

```sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-ssnoversion-instance-with-transaction-log-backups-older-than-4-hours"></a>B. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]트랜잭션 로그 백업이 4 시간 보다 오래 된 인스턴스에서 데이터베이스 확인   
다음 쿼리는 인스턴스의 데이터베이스에 대 한 마지막 로그 백업 시간을 결정 합니다.

```sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>참고 항목  
[동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
  
