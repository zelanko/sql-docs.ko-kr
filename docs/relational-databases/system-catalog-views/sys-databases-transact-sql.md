---
title: sys.databases (TRANSACT-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- databases
- databases_TSQL
- sys.databases
- sys.databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.databases catalog view
ms.assetid: 46c288c1-3410-4d68-a027-3bbf33239289
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26be52ca8c8b1b004038923a9a7fe835eba52216
ms.sourcegitcommit: ccea98fa0768d01076cb6ffef0b4bdb221b2f9d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/13/2019
ms.locfileid: "65560129"
---
# <a name="sysdatabases-transact-sql"></a>sys.databases(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 각 데이터베이스당 한 개의 행을 포함합니다.  
  
데이터베이스가 없는 경우 `ONLINE`, 또는 `AUTO_CLOSE` 로 설정 된 `ON` 데이터베이스가 닫혀, 일부 열의 값 수와 `NULL`합니다. 데이터베이스는 `OFFLINE`, 해당 행 권한이 낮은 사용자에 게 표시 되지 않습니다. 데이터베이스가 있는 경우 해당 행을 보려면 `OFFLINE`, 사용자에 게 있어야 적어도 `ALTER ANY DATABASE` 서버 수준 사용 권한 또는 `CREATE DATABASE` 에 대 한 권한과 `master` 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 또는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 서버 내에서 고유한 데이터베이스 이름입니다.|  
|**database_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 또는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 서버 내에서 고유한 데이터베이스 ID입니다.|  
|**source_database_id**|**int**|NULL이 아닌 경우 = 이 데이터베이스 스냅숏의 원본 데이터베이스 ID입니다.<br /> NULL = 데이터베이스 스냅숏이 아닙니다.|  
|**owner_sid**|**varbinary(85)**|서버에 등록된 데이터베이스 외부 소유자의 SID(보안 ID)입니다. 데이터베이스를 소유할 수 있는 사용자에 대 한 내용은 참조는 **데이터베이스에 대 한 ALTER AUTHORIZATION** 부분 [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)합니다.|  
|**create_date**|**datetime**|데이터베이스가 작성되었거나 이름이 변경된 날짜입니다. 에 대 한 **tempdb**, 서버 다시 시작 될 때마다이 값을 변경 합니다.|  
|**compatibility_level**|**tinyint**|동작이 호환되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전에 해당하는 정수입니다.<br /> **값** &#124; **에 적용 됩니다**<br /> 70 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 80 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 90 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]<br /> 100 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 을 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 110 &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 을 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 120 &#124; [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 을 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 130 &#124; [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 140 &#124; [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] <br /> 150 &#124; [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]  |  
|**collation_name**|**sysname**|데이터베이스용 데이터 정렬입니다. 데이터베이스의 기본 데이터 정렬로 사용됩니다.<br /> NULL = 데이터베이스가 온라인이 아니거나 AUTO_CLOSE가 ON으로 설정되어 있고 데이터베이스가 닫혀 있습니다.|  
|**user_access**|**tinyint**|사용자 액세스 설정입니다.<br /> 0 = MULTI_USER로 지정됩니다.<br /> 1 = SINGLE_USER로 지정됩니다.<br /> 2 = RESTRICTED_USER로 지정됩니다.|  
|**user_access_desc**|**nvarchar(60)**|사용자 액세스 설정에 대한 설명입니다.|  
|**is_read_only**|**bit**|1 = 데이터베이스가 READ_ONLY입니다.<br /> 0 = 데이터베이스가 READ_WRITE입니다.|  
|**is_auto_close_on**|**bit**|1 = AUTO_CLOSE가 ON입니다.<br /> 0 = AUTO_CLOSE가 OFF입니다.|  
|**is_auto_shrink_on**|**bit**|1 = AUTO_SHRINK가 ON입니다.<br /> 0 = AUTO_SHRINK가 OFF입니다.|  
|**state**|**tinyint**|**값 &#124; 에 적용 됩니다**<br /> 0 = ONLINE <br /> 1 = RESTORING <br /> 2 = 복구 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 3 = RECOVERY_PENDING &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 4 = SUSPECT <br /> 5 EMERGENCY = &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 6 = 오프 라인 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 7 = 복사&AMP;#124; [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /> 10 = OFFLINE_SECONDARY &#124; [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /><br /> **참고:** Always On 데이터베이스에 대 한 쿼리를 `database_state` 나 `database_state_desc` 열의 [sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)합니다.|  
|**state_desc**|**nvarchar(60)**|데이터베이스 상태에 대한 설명입니다. 상태를 참조 하세요.|  
|**is_in_standby**|**bit**|데이터베이스가 로그 복원을 위해 읽기 전용 상태임을 나타냅니다.|  
|**is_cleanly_shutdown**|**bit**|1 = 데이터베이스가 올바르게 종료되었으므로 시작할 때 복구가 필요하지 않습니다.<br /> 0 = 데이터베이스가 올바르게 종료되지 않았으므로 시작할 때 복구가 필요합니다.|  
|**is_supplemental_logging_enabled**|**bit**|1 = SUPPLEMENTAL_LOGGING이 ON입니다.<br /> 0 = SUPPLEMENTAL_LOGGING이 OFF입니다.|  
|**snapshot_isolation_state**|**tinyint**|ALLOW_SNAPSHOT_ISOLATION 옵션으로 설정되는 허용된 스냅숏 격리 트랜잭션의 상태입니다.<br /> 0 = 스냅숏 격리 상태가 OFF입니다(기본값). 스냅숏 격리가 허용되지 않습니다.<br /> 1 = 스냅숏 격리 상태가 ON입니다. 스냅숏 격리가 허용됩니다.<br /> 2 = 스냅숏 격리 상태가 OFF로 전환 중입니다. 모든 트랜잭션에는 수정 사항이 버전별로 관리됩니다. 스냅숏 격리를 사용해 새 트랜잭션을 시작할 수 없습니다. ALTER DATABASE가 실행되었을 때 활성 상태인 모든 트랜잭션이 완료될 때까지 데이터베이스는 OFF로 전환 중인 상태를 유지합니다.<br /> 3 = 스냅숏 격리 상태가 ON으로 전환 중입니다. 새 트랜잭션에는 수정 사항이 버전별로 관리됩니다. 스냅숏 격리 상태가 1(ON)이 될 때까지 트랜잭션은 스냅숏 격리를 사용할 수 없습니다. ALTER DATABASE가 실행되었을 때 활성 상태인 모든 업데이트 트랜잭션이 완료될 때까지 데이터베이스는 ON으로 전환 중인 상태를 유지합니다.|  
|**snapshot_isolation_state_desc**|**nvarchar(60)**|ALLOW_SNAPSHOT_ISOLATION 옵션으로 설정되는 허용된 스냅숏 격리 트랜잭션의 상태에 대한 설명입니다.|  
|**is_read_committed_snapshot_on**|**bit**|1 = READ_COMMITTED_SNAPSHOT 옵션은 ON입니다. READ COMMITTED 격리 수준에서의 읽기 작업은 스냅숏 검색을 기반으로 하며 잠금을 획득하지 않습니다.<br /> 0 = READ_COMMITTED_SNAPSHOT 옵션은 OFF(기본값)입니다. READ COMMITTED 격리 수준에서의 읽기 작업은 공유 잠금을 사용합니다.|  
|**recovery_model**|**tinyint**|선택된 복구 모델입니다.<br /> 1 = FULL<br /> 2 = BULK_LOGGED<br /> 3 = SIMPLE|  
|**recovery_model_desc**|**nvarchar(60)**|선택된 복구 모델에 대한 설명입니다.|  
|**page_verify_option**|**tinyint**|PAGE_VERIFY 옵션 설정입니다.<br /> 0 = 없음<br /> 1 = TORN_PAGE_DETECTION<br /> 2 = CHECKSUM|  
|**page_verify_option_desc**|**nvarchar(60)**|PAGE_VERIFY 옵션 설정에 대한 설명입니다.|  
|**is_auto_create_stats_on**|**bit**|1 = AUTO_CREATE_STATISTICS가 ON입니다.<br /> 0 = AUTO_CREATE_STATISTICS가 OFF입니다.|  
|**is_auto_create_stats_incremental_on**|**bit**|자동 통계 증분 옵션의 기본 설정을 나타냅니다.<br /> 0 = 통계 자동 작성이 비증분입니다.<br /> 1 = 통계 자동 작성이 증분입니다(가능한 경우).<br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**is_auto_update_stats_on**|**bit**|1 = AUTO_UPDATE_STATISTICS가 ON입니다.<br /> 0 = AUTO_UPDATE_STATISTICS가 OFF입니다.|  
|**is_auto_update_stats_async_on**|**bit**|1 = AUTO_UPDATE_STATISTICS_ASYNC가 ON입니다.<br /> 0 = AUTO_UPDATE_STATISTICS_ASYNC가 OFF입니다.|  
|**is_ansi_null_default_on**|**bit**|1 = ANSI_NULL_DEFAULT가 ON입니다.<br /> 0 = ANSI_NULL_DEFAULT가 OFF입니다.|  
|**is_ansi_nulls_on**|**bit**|1 = ANSI_NULLS가 ON입니다.<br /> 0 = ANSI_NULLS가 OFF입니다.|  
|**is_ansi_padding_on**|**bit**|1 = ANSI_PADDING이 ON입니다.<br /> 0 = ANSI_PADDING이 OFF입니다.|  
|**is_ansi_warnings_on**|**bit**|1 = ANSI_WARNINGS가 ON입니다.<br /> 0 = ANSI_WARNINGS가 OFF입니다.|  
|**is_arithabort_on**|**bit**|1 = ARITHABORT가 ON입니다.<br /> 0 = ARITHABORT가 OFF입니다.|  
|**is_concat_null_yields_null_on**|**bit**|1 = CONCAT_NULL_YIELDS_NULL이 ON입니다.<br /> 0 = CONCAT_NULL_YIELDS_NULL이 OFF입니다.|  
|**is_numeric_roundabort_on**|**bit**|1 = NUMERIC_ROUNDABORT가 ON입니다.<br /> 0 = NUMERIC_ROUNDABORT가 OFF입니다.|  
|**is_quoted_identifier_on**|**bit**|1 = QUOTED_IDENTIFIER가 ON입니다.<br /> 0 = QUOTED_IDENTIFIER가 OFF입니다.|  
|**is_recursive_triggers_on**|**bit**|1 = RECURSIVE_TRIGGERS가 ON입니다.<br /> 0 = RECURSIVE_TRIGGERS가 OFF입니다.|  
|**is_cursor_close_on_commit_on**|**bit**|1 = CURSOR_CLOSE_ON_COMMIT이 ON입니다.<br /> 0 = CURSOR_CLOSE_ON_COMMIT이 OFF입니다.|  
|**is_local_cursor_default**|**bit**|1 = CURSOR_DEFAULT가 로컬입니다.<br /> 0 = CURSOR_DEFAULT가 전역입니다.|  
|**is_fulltext_enabled**|**bit**|1 = 데이터베이스에서 전체 텍스트를 사용할 수 있습니다.<br /> 0 = 데이터베이스에서 전체 텍스트를 사용할 수 없습니다.|  
|**is_trustworthy_on**|**bit**|1 = 데이터베이스가 신뢰할 수 있는 것으로 표시되어 있습니다.<br /> 0 = 데이터베이스가 신뢰할 수 있는 것으로 표시되지 않았습니다.|  
|**is_db_chaining_on**|**bit**|1 = 데이터베이스 간 소유권 체인이 ON 상태입니다.<br /> 0 = 데이터베이스 간 소유권 체인이 OFF 상태입니다.|  
|**is_parameterization_forced**|**bit**|1 = 매개 변수화가 FORCED로 설정되어 있습니다.<br /> 0 = 매개 변수화가 SIMPLE로 설정되어 있습니다.|  
|**is_master_key_encrypted_by_server**|**bit**|1 = 데이터베이스에 암호화된 마스터 키가 있습니다.<br /> 0 = 데이터베이스에 암호화된 마스터 키가 없습니다.|  
|**is_query_store_on**|**bit**|1 = 쿼리 저장소는이 데이터베이스에 대해 사용 하도록 설정 합니다. 확인할 [sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) 쿼리 저장소 상태를 볼 수 있습니다.<br /> 0 = 쿼리 저장소가 비활성화 되어<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).|  
|**is_published**|**bit**|1 = 데이터베이스가 트랜잭션 또는 스냅숏 복제 토폴로지에서 게시 데이터베이스입니다.<br /> 0 = 게시 데이터베이스가 아닙니다.|  
|**is_subscribed**|**bit**|이 열은 사용되지 않으며, 데이터베이스의 구독자 상태에 관계없이 항상 0을 반환합니다.|  
|**is_merge_published**|**bit**|1 = 데이터베이스가 병합 복제 토폴로지에서 게시 데이터베이스입니다.<br /> 0 = 병합 복제 토폴로지에서 게시 데이터베이스가 아닙니다.|  
|**is_distributor**|**bit**|1 = 데이터베이스가 복제 토폴로지용 배포 데이터베이스입니다.<br /> 0 = 복제 토폴로지용 배포 데이터베이스가 아닙니다.|  
|**is_sync_with_backup**|**bit**|1 = 데이터베이스가 백업과의 복제 동기화용으로 표시되어 있습니다.<br /> 0 = 백업과의 복제 동기화용으로 표시되어 있지 않습니다.|  
|**service_broker_guid**|**uniqueidentifier**|이 데이터베이스의 Service Broker ID입니다. 로 사용 합니다 **broker_instance** 라우팅 테이블에서 대상의 합니다.|  
|**is_broker_enabled**|**bit**|1 = 이 데이터베이스의 브로커가 현재 메시지를 주고받고 있습니다.<br /> 0 = 이 데이터베이스에서 보낸 모든 메시지는 전송 큐에서 대기하며 수신된 메시지는 큐에 배치되지 않습니다.<br /> 복원되거나 첨부된 데이터베이스의 경우 브로커를 사용하지 않도록 기본 설정됩니다. 단, 장애 조치(Failover) 후 브로커가 설정된 데이터베이스 미러링은 예외입니다.|  
|**log_reuse_wait**|**tinyint**|마지막 검사점으로 다음 중 하나에서 트랜잭션 로그 공간이 다시 사용 대기 중입니다. 이러한 값의 설명, 자세한 [트랜잭션 로그](../../relational-databases/logs/the-transaction-log-sql-server.md)합니다.<br /> **값 &#124; 에 적용 됩니다**<br /> 0 = 없음<br />   1 = 검사점 (데이터베이스 복구 모델을 사용 하 여 메모리 최적화 데이터 파일 그룹을 볼 수 있어야 하는 `log_reuse_wait` checkpoint 또는 xtp_checkpoint 열을 나타냅니다.) &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  2 = 로그 백업 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  3 = 활성 백업 또는 복원 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  4 = 활성 트랜잭션 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  5 = 데이터베이스 미러링 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  6 = 복제 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  7 = 데이터베이스 스냅숏 생성 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  8 = 로그 검색 <br />  9 =는 Always On 가용성 그룹 보조 복제본은 해당 보조 데이터베이스에이 데이터베이스의 트랜잭션 로그 레코드를 적용 합니다. &#124;[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  9 = 기타 (일시적) & amp;#124 까지의 등 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]<br />  10 = 내부용 으로만 사용에 대 한 &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  11 = 내부 전용 &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 12 = 내부 전용 &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />13 = 가장 오래 된 페이지 &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 14 = 기타 &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  16 = XTP_CHECKPOINT (데이터베이스 복구 모델을 사용 하 여 메모리 최적화 데이터 파일 그룹을 기대할 수 log_reuse_wait 열이 checkpoint 또는 xtp_checkpoint를.) &#124; [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**log_reuse_wait_desc**|**nvarchar(60)**|트랜잭션 로그 공간 다시 사용을 마지막 검사점을 기다리는지에 대한 설명입니다.|  
|**is_date_correlation_on**|**bit**|1 = DATE_CORRELATION_OPTIMIZATION이 ON입니다.<br /> 0 = DATE_CORRELATION_OPTIMIZATION이 OFF입니다.|  
|**is_cdc_enabled**|**bit**|1 = 데이터베이스에 변경 데이터 캡처가 설정되어 있습니다. 자세한 내용은 [sys.sp_cdc_enable_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md)합니다.|  
|**is_encrypted**|**bit**|데이터베이스 암호화 되는지 여부를 나타냅니다 (마지막으로 사용 하 여 설정 된 상태를 반영 합니다 `ALTER DATABASE SET ENCRYPTION` 절). 다음 값 중 하나입니다.<br /> 1 = 암호화됨<br /> 0 = 암호화되지 않음<br /> 데이터 암호화에 대한 자세한 내용은 [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하십시오.<br /> 데이터베이스를 해독 하는 중에 `is_encrypted` 0 값을 보여 줍니다. 사용 하 여 암호화 프로세스의 상태를 확인할 수는 [sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 동적 관리 뷰.|  
|**is_honor_broker_priority_on**|**bit**|데이터베이스는 대화 우선 순위를 인식 하는지 여부를 나타냅니다 (마지막으로 사용 하 여 설정 된 상태를 반영 합니다 `ALTER DATABASE SET HONOR_BROKER_PRIORITY` 절). 다음 값 중 하나입니다.<br /> 1 = HONOR_BROKER_PRIORITY가 ON입니다.<br /> 0 = HONOR_BROKER_PRIORITY가 OFF입니다.|  
|**replica_id**|**uniqueidentifier**|데이터베이스가 참여하는 가용성 그룹(있는 경우)의 로컬 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 가용성 복제본에 대한 고유 식별자입니다.<br /> NULL = 데이터베이스가 가용성 그룹에 포함된 가용성 복제본의 일부가 아닙니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**group_database_id**|**uniqueidentifier**|Always On 가용성 그룹, 데이터베이스 참여 하는 경우 내 데이터베이스의 고유 식별자입니다. **group_database_id** 주 복제본에서 가용성 그룹에 조인에 데이터베이스를 모든 보조 복제본이이 데이터베이스에 대해 동일 합니다.<br /> NULL = 데이터베이스가 가용성 그룹에 포함된 가용성 복제본의 일부가 아닙니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**resource_pool_id**|**int**|이 데이터베이스에 매핑되는 리소스 풀의 ID입니다. 이 리소스 풀은 이 데이터베이스에서 메모리 최적화 테이블을 사용할 수 있는 총 메모리를 제어합니다.<br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**default_language_lcid**|**smallint**|포함된 데이터베이스의 기본 언어에 대한 로컬 ID(lcid)를 나타냅니다.<br /> **참고:** 역할을 합니다 [default language 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) 의 `sp_configure`합니다. 이 값은 **null** 포함 되지 않은 데이터베이스에 대 한 합니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_language_name**|**nvarchar(128)**|포함된 데이터베이스의 기본 언어를 나타냅니다.<br /> 이 값은 **null** 포함 되지 않은 데이터베이스에 대 한 합니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_lcid**|**int**|포함된 된 데이터베이스의 기본 전체 텍스트 언어의 로캘 id (lcid)를 나타냅니다.<br /> **참고:** 기본값이 [기본 전체 텍스트 언어 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) 의 `sp_configure`합니다. 이 값은 **null** 포함 되지 않은 데이터베이스에 대 한 합니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_name**|**nvarchar(128)**|포함된 데이터베이스의 기본 전체 텍스트 언어를 나타냅니다.<br /> 이 값은 **null** 포함 되지 않은 데이터베이스에 대 한 합니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_nested_triggers_on**|**bit**|포함된 데이터베이스에서 중첩 트리거가 허용되는지 여부를 나타냅니다.<br /> 0 = 중첩 트리거가 허용되지 않습니다.<br /> 1 = 중첩 트리거가 허용됩니다.<br /> **참고:** 역할을 합니다 [nested triggers 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) 의 `sp_configure`합니다. 이 값은 **null** 포함 되지 않은 데이터베이스에 대 한 합니다. 참조 [sys.configurations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 대 한 자세한 내용은 합니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_transform_noise_words_on**|**bit**|포함된 데이터베이스에서 의미 없는 단어가 변환되는지 여부를 나타냅니다.<br /> 0 = 의미 없는 단어가 변환되지 않습니다.<br /> 1 = 의미 없는 단어가 변환됩니다.<br /> **참고:** 역할을 합니다 [transform noise words 서버 구성 옵션](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md) 의 `sp_configure`합니다. 이 값은 **null** 포함 되지 않은 데이터베이스에 대 한 합니다. 참조 [sys.configurations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 대 한 자세한 내용은 합니다.<br /> **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**two_digit_year_cutoff**|**smallint**|두 자리 연도를 네 자리 연도로 해석하기 위한 구분 연도를 나타내는 1753에서 9999까지의 숫자 값을 나타냅니다.<br /> **참고:** 역할을 합니다 [두 자리 연도 구성 cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) 의 `sp_configure`합니다. 이 값은 **null** 포함 되지 않은 데이터베이스에 대 한 합니다. 참조 [sys.configurations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 대 한 자세한 내용은 합니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**포함**|**null이 아닌 tinyint**|데이터베이스의 포함 상태를 나타냅니다.<br />  0 = 데이터베이스가 포함되지 않습니다. **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 1 = 데이터베이스가 부분적으로 포함에서 **적용할**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**containment_desc**|**nvarchar(60) not null**|데이터베이스의 포함 상태를 나타냅니다.<br /> NONE = 레거시 데이터베이스입니다(containment = 0).<br /> PARTIAL = 부분적으로 포함된 데이터베이스입니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**target_recovery_time_in_seconds**|**int**|데이터베이스 복구 예상 시간(초)입니다. Null을 허용합니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**delayed_durability**|**int**|지연 된 내구성 설정:<br /> 0 = DISABLED<br /> 1 = 허용<br /> 2 = FORCED<br /> 자세한 내용은 [트랜잭션 내구성 제어](../../relational-databases/logs/control-transaction-durability.md)를 참조하세요.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**delayed_durability_desc**|**nvarchar(60)**|지연 된 내구성 설정:<br /> DISABLED<br /> ALLOWED<br /> FORCED<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_memory_optimized_elevate_to_snapshot_on**|**bit**|메모리 액세스에 최적화된 테이블은 세션 설정 TRANSACTION ISOLATION LEVEL이 낮은 격리 수준, READ COMMITTED 또는 READ UNCOMMITTED로 설정된 경우 SNAPSHOT 격리를 사용하여 액세스됩니다.<br /> 1 = 최소 격리 수준이 SNAPSHOT입니다.<br /> 0 = 격리 수준이 승격되지 않았습니다.|  
|**is_federation_member**|**bit**|데이터베이스가 페더레이션의 멤버인지 여부를 나타냅니다.<br /> **적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_remote_data_archive_enabled**|**bit**|데이터베이스를 늘이는 여부를 나타냅니다.<br /> 0 = 데이터베이스가 스트레치 지원 되지 않습니다.<br /> 1 = 데이터베이스가 스트레치 지원 합니다.<br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /> 자세한 내용은 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하세요.|  
|**is_mixed_page_allocation_on**|**bit**|데이터베이스의 테이블 및 인덱스 혼합된 익스텐트에서 초기 페이지를 할당할 수 있는지 여부를 나타냅니다.<br /> 0 = 테이블 및 데이터베이스의에서 인덱스를 단일 익스텐트에서 항상 초기 페이지를 할당 합니다.<br /> 1 = 테이블 및 데이터베이스의에서 인덱스를 혼합 익스텐트에서 초기 페이지를 할당할 수 있습니다.<br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /> 자세한 내용은 참조의 SET MIXED_PAGE_ALLOCATION 옵션이 [ALTER DATABASE SET 옵션 &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)합니다.|  
|**is_temporal_retention_enabled**|**bit**|임시 재방문 주기 정책 정리 작업이 사용 되는지 여부를 나타냅니다.<br /> **적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**catalog_collation_type**|**int**|카탈로그 데이터 정렬 설정:<br />0 = DATABASE_DEFAULT<br />2 = SQL_Latin_1_General_CP1_CI_AS<br /> **적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**catalog_collation_type_desc**|**nvarchar(60)**|카탈로그 데이터 정렬 설정:<br />COLLATE<br />SQL_Latin_1_General_CP1_CI_AS<br /> **적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**is_result_set_caching_on**|**int**|1 = is_result_set_caching_on 켜져</br>0 = is_result_set_caching_on 꺼져</br>**적용 대상**: Azure SQL Data Warehouse Gen2
  
## <a name="permissions"></a>사용 권한  
 경우 호출자 `sys.databases` 데이터베이스의 소유자가 아니고 및 데이터베이스가 `master` 또는 `tempdb`, 해당 행을 보는 데 필요한 최소 권한이 `ALTER ANY DATABASE` 또는 `VIEW ANY DATABASE` 서버 수준 권한이 있거나 `CREATE DATABASE` 에 대 한 권한과 `master` 데이터베이스입니다. 호출자가 연결 된 데이터베이스에서 항상 볼 수 있습니다 `sys.databases`합니다.  
  
> [!IMPORTANT]  
> 기본적으로 public 역할에는 `VIEW ANY DATABASE` 권한, 데이터베이스 정보를 보려는 모든 로그인을 허용 합니다. 데이터베이스를 검색 하는 기능에서 로그인을 차단 하려면 `REVOKE` 는 `VIEW ANY DATABASE` 사용 권한을 `public`, 또는 `DENY` 는 `VIEW ANY DATABASE` 개별 로그인에 대 한 권한을 합니다.  
  
## <a name="azure-sql-database-remarks"></a>Azure SQL 데이터베이스 설명  
[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 이 뷰는에서 사용할 수는 `master` 데이터베이스와 사용자 데이터베이스에서. 에 `master` 데이터베이스에이 뷰 정보에서 반환을 `master` 데이터베이스와 서버의 모든 사용자 데이터베이스. 사용자 데이터베이스에서 이 뷰는 현재 데이터베이스와 master 데이터베이스에 있는 정보만을 반환합니다.  
  
 새 데이터베이스가 만들어지는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 서버의 `master` 데이터베이스에서 `sys.databases` 뷰를 사용합니다. 데이터베이스 복사가 시작 되 면를 쿼리할 수 있습니다는 `sys.databases` 하며 `sys.dm_database_copies` 에서 뷰를 `master` 복사 진행률에 대 한 자세한 정보를 검색할 대상 서버의 데이터베이스.  
  
## <a name="examples"></a>예  
  
### <a name="a-query-the-sysdatabases-view"></a>1. sys.databases 뷰 쿼리  
 다음 예에 사용 가능한 열 중 일부는 `sys.databases` 보기.  
  
```sql  
SELECT name, user_access_desc, is_read_only, state_desc, recovery_model_desc  
FROM sys.databases;  
```  
  
### <a name="b-check-the-copying-status-in-includesssdsincludessssds-mdmd"></a>2. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 복사 상태 확인  
 다음 예제 쿼리에서 `sys.databases` 및 `sys.dm_database_copies` 뷰는 데이터베이스에 대 한 정보를 반환 하려면 복사 작업입니다.  
  
**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
```sql  
-- Execute from the master database.  
SELECT a.name, a.state_desc, b.start_date, b.modify_date, b.percentage_complete  
FROM sys.databases AS a  
INNER JOIN sys.dm_database_copies AS b ON a.database_id = b.database_id  
WHERE a.state = 7;  
```  
### <a name="c-check-the-temporal-retention-policy-status-in-includesssdsincludessssds-mdmd"></a>3. 임시 재방문 주기 정책 상태를 확인 합니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
 다음 예제에서는 쿼리를 `sys.databases` temporal 보존 정리 작업이 사용 되는지 여부를 정보를 반환 합니다. 복원 작업 후 임시 재방문 주기는 사용 하지 않도록 기본적으로 알아야 합니다. 사용 하 여 `ALTER DATABASE` 명시적으로 사용 하도록 설정 합니다.
  
**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
```sql  
-- Execute from the master database.  
SELECT a.name, a.is_temporal_history_retention_enabled 
FROM sys.databases AS a;
```  
  
## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.database_recovery_status &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-recovery-status-transact-sql.md)   
 [데이터베이스 및 파일 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [sys.dm_database_copies&#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)  
  
  
