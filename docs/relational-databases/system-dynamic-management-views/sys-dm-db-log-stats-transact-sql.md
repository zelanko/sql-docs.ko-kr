---
title: sys.dm_db_log_stats (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 43e5b145122f5b2586d8eb976162afb0615f89d9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47846321"
---
# <a name="sysdmdblogstats-transact-sql"></a>sys.dm_db_log_stats (TRANSACT-SQL)   
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

데이터베이스의 트랜잭션 로그 파일에 요약 수준 특성 및 정보를 반환합니다. 모니터링 및 진단의 트랜잭션 로그 상태에 대 한이 정보를 사용 합니다.   
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>인수  

*database_id* | NULL | **DEFAULT**

데이터베이스의 ID입니다. `database_id`은 `int`입니다. 올바른 입력은 데이터베이스의 ID 번호 `NULL`, 또는 `DEFAULT`합니다. 기본값은 `NULL`입니다. `NULL` 및 `DEFAULT` 는 현재 데이터베이스의 컨텍스트에서 동등한 값입니다.  
기본 제공 함수 [DB_ID](../../t-sql/functions/db-id-transact-sql.md) 지정할 수 있습니다. 사용 하는 경우 `DB_ID` 데이터베이스 이름을 지정 하지 않고 현재 데이터베이스의 호환성 수준을 90 이상 이어야 합니다.

  
## <a name="tables-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |데이터베이스 ID |  
|recovery_model |**nvarchar(60)**   |   데이터베이스의 복구 모델입니다. 가능한 값은 다음과 같습니다. <br /> SIMPLE<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar(24)**   |   현재 시작 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 트랜잭션 로그에 있습니다.|  
|log_end_lsn    |**nvarchar(24)**   |   [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 트랜잭션 로그의 마지막 로그 레코드입니다.|  
|current_vlf_sequence_number    |**bigint** |   현재 [가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 실행 시 시퀀스 번호입니다.|  
|current_vlf_size_mb    |**float**  |   현재 [가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 크기 (mb)입니다.|   
|total_vlf_count    |**bigint** |   총 수 [가상 로그 파일 (Vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 트랜잭션 로그에 있습니다. |  
|total_log_size_mb  |**float**  |   총 트랜잭션 로그 크기 (mb)입니다. |  
|active_vlf_count   |**bigint** |   총 활성 [가상 로그 파일 (Vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 트랜잭션 로그에 있습니다.|  
|active_log_size_mb |**float**  |   총 활성 트랜잭션 로그 크기 (mb)입니다.|  
|log_truncation_holdup_reason   |**nvarchar(60)**   |   로그 잘림 느려지는 이유입니다. 값이 동일 `log_reuse_wait_desc` 열의 `sys.databases`합니다.  (이러한 값의 설명, 자세한 [트랜잭션 로그](../../relational-databases/logs/the-transaction-log-sql-server.md)). <br />가능한 값은 다음과 같습니다. <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />복제<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />기타 일시적 |  
|log_backup_time    |**datetime**   |   마지막 트랜잭션 로그 백업 시간입니다.|   
|log_backup_lsn |**nvarchar(24)**   |   마지막 트랜잭션 로그 백업 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)합니다.|   
|log_since_last_log_backup_mb   |**float**  |   마지막 트랜잭션 로그 백업 이후 로그 크기 (mb) [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)합니다.|  
|log_checkpoint_lsn |**nvarchar(24)**   |   마지막 검사점 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)합니다.|  
|log_since_last_checkpoint_mb   |**float**  |   로그 크기 (mb) 마지막 검사점 이후 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)합니다.|  
|log_recovery_lsn   |**nvarchar(24)**   |   복구 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 데이터베이스입니다. 하는 경우 `log_recovery_lsn` 검사점 LSN 되기 전에 발생 `log_recovery_lsn` 그렇지 않으면 가장 오래 된 활성 트랜잭션 LSN는 `log_recovery_lsn` 는 검사점 LSN입니다.|  
|log_recovery_size_mb   |**float**  |   로그 크기 (mb) 로그 복구 이후 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)합니다.|  
|recovery_vlf_count |**bigint** |   총 수 [가상 로그 파일 (Vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 를 장애 조치 또는 서버 재시작 발생 한 경우 복구할 수 있습니다. |  


## <a name="remarks"></a>Remarks
실행 하는 경우 `sys.dm_db_log_stats` 보조 복제본으로 가용성 그룹에 참여 하는 데이터베이스에 대해 위에서 설명 하는 필드의 하위 집합만 반환 됩니다.  현재만 `database_id`하십시오 `recovery_model`, 및 `log_backup_time` 보조 데이터베이스에 대해 실행 하는 경우 반환 됩니다.   

## <a name="permissions"></a>사용 권한  
필요는 `VIEW DATABASE STATE` 데이터베이스의 권한입니다.   
  
## <a name="examples"></a>예  

### <a name="a-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-high-number-of-vlfs"></a>1. 데이터베이스를 결정 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 많은 Vlf 사용 하 여 인스턴스   
다음 쿼리는 로그 파일에 100 개가 넘는 Vlf 사용 하 여 데이터베이스를 반환합니다. 많은 Vlf 데이터베이스 시작, 복원 및 복구 시간에 영향을 줄 수입니다.

```sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-transaction-log-backups-older-than-4-hours"></a>2. 데이터베이스를 결정 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4 시간 보다 오래 된 트랜잭션 로그 백업 사용 하 여 인스턴스   
다음 쿼리는 인스턴스에서 데이터베이스에 대 한 마지막 로그 백업 시간을 결정합니다.

```sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>관련 항목  
[동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[데이터베이스 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
  
