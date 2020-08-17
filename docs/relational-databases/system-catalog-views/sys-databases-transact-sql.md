---
description: sys.databases(Transact-SQL)
title: sys. 데이터베이스 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/08/2020
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 73141e7bc09d2748ff79cba0de4ebf9d4758cd65
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88379089"
---
# <a name="sysdatabases-transact-sql"></a>sys.databases(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 각 데이터베이스당 한 개의 행을 포함합니다.  
  
데이터베이스가이 아니거나 `ONLINE` `AUTO_CLOSE` 로 설정 되 `ON` 고 데이터베이스가 닫히면 일부 열의 값은이 될 수 있습니다 `NULL` . 데이터베이스가 이면 `OFFLINE` 권한이 낮은 사용자에 게 해당 행이 표시 되지 않습니다. 데이터베이스가 인 경우 해당 행을 보려면 `OFFLINE` 최소한 `ALTER ANY DATABASE` 서버 수준 사용 권한 또는 데이터베이스에 대 한 사용 권한이 있어야 합니다 `CREATE DATABASE` `master` .  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 또는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 서버 내에서 고유한 데이터베이스 이름입니다.|  
|**database_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 또는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 서버 내에서 고유한 데이터베이스 ID입니다.|  
|**source_database_id**|**int**|NULL이 아닌 경우 = 이 데이터베이스 스냅샷의 원본 데이터베이스 ID입니다.<br /> NULL = 데이터베이스 스냅샷이 아닙니다.|  
|**owner_sid**|**varbinary(85)**|서버에 등록된 데이터베이스 외부 소유자의 SID(보안 ID)입니다. 데이터베이스를 소유할 수 있는 사람에 대 한 자세한 내용은 [ALTER authorization](../../t-sql/statements/alter-authorization-transact-sql.md)의 **데이터베이스에 대 한 alter authorization** 섹션을 참조 하십시오.|  
|**create_date**|**datetime**|데이터베이스가 작성되었거나 이름이 변경된 날짜입니다. **Tempdb**의 경우이 값은 서버가 다시 시작 될 때마다 변경 됩니다.|  
|**compatibility_level**|**tinyint**|동작이 호환되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전에 해당하는 정수입니다.<br /><br /><table border="0"><tr><td>**값**</td><td>**적용 대상**</td></tr><tr><td>70</td><td>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 ~ [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]</td></tr><tr><td>80</td><td>[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 과정 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]</td></tr><tr><td>90</td><td>[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 과정 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]</td></tr><tr><td>100</td><td>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]</td></tr><tr><td>110</td><td>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]</td></tr><tr><td>120</td><td>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]</td></tr><tr><td>130</td><td>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]</td></tr><tr><td>140</td><td>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]</td></tr><tr><td>150</td><td>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]</td></tr></table>|  
|**collation_name**|**sysname**|데이터베이스용 데이터 정렬입니다. 데이터베이스의 기본 데이터 정렬로 사용됩니다.<br /> NULL = 데이터베이스가 온라인이 아니거나 AUTO_CLOSE가 ON으로 설정되어 있고 데이터베이스가 닫혀 있습니다.|  
|**user_access**|**tinyint**|사용자 액세스 설정입니다.<br /> 0 = MULTI_USER로 지정됩니다.<br /> 1 = SINGLE_USER로 지정됩니다.<br /> 2 = RESTRICTED_USER로 지정됩니다.|  
|**user_access_desc**|**nvarchar(60)**|사용자 액세스 설정에 대한 설명입니다.|  
|**is_read_only**|**bit**|1 = 데이터베이스가 READ_ONLY입니다.<br /> 0 = 데이터베이스가 READ_WRITE입니다.|  
|**is_auto_close_on**|**bit**|1 = AUTO_CLOSE가 ON입니다.<br /> 0 = AUTO_CLOSE가 OFF입니다.|  
|**is_auto_shrink_on**|**bit**|1 = AUTO_SHRINK가 ON입니다.<br /> 0 = AUTO_SHRINK가 OFF입니다.|  
|**상태**|**tinyint**|**값**<br /> 0 = ONLINE <br /> 1 = RESTORING <br /> 2 = 복구 <sup>1</sup><br /> 3 = RECOVERY_PENDING <sup>1</sup><br /> 4 = SUSPECT <br /> 5 = 응급 <sup>1</sup><br /> 6 = 오프 라인 <sup>1</sup><br /> 7 = 복사 <sup>2</sup> <br /> 10 = OFFLINE_SECONDARY <sup>2</sup> <br /><br /> **참고:** Always On 데이터베이스의 경우 `database_state` `database_state_desc` [dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)의 또는 열을 쿼리 합니다.<br /><br /><sup>1</sup> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /><sup>2</sup> **적용**대상: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)][!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]|  
|**state_desc**|**nvarchar(60)**|데이터베이스 상태에 대한 설명입니다. 상태를 참조 하세요.|  
|**is_in_standby**|**bit**|데이터베이스가 로그 복원을 위해 읽기 전용 상태임을 나타냅니다.|  
|**is_cleanly_shutdown**|**bit**|1 = 데이터베이스가 올바르게 종료되었으므로 시작할 때 복구가 필요하지 않습니다.<br /> 0 = 데이터베이스가 올바르게 종료되지 않았으므로 시작할 때 복구가 필요합니다.|  
|**is_supplemental_logging_enabled**|**bit**|1 = SUPPLEMENTAL_LOGGING이 ON입니다.<br /> 0 = SUPPLEMENTAL_LOGGING이 OFF입니다.|  
|**snapshot_isolation_state**|**tinyint**|ALLOW_SNAPSHOT_ISOLATION 옵션으로 설정되는 허용된 스냅샷 격리 트랜잭션의 상태입니다.<br /> 0 = 스냅샷 격리 상태가 OFF입니다(기본값). 스냅샷 격리가 허용되지 않습니다.<br /> 1 = 스냅샷 격리 상태가 ON입니다. 스냅샷 격리가 허용됩니다.<br /> 2 = 스냅샷 격리 상태가 OFF로 전환 중입니다. 모든 트랜잭션에는 수정 사항이 버전별로 관리됩니다. 스냅샷 격리를 사용해 새 트랜잭션을 시작할 수 없습니다. ALTER DATABASE가 실행되었을 때 활성 상태인 모든 트랜잭션이 완료될 때까지 데이터베이스는 OFF로 전환 중인 상태를 유지합니다.<br /> 3 = 스냅샷 격리 상태가 ON으로 전환 중입니다. 새 트랜잭션에는 수정 사항이 버전별로 관리됩니다. 스냅샷 격리 상태가 1(ON)이 될 때까지 트랜잭션은 스냅샷 격리를 사용할 수 없습니다. ALTER DATABASE가 실행되었을 때 활성 상태인 모든 업데이트 트랜잭션이 완료될 때까지 데이터베이스는 ON으로 전환 중인 상태를 유지합니다.|  
|**snapshot_isolation_state_desc**|**nvarchar(60)**|ALLOW_SNAPSHOT_ISOLATION 옵션으로 설정되는 허용된 스냅샷 격리 트랜잭션의 상태에 대한 설명입니다.|  
|**is_read_committed_snapshot_on**|**bit**|1 = READ_COMMITTED_SNAPSHOT 옵션은 ON입니다. READ COMMITTED 격리 수준에서의 읽기 작업은 스냅샷 검색을 기반으로 하며 잠금을 획득하지 않습니다.<br /> 0 = READ_COMMITTED_SNAPSHOT 옵션은 OFF(기본값)입니다. READ COMMITTED 격리 수준에서의 읽기 작업은 공유 잠금을 사용합니다.|  
|**recovery_model**|**tinyint**|선택된 복구 모델입니다.<br /> 1 = FULL<br /> 2 = BULK_LOGGED<br /> 3 = SIMPLE|  
|**recovery_model_desc**|**nvarchar(60)**|선택된 복구 모델에 대한 설명입니다.|  
|**page_verify_option**|**tinyint**|PAGE_VERIFY 옵션 설정입니다.<br /> 0 = 없음<br /> 1 = TORN_PAGE_DETECTION<br /> 2 = CHECKSUM|  
|**page_verify_option_desc**|**nvarchar(60)**|PAGE_VERIFY 옵션 설정에 대한 설명입니다.|  
|**is_auto_create_stats_on**|**bit**|1 = AUTO_CREATE_STATISTICS가 ON입니다.<br /> 0 = AUTO_CREATE_STATISTICS가 OFF입니다.|  
|**is_auto_create_stats_incremental_on**|**bit**|자동 통계 증분 옵션의 기본 설정을 나타냅니다.<br /> 0 = 통계 자동 작성이 비증분입니다.<br /> 1 = 통계 자동 작성이 증분입니다(가능한 경우).<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터)|  
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
|**is_trustworthy_on**|**bit**|1 = 데이터베이스가 신뢰할 수 있는 것으로 표시되어 있습니다.<br /> 0 = 데이터베이스가 신뢰할 수 있는 것으로 표시되지 않았습니다.<br /> 기본적으로 복원 또는 연결 된 데이터베이스에는 신뢰할 수 없는 데이터베이스가 있습니다.|  
|**is_db_chaining_on**|**bit**|1 = 데이터베이스 간 소유권 체인이 ON 상태입니다.<br /> 0 = 데이터베이스 간 소유권 체인이 OFF 상태입니다.|  
|**is_parameterization_forced**|**bit**|1 = 매개 변수화가 FORCED로 설정되어 있습니다.<br /> 0 = 매개 변수화가 SIMPLE로 설정되어 있습니다.|  
|**is_master_key_encrypted_by_server**|**bit**|1 = 데이터베이스에 암호화된 마스터 키가 있습니다.<br /> 0 = 데이터베이스에 암호화된 마스터 키가 없습니다.|  
|**is_query_store_on**|**bit**|1 =이 데이터베이스에 대해 쿼리 저장소를 사용할 수 있습니다. [Database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) 확인 하 여 쿼리 저장소 상태를 확인 합니다.<br /> 0 = 쿼리 저장소를 사용할 수 없습니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터)|  
|**is_published**|**bit**|1 = 데이터베이스가 트랜잭션 또는 스냅샷 복제 토폴로지에서 게시 데이터베이스입니다.<br /> 0 = 게시 데이터베이스가 아닙니다.|  
|**is_subscribed**|**bit**|이 열은 사용되지 않으며, 데이터베이스의 구독자 상태에 관계없이 항상 0을 반환합니다.|  
|**is_merge_published**|**bit**|1 = 데이터베이스가 병합 복제 토폴로지에서 게시 데이터베이스입니다.<br /> 0 = 병합 복제 토폴로지에서 게시 데이터베이스가 아닙니다.|  
|**is_distributor**|**bit**|1 = 데이터베이스가 복제 토폴로지용 배포 데이터베이스입니다.<br /> 0 = 복제 토폴로지용 배포 데이터베이스가 아닙니다.|  
|**is_sync_with_backup**|**bit**|1 = 데이터베이스가 백업과의 복제 동기화용으로 표시되어 있습니다.<br /> 0 = 백업과의 복제 동기화용으로 표시되어 있지 않습니다.|  
|**service_broker_guid**|**uniqueidentifier**|이 데이터베이스의 Service Broker ID입니다. 라우팅 테이블에서 대상의 **broker_instance**로 사용됩니다.|  
|**is_broker_enabled**|**bit**|1 = 이 데이터베이스의 브로커가 현재 메시지를 주고받고 있습니다.<br /> 0 = 이 데이터베이스에서 보낸 모든 메시지는 전송 큐에서 대기하며 수신된 메시지는 큐에 배치되지 않습니다.<br /> 복원되거나 첨부된 데이터베이스의 경우 브로커를 사용하지 않도록 기본 설정됩니다. 단, 장애 조치(Failover) 후 브로커가 설정된 데이터베이스 미러링은 예외입니다.|  
|**log_reuse_wait**|**tinyint**|트랜잭션 로그 공간을 다시 사용 하는 것은 현재 마지막 검사점의 다음 중 하나를 기다리고 있습니다. 이러한 값에 대 한 자세한 설명은 [트랜잭션 로그](../../relational-databases/logs/the-transaction-log-sql-server.md)를 참조 하세요.<br /> **값**<br /> 0 = 없음<br /> 1 = 검사점 (데이터베이스가 복구 모델을 사용 하 고 메모리 최적화 데이터 파일 그룹을 포함 하는 경우 `log_reuse_wait` 열이 또는를 나타냄 `checkpoint` `xtp_checkpoint` ) <sup>1</sup> 을 표시 해야 합니다.<br /> 2 = 로그 백업 <sup>1</sup><br /> 3 = 활성 백업 또는 복원 <sup>1</sup><br /> 4 = 활성 트랜잭션 <sup>1</sup><br /> 5 = 데이터베이스 미러링 <sup>1</sup><br /> 6 = 복제 <sup>1</sup><br /> 7 = 데이터베이스 스냅숏 만들기 <sup>1</sup><br /> 8 = 로그 검색 <br /> 9 = Always On 가용성 그룹 보조 복제본이 해당 보조 데이터베이스에이 데이터베이스의 트랜잭션 로그 레코드를 적용 하는 중입니다. <sup>2</sup><br /> 9 = 기타 (일시적) <sup>3</sup><br /> 10 = 내부용 으로만 사용 됩니다. <sup>2</sup><br /> 11 = 내부용 으로만 사용 됩니다. <sup>2</sup><br /> 12 = 내부용 으로만 사용 됩니다. <sup>2</sup><br /> 13 = 가장 오래 된 페이지 <sup>2</sup><br /> 14 = 기타 <sup>2</sup><br />  16 = XTP_CHECKPOINT (데이터베이스가 복구 모델을 사용 하 고 메모리 최적화 데이터 파일 그룹이 있는 경우 `log_reuse_wait` `checkpoint` 또는 `xtp_checkpoint` ) <sup>4</sup> 열이 표시 되어야 합니다.<br /><br /><sup>1</sup> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] )<br /><sup>2</sup> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] )<br /><sup>3</sup> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (최대, 포함 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] )<br /><sup>4</sup> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] )|  
|**log_reuse_wait_desc**|**nvarchar(60)**|트랜잭션 로그 공간 다시 사용을 마지막 검사점을 기다리는지에 대한 설명입니다.|  
|**is_date_correlation_on**|**bit**|1 = DATE_CORRELATION_OPTIMIZATION이 ON입니다.<br /> 0 = DATE_CORRELATION_OPTIMIZATION이 OFF입니다.|  
|**is_cdc_enabled**|**bit**|1 = 데이터베이스에 변경 데이터 캡처가 설정되어 있습니다. 자세한 내용은 [sp_cdc_enable_db &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md)을 참조 하십시오.|  
|**is_encrypted**|**bit**|데이터베이스가 암호화 되었는지 여부를 나타냅니다 .는 절을 사용 하 여 마지막으로 설정 된 상태를 반영 `ALTER DATABASE SET ENCRYPTION` 합니다. 다음 값 중 하나일 수 있습니다.<br /> 1 = 암호화됨<br /> 0 = 암호화되지 않음<br /> 데이터 암호화에 대한 자세한 내용은 [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하십시오.<br /> 데이터베이스의 암호를 해독 하는 중이면에서 `is_encrypted` 0 값을 표시 합니다. [Dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 동적 관리 뷰를 사용 하 여 암호화 프로세스의 상태를 볼 수 있습니다.|  
|**is_honor_broker_priority_on**|**bit**|데이터베이스에서 대화 우선 순위를 준수 하는지 여부를 나타냅니다 .는 절을 사용 하 여 마지막으로 설정한 상태를 반영 `ALTER DATABASE SET HONOR_BROKER_PRIORITY` 합니다. 다음 값 중 하나일 수 있습니다.<br /> 1 = HONOR_BROKER_PRIORITY가 ON입니다.<br /> 0 = HONOR_BROKER_PRIORITY가 OFF입니다.<br /> 기본적으로 복원 되거나 연결 된 데이터베이스의 broker 우선 순위는 off입니다.|  
|**replica_id**|**uniqueidentifier**|데이터베이스가 참여하는 가용성 그룹(있는 경우)의 로컬 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 가용성 복제본에 대한 고유 식별자입니다.<br /> NULL = 데이터베이스가 가용성 그룹에 포함된 가용성 복제본의 일부가 아닙니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**group_database_id**|**uniqueidentifier**|데이터베이스가 참여 하는 Always On 가용성 그룹 (있는 경우) 내의 데이터베이스에 대 한 고유 식별자입니다. 주 복제본의이 데이터베이스와 데이터베이스가 가용성 그룹에 조인 된 모든 보조 복제본에 대 한 **group_database_id** 동일 합니다.<br /> NULL = 데이터베이스가 가용성 그룹에 포함된 가용성 복제본의 일부가 아닙니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**resource_pool_id**|**int**|이 데이터베이스에 매핑되는 리소스 풀의 ID입니다. 이 리소스 풀은 이 데이터베이스에서 메모리 최적화 테이블을 사용할 수 있는 총 메모리를 제어합니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] )|  
|**default_language_lcid**|**smallint**|포함된 데이터베이스의 기본 언어에 대한 로컬 ID(lcid)를 나타냅니다.<br /> **참고:** 의 [기본 언어 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) 으로 작동 `sp_configure` 합니다. 포함 되지 않은 데이터베이스의 경우이 값은 **null** 입니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_language_name**|**nvarchar(128)**|포함된 데이터베이스의 기본 언어를 나타냅니다.<br /> 포함 되지 않은 데이터베이스의 경우이 값은 **null** 입니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_lcid**|**int**|포함 된 데이터베이스의 기본 전체 텍스트 언어의 lcid (로캘 id)를 나타냅니다.<br /> **참고:** 의 기본 [전체 텍스트 언어 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) 으로 작동 `sp_configure` 합니다. 포함 되지 않은 데이터베이스의 경우이 값은 **null** 입니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_name**|**nvarchar(128)**|포함된 데이터베이스의 기본 전체 텍스트 언어를 나타냅니다.<br /> 포함 되지 않은 데이터베이스의 경우이 값은 **null** 입니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_nested_triggers_on**|**bit**|포함된 데이터베이스에서 중첩 트리거가 허용되는지 여부를 나타냅니다.<br /> 0 = 중첩 트리거가 허용되지 않습니다.<br /> 1 = 중첩 트리거가 허용됩니다.<br /> **참고:** 의 [nested Triggers 서버 구성 옵션을 구성](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) 하는 함수 `sp_configure` 입니다. 포함 되지 않은 데이터베이스의 경우이 값은 **null** 입니다. 자세한 내용은 [sys.configurations &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 를 참조 하세요.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_transform_noise_words_on**|**bit**|포함된 데이터베이스에서 의미 없는 단어가 변환되는지 여부를 나타냅니다.<br /> 0 = 의미 없는 단어가 변환되지 않습니다.<br /> 1 = 의미 없는 단어가 변환됩니다.<br /> **참고:** 의 의미 없는 [단어 변환 서버 구성 옵션](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md) 으로 작동 `sp_configure` 합니다. 포함 되지 않은 데이터베이스의 경우이 값은 **null** 입니다. 자세한 내용은 [sys.configurations &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 를 참조 하세요.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] )|  
|**two_digit_year_cutoff**|**smallint**|두 자리 연도를 네 자리 연도로 해석하기 위한 구분 연도를 나타내는 1753에서 9999까지의 숫자 값을 나타냅니다.<br /> **참고:** 의 [두 자리 연도 구분 서버 구성 옵션을 구성](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) 하는 함수입니다 `sp_configure` . 포함 되지 않은 데이터베이스의 경우이 값은 **null** 입니다. 자세한 내용은 [sys.configurations &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 를 참조 하세요.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**포함**|**tinyint not null**|데이터베이스의 포함 상태를 나타냅니다.<br />  0 = 데이터베이스가 포함되지 않습니다. **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 1 = 데이터베이스가 부분 포함에 **적용**됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] )|  
|**containment_desc**|**nvarchar (60) null이 아님**|데이터베이스의 포함 상태를 나타냅니다.<br /> NONE = 레거시 데이터베이스입니다(containment = 0).<br /> PARTIAL = 부분적으로 포함된 데이터베이스입니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**target_recovery_time_in_seconds**|**int**|데이터베이스 복구 예상 시간(초)입니다. Null을 허용합니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**delayed_durability**|**int**|지연 된 내구성 설정:<br /> 0 = 사용 안 함<br /> 1 = 허용 됨<br /> 2 = 강제<br /> 자세한 내용은 [트랜잭션 내구성 제어](../../relational-databases/logs/control-transaction-durability.md)를 참조하세요.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**delayed_durability_desc**|**nvarchar(60)**|지연 된 내구성 설정:<br /> DISABLED<br /> ALLOWED<br /> FORCED<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**is_memory_optimized_elevate_to_snapshot_on**|**bit**|메모리 액세스에 최적화된 테이블은 세션 설정 TRANSACTION ISOLATION LEVEL이 낮은 격리 수준, READ COMMITTED 또는 READ UNCOMMITTED로 설정된 경우 SNAPSHOT 격리를 사용하여 액세스됩니다.<br /> 1 = 최소 격리 수준이 SNAPSHOT입니다.<br /> 0 = 격리 수준이 승격되지 않았습니다.|  
|**is_federation_member**|**bit**|데이터베이스가 페더레이션의 멤버인지 여부를 나타냅니다.<br /> **적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_remote_data_archive_enabled**|**bit**|데이터베이스를 스트레치 하는지 여부를 나타냅니다.<br /> 0 = 스트레치를 사용 하지 않는 데이터베이스입니다.<br /> 1 = 스트레치를 사용 하도록 설정 된 데이터베이스입니다.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] )<br /> 자세한 내용은 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하세요.|  
|**is_mixed_page_allocation_on**|**bit**|데이터베이스의 테이블 및 인덱스가 혼합 익스텐트의 초기 페이지를 할당할 수 있는지 여부를 나타냅니다.<br /> 0 = 데이터베이스의 테이블 및 인덱스는 항상 단일 익스텐트의 초기 페이지를 할당 합니다.<br /> 1 = 데이터베이스의 테이블 및 인덱스는 혼합 익스텐트의 초기 페이지를 할당할 수 있습니다.<br /> 자세한 내용은 `SET MIXED_PAGE_ALLOCATION` [ALTER Database SET Options &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)의 옵션을 참조 하세요.<br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] )|  
|**is_temporal_retention_enabled**|**bit**|임시 보존 정책 정리 태스크를 사용할 수 있는지 여부를 나타냅니다.<br /><br />1 = 임시 보존이 사용 됩니다.<br />0 = 임시 보존이 사용 하지 않도록 설정 됨<br />**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**catalog_collation_type**|**int**|카탈로그 데이터 정렬 설정:<br />0 = DATABASE_DEFAULT<br />2 = SQL_Latin_1_General_CP1_CI_AS<br /> **적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**catalog_collation_type_desc**|**nvarchar(60)**|카탈로그 데이터 정렬 설정:<br />COLLATE<br />SQL_Latin_1_General_CP1_CI_AS<br /> **적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**physical_database_name**|**nvarchar(128)**|의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 데이터베이스의 물리적 이름입니다. 의 경우 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 서버의 데이터베이스에 대 한 일반 id입니다. <br />**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**is_result_set_caching_on**|**bit**|결과 집합 캐싱이 사용 되는지 여부를 나타냅니다.<br />1 = 결과 집합 캐싱이 사용 됩니다.<br />0 = 결과 집합 캐싱이 사용 되지 않습니다.<br />**적용**대상: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Gen2. 이 기능이 모든 지역으로 롤아웃 되는 동안 인스턴스에 배포 된 버전과 최신 [Azure Synapse 릴리스 정보](/azure/synapse-analytics/sql-data-warehouse/release-notes-10-0-10106-0) 및 기능 가용성에 대 한 [Gen2 업그레이드 일정](/azure/synapse-analytics/sql-data-warehouse/gen2-migration-schedule) 을 확인 하세요.|
|**is_accelerated_database_recovery_on**|**bit**|ADR (가속화 된 데이터베이스 복구)를 사용할 수 있는지 여부를 나타냅니다.<br />1 = ADR가 사용 됩니다.<br />0 = ADR가 사용 되지 않습니다.<br />**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**is_tempdb_spill_to_remote_store**|**bit**|원격 저장소에 대 한 tempdb 분산을 사용할 수 있는지 여부를 나타냅니다.<br />1 = 사용<br />0 = 사용 안 함<br />**적용**대상: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Gen2. 이 기능이 모든 지역으로 롤아웃 되는 동안 인스턴스에 배포 된 버전과 최신 [Azure Synapse 릴리스 정보](/azure/synapse-analytics/sql-data-warehouse/release-notes-10-0-10106-0) 및 기능 가용성에 대 한 [Gen2 업그레이드 일정](/azure/synapse-analytics/sql-data-warehouse/gen2-migration-schedule) 을 확인 하세요.|
|**is_stale_page_detection_on**|**bit**|오래 된 페이지 검색이 사용 되는지 여부를 나타냅니다.<br />1 = 오래 된 페이지 검색이 사용 됩니다.<br />0 = 부실 페이지 검색이 사용 하지 않도록 설정 됨<br />**적용**대상: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Gen2. 이 기능이 모든 지역으로 롤아웃 되는 동안 인스턴스에 배포 된 버전과 최신 [Azure Synapse 릴리스 정보](/azure/synapse-analytics/sql-data-warehouse/release-notes-10-0-10106-0) 및 기능 가용성에 대 한 [Gen2 업그레이드 일정](/azure/synapse-analytics/sql-data-warehouse/gen2-migration-schedule) 을 확인 하세요.|
|**is_memory_optimized_enabled**|**bit**|[하이브리드 버퍼 풀](../../database-engine/configure-windows/hybrid-buffer-pool.md)과 같은 특정 메모리 내 기능을 데이터베이스에 사용할 수 있는지 여부를 나타냅니다. 는 [메모리 내 OLTP](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)의 가용성 또는 구성 상태를 반영 하지 않습니다. <br />1 = 메모리 액세스에 최적화 된 기능 사용<br />0 = 메모리 액세스에 최적화 된 기능을 사용할 수 없습니다.<br />**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
  
## <a name="permissions"></a>사용 권한

 의 호출자 `sys.databases` 가 데이터베이스의 소유자가 아니고 데이터베이스가 또는이 아닌 경우 `master` `tempdb` 해당 행을 보는 데 필요한 최소 권한은 `ALTER ANY DATABASE` 또는 `VIEW ANY DATABASE` 데이터베이스의 서버 수준 권한 또는 `CREATE DATABASE` 사용 권한 `master` 입니다. 호출자가 연결 된 데이터베이스는 항상에서 볼 수 있습니다 `sys.databases` .  
  
> [!IMPORTANT]  
> 기본적으로 public 역할에는 `VIEW ANY DATABASE` 모든 로그인이 데이터베이스 정보를 볼 수 있는 권한이 있습니다. 로그인에서 데이터베이스를 검색 하는 기능, `REVOKE` `VIEW ANY DATABASE` 의 권한 `public` 또는 `DENY` `VIEW ANY DATABASE` 개별 로그인에 대 한 사용 권한을 차단 합니다.  
  
## <a name="azure-sql-database-remarks"></a>Azure SQL Database 설명

[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]이 보기의는 `master` 데이터베이스 및 사용자 데이터베이스에서 사용할 수 있습니다. 데이터베이스에서 `master` 이 뷰는 `master` 서버에 있는 데이터베이스와 모든 사용자 데이터베이스에 대 한 정보를 반환 합니다. 사용자 데이터베이스에서 이 뷰는 현재 데이터베이스와 master 데이터베이스에 있는 정보만을 반환합니다.  
  
 새 데이터베이스가 만들어지는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 서버의 `master` 데이터베이스에서 `sys.databases` 뷰를 사용합니다. 데이터베이스 복사가 시작 된 후 `sys.databases` `sys.dm_database_copies` 대상 서버의 데이터베이스에서 및 뷰를 쿼리하여 `master` 복사 진행에 대 한 자세한 정보를 검색할 수 있습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-query-the-sysdatabases-view"></a>A. sys.databases 뷰 쿼리

다음 예에서는 뷰에서 사용할 수 있는 열 중 일부를 반환 합니다 `sys.databases` .  
  
```sql  
SELECT name, user_access_desc, is_read_only, state_desc, recovery_model_desc  
FROM sys.databases;  
```  
  
### <a name="b-check-the-copying-status-in-sssds"></a>B. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 복사 상태 확인

다음 예에서는 `sys.databases` 및 뷰를 쿼리하여 `sys.dm_database_copies` 데이터베이스 복사 작업에 대 한 정보를 반환 합니다.  
  
**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
```sql
-- Execute from the master database.  
SELECT a.name, a.state_desc, b.start_date, b.modify_date, b.percentage_complete  
FROM sys.databases AS a  
INNER JOIN sys.dm_database_copies AS b ON a.database_id = b.database_id  
WHERE a.state = 7;  
```

### <a name="c-check-the-temporal-retention-policy-status-in-sssds"></a>C. 에서 임시 보존 정책 상태를 확인 합니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]

다음 예제에서는 `sys.databases` 임시 보존 정리 작업의 설정 여부에 대 한 정보를 반환 하는을 쿼리 합니다. 복원 작업 후 임시 보존은 기본적으로 사용 하지 않도록 설정 됩니다. `ALTER DATABASE`을 사용 하 여 명시적으로 설정 합니다.
  
**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
```sql  
-- Execute from the master database.  
SELECT a.name, a.is_temporal_history_retention_enabled 
FROM sys.databases AS a;
```  
  
## <a name="next-steps"></a>다음 단계

- [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)
- [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)
- [database_recovery_status &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-recovery-status-transact-sql.md)
- [데이터베이스 및 파일 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)
- [sys.dm_database_copies&#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)  
