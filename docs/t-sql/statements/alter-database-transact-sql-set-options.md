---
title: ALTER DATABASE SET 옵션(Transact-SQL) | Microsoft Docs
description: SQL Server 및 Azure SQL Database에서 자동 튜닝, 암호화, 쿼리 저장소와 같은 데이터베이스 옵션을 설정하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 09/04/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- online database state [SQL Server]
- database options [SQL Server]
- emergency database state [SQL Server]
- databases [SQL Server], options
- read-only databases
- recovery models [SQL Server], switching
- ALTER DATABASE statement, SET options
- offline database state [SQL Server]
- snapshot isolation framework option
- checksums [SQL Server]
- Automatic tuning
- " Data Retention Policy"
- query plan regression correction
- auto_create_statistics
- auto_update_statistics
- Query Store options
ms.assetid: f76fbd84-df59-4404-806b-8ecb4497c9cc
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current
ms.openlocfilehash: c7e35b474e33da25b2d323d4af4aced5c4fe50f1
ms.sourcegitcommit: 678f513b0c4846797ba82a3f921ac95f7a5ac863
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2020
ms.locfileid: "89511305"
---
# <a name="alter-database-set-options-transact-sql"></a>ALTER DATABASE SET 옵션(Transact-SQL)

Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 및 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서 데이터베이스 옵션을 설정합니다. 다른 ALTER DATABASE 옵션은 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.

작업 중인 특정 SQL 버전에 대한 구문, 인수, 설명, 사용 권한 및 예제를 보려면 다음 탭 중 하나를 선택합니다.

구문 표기 규칙에 대한 자세한 내용은 [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)을 참조하세요.

## <a name="select-a-product"></a>제품 선택

다음 행에서 관심이 있는 제품 이름을 선택합니다. 선택하면, 이 웹 페이지에 선택한 제품과 관련된 다른 콘텐츠가 표시됩니다.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [SQL 데이터베이스](alter-database-transact-sql-set-options.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [SQL Database<br />Managed Instance](alter-database-transact-sql-set-options.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-database-transact-sql-set-options.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server"></a>SQL Server

데이터베이스 미러링, [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 및 호환성 수준은 `SET` 옵션이지만 길이 때문에 별도의 항목에서 설명합니다. 자세한 내용은 [ALTER DATABASE 데이터베이스 미러링](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md), [ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md) 및 [ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.

데이터베이스 범위 구성은 개별 데이터베이스 수준에서 여러 데이터베이스 구성을 설정하는 데 사용됩니다. 자세한 내용은 [ALTER DATABASE SCOPED CONFIGURATION](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 참조하세요.

> [!NOTE]
> 많은 데이터베이스 설정 옵션은 현재 세션에 [SET 문](../../t-sql/statements/set-statements-transact-sql.md)을 사용하여 구성할 수 있으며, 연결된 경우 일반적으로 애플리케이션에서 구성됩니다. 세션 수준 설정 옵션은 **ALTER DATABASE SET** 값을 재정의합니다. 다음 섹션에 설명된 데이터베이스 옵션은 다른 설정 옵션 값을 명시적으로 제공하지 않는 세션에 대해 설정할 수 있는 값입니다.

## <a name="syntax"></a>구문

```syntaxsql
ALTER DATABASE { database_name | CURRENT }
SET
{
    <option_spec> [ ,...n ] [ WITH <termination> ]
}

<option_spec> ::=
{
    <accelerated_database_recovery>
  | <auto_option>
  | <automatic_tuning_option>
  | <change_tracking_option>
  | <containment_option>
  | <cursor_option>
  | <database_mirroring_option>
  | <date_correlation_optimization_option>
  | <db_encryption_option>
  | <db_state_option>
  | <db_update_option>
  | <db_user_access_option>
  | <delayed_durability_option>
  | <external_access_option>
  | FILESTREAM ( <FILESTREAM_option> )
  | <HADR_options>
  | <mixed_page_allocation_option>
  | <parameterization_option>
  | <query_store_options>
  | <recovery_option>
  | <remote_data_archive_option>
  | <service_broker_option>
  | <snapshot_option>
  | <sql_option>
  | <target_recovery_time_option>
  | <termination>
  | <temporal_history_retention>
  | <data_retention_policy>
}
;

<accelerated_database_recovery> ::=
{
    ACCELERATED_DATABASE_RECOVERY = { ON | OFF }
     [ ( PERSISTENT_VERSION_STORE_FILEGROUP = { filegroup name } ) ];
}

<auto_option> ::=
{
    AUTO_CLOSE { ON | OFF }
  | AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] }
  | AUTO_SHRINK { ON | OFF }
  | AUTO_UPDATE_STATISTICS { ON | OFF }
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }
}

<automatic_tuning_option> ::=
{
    AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = { ON | OFF } )
}

<change_tracking_option> ::=
{
    CHANGE_TRACKING
   {
       = OFF
     | = ON [ ( <change_tracking_option_list > [,...n] ) ]
     | ( <change_tracking_option_list> [,...n] )
   }
}

<change_tracking_option_list> ::=
{
   AUTO_CLEANUP = { ON | OFF }
 | CHANGE_RETENTION = retention_period { DAYS | HOURS | MINUTES }
}

<containment_option> ::=
   CONTAINMENT = { NONE | PARTIAL }

<cursor_option> ::=
{
    CURSOR_CLOSE_ON_COMMIT { ON | OFF }
  | CURSOR_DEFAULT { LOCAL | GLOBAL }
}

<database_mirroring_option>
  ALTER DATABASE Database Mirroring

<date_correlation_optimization_option> ::=
    DATE_CORRELATION_OPTIMIZATION { ON | OFF }
  
<db_encryption_option> ::=
    ENCRYPTION { ON | OFF | SUSPEND | RESUME }

<db_state_option> ::=
    { ONLINE | OFFLINE | EMERGENCY }

<db_update_option> ::=
    { READ_ONLY | READ_WRITE }

<db_user_access_option> ::=
    { SINGLE_USER | RESTRICTED_USER | MULTI_USER }

<delayed_durability_option> ::=
    DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }

<external_access_option> ::=
{
    DB_CHAINING { ON | OFF }
  | TRUSTWORTHY { ON | OFF }
  | DEFAULT_FULLTEXT_LANGUAGE = { <lcid> | <language name> | <language alias> }
  | DEFAULT_LANGUAGE = { <lcid> | <language name> | <language alias> }
  | NESTED_TRIGGERS = { OFF | ON }
  | TRANSFORM_NOISE_WORDS = { OFF | ON }
  | TWO_DIGIT_YEAR_CUTOFF = { 1753, ..., 2049, ..., 9999 }
}

<FILESTREAM_option> ::=
{
    NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL
  | DIRECTORY_NAME = <directory_name>
}

<HADR_options> ::=
    ALTER DATABASE SET HADR

<mixed_page_allocation_option> ::=
    MIXED_PAGE_ALLOCATION { OFF | ON }

<parameterization_option> ::=
    PARAMETERIZATION { SIMPLE | FORCED }

<query_store_options> ::=
{
    QUERY_STORE
    {
          = OFF [ FORCED ] 
        | = ON [ ( <query_store_option_list> [,...n] ) ]
        | ( < query_store_option_list> [,...n] )
        | CLEAR [ ALL ]
    }
}

<query_store_option_list> ::=
{
      OPERATION_MODE = { READ_WRITE | READ_ONLY }
    | CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = number )
    | DATA_FLUSH_INTERVAL_SECONDS = number
    | MAX_STORAGE_SIZE_MB = number
    | INTERVAL_LENGTH_MINUTES = number
    | SIZE_BASED_CLEANUP_MODE = { AUTO | OFF }
    | QUERY_CAPTURE_MODE = { ALL | AUTO | CUSTOM | NONE }
    | MAX_PLANS_PER_QUERY = number
    | WAIT_STATS_CAPTURE_MODE = { ON | OFF }
    | QUERY_CAPTURE_POLICY = ( <query_capture_policy_option_list> [,...n] )
}

<query_capture_policy_option_list> :: =
{
      STALE_CAPTURE_POLICY_THRESHOLD = number { DAYS | HOURS }
    | EXECUTION_COUNT = number
    | TOTAL_COMPILE_CPU_TIME_MS = number
    | TOTAL_EXECUTION_CPU_TIME_MS = number
}

<recovery_option> ::=
{
    RECOVERY { FULL | BULK_LOGGED | SIMPLE }
  | TORN_PAGE_DETECTION { ON | OFF }
  | PAGE_VERIFY { CHECKSUM | TORN_PAGE_DETECTION | NONE }
}

<remote_data_archive_option> ::=
{
    REMOTE_DATA_ARCHIVE =
    {
        ON ( SERVER = <server_name> ,
             { 
                  CREDENTIAL = <db_scoped_credential_name>
                  | FEDERATED_SERVICE_ACCOUNT = ON | OFF
             }
        )
        | OFF
    }
}

<service_broker_option> ::=
{
    ENABLE_BROKER
  | DISABLE_BROKER
  | NEW_BROKER
  | ERROR_BROKER_CONVERSATIONS
  | HONOR_BROKER_PRIORITY { ON | OFF}
}

<snapshot_option> ::=
{
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }
  | READ_COMMITTED_SNAPSHOT { ON | OFF }
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = { ON | OFF }
}
<sql_option> ::=
{
    ANSI_NULL_DEFAULT { ON | OFF }
  | ANSI_NULLS { ON | OFF }
  | ANSI_PADDING { ON | OFF }
  | ANSI_WARNINGS { ON | OFF }
  | ARITHABORT { ON | OFF }
  | COMPATIBILITY_LEVEL = { 150 | 140 | 130 | 120 | 110 | 100 }
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }
  | NUMERIC_ROUNDABORT { ON | OFF }
  | QUOTED_IDENTIFIER { ON | OFF }
  | RECURSIVE_TRIGGERS { ON | OFF }
}

<target_recovery_time_option> ::=
    TARGET_RECOVERY_TIME = target_recovery_time { SECONDS | MINUTES }

<termination>::=
{
    ROLLBACK AFTER number [ SECONDS ]
  | ROLLBACK IMMEDIATE
  | NO_WAIT
}

<temporal_history_retention> ::=
    TEMPORAL_HISTORY_RETENTION { ON | OFF }

<data_retention_policy> ::=
    DATA_RETENTION { ON | OFF }

```

## <a name="arguments"></a>인수

*database_name*     
수정할 데이터베이스의 이름입니다.

CURRENT     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 시작)

현재 데이터베이스에서 작업을 실행합니다. 모든 컨텍스트의 모든 옵션에서 `CURRENT`가 지원되는 것은 아닙니다. `CURRENT`가 실패할 경우 데이터베이스 이름을 지정해야 합니다.

**\<accelerated_database_recovery> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작)

데이터베이스별로 ADR[(가속 데이터베이스 복구)](../../relational-databases/accelerated-database-recovery-management.md)를 사용하도록 설정합니다. ADR은 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에서 기본적으로 OFF로 설정되어 있습니다. 이 구문을 사용하여 PVS(영구 버전 저장소) 데이터에 대해 특정 파일 그룹을 선택적으로 지정할 수 있습니다. 파일 그룹을 지정하지 않으면 PVS가 기본 파일 그룹에 저장됩니다. 예제와 자세한 내용은[데이터베이스 복구 가속화](../../relational-databases/accelerated-database-recovery-management.md)을 참조하세요.

**\<auto_option> ::=**      
자동 옵션을 제어합니다.

<a name="auto_close"></a> AUTO_CLOSE { ON | **OFF** }     
켜기     
마지막 사용자가 사용을 끝낸 후 데이터베이스가 종료되고 해당 리소스가 해제됩니다.

사용자가 데이터베이스를 다시 사용하려고 하면(예: 예를 들어 이 다시 열기 동작은 사용자가 `USE database_name` 문을 실행하는 경우에 발생합니다. AUTO_CLOSE가 ON으로 설정되어 있는 상태에서 데이터베이스가 완전히 종료될 수 있습니다. 이 경우 다음번에 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 다시 시작될 때 사용자가 데이터베이스를 사용하려고 할 때까지 데이터베이스가 다시 열리지 않습니다.

OFF     
마지막 사용자가 사용을 끝낸 후에도 데이터베이스는 열려 있는 상태가 됩니다.

AUTO_CLOSE 옵션을 사용하면 데이터베이스 파일을 일반 파일처럼 다룰 수 있기 때문에 데스크톱 데이터베이스에서 유용합니다. 데이터베이스 파일을 이동하거나 복사하여 백업을 만들 수도 있고, 다른 사용자에게 메일로 보낼 수도 있습니다. AUTO_CLOSE 프로세스는 비동기 프로세스이므로 데이터베이스를 반복적으로 열고 닫아도 성능이 저하되지 않습니다.

> [!NOTE]
> 포함된 데이터베이스 또는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서는 AUTO_CLOSE 옵션을 사용할 수 없습니다.
> 이 옵션의 상태는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_auto_close_on` 열 또는 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAutoClose` 속성을 검사하여 확인할 수 있습니다.
>
> AUTO_CLOSE가 ON으로 설정되어 있으면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 일부 열과 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수는 데이터베이스에서 데이터를 검색할 수 없는 경우 NULL을 반환합니다. 이 문제를 해결하려면 USE 문을 실행하여 데이터베이스를 엽니다.
>
> 데이터베이스 미러링을 사용하려면 AUTO_CLOSE가 OFF로 설정되어야 합니다.

데이터베이스가 `AUTOCLOSE = ON`으로 설정되어 있으면 자동 데이터베이스 종료를 시작하는 작업이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 대한 계획 캐시를 삭제합니다. 계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 서비스 팩 2부터 계획 캐시의 삭제된 각 캐시스토어에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 `SQL Server has encountered %d occurrence(s) of cachestore flush for the '%s' cachestore (part of plan cache) due to some database maintenance or reconfigure operations`라는 정보 메시지가 포함됩니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.

<a name="auto_create_statistics"></a> AUTO_CREATE_STATISTICS { **ON** | OFF }     
켜기     
쿼리 최적화 프로그램은 쿼리 계획 및 쿼리 성능을 개선하기 위해 필요한 경우 쿼리 조건자의 단일 열에 대한 통계를 생성합니다. 쿼리 최적화 프로그램에서 쿼리를 컴파일할 때 이러한 단일 열 통계가 생성됩니다. 단일 열 통계는 기존 통계 개체의 첫 번째 열이 아닌 열에 대해서만 생성됩니다.

기본 설정은 ON입니다. 대부분의 데이터베이스의 경우 기본 설정을 사용하는 것이 좋습니다.

OFF     
쿼리 최적화 프로그램에서 쿼리를 컴파일할 때 쿼리 조건자의 단일 열에 대한 통계를 생성하지 않습니다. 이 옵션을 OFF로 설정하면 최적이 아닌 쿼리 계획을 사용하므로 쿼리 성능이 저하됩니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_auto_create_stats_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAutoCreateStatistics` 속성을 검사하여 상태를 확인할 수도 있습니다.

자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)에서 “데이터베이스 차원의 통계 옵션 사용” 섹션을 참조하세요.

INCREMENTAL = ON | **OFF**     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

AUTO_CREATE_STATISTICS를 ON으로 설정하고 INCREMENTAL을 ON으로 설정합니다. 그러면 증분 통계가 지원될 때마다 자동으로 생성된 통계가 증분으로 설정됩니다. 기본값은 OFF입니다. 자세한 내용은 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)를 참조하세요.

<a name="auto_shrink"></a> AUTO_SHRINK { ON | **OFF** }     
켜기     
데이터베이스 파일이 주기적인 축소의 후보가 됩니다.

데이터 파일과 로그 파일 모두 자동으로 축소될 수 있습니다. AUTO_SHRINK는 데이터베이스를 단순 복구 모델로 설정하거나 로그를 백업하는 경우에만 트랜잭션 로그의 크기를 줄입니다. AUTO_SHRINK를 OFF로 설정하면, 사용되지 않는 공간을 정기적으로 검사하는 동안 데이터베이스 파일이 자동으로 축소되지 않습니다.

AUTO_SHRINK 옵션은 파일에서 사용되지 않는 공간이 25% 이상일 때 파일을 축소합니다. 이 옵션은 다음 두 크기 중 더 큰 값으로 파일을 축소합니다.

- 파일의 25%가 사용되지 않는 공간인 크기
- 파일 생성 시 파일의 크기

읽기 전용 데이터베이스는 축소할 수 없습니다.

OFF     
사용되지 않는 공간을 정기적으로 검사하는 동안에는 데이터베이스 파일을 자동으로 축소하지 않습니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_auto_shrink_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAutoShrink` 속성을 검사하여 상태를 확인할 수도 있습니다.

> [!NOTE]
> 포함된 데이터베이스에서는 AUTO_SHRINK 옵션을 사용할 수 없습니다.

<a name="auto_update_statistics"></a> AUTO_UPDATE_STATISTICS { **ON** | OFF }     
켜기     
쿼리에서 통계를 사용하거나 통계가 최신 정보가 아닌 경우 쿼리 최적화 프로그램에서 통계를 업데이트하도록 지정합니다. 삽입, 업데이트, 삭제 또는 병합 작업을 통해 테이블이나 인덱싱된 뷰의 데이터 분포가 변경되면 통계 내용이 더 이상 최신이 아니게 됩니다. 쿼리 최적화 프로그램은 마지막 통계 업데이트 이후 데이터 수정 개수를 계산한 다음, 이 수를 임계값과 비교하여 통계가 최신이 아니게 된 시점을 결정합니다. 임계값은 테이블 또는 인덱싱된 뷰의 행 수를 기준으로 합니다.

쿼리 최적화 프로그램은 쿼리를 컴파일하고 캐시된 쿼리 계획을 실행하기 전에 최신 정보가 아닌 통계가 있는지 확인합니다. 쿼리 최적화 프로그램은 쿼리 조건자의 열, 테이블 및 인덱싱된 뷰를 사용하여 어떤 통계가 최신이 아닌지 확인합니다. 쿼리 최적화 프로그램은 쿼리를 컴파일하기 전에 이 정보를 확인합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 캐시된 쿼리 계획을 실행하기 전에 쿼리 계획에서 최신 통계가 참조되는지 확인합니다.

AUTO_UPDATE_STATISTICS 옵션은 인덱스에 대해 생성된 통계, 쿼리 조건자의 단일 열 및 CREATE STATISTICS 문을 사용하여 생성된 통계에 적용됩니다. 이 옵션은 또한 필터링된 통계에도 적용됩니다.

기본값은 ON입니다. 대부분의 데이터베이스의 경우 기본 설정을 사용하는 것이 좋습니다.

AUTO_UPDATE_STATISTICS_ASYNC 옵션을 사용하여 통계를 동기적으로 업데이트할지 또는 비동기적으로 업데이트할지를 지정합니다.

OFF     
쿼리에서 통계를 사용하는 경우 쿼리 최적화 프로그램에서 통계를 업데이트하지 않도록 지정합니다. 통계가 최신이 아니게 된 경우에도 쿼리 최적화 프로그램에서 통계를 업데이트하지 않습니다. 이 옵션을 OFF로 설정하면 최적이 아닌 쿼리 계획을 사용하므로 쿼리 성능이 저하됩니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_auto_update_stats_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAutoUpdateStatistics` 속성을 검사하여 상태를 확인할 수도 있습니다.

자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)에서 “데이터베이스 차원의 통계 옵션 사용” 섹션을 참조하세요.

<a name="auto_update_statistics_async"></a> AUTO_UPDATE_STATISTICS_ASYNC { ON | **OFF** }     
켜기     
AUTO_UPDATE_STATISTICS 옵션에 대한 통계 업데이트를 비동기로 지정합니다. 쿼리 최적화 프로그램은 쿼리를 컴파일하기 전에 통계 업데이트가 완료될 때까지 기다리지 않습니다.

이 옵션을 ON으로 설정해도 AUTO_UPDATE_STATISTICS가 ON으로 설정되어 있지 않으면 영향을 주지 않습니다.

기본적으로 AUTO_UPDATE_STATISTICS_ASYNC 옵션은 OFF로 설정되므로 쿼리 최적화 프로그램은 통계를 동기적으로 업데이트합니다.

OFF     
AUTO_UPDATE_STATISTICS 옵션에 대한 통계 업데이트를 동기로 지정합니다. 쿼리 최적화 프로그램은 쿼리를 컴파일하기 전에 통계 업데이트가 완료될 때까지 기다립니다.

> [!NOTE]
> 이 옵션을 OFF로 설정해도 AUTO_UPDATE_STATISTICS가 ON으로 설정되어 있지 않으면 영향을 주지 않습니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_auto_update_stats_async_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다.

동기 통계 업데이트 또는 비동기 통계 업데이트를 사용하는 경우에 대한 자세한 설명은 [통계](../../relational-databases/statistics/statistics.md#statistics-options)에서 “통계 옵션” 섹션을 참조하세요.

<a name="auto_tuning"></a> **\<automatic_tuning_option> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]부터 시작)

`FORCE_LAST_GOOD_PLAN` [자동 튜닝](../../relational-databases/automatic-tuning/automatic-tuning.md) 옵션을 사용하거나 사용하지 않도록 설정합니다.

FORCE_LAST_GOOD_PLAN = { ON | **OFF** }     
켜기     
[!INCLUDE[ssde_md](../../includes/ssde_md.md)]은 새 SQL 계획이 성능 저하를 일으키는 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 쿼리에 마지막으로 성공한 계획을 자동으로 강제로 적용합니다. [!INCLUDE[ssde_md](../../includes/ssde_md.md)]는 강제 계획을 통해 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 쿼리의 쿼리 성능을 지속적으로 모니터링합니다.

성능이 향상되면 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]은 마지막으로 성공한 계획을 계속 사용합니다. 성능 향상이 검색되지 않으면 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]이 새 쿼리 계획을 생성합니다. 쿼리 저장소가 사용하도록 설정되지 않았거나 ‘읽기/쓰기’ 모드가 아닌 경우 문이 실패합니다.

OFF     
[!INCLUDE[ssde_md](../../includes/ssde_md.md)]은 [sys.dm_db_tuning_recommendations](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) 뷰에서 SQL 계획 변경으로 인한 잠재적인 쿼리 성능 저하를 보고합니다. 하지만 이러한 권장 사항은 자동으로 적용되지 않습니다. 사용자는 뷰에 표시된 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 스크립트를 적용하여 활성 권장 사항을 모니터링하고 확인된 문제를 해결할 수 있습니다. 기본값은 OFF입니다.

**\<change_tracking_option> ::=**      
**적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDSFull](../../includes/sssds-md.md)]

변경 내용 추적 옵션을 제어합니다. 변경 내용 추적을 설정 또는 해제하고 옵션을 설정 또는 변경할 수 있습니다. 예제는 이 문서의 뒷부분에 있는 “예제” 섹션을 참조하세요.

켜기     
데이터베이스에 변경 내용 추적을 설정합니다. 변경 내용 추적을 설정하면 AUTO CLEANUP 및 CHANGE RETENTION 옵션도 설정할 수 있습니다.

AUTO_CLEANUP = { ON | **OFF** }     
켜기     
지정된 보존 기간 후에 변경 내용 추적 정보가 자동으로 제거됩니다.

OFF     
변경 내용 추적 데이터는 데이터베이스에서 자동으로 제거되지 않습니다.

CHANGE_RETENTION = *retention_period* { **DAYS** | HOURS | MINUTES }     
데이터베이스에 변경 내용 추적 정보를 보존하는 최소 기간을 지정합니다. 데이터는 AUTO_CLEANUP 값이 ON일 때만 제거됩니다.

*retention_period*는 보존 기간의 숫자 부분을 지정하는 정수입니다.

기본 보존 기간은 **2일**입니다. 최소 보존 기간은 1분입니다. 기본 보존 형식은 **일**입니다.

OFF     
데이터베이스에서 변경 내용 추적을 해제합니다. 데이터베이스에서 변경 내용 추적을 사용 중지하려면 모든 테이블에서 변경 내용 추적을 사용하지 않도록 설정해야 합니다.

**\<containment_option> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 시작)

데이터베이스 포함 옵션을 제어합니다.

CONTAINMENT = { **NONE** | PARTIAL}     
없음     
데이터베이스가 포함된 데이터베이스가 아닙니다.

PARTIAL     
데이터베이스가 포함된 데이터베이스입니다. 데이터베이스에 복제, 변경 데이터 캡처 또는 변경 내용 추적을 사용하도록 설정되어 있는 경우 데이터베이스를 부분적으로 포함된 데이터베이스로 설정하면 실패합니다. 실패 후에는 오류 검사가 중지됩니다. 포함된 데이터베이스에 대한 자세한 내용은 [Contained Databases](../../relational-databases/databases/contained-databases.md)를 참조하십시오.

**\<cursor_option> ::=**     

커서 옵션을 제어합니다.

CURSOR_CLOSE_ON_COMMIT { ON | OFF }     
켜기     
트랜잭션을 커밋하거나 롤백할 때 열려 있는 커서가 모두 닫힙니다.

OFF     
트랜잭션 커밋 시에는 커서가 그대로 열려 있으나 트랜잭션 롤백 시에는 INSENSITIVE 또는 STATIC으로 정의된 것을 제외한 모든 커서가 닫힙니다.

SET 문을 사용하여 설정한 연결 수준 설정은 CURSOR_CLOSE_ON_COMMIT의 기본 데이터베이스 설정보다 우선적으로 적용됩니다. ODBC 및 OLE DB 클라이언트는 기본적으로 세션의 CURSOR_CLOSE_ON_COMMIT을 OFF로 설정하여 연결 수준 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET CURSOR_CLOSE_ON_COMMIT](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)을 참조하세요.

이 옵션의 상태는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_cursor_close_on_commit_on` 열 또는 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsCloseCursorsOnCommitEnabled` 속성을 검사하여 확인할 수 있습니다.

CURSOR_DEFAULT { LOCAL | GLOBAL }     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

커서 범위가 LOCAL인지 GLOBAL인지 여부를 제어합니다.

LOCAL     
LOCAL을 지정하고 커서를 만들 때 GLOBAL로 정의하지 않으면 커서 범위는 로컬로 적용됩니다. 특히 범위는 커서를 만든 일괄 처리, 저장 프로시저 또는 트리거에 로컬로 적용됩니다. 커서 이름은 그 범위 내에서만 유효합니다.

일괄 처리, 저장 프로시저, 트리거의 로컬 커서 변수 또는 저장 프로시저의 OUTPUT 매개 변수에서 커서를 참조할 수 있습니다. 커서는 일괄 처리, 저장 프로시저 또는 트리거가 종료될 때 암시적으로 할당이 취소됩니다. 또한 OUTPUT 매개 변수에서 다시 전달되지 않는 한 할당이 해제됩니다. 커서가 OUTPUT 매개 변수에서 다시 전달될 수 있습니다. 이 방법으로 커서가 다시 전달될 경우 커서를 참조하는 마지막 변수의 할당이 취소되거나 해당 변수가 범위를 벗어나면 커서의 할당이 취소됩니다.

GLOBAL     
GLOBAL을 지정하고 커서를 만들 때 LOCAL로 정의하지 않으면 커서의 범위는 연결에 전역으로 적용됩니다. 연결되어 실행하는 모든 저장 프로시저 또는 일괄 처리에서 커서 이름을 참조할 수 있습니다.

커서는 연결이 끊어질 때만 암시적으로 할당이 취소됩니다. 자세한 내용은 [DECLARE CURSOR](../../t-sql/language-elements/declare-cursor-transact-sql.md)를 참조하세요.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_local_cursor_default` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsLocalCursorsDefault` 속성을 검사하여 상태를 확인할 수도 있습니다.

**\<data_retention_policy> ::=**

**적용 대상**: Azure SQL Edge‘만’

DATA_RETENTION { ON | OFF }   
켜기    
데이터베이스에서 데이터 보존 정책 기반 정리를 사용하도록 설정합니다.

OFF   
데이터베이스에서 데이터 보존 정책 기반 정리를 사용하지 않도록 설정합니다.

**\<database_mirroring>**     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

인수에 대한 설명은 [ALTER DATABASE 데이터베이스 미러링](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)을 참조하세요.

**\<date_correlation_optimization_option> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

date_correlation_optimization 옵션을 제어합니다.

DATE_CORRELATION_OPTIMIZATION { ON | **OFF** }     
켜기     
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 FOREIGN KEY 제약 조건으로 데이터베이스의 두 테이블을 연결하고 해당 테이블에 **datetime** 열이 있는 상관 관계 통계를 유지 관리합니다.

OFF     
상관 관계 통계를 유지하지 않습니다.

DATE_CORRELATION_OPTIMIZATION을 ON으로 설정하려면 ALTER DATABASE 문을 실행하는 연결을 제외하고 데이터베이스에 대한 활성 연결이 없어야 합니다. 그런 후에는 여러 개의 연결이 지원됩니다.

이 옵션의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_date_correlation_on` 열을 검사하여 확인할 수 있습니다.

**\<db_encryption_option> ::=**      
데이터베이스 암호화 상태를 제어합니다.

ENCRYPTION { ON \| **OFF** \| SUSPEND \| RESUME }     
켜기     
데이터베이스를 암호화하도록 설정합니다.

OFF     
데이터베이스를 암호화하지 않도록 설정합니다.

SUSPEND     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작)     

투명한 데이터 암호화를 설정하거나 해제한 후 또는 암호화 키를 변경한 후 암호화 검사를 일시 중지할 수 있습니다.

RESUME     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작)

이전에 일시 중지한 암호화 검사를 다시 시작할 수 있습니다.

데이터베이스 암호화에 대한 자세한 내용은 [투명한 데이터 암호화](../../relational-databases/security/encryption/transparent-data-encryption.md) 및 [Azure SQL Database를 사용한 투명한 데이터 암호화](../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)를 참조하세요.

데이터베이스 수준에서 암호화를 사용할 수 있으면 모든 파일 그룹이 암호화됩니다. 새로운 파일 그룹은 암호화된 속성을 상속합니다. 데이터베이스의 파일 그룹이 READ ONLY로 설정되면 데이터베이스 암호화 작업이 실패합니다.

[sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 동적 관리 뷰를 사용하여 데이터베이스의 암호화 상태와 암호화 검사 상태를 확인할 수 있습니다.

**\<db_state_option> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

데이터베이스의 상태를 제어합니다.

OFFLINE     
데이터베이스가 닫히고 완전히 종료되어 오프라인 상태로 표시됩니다. 데이터베이스가 오프라인 상태인 동안에는 데이터베이스를 수정할 수 없습니다.

ONLINE     
데이터베이스가 열려 사용할 수 있게 됩니다.

EMERGENCY     
데이터베이스가 READ_ONLY로 표시되고 로깅이 비활성화되며 sysadmin 고정 서버 역할의 멤버로 액세스가 제한됩니다. EMERGENCY는 주로 문제 해결을 위해 사용됩니다. 예를 들어 손상된 로그 파일로 인해 주의 대상으로 표시된 데이터베이스를 EMERGENCY 상태로 설정할 수 있습니다. 이 설정을 사용하면 시스템 관리자가 읽기 전용으로 데이터베이스에 액세스할 수 있습니다. sysadmin 고정 서버 역할의 멤버만 데이터베이스를 EMERGENCY 상태로 설정할 수 있습니다.

데이터베이스를 오프라인 또는 비상 상태로 변경하려면 제목 데이터베이스에 대한 `ALTER DATABASE` 사용 권한과 데이터베이스를 오프라인에서 온라인으로 이동하려면 서버 수준 `ALTER ANY DATABASE` 사용 권한이 필요합니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `state`열과 `state_desc` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `Status` 속성을 검사하여 상태를 확인할 수도 있습니다. 자세한 내용은 [Database States](../../relational-databases/databases/database-states.md)을 참조하세요.

RESTORING으로 표시된 데이터베이스는 OFFLINE, ONLINE 또는 EMERGENCY로 설정할 수 없습니다. 활성 복원 작업 중이나 데이터베이스 또는 로그 파일의 복원 작업이 손상된 백업 파일로 인해 실패할 경우 데이터베이스가 RESTORING 상태일 수 있습니다.

**\<db_update_option> ::=**

데이터베이스에 대한 업데이트 허용 여부를 제어합니다.

READ_ONLY     
사용자는 데이터베이스에서 데이터를 읽을 수 있지만 수정은 할 수 없습니다.

> [!NOTE]
> 쿼리 성능을 향상시키려면 데이터베이스를 READ_ONLY로 설정하기 전에 통계를 업데이트하십시오. 데이터베이스를 READ_ONLY로 설정한 후에 추가 통계가 필요한 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 tempdb에 통계를 만듭니다. 읽기 전용 데이터베이스의 통계에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.

READ_WRITE     
데이터베이스에서 읽기와 쓰기 작업을 할 수 있습니다.

이 상태를 변경하려면 데이터베이스에 대해 배타적 액세스 권한이 있어야 합니다. 자세한 내용은 SINGLE_USER 절을 참조하십시오.

> [!NOTE]
> [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 페더레이션된 데이터베이스에서 `SET { READ_ONLY | READ_WRITE }`는 사용하지 않도록 설정됩니다.

**\<db_user_access_option> ::=**      
데이터베이스에 대한 사용자 액세스를 제어합니다.

SINGLE_USER     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

한 번에 한 사용자만 데이터베이스에 액세스할 수 있도록 지정합니다. SINGLE_USER를 지정하고 다른 사용자가 데이터베이스에 연결하면 모든 사용자가 지정된 데이터베이스에서 연결을 끊을 때까지 ALTER DATABASE 문이 차단됩니다. 이 동작을 재정의하려면 WITH \<termination> 절을 참조하세요.

옵션을 설정한 사용자가 로그아웃해도 데이터베이스는 단일 사용자 모드로 유지됩니다. 이때 다른 한 명의 사용자만 데이터베이스에 연결할 수 있습니다.

데이터베이스를 SINGLE_USER로 설정하기 전에 AUTO_UPDATE_STATISTICS_ASYNC 옵션이 OFF로 설정되어 있는지 확인합니다. 이 옵션이 ON으로 설정되면 통계 업데이트에 사용되는 백그라운드 스레드가 데이터베이스에 대한 연결을 점유하므로 단일 사용자 모드로 데이터베이스에 액세스할 수 없습니다. 이 옵션의 상태를 보려면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_auto_update_stats_async_on` 열을 쿼리합니다. 옵션이 ON으로 설정되어 있으면 다음 태스크를 수행합니다.

1. AUTO_UPDATE_STATISTICS_ASYNC를 OFF로 설정합니다.

2. [sys.dm_exec_background_job_queue](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md) 동적 관리 뷰를 쿼리하여 활성 비동기 통계 작업을 검사합니다.

활성 작업이 있을 경우 [KILL STATS JOB](../../t-sql/language-elements/kill-stats-job-transact-sql.md)을 사용하여 해당 작업을 완료하도록 허용하거나 수동으로 종료합니다.

RESTRICTED_USER     
`db_owner` 고정 데이터베이스 역할 및 `dbcreator`와 `sysadmin` 고정 서버 역할의 멤버만 데이터베이스에 연결할 수 있습니다. RESTRICTED_USER는 연결되는 수를 제한하지 않습니다. ALTER DATABASE 문의 termination 절에 지정된 기간을 사용하여 데이터베이스에 대한 모든 연결을 끊습니다. 데이터베이스가 RESTRICTED_USER 상태로 바뀐 후 자격이 없는 사용자의 연결 시도는 거부됩니다.

MULTI_USER     
데이터베이스에 연결할 수 있는 적절한 권한이 있는 모든 사용자의 연결을 허용합니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `user_access` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `UserAccess` 속성을 검사하여 상태를 확인할 수도 있습니다.

**\<delayed_durability_option> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 시작)

트랜잭션이 완전한 내구성이 있게 커밋될지 아니면 지연된 내구성이 있게 커밋될지 제어합니다.

DISABLED     
`SET DISABLED` 다음의 모든 트랜잭션은 완전한 내구성이 있습니다. ATOMIC 블록이나 COMMIT 문에 설정된 내구성 옵션은 무시됩니다.

ALLOWED     
`SET ALLOWED` 다음의 모든 트랜잭션은 ATOMIC 블록이나 COMMIT 문에 설정된 내구성 옵션에 따라 완전한 내구성이 있거나 지연된 내구성이 있습니다.

FORCED     
`SET FORCED` 다음의 모든 트랜잭션은 지연된 내구성이 있습니다. ATOMIC 블록이나 COMMIT 문에 설정된 내구성 옵션은 무시됩니다.

**\<external_access_option> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

다른 데이터베이스의 개체와 같은 외부 리소스에서 데이터베이스에 액세스할 수 있는지 여부를 제어합니다.

DB_CHAINING { ON | **OFF** }     
켜기     
데이터베이스가 데이터베이스 간 소유권 체인의 원본이나 대상이 될 수 있습니다.

OFF     
데이터베이스가 데이터베이스 간 소유권 체인에 참여할 수 없습니다.

> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 cross db ownership chaining 서버 옵션이 0(OFF)일 때 이 설정을 인식할 수 있습니다. cross db ownership chaining이 1(ON)이면 모든 사용자 데이터베이스는 이 옵션 값에 관계없이 데이터베이스 간 소유권 체인에 참여할 수 있습니다. 이 옵션은 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용하여 설정합니다.

이 옵션을 설정하려면 데이터베이스에 대한 `CONTROL SERVER` 권한이 필요합니다.

DB_CHAINING 옵션은 master, model 및 tempdb 시스템 데이터베이스에서는 설정할 수 없습니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_db_chaining_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다.

TRUSTWORTHY { ON | **OFF** }     
켜기     
가장 컨텍스트를 사용하는 데이터베이스 모듈(예: 사용자 정의 함수 또는 저장 프로시저)이 데이터베이스 외부의 리소스에 액세스할 수 있습니다.

OFF     
가장 컨텍스트의 데이터베이스 모듈이 데이터베이스 외부 리소스에 액세스할 수 없습니다.

TRUSTWORTHY는 데이터베이스가 연결될 때마다 OFF로 설정됩니다.

기본적으로 msdb 데이터베이스를 제외한 모든 시스템 데이터베이스는 TRUSTWORTHY가 OFF로 설정되어 있습니다. model 및 tempdb 데이터베이스에 대해서는 이 값을 변경할 수 없습니다. master 데이터베이스의 경우 TRUSTWORTHY 옵션을 ON으로 설정하지 않는 것이 좋습니다.

이 옵션을 설정하려면 데이터베이스에 대한 `CONTROL SERVER` 권한이 필요합니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_trustworthy_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다.

DEFAULT_FULLTEXT_LANGUAGE     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 시작)

전체 텍스트 인덱싱된 열에 대한 기본 언어 값을 지정합니다.

> [!IMPORTANT]
> 이 옵션은 CONTAINMENT가 PARTIAL로 설정된 경우에만 사용할 수 있습니다. CONTAINMENT가 NONE으로 설정되어 있으면 오류가 발생합니다.

DEFAULT_LANGUAGE     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 시작)

새로 생성된 모든 로그인에 대한 기본 언어를 지정합니다. LCID(로컬 ID), 언어 이름 또는 언어 별칭을 제공하여 언어를 지정할 수 있습니다. 사용 가능한 언어 이름 및 별칭 목록은 [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)를 참조하세요. 이 옵션은 CONTAINMENT가 PARTIAL로 설정된 경우에만 사용할 수 있습니다. CONTAINMENT가 NONE으로 설정되어 있으면 오류가 발생합니다.

NESTED_TRIGGERS     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 시작)

AFTER 트리거의 중첩(한 트리거가 다른 트리거를 시작하는 과정이 반복되는 동작) 여부를 지정합니다. 이 옵션은 CONTAINMENT가 PARTIAL로 설정된 경우에만 사용할 수 있습니다. CONTAINMENT가 NONE으로 설정되어 있으면 오류가 발생합니다.

TRANSFORM_NOISE_WORDS     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 시작)

의미 없는 단어 또는 중지 단어로 인해 전체 텍스트 쿼리에 대한 부울 연산이 실패할 경우 오류 메시지를 표시하지 않는 데 사용됩니다. 이 옵션은 CONTAINMENT가 PARTIAL로 설정된 경우에만 사용할 수 있습니다. CONTAINMENT가 NONE으로 설정되어 있으면 오류가 발생합니다.

TWO_DIGIT_YEAR_CUTOFF     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 시작)

두 자리 연도를 네 자리 연도로 해석하기 위한 구분 연도를 나타내는 1753에서 9999까지의 정수를 지정합니다. 이 옵션은 CONTAINMENT가 PARTIAL로 설정된 경우에만 사용할 수 있습니다. CONTAINMENT가 NONE으로 설정되어 있으면 오류가 발생합니다.

**\<FILESTREAM_option> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 시작)

FileTable에 대한 설정을 제어합니다.

NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL }     
OFF     
FileTable 데이터에 대한 비트랜잭션 액세스를 사용하지 않도록 설정합니다.

READ_ONLY     
비트랜잭션 프로세스에서 이 데이터베이스의 FileTable에 있는 FILESTREAM 데이터를 읽을 수 있습니다.

FULL     
FileTable의 FILESTREAM 데이터에 대한 전체 비트랜잭션 액세스를 사용하도록 설정합니다.

DIRECTORY_NAME = *\<directory_name>*      
Windows 호환 디렉터리 이름입니다. 이 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 데이터베이스 수준 디렉터리 이름 중에서 고유해야 합니다. 고유성을 비교할 때는 데이터 정렬 설정과 관계없이 대/소문자가 구분되지 않습니다. 데이터베이스에 FileTable을 만들기 전에 이 옵션을 설정해야 합니다.

**\<HADR_options> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

[ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)을 참조하세요.

**\<mixed_page_allocation_option> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 시작)

데이터베이스가 테이블이나 인덱스의 첫 8페이지에 대해 혼합 익스텐트를 사용하여 초기 페이지를 만들 수 있는지 여부를 제어합니다.

MIXED_PAGE_ALLOCATION { OFF | **ON** }     
OFF     
데이터베이스는 항상 단일 익스텐트를 사용하여 초기 페이지를 만듭니다. OFF가 기본값입니다.

켜기     
데이터베이스는 혼합 익스텐트를 사용하여 초기 페이지를 만들 수 있습니다.

이 설정은 모든 시스템 데이터베이스에 대해 ON입니다. **tempdb**는 OFF를 지원하는 유일한 시스템 데이터베이스입니다.

**\<PARAMETERIZATION_option> ::=**      
매개 변수화 옵션을 제어합니다. 매개 변수화에 대한 자세한 내용은 [쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md#SimpleParam)를 참조하세요.

PARAMETERIZATION { **SIMPLE** | FORCED }     
SIMPLE     
데이터베이스의 기본 동작에 따라 쿼리를 매개 변수화합니다.

FORCED     
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스의 모든 쿼리를 매개 변수화합니다.

이 옵션의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_parameterization_forced column` 열을 검사하여 확인할 수 있습니다.

<a name="query-store"></a> **\<query_store_options> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 시작)

ON | **OFF** [ FORCED ] | CLEAR [ ALL ]     
이 데이터베이스에서 쿼리 저장소를 사용할 수 있는지 여부를 제어하고, 쿼리 저장소의 내용 제거도 제어합니다. 자세한 내용은 [쿼리 스토리지 사용 시나리오](../../relational-databases/performance/query-store-usage-scenarios.md)를 참조하세요.

켜기     
쿼리 저장소를 사용하도록 설정합니다.

OFF      
쿼리 저장소를 사용하지 않도록 합니다. OFF가 기본값입니다. FORCED는 선택 사항입니다. FORCED는 실행 중인 모든 쿼리 저장소 백그라운드 태스크를 중단하고, 쿼리 저장소가 해제된 경우 동기 플러시를 건너뜁니다. 쿼리 저장소가 최대한 빨리 종료되도록 합니다. FORCED가 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CU6 이상 빌드에 적용됩니다.

> [!NOTE]  
> 쿼리 저장소는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 단일 데이터베이스 및 탄력적 풀에서 사용하지 않도록 설정할 수 없습니다. `ALTER DATABASE [database] SET QUERY_STORE = OFF`를 실행하면 경고 `'QUERY_STORE=OFF' is not supported in this version of SQL Server.`가 반환됩니다. 

CLEAR     
쿼리 저장소에서 쿼리 관련 데이터를 제거합니다. ALL은 선택 사항입니다. ALL은 쿼리 저장소에서 쿼리 관련 데이터와 메타데이터를 제거합니다.

OPERATION_MODE { READ_ONLY | READ_WRITE }     
쿼리 저장소의 작업 모드를 설명합니다.

READ_WRITE     
쿼리 저장소는 쿼리 계획 및 런타임 실행 통계 정보를 수집하고 유지합니다.

READ_ONLY     
쿼리 저장소에서 정보를 읽을 수 있지만 새 정보는 추가되지 않습니다. 쿼리 저장소의 최대 발급 공간이 최대값에 도달하면 쿼리 저장소는 작업 모드를 READ_ONLY로 변경합니다.

CLEANUP_POLICY     
쿼리 저장소의 데이터 보존 정책을 설명합니다. STALE_QUERY_THRESHOLD_DAYS는 쿼리에 대한 정보가 쿼리 저장소에 보존되는 일 수를 결정합니다. STALE_QUERY_THRESHOLD_DAYS는 **bigint** 형식입니다. 기본값은 30입니다.

DATA_FLUSH_INTERVAL_SECONDS     
쿼리 저장소에 기록된 데이터가 디스크에 유지되는 빈도를 결정합니다. 성능 최적화를 위해 쿼리 저장소에서 수집한 데이터는 디스크에 비동기적으로 기록됩니다. 비동기 전송이 발생하는 빈도는 DATA_FLUSH_INTERVAL_SECONDS 인수를 사용하여 구성됩니다. DATA_FLUSH_INTERVAL_SECONDS는 **bigint** 형식입니다. 기본값은 **900**(15분)입니다.

MAX_STORAGE_SIZE_MB     
쿼리 저장소에 발급되는 공간을 결정합니다. MAX_STORAGE_SIZE_MB는 **bigint** 형식입니다. 기본값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 경우 **100MB**입니다([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]까지). [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 기본값은 **1GB**입니다.

> [!NOTE]
> `MAX_STORAGE_SIZE_MB` 한도는 엄격하게 적용되지 않습니다. 쿼리 저장소가 디스크에 데이터를 쓰는 경우에만 스토리지 크기가 확인됩니다. 이 간격은 `DATA_FLUSH_INTERVAL_SECONDS` 옵션 또는 [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 쿼리 저장소 대화 상자 옵션 **데이터 플러시 간격**에서 설정됩니다. 간격 기본값은 900초, 즉 15분입니다.
> 쿼리 저장소가 스토리지 크기 검사 간에 `MAX_STORAGE_SIZE_MB` 한도를 위반할 경우 읽기 전용 모드로 전환됩니다. `SIZE_BASED_CLEANUP_MODE`가 사용하도록 설정된 경우 `MAX_STORAGE_SIZE_MB` 한도를 적용하는 정리 메커니즘도 트리거됩니다.
> 충분한 공간이 확보되면 쿼리 저장소 모드가 자동으로 읽기/쓰기로 다시 전환됩니다.

> [!IMPORTANT]
> 워크로드 캡처에 10GB 이상의 디스크 공간이 필요하다고 생각되는 경우 워크로드를 재고하여 쿼리 계획을 다시 사용하도록 최적화하는 것이 좋습니다. 예를 들어 [강제 매개 변수화](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)를 사용하거나 쿼리 저장소 구성을 조정할 수 있습니다.    
> [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 쿼리 캡처 정책에 대한 추가 제어를 위해 `QUERY_CAPTURE_MODE`을 CUSTOM으로 설정할 수 있습니다.

INTERVAL_LENGTH_MINUTES     
런타임 실행 통계 데이터가 쿼리 저장소로 집계되는 간격을 결정합니다. 공간 사용을 최적화하기 위해 런타임 통계 저장소의 런타임 실행 통계는 고정된 시간 창을 통해 집계됩니다. 고정된 시간 창은 INTERVAL_LENGTH_MINUTES 인수를 사용하여 구성됩니다. INTERVAL_LENGTH_MINUTES는 **bigint** 형식입니다. 기본값은 **60**입니다.

SIZE_BASED_CLEANUP_MODE { **AUTO** | OFF }     
총 데이터양이 최대 크기에 가까워지면 정리를 자동으로 활성화할지 여부를 제어합니다.

AUTO     
디스크의 크기가 **MAX_STORAGE_SIZE_MB**의 90%에 도달하면 크기 기반 정리가 자동으로 활성화됩니다. 크기 기반 정리는 가장 저렴하고 가장 오래된 쿼리를 먼저 제거합니다. **MAX_STORAGE_SIZE_MB**가 약 80%가 되면 멈춥니다. 이 값은 기본 구성 값입니다.

OFF     
크기 기반 정리가 자동으로 활성화되지 않습니다.

SIZE_BASED_CLEANUP_MODE는 **nvarchar** 형식입니다.

QUERY_CAPTURE_MODE { ALL \| AUTO \| CUSTOM \| NONE }     
현재 활성 쿼리 캡처 모드를 지정합니다. 각 모드는 특정 쿼리 캡처 정책을 정의합니다.

> [!NOTE]
> 쿼리 캡처 모드를 모두, 자동 또는 사용자 지정으로 설정하면 커서, 저장 프로시저 내부 쿼리 및 고유하게 컴파일된 쿼리가 항상 캡처됩니다.

ALL     
쿼리를 모두 캡처합니다. **ALL**은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 통한 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])의 기본 구성 값입니다.

AUTO     
실행 횟수 및 리소스 사용을 기반으로 관련 쿼리를 캡처합니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에서 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]의 기본 구성 값입니다.

없음     
새 쿼리 캡처를 중지합니다. 쿼리 저장소는 이미 캡처된 쿼리에 대한 컴파일 및 런타임 통계를 계속 수집합니다. 중요한 쿼리 캡처를 놓칠 수 있으므로 이 구성은 주의해서 사용해야 합니다.

CUSTOM     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작)

QUERY_CAPTURE_POLICY 옵션에 대해 제어할 수 있습니다.

QUERY_CAPTURE_MODE는 **nvarchar** 형식입니다. 

max_plans_per_query     
각 쿼리에 대해 유지 관리되는 최대 계획 수를 정의합니다. MAX_PLANS_PER_QUERY는 **int** 형식입니다. 기본값은 **200**입니다.

WAIT_STATS_CAPTURE_MODE { **ON** | OFF }     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 시작))

쿼리별 대기 통계를 캡처할지 여부를 제어합니다.

켜기    
쿼리별 대기 통계 정보를 캡처합니다. 이 값은 기본 구성 값입니다.

OFF    
쿼리별 대기 통계 정보를 캡처하지 않습니다.

**\<query_capture_policy_option_list> :: =**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작)

쿼리 저장소 캡처 정책 옵션을 제어합니다. STALE_CAPTURE_POLICY_THRESHOLD를 제외하고 이 옵션은 정의된 부실 캡처 정책 임계값에 캡처해야 할 쿼리에 대해 수행해야 할 OR 조건을 정의합니다.

STALE_CAPTURE_POLICY_THRESHOLD = *number* { DAYS | HOURS }     
쿼리가 캡처되어야 하는지 여부를 결정하는 평가 간격 기간을 정의합니다. 기본값은 1일이며 1시간에서 7일까지 설정할 수 있습니다. *number*는 **int** 형식입니다.

EXECUTION_COUNT     
평가 기간 동안 쿼리가 실행되는 횟수를 정의합니다. 기본값은 30으로, 기본 부실 캡처 정책 임계값의 경우 쿼리가 쿼리 저장소에 유지되려면 하루에 30회 이상 실행되어야 합니다. EXECUTION_COUNT는 **int** 형식입니다.

TOTAL_COMPILE_CPU_TIME_MS     
평가 기간 동안 쿼리에 사용하는 총 경과 컴파일 CPU 시간을 정의합니다. 기본값은 1000으로, 기본 부실 캡처 정책 임계값의 경우 쿼리가 쿼리 저장소에 유지되려면 하루에 쿼리 컴파일에 사용된 총 CPU 시간이 1초 이상이어야 합니다. TOTAL_COMPILE_CPU_TIME_MS는 **int** 형식입니다.

TOTAL_EXECUTION_CPU_TIME_MS     
평가 기간 동안 쿼리에 사용하는 총 경과 실행 CPU 시간을 정의합니다. 기본값은 100으로, 기본 부실 캡처 정책 임계값의 경우 쿼리가 쿼리 저장소에 유지되려면 하루에 실행에 사용된 총 CPU 시간이 100ms 이상이어야 합니다. TOTAL_EXECUTION_CPU_TIME_MS는 **int** 형식입니다.

**\<recovery_option> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

데이터베이스 복구 옵션과 디스크 I/O 오류 검사를 제어합니다.

FULL     
미디어 오류가 발생한 후에는 트랜잭션 로그 백업을 사용하여 전체 복구를 제공합니다. 데이터 파일이 손상된 경우 미디어 복구 기능을 통해 모든 커밋된 트랜잭션을 복원할 수 있습니다. 자세한 내용은 [복구 모델](../../relational-databases/backup-restore/recovery-models-sql-server.md)을 참조하세요.

BULK_LOGGED     
미디어 오류가 발생한 후 복구를 제공합니다. 특정 대규모 또는 대량 작업에 대해 성능을 최적화하고 로그 공간 사용을 최소화합니다. 최소 로깅이 가능한 작업에 대한 자세한 내용은 [트랜잭션 로그](../../relational-databases/logs/the-transaction-log-sql-server.md)를 참조하세요. BULK_LOGGED 복구 모델에서는 이러한 작업에 대해서 최소 로깅이 사용됩니다. 자세한 내용은 [복구 모델](../../relational-databases/backup-restore/recovery-models-sql-server.md)을 참조하세요.

SIMPLE     
최소 로그 공간을 사용하는 단순 백업 전략을 제공합니다. 서버 오류 복구에 더 이상 필요 없는 로그 공간은 자동으로 재사용됩니다. 자세한 내용은 [복구 모델](../../relational-databases/backup-restore/recovery-models-sql-server.md)을 참조하세요.

> [!IMPORTANT]
> 단순 복구 모델은 다른 두 모델보다 관리하기는 쉽지만 데이터 파일이 손상된 경우 데이터 손실 위험은 더 큽니다. 최신 데이터베이스 또는 차등 데이터베이스 백업이 손실된 이후의 변경 사항은 모두 수동으로 다시 입력해야 합니다.

기본 복구 모델은 **model** 데이터베이스의 복구 모델에 의해 결정됩니다. 적절한 복구 모델을 선택하는 방법에 대한 자세한 내용은 [복구 모델](../../relational-databases/backup-restore/recovery-models-sql-server.md)을 참조하세요.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 **recovery_model** 및 **recovery_model_desc** 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `Recovery` 속성을 검사하여 상태를 확인할 수도 있습니다.

TORN_PAGE_DETECTION { ON | **OFF** }     
켜기     
[!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 완료되지 않은 페이지를 검색할 수 있습니다.

OFF     
[!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 완료되지 않은 페이지를 검색할 수 없습니다.

> [!IMPORTANT]
> TORN_PAGE_DETECTION ON | OFF 구문 구조는 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 제거될 예정입니다. 새 개발 작업에서는 이 구문 구조를 사용하지 않도록 하고 현재 이 구문 구조를 사용하는 애플리케이션은 수정하십시오. 대신 PAGE_VERIFY 옵션을 사용하십시오.

<a name="page_verify"></a> PAGE_VERIFY { **CHECKSUM** | TORN_PAGE_DETECTION | NONE }     
디스크 I/O 경로 오류로 인해 손상된 데이터베이스 페이지를 찾습니다. Disk I/O 경로 오류로 인해 데이터베이스 손상 문제가 발생할 수 있습니다. 이 오류는 대부분 페이지를 디스크에 쓸 때 전원 오류나 디스크 하드웨어 오류로 인해 발생합니다.

CHECKSUM     
페이지를 디스크에 쓸 때 전체 페이지의 내용에 대한 체크섬을 계산하고 이 값을 페이지 헤더에 저장합니다. 디스크에서 페이지를 읽으면 체크섬이 다시 계산되어 페이지 헤더에 저장된 체크섬 값과 비교됩니다. 두 값이 일치하지 않으면 체크섬 오류를 나타내는 824 오류 메시지가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 Windows 이벤트 로그에 보고됩니다. 체크섬 오류는 I/O 경로 문제를 나타냅니다. 오류에 대한 근본 원인을 확인하려면 하드웨어, 펌웨어 드라이버, BIOS, 필터 드라이버(예: 바이러스 소프트웨어) 및 기타 I/O 경로 구성 요소를 조사해야 합니다.

TORN_PAGE_DETECTION     
페이지를 디스크에 쓸 때 8KB 데이터베이스 페이지의 각 512바이트 섹터에 대해 특정 2비트 패턴을 데이터베이스 페이지 헤더에 저장합니다. 디스크에서 페이지를 읽으면 페이지 헤더에 저장된 조각난 비트가 실제 페이지 섹터 정보와 비교됩니다.

값이 일치하지 않으면 페이지의 일부분만 디스크에 쓰여졌음을 의미합니다. 이 경우 조각난 페이지 오류를 나타내는 824 오류 메시지가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 Windows 이벤트 로그에 보고됩니다. 조각난 페이지가 실제로 쓰기가 완료되지 않은 페이지인 경우 조각난 페이지는 보통 데이터베이스 복구에서 검색됩니다. 그러나 다른 I/O 경로 오류도 언제든 조각난 페이지의 원인이 될 수 있습니다.

없음     
데이터베이스 페이지 쓰기에서 CHECKSUM 또는 TORN_PAGE_DETECTION 값을 생성하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 페이지 헤더에 CHECKSUM 또는 TORN_PAGE_DETECTION 값이 있는 경우에도 읽기 중 체크섬이나 조각난 페이지를 확인하지 않습니다.

PAGE_VERIFY 옵션을 사용하는 경우 다음 중요 사항을 고려하십시오.

- 기본값은 **CHECKSUM**입니다.
- 사용자 또는 시스템 데이터베이스를 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전으로 업그레이드하는 경우 PAGE_VERIFY 값(NONE 또는 TORN_PAGE_DETECTION)이 유지됩니다. CHECKSUM으로 변경하는 것이 좋습니다.

    > [!NOTE]
    > 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 TempDB 데이터베이스의 PAGE_VERIFY 데이터베이스 옵션이 NONE으로 설정되며 수정할 수 없습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 새로 설치한 경우 TempDB 데이터베이스의 기본값은 CHECKSUM입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치를 업그레이드하면 기본값이 NONE으로 유지됩니다. 이 옵션은 수정할 수 없습니다. tempdb 데이터베이스에는 CHECKSUM을 사용하는 것이 좋습니다.

- TORN_PAGE_DETECTION은 리소스는 덜 사용하지만 CHECKSUM 보호를 최소한으로 제공합니다.
- PAGE_VERIFY는 데이터베이스를 잠그거나 오프라인으로 설정하지 않고 즉, 데이터베이스의 동시성을 방해하지 않고 설정할 수 있습니다.
- CHECKSUM과 TORN_PAGE_DETECTION은 상호 배타적이므로 두 옵션을 동시에 사용할 수 없습니다.

조각난 페이지나 체크섬 오류가 검색되면 데이터를 복원하거나 오류가 인덱스 페이지에만 해당되는 경우 인덱스를 다시 작성하여 복구할 수 있습니다. 체크섬 오류가 발생하면 DBCC CHECKDB를 실행하여 이 오류의 영향을 받는 데이터베이스 페이지의 형식 또는 페이지를 확인할 수 있습니다. 복원 옵션에 대한 자세한 내용은 [RESTORE 인수](../../t-sql/statements/restore-statements-arguments-transact-sql.md)를 참조하세요. 데이터를 복원하면 데이터 손상 문제를 해결할 수 있지만 오류가 계속 발생하지 않도록 하려면 하드웨어 오류 등의 근본 원인을 진단하여 수정해야 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 체크섬, 조각난 페이지 또는 기타 I/O 오류로 읽기가 실패할 경우 4번 다시 시도합니다. 다시 시도 중에 한 번이라도 읽기가 성공하면 오류 로그에 메시지가 기록됩니다. 해당 읽기를 트리거한 명령이 계속 진행됩니다. 다시 시도가 실패하면 824 오류 메시지와 함께 명령이 실패합니다.

823, 824 및 825 오류 메시지에 대한 자세한 내용은 다음을 참조하세요.

- [SQL Server에서 메시지 823 오류 문제를 해결하는 방법](https://support.microsoft.com/help/2015755)
- [SQL Server에서 메시지 824 문제를 해결하는 방법](https://support.microsoft.com/help/2015756)
- [메시지 - 읽기 다시 시도 문제를 해결하는 방법](https://support.microsoft.com/help/2015757)

이 옵션의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `page_verify_option` 열이나 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsTornPageDetectionEnabled` 속성을 검사하여 확인할 수 있습니다.

**\<remote_data_archive_option> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 시작)

데이터베이스에 Stretch Database를 사용하거나 사용하지 않도록 설정합니다. 자세한 내용은 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하십시오.

REMOTE_DATA_ARCHIVE = { ON ( SERVER = \<server_name> , { CREDENTIAL = \<db_scoped_credential_name> \| FEDERATED_SERVICE_ACCOUNT = ON \| OFF } )\| **OFF**     
켜기     
데이터베이스에 Stretch Database를 사용하도록 설정합니다. 추가 필수 구성 요소를 비롯한 자세한 내용은 [데이터베이스에서 Stretch Database 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)를 참조하세요.

테이블 Stretch Database를 활성화하려면 `db_owner` 권한이 필요합니다. 데이터베이스 Stretch Database를 활성화하려면 `db_owner` 및 `CONTROL DATABASE` 권한이 필요합니다.

SERVER = \<server_name>     
Azure 서버의 주소를 지정합니다. 이름의 `.database.windows.net` 부분을 포함합니다. 예들 들어 `MyStretchDatabaseServer.database.windows.net`입니다.

CREDENTIAL = \<db_scoped_credential_name>     
Azure 서버에 연결하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 사용하는 데이터베이스 범위 자격 증명을 지정합니다. 이 명령을 실행하기 전에 자격 증명이 있는지 확인해야 합니다. 자세한 내용은 [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)을 참조하세요.

FEDERATED_SERVICE_ACCOUNT = { ON | OFF }     
다음 조건이 모두 참인 경우 원격 Azure 서버와 통신하기 위해 온-프레미스 SQL Server용 페더레이션된 서비스 계정을 사용할 수 있습니다.

- SQL Server 인스턴스를 실행하는 서비스 계정은 도메인 계정입니다.
- 이 도메인 계정은 Active Directory가 Azure Active Directory와 페더레이션된 도메인에 속합니다.
- 원격 Azure 서버는 Azure Active Directory 인증을 지원하도록 구성됩니다.
- SQL Server 인스턴스를 실행하는 서비스 계정은 원격 Azure 서버에서 `dbmanager` 또는 `sysadmin` 계정으로 구성되어야 합니다.

페더레이션된 서비스 계정을 ON으로 지정하면 CREDENTIAL 인수도 지정할 수 없습니다. OFF를 지정하면 CREDENTIAL 인수를 제공합니다.

OFF     
데이터베이스에 Stretch Database를 사용하지 않도록 설정합니다. 자세한 내용은 [Stretch Database 비활성화 및 원격 데이터 다시 가져오기](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)를 사용하세요.

Stretch Database를 사용하도록 설정된 테이블이 데이터베이스에 더 이상 포함되어 있지 않은 경우에만 데이터베이스에 Stretch Database를 사용하지 않도록 설정할 수 있습니다. Stretch Database를 사용하지 않도록 설정한 후 데이터 마이그레이션이 중지합니다. 또한 쿼리 결과에 원격 테이블의 결과가 더 이상 포함되지 않습니다.

Stretch를 사용하지 않도록 설정해도 원격 데이터베이스는 제거되지 않습니다. 원격 데이터베이스를 삭제하려면 Azure Portal을 사용하여 삭제해야 합니다.

**\<service_broker_option> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

메시지 배달을 사용 또는 사용하지 않도록 설정하거나, 새 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자를 설정하거나, 대화 우선 순위를 ON 또는 OFF로 설정하는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 옵션을 제어합니다.

ENABLE_BROKER     
지정된 데이터베이스에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용할 수 있도록 지정합니다. 메시지 배달이 시작되고 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰에서 is_broker_enabled 플래그가 true로 설정됩니다. 데이터베이스에 기존 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자가 유지됩니다. 데이터베이스가 데이터베이스 미러링 구성에서 보안 주체인 경우에는 Service Broker를 사용할 수 없습니다.

> [!NOTE]
> ENABLE_BROKER를 사용하려면 배타적 데이터베이스 잠금이 필요합니다. 다른 세션이 데이터베이스의 리소스를 잠근 경우 ENABLE_BROKER는 다른 세션이 해당 잠금을 해제할 때까지 기다립니다. 사용자 데이터베이스에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용하도록 설정하려면 데이터베이스를 단일 사용자 모드로 설정하는 등의 방법으로 데이터베이스가 다른 세션에 의해 사용되지 않도록 한 다음 ALTER DATABASE SET ENABLE_BROKER 문을 실행합니다. msdb 데이터베이스에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용하도록 설정하려면 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 중지하여 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서 필요한 잠금을 획득할 수 있도록 합니다.

DISABLE_BROKER     
지정된 데이터베이스에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용하지 않도록 지정합니다. 메시지 배달이 중지되고 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰에서 is_broker_enabled 플래그가 false로 설정됩니다. 데이터베이스에 기존 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자가 유지됩니다.

NEW_BROKER     
데이터베이스가 새 Broker 식별자를 받도록 지정합니다. 데이터베이스가 Service Broker 역할을 수행합니다. 데이터베이스 내의 모든 기존 대화는 종료 대화 메시지 없이 즉시 제거됩니다. 이전 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자를 참조하는 경로는 새 식별자로 다시 만들어야 합니다.

ERROR_BROKER_CONVERSATIONS     
[!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 배달을 사용하도록 지정합니다. 이 설정을 적용하면 데이터베이스에 대한 기존 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자가 유지됩니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 오류가 있는 데이터베이스의 모든 대화를 종료합니다. 이 설정을 적용하면 애플리케이션에서 기존 대화에 대해 주기적인 정리 작업을 실행할 수 있습니다.

HONOR_BROKER_PRIORITY {ON | OFF}     
켜기     
보내기 작업에서 대화에 할당된 우선 순위 수준을 고려합니다. 우선 순위 수준이 높은 대화의 메시지는 우선 순위 수준이 낮은 대화의 메시지보다 먼저 전송됩니다.

OFF     
모든 대화에 기본 우선 순위 수준이 할당된 것으로 간주하고 보내기 작업이 실행됩니다.

HONOR_BROKER_PRIORITY 옵션의 변경 내용은 전송 대기 중인 메시지가 없는 대화 또는 새 대화에 즉시 적용됩니다. ALTER DATABASE가 실행될 때 대화에 전송할 메시지가 있는 경우에는 대화의 일부 메시지가 전송될 때까지 새 설정이 적용되지 않습니다. 모든 대화에 새 설정이 적용되는 데 걸리는 시간은 상황에 따라 크게 다를 수 있습니다.

이 속성의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_broker_priority_honored` 열에 보고됩니다.

**\<snapshot_option> ::=**      
트랜잭션 격리 수준을 계산합니다.

ALLOW_SNAPSHOT_ISOLATION { ON | **OFF** }     
켜기     
데이터베이스 수준에서 스냅샷 옵션을 사용하도록 설정합니다. 이 옵션을 사용하면 트랜잭션에서 스냅샷 격리를 사용하지 않는 경우에도 DML 문에서 행 버전을 생성하기 시작합니다. 이 옵션을 사용하도록 설정하면 트랜잭션에서 SNAPSHOT 트랜잭션 격리 수준을 지정할 수 있습니다. 트랜잭션이 SNAPSHOT 격리 수준에서 실행되면 모든 문에서 트랜잭션 시작 시점의 상태로 데이터 스냅샷을 봅니다. SNAPSHOT 격리 수준에서 실행되는 트랜잭션이 여러 데이터베이스의 데이터에 액세스할 경우 모든 데이터베이스에서 ALLOW_SNAPSHOT_ISOLATION이 ON으로 설정되어 있어야 합니다. 그렇지 않고 ALLOW_SNAPSHOT_ISOLATION이 OFF로 설정된 경우에는 트랜잭션 내의 각 문에서는 FROM 절의 참조에서 데이터베이스의 테이블에 대한 잠금 힌트를 사용해야 합니다.

OFF     
데이터베이스 수준에서 스냅샷 옵션을 해제합니다. 트랜잭션을 SNAPSHOT 트랜잭션 격리 수준으로 지정할 수 없습니다.

ALLOW_SNAPSHOT_ISOLATION을 새 상태로 설정하는 경우(ON에서 OFF로 또는 OFF에서 ON으로) ALTER DATABASE는 데이터베이스 내의 기존 트랜잭션이 모두 커밋될 때까지 호출자에게 제어권을 반환하지 않습니다. 데이터베이스가 이미 ALTER DATABASE 문에 지정된 상태인 경우 제어권은 호출자에게 즉시 반환됩니다. ALTER DATABASE 문이 제어권을 빨리 반환하지 않는 경우 [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md)를 사용하여 장기 트랜잭션이 있는지 여부를 확인합니다. ALTER DATABASE 문을 취소하면 데이터베이스는 ALTER DATABASE가 시작된 시점의 상태로 남게 됩니다. [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰는 데이터베이스에 있는 스냅샷 격리 트랜잭션의 상태를 나타냅니다. **snapshot_isolation_state_desc** = IN_TRANSITION_TO_ON인 경우 ALTER DATABASE ALLOW_SNAPSHOT_ISOLATION을 OFF로 설정하는 작업은 6초간 일시 중지된 다음, 다시 시도됩니다.

데이터베이스가 OFFLINE인 경우 ALLOW_SNAPSHOT_ISOLATION의 상태를 변경할 수 없습니다.

READ_ONLY 데이터베이스에서 ALLOW_SNAPSHOT_ISOLATION을 설정하는 경우 데이터베이스가 이후에 READ_WRITE로 설정되어도 이 설정은 그대로 유지됩니다.

master, model, msdb 및 tempdb 데이터베이스에 대해 ALLOW_SNAPSHOT_ISOLATION 설정을 변경할 수 있습니다. tempdb에 대한 설정을 변경하면 이 설정은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 중지 후 다시 시작할 때마다 유지됩니다. model 데이터베이스에 대한 설정을 변경하면 이 설정은 새로 생성된 모든 데이터베이스(tempdb 제외)의 기본값이 됩니다.

master 및 msdb 데이터베이스에 대해 이 옵션은 기본적으로 ON입니다.

이 옵션의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `snapshot_isolation_state` 열을 검사하여 확인할 수 있습니다.

READ_COMMITTED_SNAPSHOT { ON | OFF }     
켜기     
데이터베이스 수준에서 커밋된 읽기 스냅샷 옵션을 사용하도록 설정합니다. 이 옵션을 사용하면 트랜잭션에서 스냅샷 격리를 사용하지 않는 경우에도 DML 문에서 행 버전을 생성하기 시작합니다. 이 옵션을 사용하도록 설정하면 커밋된 읽기 스냅숏 격리 수준을 지정하는 트랜잭션에서는 잠금 대신 행 버전 관리를 사용합니다. 트랜잭션이 READ COMMITTED 격리 수준에서 실행되면, 모든 문에 문 시작 시의 데이터 스냅샷이 표시됩니다.

OFF     
데이터베이스 수준에서 커밋된 읽기 스냅샷 옵션을 해제합니다. READ COMMITTED 격리 수준을 지정하는 트랜잭션에서는 잠금을 사용합니다.

READ_COMMITTED_SNAPSHOT을 ON 또는 OFF로 설정하려면 ALTER DATABASE 명령을 실행하는 연결을 제외하고 데이터베이스에 대한 활성 상태의 연결이 없어야 합니다. 그러나 데이터베이스가 단일 사용자 모드에 있을 필요는 없습니다. 데이터베이스가 OFFLINE인 경우 이 옵션의 상태를 변경할 수 없습니다.

READ_ONLY 데이터베이스에서 READ_COMMITTED_SNAPSHOT을 설정하는 경우 데이터베이스가 이후에 READ_WRITE로 설정되어도 이 설정은 그대로 유지됩니다.

master, tempdb 또는 msdb 시스템 데이터베이스에 대해서는 READ_COMMITTED_SNAPSHOT을 ON으로 설정할 수 없습니다. model 데이터베이스에 대한 설정을 변경하면 이 설정은 새로 생성된 모든 데이터베이스(tempdb 제외)의 기본값이 됩니다.

이 옵션의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_read_committed_snapshot_on` 열을 검사하여 확인할 수 있습니다.

> [!WARNING]
> **DURABILITY = SCHEMA_ONLY**를 사용하여 테이블이 만들어지고 그 후에 **READ_COMMITTED_SNAPSHOT**이 **ALTER DATABASE**를 사용하여 변경되면 테이블의 데이터는 손실됩니다.

MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT { ON | **OFF** }     
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 시작)

켜기     
트랜잭션 격리 수준이 SNAPSHOT보다 낮은 격리 수준으로 설정된 경우 메모리 최적화 테이블에 대한 해석된 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업이 SNAPSHOT 격리로 실행됩니다. 스냅샷보다 낮은 격리 수준의 예는 READ COMMITTED 또는 READ UNCOMMITTED입니다. 이 작업은 세션 수준에서 트랜잭션 격리 수준이 명시적으로 설정되었거나 기본값이 암시적으로 사용되는지에 관계없이 실행됩니다.

OFF     
메모리 최적화 테이블에서 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업에 대해 트랜잭션 격리 수준을 승격하지 않습니다.

데이터베이스가 OFFLINE인 경우 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT의 상태를 변경할 수 없습니다.

기본 옵션은 OFF입니다.

이 옵션의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_memory_optimized_elevate_to_snapshot_on` 열을 검사하여 확인할 수 있습니다.

**\<sql_option> ::=**      
ANSI 호환 옵션을 데이터베이스 수준에서 제어합니다.

ANSI_NULL_DEFAULT { ON | **OFF** }     
CREATE TABLE 또는 ALTER TABLE 문에서 Null 허용 여부가 명시적으로 정의되어 있지 않은 열 또는 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)에 대한 기본값(NULL 또는 NOT NULL)을 결정합니다. 제약 조건이 정의된 열은 이 설정이 무엇이든 관계없이 제약 조건 규칙을 따릅니다.

켜기     
정의되지 않은 열에 대한 기본값은 NULL입니다.

OFF     
정의되지 않은 열에 대한 기본값은 NULL이 아닙니다.

SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_NULL_DEFAULT에 대한 기본 데이터베이스 수준 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 세션의 ANSI_NULL_DEFAULT를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET ANSI_NULL_DFLT_ON](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)을 참조하세요.

ANSI 호환성을 위해 ANSI_NULL_DEFAULT 데이터베이스 옵션을 ON으로 설정하면 데이터베이스의 기본값이 NULL로 변경됩니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_ansi_null_default_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAnsiNullDefault` 속성을 검사하여 상태를 확인할 수도 있습니다.

ANSI_NULLS { ON | **OFF** }     
켜기     
Null 값에 대한 모든 비교는 UNKNOWN으로 평가됩니다.

OFF     
Null 값에 대한 비-UNICODE 값 비교는 두 값이 모두 NULL인 경우 TRUE로 평가됩니다.

> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 ANSI_NULLS가 항상 ON으로 설정되므로 명시적으로 이 옵션을 OFF로 설정한 애플리케이션에서는 오류가 발생합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.

SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_NULLS에 대한 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 세션의 ANSI_NULLS를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET ANSI_NULLS](../../t-sql/statements/set-ansi-nulls-transact-sql.md)를 참조하세요.

> [!IMPORTANT]
> 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경하는 경우에도 SET ANSI_NULLS를 ON으로 설정해야 합니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_ansi_nulls_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAnsiNullsEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

ANSI_PADDING { ON | **OFF** }     
켜기     
변환하기 전에 문자열이 동일한 길이만큼 채워집니다. 문자열을 동일한 길이만큼 채운 후에 **varchar** 또는 **nvarchar** 데이터 형식에 대해 삽입합니다.

OFF     
문자 값의 후행 공백을 **varchar** 또는 **nvarchar** 열에 삽입합니다. 또한 **varbinary** 열에 삽입된 이진 값에서 후행 0을 유지합니다. 값은 열의 크기만큼 오른쪽에 공백으로 채워집니다.

OFF로 지정하면 이 설정은 새 열의 정의에만 영향을 줍니다.

> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 ANSI_PADDING이 항상 ON으로 설정되므로 명시적으로 이 옵션을 OFF로 설정한 애플리케이션에서는 오류가 발생합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. ANSI_PADDING은 항상 ON으로 설정하는 것이 좋습니다. 계산 열이나 인덱싱된 뷰에서 인덱스를 만들거나 조작할 때는 ANSI_PADDING을 ON으로 설정해야 합니다.

ANSI_PADDING을 ON으로 설정하면 Null을 허용하는 **char(_n_)** 및 **binary(_n_)** 열이 열 길이만큼 채워집니다. ANSI_PADDING이 OFF이면 후행 공백과 0이 잘립니다. Null을 허용하지 않는 **char(_n_)** 및 **binary(_n_)** 열은 항상 열 길이만큼 채워집니다.

SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_PADDING에 대한 기본 데이터베이스 수준 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 세션의 ANSI_PADDING을 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET ANSI_PADDING](../../t-sql/statements/set-ansi-padding-transact-sql.md)을 참조하세요.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_ansi_padding_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAnsiPaddingEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

ANSI_WARNINGS { ON | **OFF** }     
켜기     
0으로 나누기 등의 조건이 발생할 때 오류 또는 경고가 발생합니다. 집계 함수에 Null 값이 나타나는 경우에도 오류 또는 경고가 발생합니다.

OFF     
0으로 나누기와 같은 상황이 발생해도 아무런 경고도 발생하지 않으며 Null 값이 반환됩니다.

> [!IMPORTANT]
> 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경하는 경우 SET ANSI_WARNINGS를 ON으로 설정해야 합니다.

SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_WARNINGS에 대한 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 세션의 ANSI_WARNINGS를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET ANSI_WARNINGS](../../t-sql/statements/set-ansi-warnings-transact-sql.md)를 참조하세요.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_ansi_warnings_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAnsiWarningsEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

ARITHABORT { ON | OFF }     
켜기     
쿼리 실행 중 오버플로 또는 0으로 나누기 오류가 발생하면 쿼리를 종료합니다.

OFF     
해당 오류 중 하나가 발생하면 경고 메시지가 표시됩니다. 경고 메시지가 표시되더라도 오류가 발생하지 않으면 쿼리, 일괄 처리 또는 트랜잭션이 계속 진행됩니다.

> [!IMPORTANT]
> 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때 SET ARITHABORT를 ON으로 설정해야 합니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_arithabort_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsArithmeticAbortEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

COMPATIBILITY_LEVEL = { 150 | 140 | 130 | 120 | 110 | 100 }     

자세한 내용은 [ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.

CONCAT_NULL_YIELDS_NULL { ON | **OFF** }     
켜기     
피연산자 중 하나가 NULL일 경우 연결 연산의 결과는 NULL입니다. 예를 들어 문자열 “This is”와 NULL을 연결하면 “This is” 값 대신 NULL 값이 반환됩니다.

OFF     
Null 값은 빈 문자열로 취급됩니다.

> [중요] 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때 SET CONCAT_NULL_YIELDS_NULL은 반드시 ON으로 설정되어야 합니다.
>
> 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CONCAT_NULL_YIELDS_NULL이 항상 ON으로 설정되므로, 명시적으로 이 옵션을 OFF로 설정한 애플리케이션에서 오류가 트리거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.

SET 문을 사용하여 설정한 연결 수준의 설정은 CONCAT_NULL_YIELDS_NULL의 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 때 세션의 CONCAT_NULL_YIELDS_NULL을 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. 자세한 내용은 [SET CONCAT_NULL_YIELDS_NULL](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)을 참조하세요.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_concat_null_yields_null_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsNullConcat` 속성을 검사하여 상태를 확인할 수도 있습니다.

QUOTED_IDENTIFIER { ON | OFF }     
켜기     
큰따옴표는 구분 식별자를 묶을 때 사용할 수 있습니다.

큰따옴표로 구분되는 모든 문자열은 개체 식별자로 해석됩니다. 따옴표 붙은 식별자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자 규칙을 따르지 않아도 됩니다. 따옴표 붙은 식별자는 키워드일 수 있으며, [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자에서 허용되지 않는 문자를 포함할 수 있습니다. 작은따옴표(')가 리터럴 문자열의 일부로 포함되면 큰따옴표(")로 나타낼 수 있습니다.

OFF     
식별자는 따옴표 안에 있을 수 없으며 식별자에 대한 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 규칙을 따라야 합니다. 리터럴은 작은따옴표 또는 큰따옴표로 구분할 수 있습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서도 식별자를 대괄호([ ])로 구분할 수 있습니다. 대괄호로 묶은 식별자는 QUOTED_IDENTIFIER의 설정이 무엇이든 관계없이 항상 사용할 수 있습니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.

테이블이 생성될 때 QUOTED IDENTIFIER 옵션은 해당 테이블의 메타데이터에서 항상 ON으로 저장됩니다. 이 옵션은 테이블이 생성될 때 OFF로 설정되는 경우에도 저장됩니다.

SET 문을 사용하여 설정한 연결 수준의 설정은 QUOTED_IDENTIFIER의 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 QUOTED_IDENTIFIER를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_quoted_identifier_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsQuotedIdentifiersEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

NUMERIC_ROUNDABORT { ON | OFF }     
켜기     
식에서 전체 자릿수가 손실되면 오류가 발생합니다.

OFF     
정밀도가 손실되어도 오류 메시지가 생성되지 않으며, 결과를 저장하는 열 또는 변수의 정밀도로 결과가 반올림됩니다.

> [!IMPORTANT]
> 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때 NUMERIC_ROUNDABORT는 OFF로 설정되어야 합니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_numeric_roundabort_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsNumericRoundAbortEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

RECURSIVE_TRIGGERS { ON | OFF }     
켜기     
AFTER 트리거의 재귀적 실행이 허용됩니다.

OFF     
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_recursive_triggers_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsRecursiveTriggersEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

> [!NOTE]
> RECURSIVE_TRIGGERS가 OFF로 설정되면 직접 재귀만 금지됩니다. 간접 재귀를 사용하지 않도록 하려면 nested triggers 서버 옵션을 0으로 설정해야 합니다.

이 옵션의 상태는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_recursive_triggers_on` 열 또는 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsRecursiveTriggersEnabled` 속성을 검사하여 확인할 수 있습니다.

**\<target_recovery_time_option> ::=**      
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 시작)

데이터베이스 단위로 간접 검사점의 빈도를 지정합니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 새 데이터베이스의 기본값은 **1분**이며, 이 값은 데이터베이스에서 간접 검사점을 사용한다는 것을 나타냅니다. 이전 버전의 기본값 0은 데이터베이스가 자동 검사점을 사용함을 나타내며, 빈도는 서버 인스턴스의 복구 간격 설정에 따라 달라집니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서는 대부분의 시스템에 1분을 권장합니다.

TARGET_RECOVERY_TIME **=** *target_recovery_time* { SECONDS | MINUTES }     
*target_recovery_time*     
충돌 시 지정된 데이터베이스를 복구하는 데 걸리는 최대 시간을 지정합니다. *target_recovery_time*은 **int** 형식입니다.

SECONDS     
*target_recovery_time* 이 초 단위로 표현됨을 나타냅니다.

MINUTES     
*target_recovery_time* 이 분 단위로 표현됨을 나타냅니다.

간접 검사점에 대한 자세한 내용은 [데이터베이스 검사점](../../relational-databases/logs/database-checkpoints-sql-server.md)을 참조하세요.

**WITH \<termination> ::=**      
데이터베이스가 다른 상태로 바뀔 때 완료되지 않은 트랜잭션을 롤백할 시점을 지정합니다. termination 절을 생략하면 데이터베이스에 잠금이 있는 경우 ALTER DATABASE 문이 무기한 대기합니다. termination 절은 SET 절 다음에 한 번만 지정할 수 있습니다.

> [!NOTE]
> 모든 데이터베이스 옵션에서 WITH \<termination> 절을 사용하는 것은 아닙니다. 자세한 내용은 이 문서의 “주의” 섹션에서 “[옵션 설정](#SettingOptions)” 아래에 있는 표를 참조하세요.

ROLLBACK AFTER *number* [SECONDS] | ROLLBACK IMMEDIATE     
지정한 시간(초)이 경과한 후 롤백할 것인지 또는 즉시 롤백할 것인지를 지정합니다. *number*는 **int** 형식입니다.

NO_WAIT     
요청된 데이터베이스 상태 또는 옵션 변경을 즉시 완료할 수 없는 경우 요청이 실패하도록 지정합니다. 즉시 완료는 트랜잭션이 자체적으로 커밋되거나 롤백되기를 기다리지 않음을 의미합니다.

## <a name="setting-options"></a><a name="SettingOptions"></a> 옵션 설정
데이터베이스 옵션에 대한 현재 설정을 검색하려면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰 또는 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)를 사용합니다.

데이터베이스 옵션을 설정하면 새 설정이 즉시 적용됩니다.

새로 만드는 모든 데이터베이스에 대한 데이터베이스 옵션의 기본값을 변경할 수 있습니다. 이렇게 하려면 model 데이터베이스에서 해당 데이터베이스 옵션을 변경합니다.

모든 데이터베이스 옵션에서 WITH \<termination> 절을 사용하거나 데이터베이스 옵션을 다른 옵션과 조합하여 지정할 수 있는 것은 아닙니다. 다음 표에서는 이러한 옵션 및 이들의 옵션과 종료 상태를 나열합니다.

|옵션 범주|다른 옵션과 함께 지정할 수 있음|WITH \<termination> 절을 사용할 수 있음|
|----------------------|-----------------------------------------|---------------------------------------------|
|\<db_state_option>|예|예|
|\<db_user_access_option>|예|예|
|\<db_update_option>|예|예|
|\<delayed_durability_option>|예|예|
|\<external_access_option>|예|아니요|
|\<cursor_option>|예|예|
|\<auto_option>|예|예|
|\<sql_option>|예|아니요|
|\<recovery_option>|예|예|
|\<target_recovery_time_option>|아니요|예|
|\<database_mirroring_option>|아니요|예|
|ALLOW_SNAPSHOT_ISOLATION|예|예|
|READ_COMMITTED_SNAPSHOT|예|예|
|MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT|예|예|
|\<service_broker_option>|예|예|
|DATE_CORRELATION_OPTIMIZATION|예|예|
|\<parameterization_option>|예|예|
|\<change_tracking_option>|예|예|
|\<db_encryption_option>|예|예|

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스에 대한 계획 캐시는 다음 옵션 중 하나를 설정하여 삭제됩니다.

:::row:::
    :::column:::
        OFFLINE
    :::column-end:::
    :::column:::
        ONLINE
    :::column-end:::
    :::column:::
        MODIFY_NAME
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        COLLATE
    :::column-end:::
    :::column:::
        READ_ONLY
    :::column-end:::
    :::column:::
        READ_WRITE
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        MODIFY FILEGROUP DEFAULT
    :::column-end:::
    :::column:::
        MODIFY FILEGROUP READ_WRITE
    :::column-end:::
    :::column:::
        MODIFY FILEGROUP READ_ONLY
    :::column-end:::
:::row-end:::

계획 캐시는 다음 시나리오에서도 플러시됩니다.

- 데이터베이스에서 AUTO_CLOSE 데이터베이스 옵션이 ON으로 설정되어 있습니다. 사용자 연결이 데이터베이스를 참조하거나 사용하지 않으면 백그라운드 작업에서 자동으로 데이터베이스를 닫고 종료하려고 합니다.
- 기본 옵션이 있는 데이터베이스에 대해 여러 가지 쿼리를 실행합니다. 그러면 데이터베이스가 삭제됩니다.
- 원본 데이터베이스에 대한 데이터베이스 스냅샷이 삭제됩니다.
- 데이터베이스에 대한 트랜잭션 로그를 성공적으로 다시 작성합니다.
- 데이터베이스 백업을 복원합니다.
- 데이터베이스를 분리합니다.

계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. 계획 캐시의 삭제된 각 캐시스토어에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 `SQL Server has encountered %d occurrence(s) of cachestore flush for the '%s' cachestore (part of plan cache) due to some database maintenance or reconfigure operations`라는 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.

## <a name="examples"></a>예제

### <a name="a-setting-options-on-a-database"></a>A. 데이터베이스 옵션 설정

다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스에 대해 복구 모델 및 데이터 페이지 확인 옵션을 설정합니다.

```sql
USE master;
GO
ALTER DATABASE [database_name]
SET RECOVERY FULL PAGE_VERIFY CHECKSUM;
GO

```

### <a name="b-setting-the-database-to-read_only"></a>B. 데이터베이스를 READ_ONLY로 설정

데이터베이스 또는 파일 그룹의 상태를 READ_ONLY 또는 READ_WRITE로 변경하려면 데이터베이스에 대한 단독 액세스 권한이 필요합니다. 다음 예에서는 데이터베이스를 `SINGLE_USER` 모드로 설정하여 배타적 액세스 권한을 확보한 다음 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 상태를 `READ_ONLY` 로 설정한 후 데이터베이스 액세스를 모든 사용자에게 반환합니다.

> [!NOTE]
> 이 예에서는 첫 번째 `WITH ROLLBACK IMMEDIATE` 문에서 `ALTER DATABASE` 종료 옵션을 사용합니다. 완료되지 않은 트랜잭션은 모두 롤백되며 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대한 다른 모든 연결은 즉시 끊어집니다.

```sql
USE master;
GO
ALTER DATABASE [database_name]
SET SINGLE_USER
WITH ROLLBACK IMMEDIATE;
GO
ALTER DATABASE [database_name]
SET READ_ONLY
GO
ALTER DATABASE [database_name]
SET MULTI_USER;
GO
```

### <a name="c-enabling-snapshot-isolation-on-a-database"></a>C. 데이터베이스에서 스냅샷 격리 활성화

다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대해 스냅샷 격리 프레임워크 옵션을 활성화합니다.

```sql
USE [database_name];
USE master;
GO
ALTER DATABASE [database_name]
SET ALLOW_SNAPSHOT_ISOLATION ON;
GO
-- Check the state of the snapshot_isolation_framework
-- in the database.
SELECT name, snapshot_isolation_state,
    snapshot_isolation_state_desc AS description
FROM sys.databases
WHERE name = N'[database_name]';
GO

```

결과 집합은 스냅샷 격리 프레임워크가 활성화되었음을 보여 줍니다.

|name |snapshot_isolation_state |description|
|-------------------- |------------------------|----------|
|[database_name] |1| 켜기 |

### <a name="d-enabling-modifying-and-disabling-change-tracking"></a>D. 변경 내용 추적 설정, 수정 및 해제

다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대해 변경 내용 추적을 설정하고 보존 기간을 `2` 일로 설정합니다.

```sql
ALTER DATABASE [database_name]
SET CHANGE_TRACKING = ON
(AUTO_CLEANUP = ON, CHANGE_RETENTION = 2 DAYS);
```

다음 예에서는 보존 기간을 `3` 일로 바꾸는 방법을 보여 줍니다.

```sql
ALTER DATABASE [database_name]
SET CHANGE_TRACKING (CHANGE_RETENTION = 3 DAYS);
```

다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대한 변경 내용 추적을 해제하는 방법을 보여 줍니다.

```sql
ALTER DATABASE [database_name]
SET CHANGE_TRACKING = OFF;
```

### <a name="e-enabling-the-query-store"></a>E. 쿼리 저장소를 사용하도록 설정

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 시작)

다음 예제에서는 쿼리 저장소를 사용하도록 설정하고 쿼리 저장소와 매개 변수를 구성합니다.

```sql
ALTER DATABASE [database_name]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1024,
      INTERVAL_LENGTH_MINUTES = 60
    );
```

### <a name="f-enabling-the-query-store-with-wait-statistics"></a>F. 대기 통계가 포함된 쿼리 저장소를 사용하도록 설정

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 시작)

다음 예제에서는 쿼리 저장소를 사용하도록 설정하고 쿼리 저장소와 매개 변수를 구성합니다.

```sql
ALTER DATABASE [database_name]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      MAX_STORAGE_SIZE_MB = 1024,
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO,
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
    );
```

### <a name="g-enabling-the-query-store-with-custom-capture-policy-options"></a>G. 사용자 지정 캡처 정책 옵션이 포함된 쿼리 저장소를 사용하도록 설정

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작)

다음 예제에서는 쿼리 저장소를 사용하도록 설정하고 쿼리 저장소와 매개 변수를 구성합니다.

```sql
ALTER DATABASE [database_name]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      MAX_STORAGE_SIZE_MB = 1024,
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO,
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
      QUERY_CAPTURE_MODE = CUSTOM,
      QUERY_CAPTURE_POLICY = (
        STALE_CAPTURE_POLICY_THRESHOLD = 24 HOURS,
        EXECUTION_COUNT = 30,
        TOTAL_COMPILE_CPU_TIME_MS = 1000,
        TOTAL_EXECUTION_CPU_TIME_MS = 100
      )
    );
```

## <a name="see-also"></a>참고 항목

- [ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)
- [ALTER DATABASE 데이터베이스 미러링](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)
- [ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)
- [통계](../../relational-databases/statistics/statistics.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [변경 내용 추적 설정 및 해제](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [쿼리 저장소에 대한 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md)

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-database-transact-sql-set-options.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        **_\* SQL Database \*_** &nbsp;
    :::column-end:::
    :::column:::
        [SQL Database<br />Managed Instance](alter-database-transact-sql-set-options.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-database-transact-sql-set-options.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-database"></a>SQL Database

호환성 수준은 `SET` 옵션이지만 [ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)에서 설명합니다.

> [!NOTE]
> 많은 데이터베이스 설정 옵션은 현재 세션에 [SET 문](../../t-sql/statements/set-statements-transact-sql.md)을 사용하여 구성할 수 있으며 연결된 경우 일반적으로 애플리케이션에 의해 구성됩니다. 세션 수준 설정 옵션은 **ALTER DATABASE SET** 값을 재정의합니다. 다음 섹션에 설명된 데이터베이스 옵션은 다른 설정 옵션 값을 명시적으로 제공하지 않는 세션에 대해 설정할 수 있는 값입니다.

## <a name="syntax"></a>구문

```syntaxsql
ALTER DATABASE { database_name | Current }
SET
{
    <option_spec> [ ,...n ] [ WITH <termination> ]
}
;

<option_spec> ::=
{
    <auto_option>
  | <automatic_tuning_option>
  | <change_tracking_option>
  | <cursor_option>
  | <db_encryption_option>
  | <db_update_option>
  | <db_user_access_option>
  | <delayed_durability_option>
  | <parameterization_option>
  | <query_store_options>
  | <snapshot_option>
  | <sql_option>
  | <target_recovery_time_option>
  | <termination>
  | <temporal_history_retention>
}
;

<auto_option> ::=
{
    AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] }
  | AUTO_SHRINK { ON | OFF }
  | AUTO_UPDATE_STATISTICS { ON | OFF }
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }
}

<automatic_tuning_option> ::=
{
    AUTOMATIC_TUNING = { AUTO | INHERIT | CUSTOM }
  | AUTOMATIC_TUNING ( CREATE_INDEX = { DEFAULT | ON | OFF } )
  | AUTOMATIC_TUNING ( DROP_INDEX = { DEFAULT | ON | OFF } )
  | AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = { DEFAULT | ON | OFF } )
}

<change_tracking_option> ::=
{
    CHANGE_TRACKING
    {
        = OFF
      | = ON [ ( <change_tracking_option_list > [,...n] ) ]
      | ( <change_tracking_option_list> [,...n] )
    }
}

<change_tracking_option_list> ::=
   {
       AUTO_CLEANUP = { ON | OFF }
     | CHANGE_RETENTION = retention_period { DAYS | HOURS | MINUTES }
   }

<cursor_option> ::=
{
    CURSOR_CLOSE_ON_COMMIT { ON | OFF }
}

<db_encryption_option> ::=
  ENCRYPTION { ON | OFF }

<db_update_option> ::=
  { READ_ONLY | READ_WRITE }

<db_user_access_option> ::=
  { RESTRICTED_USER | MULTI_USER }

<delayed_durability_option> ::= DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }

<parameterization_option> ::=
  PARAMETERIZATION { SIMPLE | FORCED }

<query_store_options> ::=
{
  QUERY_STORE
  {
      = OFF
    | = ON [ ( <query_store_option_list> [,... n] ) ]
    | ( < query_store_option_list> [,... n] )
    | CLEAR [ ALL ]
  }
}

<query_store_option_list> ::=
{
  OPERATION_MODE = { READ_WRITE | READ_ONLY }
  | CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = number )
  | DATA_FLUSH_INTERVAL_SECONDS = number
  | MAX_STORAGE_SIZE_MB = number
  | INTERVAL_LENGTH_MINUTES = number
  | SIZE_BASED_CLEANUP_MODE = { AUTO | OFF }
  | QUERY_CAPTURE_MODE = { ALL | AUTO | CUSTOM | NONE }
  | MAX_PLANS_PER_QUERY = number
  | WAIT_STATS_CAPTURE_MODE = { ON | OFF }
  | QUERY_CAPTURE_POLICY = ( <query_capture_policy_option_list> [,...n] )
}

<query_capture_policy_option_list> :: =
{
    STALE_CAPTURE_POLICY_THRESHOLD = number { DAYS | HOURS }
    | EXECUTION_COUNT = number
    | TOTAL_COMPILE_CPU_TIME_MS = number
    | TOTAL_EXECUTION_CPU_TIME_MS = number
}

<snapshot_option> ::=
{
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }
  | READ_COMMITTED_SNAPSHOT {ON | OFF }
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT {ON | OFF }
}
<sql_option> ::=
{
    ANSI_NULL_DEFAULT { ON | OFF }
  | ANSI_NULLS { ON | OFF }
  | ANSI_PADDING { ON | OFF }
  | ANSI_WARNINGS { ON | OFF }
  | ARITHABORT { ON | OFF }
  | COMPATIBILITY_LEVEL = { 150 | 140 | 130 | 120 | 110 | 100 }
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }
  | NUMERIC_ROUNDABORT { ON | OFF }
  | QUOTED_IDENTIFIER { ON | OFF }
  | RECURSIVE_TRIGGERS { ON | OFF }
}

<termination>::=
{
    ROLLBACK AFTER integer [ SECONDS ]
  | ROLLBACK IMMEDIATE
  | NO_WAIT
}

<temporal_history_retention>::=TEMPORAL_HISTORY_RETENTION { ON | OFF }
```

## <a name="arguments"></a>인수

*database_name*     
수정할 데이터베이스의 이름입니다.

CURRENT     
`CURRENT`는 현재 데이터베이스에서 작업을 실행합니다. 모든 컨텍스트의 모든 옵션에서 `CURRENT`가 지원되는 것은 아닙니다. `CURRENT`가 실패할 경우 데이터베이스 이름을 지정해야 합니다.

**\<auto_option> ::=**      
자동 옵션을 제어합니다.

<a name="auto_create_statistics"></a> AUTO_CREATE_STATISTICS { ON | OFF }     
켜기     
쿼리 최적화 프로그램에서 필요에 따라 쿼리 조건자의 단일 열에 대한 통계를 생성하여 쿼리 계획 및 쿼리 성능을 향상합니다. 쿼리 최적화 프로그램에서 쿼리를 컴파일할 때 이러한 단일 열 통계가 생성됩니다. 단일 열 통계는 기존 통계 개체의 첫 번째 열이 아닌 열에 대해서만 생성됩니다.

기본값은 ON입니다. 대부분의 데이터베이스의 경우 기본 설정을 사용하는 것이 좋습니다.

OFF     
쿼리 최적화 프로그램에서 쿼리를 컴파일할 때 쿼리 조건자의 단일 열에 대한 통계를 생성하지 않습니다. 이 옵션을 OFF로 설정하면 최적이 아닌 쿼리 계획을 사용하므로 쿼리 성능이 저하됩니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_auto_create_stats_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAutoCreateStatistics` 속성을 검사하여 상태를 확인할 수도 있습니다.

자세한 내용은 [통계](../../relational-databases/statistics/statistics.md#statistics-options)에서 “통계 옵션” 섹션을 참조하세요.

INCREMENTAL = ON | **OFF**     
AUTO_CREATE_STATISTICS를 ON으로 설정하고 INCREMENTAL을 ON으로 설정합니다. 이 설정은 증분 통계가 지원될 때마다 자동으로 생성된 통계를 증분으로 만듭니다. 기본값은 OFF입니다. 자세한 내용은 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)를 참조하세요.

<a name="auto_shrink"></a> AUTO_SHRINK { ON | **OFF** }     
켜기     
데이터베이스 파일이 주기적인 축소의 후보가 됩니다.

데이터 파일과 로그 파일 모두 자동으로 축소될 수 있습니다. AUTO_SHRINK는 데이터베이스를 단순 복구 모델로 설정하거나 로그를 백업하는 경우에만 트랜잭션 로그의 크기를 줄입니다. 이 옵션이 OFF로 설정되면 사용되지 않는 공간을 정기적으로 검사하는 동안 데이터베이스 파일을 자동으로 축소하지 않습니다.

AUTO_SHRINK 옵션은 파일에서 사용되지 않는 공간이 25% 이상일 때 파일을 축소합니다. 이 옵션을 사용하면 파일이 두 가지 크기 중 하나로 축소됩니다. 다음 두 크기 중 더 큰 크기로 축소됩니다.

- 파일의 25%가 사용되지 않는 공간인 크기
- 파일 생성 시 파일의 크기

읽기 전용 데이터베이스는 축소할 수 없습니다.

OFF     
사용되지 않는 공간을 정기적으로 검사하는 동안에는 데이터베이스 파일을 자동으로 축소하지 않습니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_auto_shrink_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAutoShrink` 속성을 검사하여 상태를 확인할 수도 있습니다.

> [!NOTE]
> 포함된 데이터베이스에서는 AUTO_SHRINK 옵션을 사용할 수 없습니다.

<a name="auto_update_statistics"></a> AUTO_UPDATE_STATISTICS { **ON** | OFF }     
켜기     
쿼리에서 통계를 사용하거나 통계가 최신 정보가 아닌 경우 쿼리 최적화 프로그램에서 통계를 업데이트하도록 지정합니다. 삽입, 업데이트, 삭제 또는 병합 작업을 통해 테이블이나 인덱싱된 뷰의 데이터 분포가 변경되면 통계 내용이 더 이상 최신이 아니게 됩니다. 쿼리 최적화 프로그램은 마지막 통계 업데이트 이후 데이터 수정 개수를 계산한 다음, 이 수를 임계값과 비교하여 통계가 최신이 아니게 된 시점을 결정합니다. 임계값은 테이블 또는 인덱싱된 뷰의 행 수를 기준으로 합니다.

쿼리 최적화 프로그램은 쿼리를 컴파일하고 캐시된 쿼리 계획을 실행하기 전에 최신 정보가 아닌 통계가 있는지 확인합니다. 쿼리 최적화 프로그램은 쿼리 조건자의 열, 테이블 및 인덱싱된 뷰를 사용하여 어떤 통계가 최신이 아닌지 확인합니다. 쿼리 최적화 프로그램은 쿼리를 컴파일하기 전에 이 정보를 확인합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 캐시된 쿼리 계획을 실행하기 전에 쿼리 계획에서 최신 통계가 참조되는지 확인합니다.

AUTO_UPDATE_STATISTICS 옵션은 인덱스에 대해 생성된 통계, 쿼리 조건자의 단일 열 및 CREATE STATISTICS 문을 사용하여 생성된 통계에 적용됩니다. 이 옵션은 또한 필터링된 통계에도 적용됩니다.

기본값은 ON입니다. 대부분의 데이터베이스의 경우 기본 설정을 사용하는 것이 좋습니다.

AUTO_UPDATE_STATISTICS_ASYNC 옵션을 사용하여 통계를 동기적으로 업데이트할지 또는 비동기적으로 업데이트할지를 지정합니다.

OFF     
쿼리에서 통계를 사용하는 경우 쿼리 최적화 프로그램에서 통계를 업데이트하지 않도록 지정합니다. 통계가 최신이 아니게 된 경우에도 쿼리 최적화 프로그램에서 통계를 업데이트하지 않습니다. 이 옵션을 OFF로 설정하면 최적이 아닌 쿼리 계획을 사용하므로 쿼리 성능이 저하됩니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_auto_update_stats_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAutoUpdateStatistics` 속성을 검사하여 상태를 확인할 수도 있습니다.

자세한 내용은 [통계](../../relational-databases/statistics/statistics.md#statistics-options)에서 “통계 옵션” 섹션을 참조하세요.

<a name="auto_update_statistics_async"></a> AUTO_UPDATE_STATISTICS_ASYNC { ON | **OFF** }     
켜기     
AUTO_UPDATE_STATISTICS 옵션에 대한 통계 업데이트를 비동기로 지정합니다. 쿼리 최적화 프로그램은 쿼리를 컴파일하기 전에 통계 업데이트가 완료될 때까지 기다리지 않습니다.

이 옵션을 ON으로 설정해도 AUTO_UPDATE_STATISTICS가 ON으로 설정되어 있지 않으면 영향을 주지 않습니다.

기본적으로 AUTO_UPDATE_STATISTICS_ASYNC 옵션은 OFF로 설정되어 있으므로 쿼리 최적화 프로그램은 통계를 동기적으로 업데이트합니다.

OFF     
AUTO_UPDATE_STATISTICS 옵션에 대한 통계 업데이트를 동기로 지정합니다. 쿼리 최적화 프로그램은 쿼리를 컴파일하기 전에 통계 업데이트가 완료될 때까지 기다립니다.

이 옵션을 OFF로 설정해도 AUTO_UPDATE_STATISTICS가 ON으로 설정되어 있지 않으면 영향을 주지 않습니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_auto_update_stats_async_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다.

동기 통계 업데이트 또는 비동기 통계 업데이트를 사용하는 경우에 대한 자세한 설명은 [통계](../../relational-databases/statistics/statistics.md#statistics-options)에서 “통계 옵션” 섹션을 참조하세요.

<a name="auto_tuning"></a> **\<automatic_tuning_option> ::=**      
**적용 대상**: [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]

[자동 튜닝](../../relational-databases/automatic-tuning/automatic-tuning.md)에 대한 자동 옵션을 제어합니다.

AUTOMATIC_TUNING = { AUTO | INHERIT | CUSTOM }     
AUTO     
자동 튜닝 값을 AUTO로 설정하면 자동 튜닝에 대해 Azure 구성 기본값을 적용합니다.

INHERIT     
INHERIT 값을 사용하면 부모 서버에서 기본 구성이 상속됩니다. 부모 서버에서 자동 튜닝 구성을 사용자 지정하고 해당 서버의 모든 데이터베이스에 이 사용자 지정 설정을 상속하려는 경우에 특히 유용합니다. 상속이 작동하기 위해 FORCE_LAST_GOOD_PLAN, CREATE_INDEX 및 DROP_INDEX라는 세 가지 개별 튜닝 옵션을 데이터베이스에서 기본값으로 설정해야 합니다.

CUSTOM     
CUSTOM 값을 사용하는 경우, 데이터베이스에서 사용할 수 있는 자동 튜닝 옵션을 각각 사용자 지정 구성해야 합니다.

[자동 튜닝](../../relational-databases/automatic-tuning/automatic-tuning.md)의 자동 인덱스 관리 `CREATE_INDEX` 옵션을 사용하거나 사용하지 않도록 설정합니다.

CREATE_INDEX = { DEFAULT | ON | OFF }     
DEFAULT     
서버의 기본 설정을 상속합니다. 이 경우에 개별 자동 조정 기능을 사용하거나 사용하지 않도록 설정하는 옵션은 서버 수준에서 정의됩니다.

켜기     
사용하도록 설정하면 누락된 인덱스는 데이터베이스에서 자동으로 생성됩니다. 인덱스 생성을 수행하여 워크로드의 성능이 향상되었는지 확인합니다. 이렇게 만든 인덱스가 더 이상 워크로드 성능을 향상시키지 않으면 자동으로 되돌려집니다. 자동으로 생성된 인덱스는 시스템 생성 인덱스로 플래그가 지정됩니다.

OFF     
데이터베이스에서 누락된 인덱스를 자동으로 생성하지 않습니다.

[자동 튜닝](../../relational-databases/automatic-tuning/automatic-tuning.md)의 자동 인덱스 관리 `DROP_INDEX` 옵션을 사용하거나 사용하지 않도록 설정합니다.

DROP_INDEX = { DEFAULT | ON | OFF }     
DEFAULT     
서버의 기본 설정을 상속합니다. 이 경우에 개별 자동 조정 기능을 사용하거나 사용하지 않도록 설정하는 옵션은 서버 수준에서 정의됩니다.

켜기     
성능 워크로드에 대한 중복 인덱스 또는 더 이상 유용하지 않은 인덱스를 자동으로 삭제합니다.

OFF     
데이터베이스에서 누락된 인덱스를 자동으로 삭제하지 않습니다.

[자동 튜닝](../../relational-databases/automatic-tuning/automatic-tuning.md)의 자동 계획 수정 `FORCE_LAST_GOOD_PLAN` 옵션을 사용하거나 사용하지 않도록 설정합니다.

FORCE_LAST_GOOD_PLAN = { DEFAULT | ON | OFF }     
DEFAULT     
서버의 기본 설정을 상속합니다. 이 경우에 개별 자동 조정 기능을 사용하거나 사용하지 않도록 설정하는 옵션은 서버 수준에서 정의됩니다.

켜기     
[!INCLUDE[ssde_md](../../includes/ssde_md.md)]은 새 SQL 계획이 성능 저하를 일으키는 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 쿼리에 마지막으로 성공한 계획을 자동으로 강제로 적용합니다. [!INCLUDE[ssde_md](../../includes/ssde_md.md)]는 강제 계획을 통해 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 쿼리의 쿼리 성능을 지속적으로 모니터링합니다. 성능이 향상되면 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]은 마지막으로 성공한 계획을 계속 사용합니다. 성능 향상이 검색되지 않으면 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]이 새 쿼리 계획을 생성합니다. 쿼리 저장소를 사용할 수 없거나 ‘읽기/쓰기’ 모드가 아닌 경우 문이 실패합니다.

OFF     
[!INCLUDE[ssde_md](../../includes/ssde_md.md)]은 [sys.dm_db_tuning_recommendations](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) 뷰에서 SQL 계획 변경으로 인한 잠재적인 쿼리 성능 저하를 보고합니다. 하지만 이러한 권장 사항은 자동으로 적용되지 않습니다. 사용자는 뷰에 표시된 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 스크립트를 적용하여 활성 권장 사항을 모니터링하고 확인된 문제를 해결할 수 있습니다. 이것은 기본값입니다.

**\<change_tracking_option> ::=**      
변경 내용 추적 옵션을 제어합니다. 변경 내용 추적을 설정 또는 해제하고 옵션을 설정 또는 변경할 수 있습니다. 예제는 이 문서의 뒷부분에 있는 “예제” 섹션을 참조하세요.

켜기     
데이터베이스에 변경 내용 추적을 설정합니다. 변경 내용 추적을 설정하면 AUTO CLEANUP 및 CHANGE RETENTION 옵션도 설정할 수 있습니다.

AUTO_CLEANUP = { ON | OFF }     
켜기     
지정된 보존 기간 후에 변경 내용 추적 정보가 자동으로 제거됩니다.

OFF     
변경 내용 추적 데이터가 데이터베이스에서 제거되지 않습니다.

CHANGE_RETENTION = *retention_period* { **DAYS** | HOURS | MINUTES }     
데이터베이스에 변경 내용 추적 정보를 보존하는 최소 기간을 지정합니다. 데이터는 AUTO_CLEANUP 값이 ON일 때만 제거됩니다.

*retention_period*는 보존 기간의 숫자 부분을 지정하는 정수입니다.

기본 보존 기간은 **2일**입니다. 최소 보존 기간은 1분입니다. 기본 보존 형식은 **일**입니다.

OFF     
데이터베이스에서 변경 내용 추적을 해제합니다. 데이터베이스에서 변경 내용 추적을 사용 중지하려면 모든 테이블에서 변경 내용 추적을 사용하지 않도록 설정해야 합니다.

**\<cursor_option> ::=**      
커서 옵션을 제어합니다.

CURSOR_CLOSE_ON_COMMIT { ON | OFF }     
켜기     
트랜잭션을 커밋하거나 롤백할 때 열려 있는 커서가 모두 닫힙니다.

OFF     
트랜잭션 커밋 시에는 커서가 그대로 열려 있으나 트랜잭션 롤백 시에는 INSENSITIVE 또는 STATIC으로 정의된 것을 제외한 모든 커서가 닫힙니다.

SET 문을 사용하여 설정한 연결 수준 설정은 CURSOR_CLOSE_ON_COMMIT의 기본 데이터베이스 설정보다 우선적으로 적용됩니다. ODBC 및 OLE DB 클라이언트는 기본적으로 세션의 CURSOR_CLOSE_ON_COMMIT을 OFF로 설정하여 연결 수준 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET CURSOR_CLOSE_ON_COMMIT](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)을 참조하세요.

이 옵션의 상태는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_cursor_close_on_commit_on` 열 또는 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsCloseCursorsOnCommitEnabled` 속성을 검사하여 확인할 수 있습니다. 커서는 연결이 끊어질 때만 암시적으로 할당이 취소됩니다. 자세한 내용은 [DECLARE CURSOR](../../t-sql/language-elements/declare-cursor-transact-sql.md)를 참조하세요.

**\<db_encryption_option> ::=**      
데이터베이스 암호화 상태를 제어합니다.

ENCRYPTION { ON | OFF }     
데이터베이스를 암호화하거나(ON) 암호화하지 않도록(OFF) 설정합니다. 데이터베이스 암호화에 대한 자세한 내용은 [투명한 데이터 암호화](../../relational-databases/security/encryption/transparent-data-encryption.md) 및 [Azure SQL Database를 사용한 투명한 데이터 암호화](../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)를 참조하세요.

데이터베이스 수준에서 암호화를 사용할 수 있으면 모든 파일 그룹이 암호화됩니다. 새로운 파일 그룹은 암호화된 속성을 상속합니다. 데이터베이스의 파일 그룹이 READ ONLY로 설정되면 데이터베이스 암호화 작업이 실패합니다.

[sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 동적 관리 뷰를 사용하면 데이터베이스의 암호화 상태를 확인할 수 있습니다.

**\<db_update_option> ::=**      
데이터베이스에 대한 업데이트 허용 여부를 제어합니다.

READ_ONLY     
사용자는 데이터베이스에서 데이터를 읽을 수 있지만 수정은 할 수 없습니다.

> [!NOTE]
> 쿼리 성능을 향상시키려면 데이터베이스를 READ_ONLY로 설정하기 전에 통계를 업데이트하십시오. 데이터베이스를 READ_ONLY로 설정한 후에 추가 통계가 필요한 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 tempdb에 통계를 만듭니다. 읽기 전용 데이터베이스의 통계에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.

READ_WRITE     
데이터베이스에서 읽기와 쓰기 작업을 할 수 있습니다.

이 상태를 변경하려면 데이터베이스에 대해 배타적 액세스 권한이 있어야 합니다. 자세한 내용은 SINGLE_USER 절을 참조하십시오.

> [!NOTE]
> [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 페더레이션된 데이터베이스에서 `SET { READ_ONLY | READ_WRITE }`는 사용하지 않도록 설정됩니다.

**\<db_user_access_option> ::=**      
데이터베이스에 대한 사용자 액세스를 제어합니다.

RESTRICTED_USER     
`db_owner` 고정 데이터베이스 역할과 `dbcreator` 및 `sysadmin` 고정 서버 역할의 멤버만 데이터베이스에 연결할 수 있습니다. 연결할 수 있는 멤버의 수에는 제한이 없습니다. 데이터베이스에 대한 모든 연결은 ALTER DATABASE 문의 termination 절에 지정된 시간대에 끊어집니다. 데이터베이스가 RESTRICTED_USER 상태로 바뀐 후 자격이 없는 사용자의 연결 시도는 거부됩니다. SQL Managed Instance를 사용하여 **RESTRICTED_USER**를 수정할 수 없습니다.

MULTI_USER     
데이터베이스에 연결할 수 있는 적절한 권한이 있는 모든 사용자의 연결을 허용합니다.

이 옵션의 상태는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `user_access` 열 또는 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `UserAccess` 속성을 검사하여 확인할 수 있습니다.

**\<delayed_durability_option> ::=**      
트랜잭션이 완전한 내구성이 있게 커밋될지 아니면 지연된 내구성이 있게 커밋될지 제어합니다.

DISABLED     
`SET DISABLED` 다음의 모든 트랜잭션은 완전한 내구성이 있습니다. ATOMIC 블록이나 COMMIT 문에 설정된 내구성 옵션은 무시됩니다.

ALLOWED     
`SET ALLOWED` 다음의 모든 트랜잭션은 ATOMIC 블록이나 COMMIT 문에 설정된 내구성 옵션에 따라 완전한 내구성이 있거나 지연된 내구성이 있습니다.

FORCED     
`SET FORCED` 다음의 모든 트랜잭션은 지연된 내구성이 있습니다. ATOMIC 블록이나 COMMIT 문에 설정된 내구성 옵션은 무시됩니다.

**\<PARAMETERIZATION_option> ::=**      
매개 변수화 옵션을 제어합니다.

PARAMETERIZATION { **SIMPLE** | FORCED }     
SIMPLE     
데이터베이스의 기본 동작에 따라 쿼리를 매개 변수화합니다.

FORCED     
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스의 모든 쿼리를 매개 변수화합니다.

이 옵션의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_parameterization_forced` 열을 검사하여 확인할 수 있습니다.

<a name="query-store"></a> **\<query_store_options> ::=**

ON | OFF | CLEAR [ ALL ]     
이 데이터베이스에서 쿼리 저장소를 사용할 수 있는지 여부를 제어하고, 쿼리 저장소의 내용 제거도 제어합니다.

켜기     
쿼리 저장소를 사용하도록 설정합니다. 기본값은 ON입니다.

OFF     
쿼리 저장소를 사용하지 않도록 합니다. 

> [!NOTE]  
> 쿼리 저장소는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 단일 데이터베이스 및 탄력적 풀에서 사용하지 않도록 설정할 수 없습니다. `ALTER DATABASE [database] SET QUERY_STORE = OFF`를 실행하면 경고 `'QUERY_STORE=OFF' is not supported in this version of SQL Server.`가 반환됩니다. 

CLEAR     
쿼리 저장소의 내용을 제거합니다.

OPERATION_MODE     
쿼리 저장소의 작업 모드를 설명합니다. 유효한 값은 READ_ONLY 및 READ_WRITE입니다. READ_WRITE 모드에서 쿼리 저장소는 쿼리 계획 및 런타임 실행 통계 정보를 수집하고 유지합니다. READ_ONLY 모드에서는 쿼리 저장소에서 정보를 읽을 수 있지만 새 정보는 추가되지 않습니다. 쿼리 저장소의 최대 할당 공간이 최대값에 도달하면 쿼리 저장소는 작업 모드를 READ_ONLY로 변경합니다.

CLEANUP_POLICY     
쿼리 저장소의 데이터 보존 정책을 설명합니다. STALE_QUERY_THRESHOLD_DAYS는 쿼리에 대한 정보가 쿼리 저장소에 보존되는 일 수를 결정합니다. STALE_QUERY_THRESHOLD_DAYS는 **bigint** 형식입니다. 기본값은 30입니다. [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic 버전의 경우 기본값은 **7**일입니다.

DATA_FLUSH_INTERVAL_SECONDS     
쿼리 저장소에 기록된 데이터가 디스크에 유지되는 빈도를 결정합니다. 성능 최적화를 위해 쿼리 저장소에서 수집한 데이터는 디스크에 비동기적으로 기록됩니다. 비동기 전송이 발생하는 빈도는 DATA_FLUSH_INTERVAL_SECONDS 인수를 사용하여 구성됩니다. DATA_FLUSH_INTERVAL_SECONDS는 **bigint** 형식입니다. 기본값은 **900**(15분)입니다.

MAX_STORAGE_SIZE_MB     
쿼리 저장소에 할당되는 공간을 결정합니다. MAX_STORAGE_SIZE_MB는 **bigint** 형식입니다. [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium Edition의 경우 기본값은 **1GB**이고, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic Edition의 경우 기본값은 **10MB**입니다.

> [!NOTE]
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 `MAX_STORAGE_SIZE_MB` 설정 한도는 10,240MB입니다. 

> [!NOTE]
> `MAX_STORAGE_SIZE_MB` 한도는 엄격하게 적용되지 않습니다. 쿼리 저장소가 디스크에 데이터를 쓰는 경우에만 스토리지 크기가 확인됩니다. 이 간격은 `DATA_FLUSH_INTERVAL_SECONDS` 옵션 또는 [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 쿼리 저장소 대화 상자 옵션 **데이터 플러시 간격**에서 설정됩니다. 간격 기본값은 900초, 즉 15분입니다.
> 쿼리 저장소가 스토리지 크기 검사 간에 `MAX_STORAGE_SIZE_MB` 한도를 위반할 경우 읽기 전용 모드로 전환됩니다. `SIZE_BASED_CLEANUP_MODE`가 사용하도록 설정된 경우 `MAX_STORAGE_SIZE_MB` 한도를 적용하는 정리 메커니즘도 트리거됩니다.
> 충분한 공간이 확보되면 쿼리 저장소 모드가 자동으로 읽기/쓰기로 다시 전환됩니다.

> [!IMPORTANT]
> 워크로드 캡처에 10GB 이상의 디스크 공간이 필요하다고 생각되는 경우 워크로드를 재고하여 쿼리 계획을 다시 사용하도록 최적화하는 것이 좋습니다. 예를 들어 [강제 매개 변수화](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)를 사용하거나 쿼리 저장소 구성을 조정할 수 있습니다.    
> [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 쿼리 캡처 정책에 대한 추가 제어를 위해 `QUERY_CAPTURE_MODE`을 CUSTOM으로 설정할 수 있습니다.

INTERVAL_LENGTH_MINUTES     
런타임 실행 통계 데이터가 쿼리 저장소로 집계되는 간격을 결정합니다. 공간 사용을 최적화하기 위해 런타임 통계 저장소의 런타임 실행 통계는 고정된 시간 창을 통해 집계됩니다. 고정된 시간 창은 INTERVAL_LENGTH_MINUTES 인수를 사용하여 구성됩니다. INTERVAL_LENGTH_MINUTES는 **bigint** 형식입니다. 기본값은 **60**입니다.

SIZE_BASED_CLEANUP_MODE     
총 데이터양이 최대 크기에 가까워지면 정리를 자동으로 활성화할지 여부를 제어합니다.

OFF     
크기 기반 정리가 자동으로 활성화되지 않습니다.

AUTO     
디스크의 크기가 **max_storage_size_mb**의 90%에 도달하면 크기 기반 정리가 자동으로 활성화됩니다. 크기 기반 정리는 가장 저렴하고 가장 오래된 쿼리를 먼저 제거합니다. **max_storage_size_mb**가 약 80%가 되면 멈춥니다. 이것은 기본 구성 값입니다.

SIZE_BASED_CLEANUP_MODE는 **nvarchar** 형식입니다.

QUERY_CAPTURE_MODE { ALL \| AUTO \| CUSTOM \| NONE }     
현재 활성 쿼리 캡처 모드를 지정합니다. 각 모드는 특정 쿼리 캡처 정책을 정의합니다.   

> [!NOTE]
> 쿼리 캡처 모드를 모두, 자동 또는 사용자 지정으로 설정하면 커서, 저장 프로시저 내부 쿼리 및 고유하게 컴파일된 쿼리가 항상 캡처됩니다.

ALL     
쿼리를 모두 캡처합니다.

AUTO     
실행 횟수 및 리소스 사용을 기반으로 관련 쿼리를 캡처합니다. 이것이 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에 대한 기본 구성 값입니다.

없음     
새 쿼리 캡처를 중지합니다. 쿼리 저장소는 이미 캡처된 쿼리에 대한 컴파일 및 런타임 통계를 계속 수집합니다. 중요한 쿼리 캡처를 놓칠 수 있으므로 이 구성은 주의해서 사용해야 합니다.

CUSTOM     
QUERY_CAPTURE_POLICY 옵션에 대해 제어할 수 있습니다.

QUERY_CAPTURE_MODE는 **nvarchar** 형식입니다.

max_plans_per_query     
각 쿼리에 대해 유지 관리되는 최대 계획 수를 정의합니다. MAX_PLANS_PER_QUERY는 **int** 형식입니다. 기본값은 **200**입니다.

WAIT_STATS_CAPTURE_MODE { **ON** | OFF }     
쿼리별 대기 통계를 캡처할지 여부를 제어합니다.

켜기    
쿼리별 대기 통계 정보를 캡처합니다. 이 값은 기본 구성 값입니다.

OFF    
쿼리별 대기 통계 정보를 캡처하지 않습니다.

**\<query_capture_policy_option_list> :: =**      
쿼리 저장소 캡처 정책 옵션을 제어합니다. STALE_CAPTURE_POLICY_THRESHOLD를 제외하고 이 옵션은 정의된 부실 캡처 정책 임계값에 캡처해야 할 쿼리에 대해 수행해야 할 OR 조건을 정의합니다.

STALE_CAPTURE_POLICY_THRESHOLD = *number* { DAYS | HOURS }     
쿼리가 캡처되어야 하는지 여부를 결정하는 평가 간격 기간을 정의합니다. 기본값은 1일이며 1시간에서 7일까지 설정할 수 있습니다. *number*는 **int** 형식입니다.

EXECUTION_COUNT     
평가 기간 동안 쿼리가 실행되는 횟수를 정의합니다. 기본값은 30으로, 기본 부실 캡처 정책 임계값의 경우 쿼리가 쿼리 저장소에 유지되려면 하루에 30회 이상 실행되어야 합니다. EXECUTION_COUNT는 **int** 형식입니다.

TOTAL_COMPILE_CPU_TIME_MS     
평가 기간 동안 쿼리에 사용하는 총 경과 컴파일 CPU 시간을 정의합니다. 기본값은 1000으로, 기본 부실 캡처 정책 임계값의 경우 쿼리가 쿼리 저장소에 유지되려면 하루에 쿼리 컴파일에 사용된 총 CPU 시간이 1초 이상이어야 합니다. TOTAL_COMPILE_CPU_TIME_MS는 **int** 형식입니다.

TOTAL_EXECUTION_CPU_TIME_MS     
평가 기간 동안 쿼리에 사용하는 총 경과 실행 CPU 시간을 정의합니다. 기본값은 100으로, 기본 부실 캡처 정책 임계값의 경우 쿼리가 쿼리 저장소에 유지되려면 하루에 실행에 사용된 총 CPU 시간이 100ms 이상이어야 합니다. TOTAL_EXECUTION_CPU_TIME_MS는 **int** 형식입니다.

**\<snapshot_option> ::=**      
트랜잭션 격리 수준을 결정합니다.

ALLOW_SNAPSHOT_ISOLATION { ON | **OFF** }     
켜기     
데이터베이스 수준에서 스냅샷 옵션을 사용하도록 설정합니다. 이 옵션을 사용하면 트랜잭션에서 스냅샷 격리를 사용하지 않는 경우에도 DML 문에서 행 버전을 생성하기 시작합니다. 이 옵션을 사용하도록 설정하면 트랜잭션에서 SNAPSHOT 트랜잭션 격리 수준을 지정할 수 있습니다. 트랜잭션이 SNAPSHOT 격리 수준에서 실행되면 모든 문에서 트랜잭션 시작 시점의 상태로 데이터 스냅샷을 봅니다. SNAPSHOT 격리 수준에서 실행되는 트랜잭션이 여러 데이터베이스의 데이터에 액세스할 경우 모든 데이터베이스에서 ALLOW_SNAPSHOT_ISOLATION이 ON으로 설정되어 있어야 합니다. 그렇지 않고 ALLOW_SNAPSHOT_ISOLATION이 OFF로 설정된 경우에는 트랜잭션 내의 각 문에서는 FROM 절의 참조에서 데이터베이스의 테이블에 대한 잠금 힌트를 사용해야 합니다.

OFF     
데이터베이스 수준에서 스냅샷 옵션을 해제합니다. 트랜잭션을 SNAPSHOT 트랜잭션 격리 수준으로 지정할 수 없습니다.

ALLOW_SNAPSHOT_ISOLATION을 새 상태로 설정하는 경우(ON에서 OFF로 또는 OFF에서 ON으로) ALTER DATABASE는 데이터베이스 내의 기존 트랜잭션이 모두 커밋될 때까지 호출자에게 제어권을 반환하지 않습니다. 데이터베이스가 이미 ALTER DATABASE 문에 지정된 상태인 경우 제어권은 호출자에게 즉시 반환됩니다. ALTER DATABASE 문이 제어권을 빨리 반환하지 않는 경우 [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md)를 사용하여 장기 트랜잭션이 있는지 여부를 확인합니다. ALTER DATABASE 문을 취소하면 데이터베이스는 ALTER DATABASE가 시작된 시점의 상태로 남게 됩니다. [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰는 데이터베이스에 있는 스냅샷 격리 트랜잭션의 상태를 나타냅니다. **snapshot_isolation_state_desc** = IN_TRANSITION_TO_ON인 경우 ALTER DATABASE ALLOW_SNAPSHOT_ISOLATION을 OFF로 설정하는 작업은 6초간 일시 중지된 다음, 다시 시도됩니다.

데이터베이스가 OFFLINE인 경우 ALLOW_SNAPSHOT_ISOLATION의 상태를 변경할 수 없습니다.

READ_ONLY 데이터베이스에서 ALLOW_SNAPSHOT_ISOLATION을 설정하는 경우 데이터베이스가 이후에 READ_WRITE로 설정되어도 이 설정은 그대로 유지됩니다.

master, model, msdb 및 tempdb 데이터베이스에 대해 ALLOW_SNAPSHOT_ISOLATION 설정을 변경할 수 있습니다. tempdb에 대한 설정을 변경하면 이 설정은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 중지 후 다시 시작할 때마다 유지됩니다. model 데이터베이스에 대한 설정을 변경하면 이 설정은 새로 생성된 모든 데이터베이스(tempdb 제외)의 기본값이 됩니다.

master 및 msdb 데이터베이스에 대해 이 옵션은 기본적으로 ON입니다.

이 옵션의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `snapshot_isolation_state` 열을 검사하여 확인할 수 있습니다.

READ_COMMITTED_SNAPSHOT { ON | OFF }     
켜기     
데이터베이스 수준에서 커밋된 읽기 스냅샷 옵션을 사용하도록 설정합니다. 이 옵션을 사용하면 트랜잭션에서 스냅샷 격리를 사용하지 않는 경우에도 DML 문에서 행 버전을 생성하기 시작합니다. 이 옵션을 사용하도록 설정하면 READ COMMITTED 스냅샷 격리 수준을 지정하는 트랜잭션에서는 잠금 대신 행 버전 관리를 사용합니다. 트랜잭션이 READ COMMITTED 격리 수준에서 실행되면, 모든 문에 문 시작 시의 데이터 스냅샷이 표시됩니다.

OFF     
데이터베이스 수준에서 커밋된 읽기 스냅샷 옵션을 해제합니다. READ COMMITTED 격리 수준을 지정하는 트랜잭션에서는 잠금을 사용합니다.

READ_COMMITTED_SNAPSHOT을 ON 또는 OFF로 설정하려면 ALTER DATABASE 명령을 실행하는 연결을 제외하고 데이터베이스에 대한 활성 상태의 연결이 없어야 합니다. 그러나 데이터베이스가 단일 사용자 모드에 있을 필요는 없습니다. 데이터베이스가 OFFLINE인 경우 이 옵션의 상태를 변경할 수 없습니다.

READ_ONLY 데이터베이스에서 READ_COMMITTED_SNAPSHOT을 설정하는 경우 데이터베이스가 이후에 READ_WRITE로 설정되어도 이 설정은 그대로 유지됩니다.

master, tempdb 또는 msdb 시스템 데이터베이스에 대해서는 READ_COMMITTED_SNAPSHOT을 ON으로 설정할 수 없습니다. model 데이터베이스에 대한 설정을 변경하면 이 설정은 새로 생성된 모든 데이터베이스(tempdb 제외)의 기본값이 됩니다.

이 옵션의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_read_committed_snapshot_on` 열을 검사하여 확인할 수 있습니다.

> [!WARNING]
> `DURABILITY = SCHEMA_ONLY`를 사용해서 테이블을 만들었고 **READ_COMMITTED_SNAPSHOT**이 이후에 `ALTER DATABASE`를 사용해서 변경된 경우, 테이블의 데이터가 손실됩니다.

MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT { ON | **OFF** }     
켜기     
트랜잭션 격리 수준이 SNAPSHOT보다 낮은 격리 수준으로 설정된 경우 메모리 최적화 테이블에 대한 해석된 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업이 SNAPSHOT 격리로 실행됩니다. 스냅샷보다 낮은 격리 수준의 예는 READ COMMITTED 또는 READ UNCOMMITTED입니다. 이 작업은 세션 수준에서 트랜잭션 격리 수준이 명시적으로 설정되었거나 기본값이 암시적으로 사용되는지에 관계없이 실행됩니다.

OFF     
메모리 최적화 테이블에서 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업에 대해 트랜잭션 격리 수준을 승격하지 않습니다.

데이터베이스가 OFFLINE인 경우 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT의 상태를 변경할 수 없습니다.

기본값은 OFF입니다.

이 옵션의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_memory_optimized_elevate_to_snapshot_on` 열을 검사하여 확인할 수 있습니다.

**\<sql_option> ::=**      
ANSI 호환 옵션을 데이터베이스 수준에서 제어합니다.

ANSI_NULL_DEFAULT { ON | **OFF** }     
CREATE TABLE 또는 ALTER TABLE 문에서 Null 허용 여부가 명시적으로 정의되어 있지 않은 열 또는 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)에 대한 기본값(NULL 또는 NOT NULL)을 결정합니다. 제약 조건이 정의된 열은 이 설정이 무엇이든 관계없이 제약 조건 규칙을 따릅니다.

켜기     
기본값은 NULL입니다.

OFF     
기본값이 NOT NULL입니다.

SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_NULL_DEFAULT에 대한 기본 데이터베이스 수준 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 세션의 ANSI_NULL_DEFAULT를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET ANSI_NULL_DFLT_ON](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)을 참조하세요.

ANSI 호환성을 위해 ANSI_NULL_DEFAULT 데이터베이스 옵션을 ON으로 설정하면 데이터베이스의 기본값이 NULL로 변경됩니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_ansi_null_default_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAnsiNullDefault` 속성을 검사하여 상태를 확인할 수도 있습니다.

ANSI_NULLS { ON | **OFF** }     
켜기     
Null 값에 대한 모든 비교는 UNKNOWN으로 평가됩니다.

OFF     
Null 값에 대한 비-UNICODE 값 비교는 두 값이 모두 NULL인 경우 TRUE로 평가됩니다.

> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 ANSI_NULLS가 항상 ON으로 설정되므로 명시적으로 이 옵션을 OFF로 설정한 애플리케이션에서는 오류가 발생합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.

SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_NULLS에 대한 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 세션의 ANSI_NULLS를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET ANSI_NULLS](../../t-sql/statements/set-ansi-nulls-transact-sql.md)를 참조하세요.

> [!NOTE]
> 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경하는 경우에도 SET ANSI_NULLS를 ON으로 설정해야 합니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_ansi_nulls_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAnsiNullsEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

ANSI_PADDING { ON | **OFF** }     
켜기     
변환하기 전에 문자열이 동일한 길이만큼 채워집니다. 문자열을 동일한 길이만큼 채운 후에 **varchar** 또는 **nvarchar** 데이터 형식에 대해 삽입합니다.

OFF     
문자 값의 후행 공백을 **varchar** 또는 **nvarchar** 열에 삽입합니다. 또한 **varbinary** 열에 삽입된 이진 값에서 후행 0을 유지합니다. 값은 열의 크기만큼 오른쪽에 공백으로 채워집니다.

OFF로 지정하면 이 설정은 새 열의 정의에만 영향을 줍니다.

> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 ANSI_PADDING이 항상 ON으로 설정되므로 명시적으로 이 옵션을 OFF로 설정한 애플리케이션에서는 오류가 발생합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. ANSI_PADDING은 항상 ON으로 설정하는 것이 좋습니다. 계산 열이나 인덱싱된 뷰에서 인덱스를 만들거나 조작할 때는 ANSI_PADDING을 ON으로 설정해야 합니다.

ANSI_PADDING을 ON으로 설정하면 Null을 허용하는 **char(_n_)** 및 **binary(_n_)** 열이 열 길이만큼 채워집니다. ANSI_PADDING이 OFF이면 후행 공백과 0이 잘립니다. Null을 허용하지 않는 **char(_n_)** 및 **binary(_n_)** 열은 항상 열 길이만큼 채워집니다.

SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_PADDING에 대한 기본 데이터베이스 수준 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 세션의 ANSI_PADDING을 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET ANSI_PADDING](../../t-sql/statements/set-ansi-padding-transact-sql.md)을 참조하세요.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_ansi_padding_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAnsiPaddingEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

ANSI_WARNINGS { ON | **OFF** }     
켜기     
0으로 나누기 등의 조건이 발생할 때 오류 또는 경고가 발생합니다. 집계 함수에 Null 값이 나타나는 경우에도 오류 또는 경고가 발생합니다.

OFF     
0으로 나누기와 같은 상황이 발생해도 아무런 경고도 발생하지 않으며 Null 값이 반환됩니다.

> [!NOTE]
> 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경하는 경우 SET ANSI_WARNINGS를 ON으로 설정해야 합니다.

SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_WARNINGS에 대한 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 세션의 ANSI_WARNINGS를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET ANSI_WARNINGS](../../t-sql/statements/set-ansi-warnings-transact-sql.md)를 참조하세요.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_ansi_warnings_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAnsiWarningsEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

ARITHABORT { ON | OFF }     
켜기     
쿼리 실행 중 오버플로 또는 0으로 나누기 오류가 발생하면 쿼리를 종료합니다.

OFF     
해당 오류 중 하나가 발생하면 경고 메시지가 표시됩니다. 경고 메시지가 표시되더라도 오류가 발생하지 않으면 쿼리, 일괄 처리 또는 트랜잭션이 계속 진행됩니다.

> [!NOTE]
> 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때 SET ARITHABORT를 ON으로 설정해야 합니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_arithabort_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsArithmeticAbortEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

COMPATIBILITY_LEVEL = { 150 \| 140 \| 130 \| 120 \| 110 \| 100 }     
자세한 내용은 [ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.

CONCAT_NULL_YIELDS_NULL { ON | **OFF** }     
켜기     
피연산자 중 하나가 NULL일 경우 연결 연산의 결과는 NULL입니다. 예를 들어 문자열 "This is"와 NULL을 연결하면 결과는 "This is"가 아니라 NULL이 됩니다.

OFF     
Null 값은 빈 문자열로 취급됩니다.

> [!NOTE]
> 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때 SET CONCAT_NULL_YIELDS_NULL은 반드시 ON으로 설정되어야 합니다.
>
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 CONCAT_NULL_YIELDS_NULL이 항상 ON으로 설정되므로 명시적으로 이 옵션을 OFF로 설정한 애플리케이션에서는 오류가 발생합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.

SET 문을 사용하여 설정한 연결 수준의 설정은 CONCAT_NULL_YIELDS_NULL의 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 때 세션의 CONCAT_NULL_YIELDS_NULL을 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. 자세한 내용은 [SET CONCAT_NULL_YIELDS_NULL](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)을 참조하세요.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_concat_null_yields_null_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsNullConcat` 속성을 검사하여 상태를 확인할 수도 있습니다.

QUOTED_IDENTIFIER { ON | OFF }     
켜기     
큰따옴표는 구분 식별자를 묶을 때 사용할 수 있습니다.

큰따옴표로 구분되는 모든 문자열은 개체 식별자로 해석됩니다. 따옴표 붙은 식별자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자 규칙을 따르지 않아도 됩니다. 따옴표 붙은 식별자는 키워드일 수 있으며 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자에서 허용되지 않는 문자를 포함할 수 있습니다. 작은따옴표(')가 리터럴 문자열의 일부로 포함되면 큰따옴표(")로 나타낼 수 있습니다.

OFF     
식별자는 따옴표 안에 있을 수 없으며 식별자에 대한 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 규칙을 따라야 합니다. 리터럴은 작은따옴표 또는 큰따옴표로 구분할 수 있습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서도 식별자를 대괄호([ ])로 구분할 수 있습니다. 대괄호로 묶은 식별자는 QUOTED_IDENTIFIER의 설정이 무엇이든 관계없이 항상 사용할 수 있습니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.

테이블이 생성될 때 QUOTED IDENTIFIER 옵션은 해당 테이블의 메타데이터에서 항상 ON으로 저장됩니다. 이 옵션은 테이블이 생성될 때 OFF로 설정되는 경우에도 저장됩니다.

SET 문을 사용하여 설정한 연결 수준의 설정은 QUOTED_IDENTIFIER의 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 QUOTED_IDENTIFIER를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_quoted_identifier_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsQuotedIdentifiersEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

NUMERIC_ROUNDABORT { ON | OFF }     
켜기     
식에서 전체 자릿수가 손실되면 오류가 발생합니다.

OFF     
정밀도가 손실되어도 오류 메시지가 생성되지 않으며, 결과를 저장하는 열 또는 변수의 정밀도로 결과가 반올림됩니다.

> [!IMPORTANT]
> 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때 NUMERIC_ROUNDABORT는 OFF로 설정되어야 합니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_numeric_roundabort_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsNumericRoundAbortEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

RECURSIVE_TRIGGERS { ON | OFF }     
켜기     
AFTER 트리거의 재귀적 실행이 허용됩니다.

OFF     
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_recursive_triggers_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsRecursiveTriggersEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

> [!NOTE]
> RECURSIVE_TRIGGERS가 OFF로 설정되면 직접 재귀만 금지됩니다. 간접 재귀를 사용하지 않도록 하려면 nested triggers 서버 옵션을 0으로 설정해야 합니다.

이 옵션의 상태는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_recursive_triggers_on` 열 또는 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsRecursiveTriggersEnabled` 속성을 검사하여 확인할 수 있습니다.

**\<target_recovery_time_option> ::=**      
데이터베이스 단위로 간접 검사점의 빈도를 지정합니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 새 데이터베이스의 기본값은 1분이며, 이 값은 데이터베이스에서 간접 검사점을 사용한다는 것을 나타냅니다. 이전 버전의 기본값 0은 데이터베이스가 자동 검사점을 사용함을 나타내며, 빈도는 서버 인스턴스의 복구 간격 설정에 따라 달라집니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서는 대부분의 시스템에 1분을 권장합니다.

TARGET_RECOVERY_TIME **=** target_recovery_time { SECONDS | MINUTES }     
*target_recovery_time*     
충돌 시 지정된 데이터베이스를 복구하는 데 걸리는 최대 시간을 지정합니다.

SECONDS     
*target_recovery_time* 이 초 단위로 표현됨을 나타냅니다.

MINUTES     
*target_recovery_time* 이 분 단위로 표현됨을 나타냅니다.

간접 검사점에 대한 자세한 내용은 [데이터베이스 검사점](../../relational-databases/logs/database-checkpoints-sql-server.md)을 참조하세요.

**WITH \<termination> ::=**      
데이터베이스가 다른 상태로 바뀔 때 완료되지 않은 트랜잭션을 롤백할 시점을 지정합니다. termination 절을 생략하면 데이터베이스에 잠금이 있는 경우 ALTER DATABASE 문이 무기한 대기합니다. termination 절은 SET 절 다음에 한 번만 지정할 수 있습니다.

> [!NOTE]
> 모든 데이터베이스 옵션에서 WITH \<termination> 절을 사용하는 것은 아닙니다. 자세한 내용은 이 문서의 “주의” 섹션에서 “[옵션 설정](#SettingOptions)” 아래에 있는 표를 참조하세요.

ROLLBACK AFTER *integer* [SECONDS] | ROLLBACK IMMEDIATE     
지정한 시간(초)이 경과한 후 롤백할 것인지 또는 즉시 롤백할 것인지를 지정합니다.

NO_WAIT     
요청된 데이터베이스 상태 또는 옵션 변경을 즉시 완료할 수 없는 경우 요청이 실패하도록 지정합니다. 즉시 완료는 트랜잭션이 자체적으로 커밋되거나 롤백되기를 기다리지 않음을 의미합니다.

## <a name="setting-options"></a><a name="SettingOptions"></a> 옵션 설정

데이터베이스 옵션에 대한 현재 설정을 검색하려면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰 또는 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)를 사용합니다.

데이터베이스 옵션을 설정하면 새 설정이 즉시 적용됩니다.

새로 만드는 모든 데이터베이스에 대한 데이터베이스 옵션의 기본값을 변경할 수 있습니다. 이렇게 하려면 model 데이터베이스에서 해당 데이터베이스 옵션을 변경합니다.

모든 데이터베이스 옵션에서 WITH \<termination> 절을 사용하거나 데이터베이스 옵션을 다른 옵션과 조합하여 지정할 수 있는 것은 아닙니다. 다음 표에서는 이러한 옵션 및 이들의 옵션과 종료 상태를 나열합니다.

|옵션 범주|다른 옵션과 함께 지정할 수 있음|WITH \<termination> 절을 사용할 수 있음|
|----------------------|-----------------------------------------|---------------------------------------------|
|\<auto_option>|예|아니요|
|\<change_tracking_option>|예|예|
|\<cursor_option>|예|아니요|
|\<db_encryption_option>|예|아니요|
|\<db_update_option>|예|예|
|\<db_user_access_option>|예|예|
|\<delayed_durability_option>|예|예|
|\<parameterization_option>|예|예|
|ALLOW_SNAPSHOT_ISOLATION|예|예|
|READ_COMMITTED_SNAPSHOT|예|예|
|MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT|예|예|
|DATE_CORRELATION_OPTIMIZATION|예|예|
|\<sql_option>|예|아니요|
|\<target_recovery_time_option>|아니요|예|

## <a name="examples"></a>예제

### <a name="a-setting-the-database-to-read_only"></a>A. 데이터베이스를 READ_ONLY로 설정
데이터베이스 또는 파일 그룹의 상태를 READ_ONLY 또는 READ_WRITE로 변경하려면 데이터베이스에 대한 단독 액세스 권한이 필요합니다. 다음 예제에서는 데이터베이스를 `RESTRICTED_USER` 모드로 설정하여 액세스를 제한합니다. [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 상태를 `READ_ONLY` 로 설정한 후 데이터베이스 액세스를 모든 사용자에게 반환합니다.

```sql
USE master;
GO
ALTER DATABASE [database_name]
SET RESTRICTED_USER;
GO
ALTER DATABASE [database_name]
SET READ_ONLY
GO
ALTER DATABASE [database_name]
SET MULTI_USER;
GO

```

### <a name="b-enabling-snapshot-isolation-on-a-database"></a>B. 데이터베이스에서 스냅샷 격리 활성화
다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대해 스냅샷 격리 프레임워크 옵션을 활성화합니다.

```sql
USE [database_name];
USE master;
GO
ALTER DATABASE [database_name]
SET ALLOW_SNAPSHOT_ISOLATION ON;
GO
-- Check the state of the snapshot_isolation_framework
-- in the database.
SELECT name, snapshot_isolation_state,
    snapshot_isolation_state_desc AS description
FROM sys.databases
WHERE name = N'[database_name]';
GO
```

결과 집합은 스냅샷 격리 프레임워크가 활성화되었음을 보여 줍니다.

|name |snapshot_isolation_state |description|
|-------------------- |------------------------|----------|
|[database_name] |1| 켜기 |

### <a name="c-enabling-modifying-and-disabling-change-tracking"></a>C. 변경 내용 추적 설정, 수정 및 해제
다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대해 변경 내용 추적을 설정하고 보존 기간을 `2` 일로 설정합니다.

```sql
ALTER DATABASE [database_name]
SET CHANGE_TRACKING = ON
(AUTO_CLEANUP = ON, CHANGE_RETENTION = 2 DAYS);
```

다음 예에서는 보존 기간을 3일로 바꾸는 방법을 보여 줍니다.

```sql
ALTER DATABASE [database_name]
SET CHANGE_TRACKING (CHANGE_RETENTION = 3 DAYS);
```

다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대한 변경 내용 추적을 해제하는 방법을 보여 줍니다.

```sql
ALTER DATABASE [database_name]
SET CHANGE_TRACKING = OFF;
```

### <a name="d-enabling-the-query-store"></a>D. 쿼리 저장소를 사용하도록 설정
다음 예제에서는 쿼리 저장소를 사용하도록 설정하고 쿼리 저장소 매개 변수를 구성합니다.

```sql
ALTER DATABASE [database_name]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1024,
      INTERVAL_LENGTH_MINUTES = 60
    );
```

### <a name="e-enabling-the-query-store-with-wait-statistics"></a>E. 대기 통계가 포함된 쿼리 저장소를 사용하도록 설정
다음 예제에서는 쿼리 저장소를 사용하도록 설정하고 쿼리 저장소와 매개 변수를 구성합니다.

```sql
ALTER DATABASE [database_name]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      MAX_STORAGE_SIZE_MB = 1024,
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO,
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
    );
```

### <a name="f-enabling-the-query-store-with-custom-capture-policy-options"></a>F. 사용자 지정 캡처 정책 옵션이 포함된 쿼리 저장소를 사용하도록 설정
다음 예제에서는 쿼리 저장소를 사용하도록 설정하고 쿼리 저장소와 매개 변수를 구성합니다.

```sql
ALTER DATABASE [database_name]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      MAX_STORAGE_SIZE_MB = 1024,
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO,
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
      QUERY_CAPTURE_MODE = CUSTOM,
      QUERY_CAPTURE_POLICY = (
        STALE_CAPTURE_POLICY_THRESHOLD = 24 HOURS,
        EXECUTION_COUNT = 30,
        TOTAL_COMPILE_CPU_TIME_MS = 1000,
        TOTAL_EXECUTION_CPU_TIME_MS = 100
      )
    );
```

## <a name="see-also"></a>참고 항목

- [ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)
- [ALTER DATABASE 데이터베이스 미러링](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)
- [통계](../../relational-databases/statistics/statistics.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=azuresqldb-currentls)
- [변경 내용 추적 설정 및 해제](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [쿼리 저장소에 대한 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-database-transact-sql-set-options.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [SQL 데이터베이스](alter-database-transact-sql-set-options.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        **_\* SQL Database<br />Managed Instance \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-database-transact-sql-set-options.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-sql-managed-instance"></a>Azure SQL Managed Instance

호환성 수준은 `SET` 옵션이지만 [ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)에서 설명합니다.

> [!NOTE]
> 많은 데이터베이스 설정 옵션은 현재 세션에 [SET 문](../../t-sql/statements/set-statements-transact-sql.md)을 사용하여 구성할 수 있으며 연결된 경우 일반적으로 애플리케이션에 의해 구성됩니다. 세션 수준 설정 옵션은 **ALTER DATABASE SET** 값을 재정의합니다. 다음 섹션에 설명된 데이터베이스 옵션은 다른 설정 옵션 값을 명시적으로 제공하지 않는 세션에 대해 설정할 수 있는 값입니다.

## <a name="syntax"></a>구문

```syntaxsql
ALTER DATABASE { database_name | Current }
SET
{
    <optionspec> [ ,...n ]
}
;

<optionspec> ::=
{
    <auto_option>
  | <change_tracking_option>
  | <cursor_option>
  | <db_encryption_option>
  | <delayed_durability_option>
  | <parameterization_option>
  | <query_store_options>
  | <snapshot_option>
  | <sql_option>
  | <target_recovery_time_option>
  | <termination>
  | <temporal_history_retention>
}
;
<auto_option> ::=
{
    AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] }
  | AUTO_SHRINK { ON | OFF }
  | AUTO_UPDATE_STATISTICS { ON | OFF }
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }
}

<automatic_tuning_option> ::=
{
    AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = { ON | OFF } )
}

<change_tracking_option> ::=
{
    CHANGE_TRACKING
    {
       = OFF
     | = ON [ ( <change_tracking_option_list > [,...n] ) ]
     | ( <change_tracking_option_list> [,...n] )
    }
}

<change_tracking_option_list> ::=
   {
       AUTO_CLEANUP = { ON | OFF }
     | CHANGE_RETENTION = retention_period { DAYS | HOURS | MINUTES }
   }

<cursor_option> ::=
{
    CURSOR_CLOSE_ON_COMMIT { ON | OFF }
}

<db_encryption_option> ::=
  ENCRYPTION { ON | OFF }

<delayed_durability_option> ::=DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }

<parameterization_option> ::=
  PARAMETERIZATION { SIMPLE | FORCED }

<query_store_options> ::=
{
  QUERY_STORE
  {
    = OFF
    | = ON [ ( <query_store_option_list> [,... n] ) ]
    | ( < query_store_option_list> [,... n] )
    | CLEAR [ ALL ]
  }
}

<query_store_option_list> ::=
{
  OPERATION_MODE = { READ_WRITE | READ_ONLY }
  | CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = number )
  | DATA_FLUSH_INTERVAL_SECONDS = number
  | MAX_STORAGE_SIZE_MB = number
  | INTERVAL_LENGTH_MINUTES = number
  | SIZE_BASED_CLEANUP_MODE = { AUTO | OFF }
  | QUERY_CAPTURE_MODE = { ALL | AUTO | CUSTOM | NONE }
  | MAX_PLANS_PER_QUERY = number
  | WAIT_STATS_CAPTURE_MODE = { ON | OFF }
  | QUERY_CAPTURE_POLICY = ( <query_capture_policy_option_list> [,...n] )
}

<query_capture_policy_option_list> :: =
{
    STALE_CAPTURE_POLICY_THRESHOLD = number { DAYS | HOURS }
    | EXECUTION_COUNT = number
    | TOTAL_COMPILE_CPU_TIME_MS = number
    | TOTAL_EXECUTION_CPU_TIME_MS = number
}

<snapshot_option> ::=
{
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }
  | READ_COMMITTED_SNAPSHOT {ON | OFF }
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT {ON | OFF }
}
<sql_option> ::=
{
    ANSI_NULL_DEFAULT { ON | OFF }
  | ANSI_NULLS { ON | OFF }
  | ANSI_PADDING { ON | OFF }
  | ANSI_WARNINGS { ON | OFF }
  | ARITHABORT { ON | OFF }
  | COMPATIBILITY_LEVEL = { 150 | 140 | 130 | 120 | 110 | 100 }
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }
  | NUMERIC_ROUNDABORT { ON | OFF }
  | QUOTED_IDENTIFIER { ON | OFF }
  | RECURSIVE_TRIGGERS { ON | OFF }
}

<temporal_history_retention>::= TEMPORAL_HISTORY_RETENTION { ON | OFF }
```

## <a name="arguments"></a>인수

*database_name*     
수정할 데이터베이스의 이름입니다.

CURRENT     
`CURRENT`는 현재 데이터베이스에서 작업을 실행합니다. 모든 컨텍스트의 모든 옵션에서 `CURRENT`가 지원되는 것은 아닙니다. `CURRENT`가 실패할 경우 데이터베이스 이름을 지정해야 합니다.

**\<auto_option> ::=**      
자동 옵션을 제어합니다.

<a name="auto_create_statistics"></a> AUTO_CREATE_STATISTICS { **ON** | OFF }     
켜기     
쿼리 최적화 프로그램에서 필요에 따라 쿼리 조건자의 단일 열에 대한 통계를 생성하여 쿼리 계획 및 쿼리 성능을 향상합니다. 쿼리 최적화 프로그램에서 쿼리를 컴파일할 때 이러한 단일 열 통계가 생성됩니다. 단일 열 통계는 기존 통계 개체의 첫 번째 열이 아닌 열에 대해서만 생성됩니다.

기본값은 ON입니다. 대부분의 데이터베이스의 경우 기본 설정을 사용하는 것이 좋습니다.

OFF     
쿼리 최적화 프로그램에서 쿼리를 컴파일할 때 쿼리 조건자의 단일 열에 대한 통계를 생성하지 않습니다. 이 옵션을 OFF로 설정하면 최적이 아닌 쿼리 계획을 사용하므로 쿼리 성능이 저하됩니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_auto_create_stats_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAutoCreateStatistics` 속성을 검사하여 상태를 확인할 수도 있습니다.

자세한 내용은 [통계](../../relational-databases/statistics/statistics.md#statistics-options)에서 “통계 옵션” 섹션을 참조하세요.

INCREMENTAL = ON | **OFF**     
AUTO_CREATE_STATISTICS를 ON으로 설정하고 INCREMENTAL을 ON으로 설정합니다. 이 설정은 증분 통계가 지원될 때마다 자동으로 생성된 통계를 증분으로 만듭니다. 기본값은 OFF입니다. 자세한 내용은 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)를 참조하세요.

<a name="auto_shrink"></a> AUTO_SHRINK { ON | **OFF** }     
켜기     
데이터베이스 파일이 주기적인 축소의 후보가 됩니다.

데이터 파일과 로그 파일 모두 자동으로 축소될 수 있습니다. AUTO_SHRINK는 데이터베이스를 단순 복구 모델로 설정하거나 로그를 백업하는 경우에만 트랜잭션 로그의 크기를 줄입니다. 이 옵션이 OFF로 설정되면 사용되지 않는 공간을 정기적으로 검사하는 동안 데이터베이스 파일을 자동으로 축소하지 않습니다.

AUTO_SHRINK 옵션은 파일에서 사용되지 않는 공간이 25% 이상일 때 파일을 축소합니다. 이 옵션을 사용하면 파일이 두 가지 크기 중 하나로 축소됩니다. 다음 두 크기 중 더 큰 크기로 축소됩니다.

- 파일의 25%가 사용되지 않는 공간인 크기
- 파일 생성 시 파일의 크기

읽기 전용 데이터베이스는 축소할 수 없습니다.

OFF     
사용되지 않는 공간을 정기적으로 검사하는 동안에는 데이터베이스 파일을 자동으로 축소하지 않습니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_auto_shrink_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAutoShrink` 속성을 검사하여 상태를 확인할 수도 있습니다.

> [!NOTE]
> 포함된 데이터베이스에서는 AUTO_SHRINK 옵션을 사용할 수 없습니다.

<a name="auto_update_statistics"></a> AUTO_UPDATE_STATISTICS { **ON** | OFF }     
켜기     
쿼리에서 통계를 사용하거나 통계가 최신 정보가 아닌 경우 쿼리 최적화 프로그램에서 통계를 업데이트하도록 지정합니다. 삽입, 업데이트, 삭제 또는 병합 작업을 통해 테이블이나 인덱싱된 뷰의 데이터 분포가 변경되면 통계 내용이 더 이상 최신이 아니게 됩니다. 쿼리 최적화 프로그램은 마지막 통계 업데이트 이후 데이터 수정 개수를 계산한 다음, 이 수를 임계값과 비교하여 통계가 최신이 아니게 된 시점을 결정합니다. 임계값은 테이블 또는 인덱싱된 뷰의 행 수를 기준으로 합니다.

쿼리 최적화 프로그램은 쿼리를 컴파일하고 캐시된 쿼리 계획을 실행하기 전에 최신 정보가 아닌 통계가 있는지 확인합니다. 쿼리 최적화 프로그램은 쿼리 조건자의 열, 테이블 및 인덱싱된 뷰를 사용하여 어떤 통계가 최신이 아닌지 확인합니다. 쿼리 최적화 프로그램은 쿼리를 컴파일하기 전에 이 정보를 확인합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 캐시된 쿼리 계획을 실행하기 전에 쿼리 계획에서 최신 통계가 참조되는지 확인합니다.

AUTO_UPDATE_STATISTICS 옵션은 인덱스에 대해 생성된 통계, 쿼리 조건자의 단일 열 및 CREATE STATISTICS 문을 사용하여 생성된 통계에 적용됩니다. 이 옵션은 또한 필터링된 통계에도 적용됩니다.

기본값은 ON입니다. 대부분의 데이터베이스의 경우 기본 설정을 사용하는 것이 좋습니다.

AUTO_UPDATE_STATISTICS_ASYNC 옵션을 사용하여 통계를 동기적으로 업데이트할지 또는 비동기적으로 업데이트할지를 지정합니다.

OFF     
쿼리에서 통계를 사용하는 경우 쿼리 최적화 프로그램에서 통계를 업데이트하지 않도록 지정합니다. 통계가 최신이 아니게 된 경우에도 쿼리 최적화 프로그램에서 통계를 업데이트하지 않습니다. 이 옵션을 OFF로 설정하면 최적이 아닌 쿼리 계획을 사용하므로 쿼리 성능이 저하됩니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 is_auto_update_stats_on 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAutoUpdateStatistics` 속성을 검사하여 상태를 확인할 수도 있습니다.

자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)에서 “데이터베이스 차원의 통계 옵션 사용” 섹션을 참조하세요.

<a name="auto_update_statistics_async"></a> AUTO_UPDATE_STATISTICS_ASYNC { ON | **OFF** }     
켜기     
AUTO_UPDATE_STATISTICS 옵션에 대한 통계 업데이트를 비동기로 지정합니다. 쿼리 최적화 프로그램은 쿼리를 컴파일하기 전에 통계 업데이트가 완료될 때까지 기다리지 않습니다.

이 옵션을 ON으로 설정해도 AUTO_UPDATE_STATISTICS가 ON으로 설정되어 있지 않으면 영향을 주지 않습니다.

기본적으로 AUTO_UPDATE_STATISTICS_ASYNC 옵션은 OFF로 설정되어 있으므로 쿼리 최적화 프로그램은 통계를 동기적으로 업데이트합니다.

OFF     
AUTO_UPDATE_STATISTICS 옵션에 대한 통계 업데이트를 동기로 지정합니다. 쿼리 최적화 프로그램은 쿼리를 컴파일하기 전에 통계 업데이트가 완료될 때까지 기다립니다.

이 옵션을 OFF로 설정해도 AUTO_UPDATE_STATISTICS가 ON으로 설정되어 있지 않으면 영향을 주지 않습니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 is_auto_update_stats_async_on 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다.

동기 통계 업데이트 또는 비동기 통계 업데이트를 사용하는 경우에 대한 자세한 설명은 [통계](../../relational-databases/statistics/statistics.md)에서 “데이터베이스 차원의 통계 옵션 사용” 섹션을 참조하세요.

<a name="auto_tuning"></a> **\<automatic_tuning_option> ::=**      
**적용 대상**: [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]

`FORCE_LAST_GOOD_PLAN` [자동 튜닝](../../relational-databases/automatic-tuning/automatic-tuning.md) 옵션을 사용하거나 사용하지 않도록 설정합니다.

FORCE_LAST_GOOD_PLAN = { ON | **OFF** }     
켜기     
[!INCLUDE[ssde_md](../../includes/ssde_md.md)]은 새 SQL 계획이 성능 저하를 일으키는 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 쿼리에 마지막으로 성공한 계획을 자동으로 강제로 적용합니다. [!INCLUDE[ssde_md](../../includes/ssde_md.md)]는 강제 계획을 통해 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 쿼리의 쿼리 성능을 지속적으로 모니터링합니다. 성능이 향상되면 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]은 마지막으로 성공한 계획을 계속 사용합니다. 성능 향상이 검색되지 않으면 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]이 새 쿼리 계획을 생성합니다. 쿼리 저장소를 사용할 수 없거나 ‘읽기/쓰기’ 모드가 아닌 경우 문이 실패합니다.

OFF     
[!INCLUDE[ssde_md](../../includes/ssde_md.md)]은 [sys.dm_db_tuning_recommendations](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) 뷰에서 SQL 계획 변경으로 인한 잠재적인 쿼리 성능 저하를 보고합니다. 하지만 이러한 권장 사항은 자동으로 적용되지 않습니다. 사용자는 뷰에 표시된 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 스크립트를 적용하여 활성 권장 사항을 모니터링하고 확인된 문제를 해결할 수 있습니다. 이것은 기본값입니다.

**\<change_tracking_option> ::=**      
변경 내용 추적 옵션을 제어합니다. 변경 내용 추적을 설정 또는 해제하고 옵션을 설정 또는 변경할 수 있습니다. 예제는 이 문서의 뒷부분에 있는 “예제” 섹션을 참조하세요.

ON 데이터베이스에 변경 내용 추적을 사용하도록 설정합니다. 변경 내용 추적을 설정하면 AUTO CLEANUP 및 CHANGE RETENTION 옵션도 설정할 수 있습니다.

AUTO_CLEANUP = { ON | OFF }     
켜기     
지정된 보존 기간 후에 변경 내용 추적 정보가 자동으로 제거됩니다.

OFF     
변경 내용 추적 데이터가 데이터베이스에서 제거되지 않습니다.

CHANGE_RETENTION = *retention_period* { **DAYS** | HOURS | MINUTES }     
데이터베이스에 변경 내용 추적 정보를 보존하는 최소 기간을 지정합니다. 데이터는 AUTO_CLEANUP 값이 ON일 때만 제거됩니다.

*retention_period*는 보존 기간의 숫자 부분을 지정하는 정수입니다.

기본 보존 기간은 **2일**입니다. 최소 보존 기간은 1분입니다. 기본 보존 형식은 **일**입니다.

OFF     
데이터베이스에서 변경 내용 추적을 해제합니다. 데이터베이스에서 변경 내용 추적을 사용 중지하려면 모든 테이블에서 변경 내용 추적을 사용하지 않도록 설정해야 합니다.

**\<cursor_option> ::=**      
커서 옵션을 제어합니다.

CURSOR_CLOSE_ON_COMMIT { ON | OFF }     
켜기     
트랜잭션을 커밋하거나 롤백할 때 열려 있는 커서가 모두 닫힙니다.

OFF     
트랜잭션 커밋 시에는 커서가 그대로 열려 있으나 트랜잭션 롤백 시에는 INSENSITIVE 또는 STATIC으로 정의된 것을 제외한 모든 커서가 닫힙니다.

SET 문을 사용하여 설정한 연결 수준 설정은 CURSOR_CLOSE_ON_COMMIT의 기본 데이터베이스 설정보다 우선적으로 적용됩니다. ODBC 및 OLE DB 클라이언트는 기본적으로 세션의 CURSOR_CLOSE_ON_COMMIT을 OFF로 설정하여 연결 수준 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET CURSOR_CLOSE_ON_COMMIT](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)을 참조하세요.

이 옵션의 상태는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 is_cursor_close_on_commit_on 열 또는 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 IsCloseCursorsOnCommitEnabled 속성을 검사하여 확인할 수 있습니다. 커서는 연결이 끊어질 때만 암시적으로 할당이 취소됩니다. 자세한 내용은 [DECLARE CURSOR](../../t-sql/language-elements/declare-cursor-transact-sql.md)를 참조하세요.

**\<db_encryption_option> ::=**      
데이터베이스 암호화 상태를 제어합니다.

ENCRYPTION { ON | **OFF** }     
데이터베이스를 암호화하거나(ON) 암호화하지 않도록(OFF) 설정합니다. 데이터베이스 암호화에 대한 자세한 내용은 [투명한 데이터 암호화](../../relational-databases/security/encryption/transparent-data-encryption.md) 및 [Azure SQL Database를 사용한 투명한 데이터 암호화](../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)를 참조하세요.

데이터베이스 수준에서 암호화를 사용할 수 있으면 모든 파일 그룹이 암호화됩니다. 새로운 파일 그룹은 암호화된 속성을 상속합니다. 데이터베이스의 파일 그룹이 READ ONLY로 설정되면 데이터베이스 암호화 작업이 실패합니다.

[sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 동적 관리 뷰를 사용하면 데이터베이스의 암호화 상태를 확인할 수 있습니다.

**\<db_update_option> ::=**      
데이터베이스에 대한 업데이트 허용 여부를 제어합니다.

READ_ONLY     
사용자는 데이터베이스에서 데이터를 읽을 수 있지만 수정은 할 수 없습니다.

> [!NOTE]
> 쿼리 성능을 향상시키려면 데이터베이스를 READ_ONLY로 설정하기 전에 통계를 업데이트하십시오. 데이터베이스를 READ_ONLY로 설정한 후에 추가 통계가 필요한 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 tempdb에 통계를 만듭니다. 읽기 전용 데이터베이스의 통계에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.

READ_WRITE     
데이터베이스에서 읽기와 쓰기 작업을 할 수 있습니다.

이 상태를 변경하려면 데이터베이스에 대해 배타적 액세스 권한이 있어야 합니다.

**\<db_user_access_option> ::=**      
데이터베이스에 대한 사용자 액세스를 제어합니다.

RESTRICTED_USER     
`db_owner` 고정 데이터베이스 역할과 `dbcreator` 및 `sysadmin` 고정 서버 역할의 멤버만 데이터베이스에 연결할 수 있습니다. 연결할 수 있는 멤버의 수에는 제한이 없습니다. 데이터베이스에 대한 모든 연결은 ALTER DATABASE 문의 termination 절에 지정된 시간대에 끊어집니다. 데이터베이스가 RESTRICTED_USER 상태로 바뀐 후 자격이 없는 사용자의 연결 시도는 거부됩니다. SQL Managed Instance를 사용하여 **RESTRICTED_USER**를 수정할 수 없습니다.

MULTI_USER     
데이터베이스에 연결할 수 있는 적절한 권한이 있는 모든 사용자의 연결을 허용합니다.

이 옵션의 상태는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 user_access 열 또는 `UserAccess` property of the [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 UserAccess 속성을 검사하여 확인할 수 있습니다.

**\<delayed_durability_option> ::=**      
트랜잭션이 완전한 내구성이 있게 커밋될지 아니면 지연된 내구성이 있게 커밋될지 제어합니다.

DISABLED     
`SET DISABLED` 다음의 모든 트랜잭션은 완전한 내구성이 있습니다. ATOMIC 블록이나 COMMIT 문에 설정된 내구성 옵션은 무시됩니다.

ALLOWED     
`SET ALLOWED` 다음의 모든 트랜잭션은 ATOMIC 블록이나 COMMIT 문에 설정된 내구성 옵션에 따라 완전한 내구성이 있거나 지연된 내구성이 있습니다.

FORCED     
`SET FORCED` 다음의 모든 트랜잭션은 지연된 내구성이 있습니다. ATOMIC 블록이나 COMMIT 문에 설정된 내구성 옵션은 무시됩니다.

**\<PARAMETERIZATION_option> ::=**      
매개 변수화 옵션을 제어합니다.

PARAMETERIZATION { **SIMPLE** | FORCED }     
SIMPLE     
데이터베이스의 기본 동작에 따라 쿼리를 매개 변수화합니다.

FORCED     
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스의 모든 쿼리를 매개 변수화합니다.

이 옵션의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_parameterization_forced` 열을 검사하여 확인할 수 있습니다.

<a name="query-store"></a> **\<query_store_options> ::=**

ON | OFF | CLEAR [ ALL ]     
이 데이터베이스에서 쿼리 저장소를 사용할 수 있는지 여부를 제어하고, 쿼리 저장소의 내용 제거도 제어합니다.

켜기     
쿼리 저장소를 사용하도록 설정합니다.

OFF     
쿼리 저장소를 사용하지 않도록 합니다. 이것은 기본값입니다.

CLEAR     
쿼리 저장소의 내용을 제거합니다.

OPERATION_MODE     
쿼리 저장소의 작업 모드를 설명합니다. 유효한 값은 READ_ONLY 및 READ_WRITE입니다. READ_WRITE 모드에서 쿼리 저장소는 쿼리 계획 및 런타임 실행 통계 정보를 수집하고 유지합니다. READ_ONLY 모드에서는 쿼리 저장소에서 정보를 읽을 수 있지만 새 정보는 추가되지 않습니다. 쿼리 저장소의 최대 할당 공간이 최대값에 도달하면 쿼리 저장소는 작업 모드를 READ_ONLY로 변경합니다.

CLEANUP_POLICY     
쿼리 저장소의 데이터 보존 정책을 설명합니다. STALE_QUERY_THRESHOLD_DAYS는 쿼리에 대한 정보가 쿼리 저장소에 보존되는 일 수를 결정합니다. STALE_QUERY_THRESHOLD_DAYS는 **bigint** 형식입니다. 기본값은 30입니다. [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic 버전의 경우 기본값은 **7**일입니다.

DATA_FLUSH_INTERVAL_SECONDS     
쿼리 저장소에 기록된 데이터가 디스크에 유지되는 빈도를 결정합니다. 성능 최적화를 위해 쿼리 저장소에서 수집한 데이터는 디스크에 비동기적으로 기록됩니다. 비동기 전송이 발생하는 빈도는 DATA_FLUSH_INTERVAL_SECONDS 인수를 사용하여 구성됩니다. DATA_FLUSH_INTERVAL_SECONDS는 **bigint** 형식입니다. 기본값은 **900**(15분)입니다.

MAX_STORAGE_SIZE_MB     
쿼리 저장소에 할당되는 공간을 결정합니다. MAX_STORAGE_SIZE_MB는 **bigint** 형식입니다. 기본값은 **100MB**입니다.

> [!NOTE]
> `MAX_STORAGE_SIZE_MB` 한도는 엄격하게 적용되지 않습니다. 쿼리 저장소가 디스크에 데이터를 쓰는 경우에만 스토리지 크기가 확인됩니다. 이 간격은 `DATA_FLUSH_INTERVAL_SECONDS` 옵션 또는 [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 쿼리 저장소 대화 상자 옵션 **데이터 플러시 간격**에서 설정됩니다. 간격 기본값은 900초, 즉 15분입니다.
> 쿼리 저장소가 스토리지 크기 검사 간에 `MAX_STORAGE_SIZE_MB` 한도를 위반할 경우 읽기 전용 모드로 전환됩니다. `SIZE_BASED_CLEANUP_MODE`가 사용하도록 설정된 경우 `MAX_STORAGE_SIZE_MB` 한도를 적용하는 정리 메커니즘도 트리거됩니다.
> 충분한 공간이 확보되면 쿼리 저장소 모드가 자동으로 읽기/쓰기로 다시 전환됩니다.

> [!IMPORTANT]
> 워크로드 캡처에 10GB 이상의 디스크 공간이 필요하다고 생각되는 경우 워크로드를 재고하여 쿼리 계획을 다시 사용하도록 최적화하는 것이 좋습니다. 예를 들어 [강제 매개 변수화](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)를 사용하거나 쿼리 저장소 구성을 조정할 수 있습니다.    
> [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 쿼리 캡처 정책에 대한 추가 제어를 위해 `QUERY_CAPTURE_MODE`을 CUSTOM으로 설정할 수 있습니다.

INTERVAL_LENGTH_MINUTES     
런타임 실행 통계 데이터가 쿼리 저장소로 집계되는 간격을 결정합니다. 공간 사용을 최적화하기 위해 런타임 통계 저장소의 런타임 실행 통계는 고정된 시간 창을 통해 집계됩니다. 고정된 시간 창은 INTERVAL_LENGTH_MINUTES 인수를 사용하여 구성됩니다. INTERVAL_LENGTH_MINUTES는 **bigint** 형식입니다. 기본값은 **60**입니다.

SIZE_BASED_CLEANUP_MODE     
총 데이터양이 최대 크기에 가까워지면 정리를 자동으로 활성화할지 여부를 제어합니다.

OFF     
크기 기반 정리가 자동으로 활성화되지 않습니다.

AUTO     
디스크의 크기가 **max_storage_size_mb**의 90%에 도달하면 크기 기반 정리가 자동으로 활성화됩니다. 크기 기반 정리는 가장 저렴하고 가장 오래된 쿼리를 먼저 제거합니다. **max_storage_size_mb**가 약 80%가 되면 멈춥니다. 이것은 기본 구성 값입니다.

SIZE_BASED_CLEANUP_MODE는 **nvarchar** 형식입니다.

QUERY_CAPTURE_MODE { ALL \| AUTO \| CUSTOM \| NONE }     
현재 활성 쿼리 캡처 모드를 지정합니다.

ALL     
모든 쿼리가 캡처됩니다.

AUTO     
실행 횟수 및 리소스 사용을 기반으로 관련 쿼리를 캡처합니다. 이것이 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에 대한 기본 구성 값입니다.

없음     
새 쿼리 캡처를 중지합니다. 쿼리 저장소는 이미 캡처된 쿼리에 대한 컴파일 및 런타임 통계를 계속 수집합니다. 중요한 쿼리 캡처를 놓칠 수 있으므로 이 구성은 주의해서 사용해야 합니다.

QUERY_CAPTURE_MODE는 **nvarchar** 형식입니다.

max_plans_per_query     
각 쿼리에 대하여 유지되는 계획의 수를 나타내는 정수입니다. MAX_PLANS_PER_QUERY는 **int** 형식입니다. 기본값은 **200**입니다.

WAIT_STATS_CAPTURE_MODE { **ON** | OFF }     
쿼리별 대기 통계를 캡처할지 여부를 제어합니다.

켜기    
쿼리별 대기 통계 정보를 캡처합니다. 이 값은 기본 구성 값입니다.

OFF    
쿼리별 대기 통계 정보를 캡처하지 않습니다.

**\<query_capture_policy_option_list> :: =**      
쿼리 저장소 캡처 정책 옵션을 제어합니다. STALE_CAPTURE_POLICY_THRESHOLD를 제외하고 이 옵션은 정의된 부실 캡처 정책 임계값에 캡처해야 할 쿼리에 대해 수행해야 할 OR 조건을 정의합니다.

STALE_CAPTURE_POLICY_THRESHOLD = *number* { DAYS | HOURS }     
쿼리가 캡처되어야 하는지 여부를 결정하는 평가 간격 기간을 정의합니다. 기본값은 1일이며 1시간에서 7일까지 설정할 수 있습니다. *number*는 **int** 형식입니다.

EXECUTION_COUNT     
평가 기간 동안 쿼리가 실행되는 횟수를 정의합니다. 기본값은 30으로, 기본 부실 캡처 정책 임계값의 경우 쿼리가 쿼리 저장소에 유지되려면 하루에 30회 이상 실행되어야 합니다. EXECUTION_COUNT는 **int** 형식입니다.

TOTAL_COMPILE_CPU_TIME_MS     
평가 기간 동안 쿼리에 사용하는 총 경과 컴파일 CPU 시간을 정의합니다. 기본값은 1000으로, 기본 부실 캡처 정책 임계값의 경우 쿼리가 쿼리 저장소에 유지되려면 하루에 쿼리 컴파일에 사용된 총 CPU 시간이 1초 이상이어야 합니다. TOTAL_COMPILE_CPU_TIME_MS는 **int** 형식입니다.

TOTAL_EXECUTION_CPU_TIME_MS     
평가 기간 동안 쿼리에 사용하는 총 경과 실행 CPU 시간을 정의합니다. 기본값은 100으로, 기본 부실 캡처 정책 임계값의 경우 쿼리가 쿼리 저장소에 유지되려면 하루에 실행에 사용된 총 CPU 시간이 100ms 이상이어야 합니다. TOTAL_EXECUTION_CPU_TIME_MS는 **int** 형식입니다.

**\<snapshot_option> ::=**

트랜잭션 격리 수준을 결정합니다.

ALLOW_SNAPSHOT_ISOLATION { ON | OFF }     
켜기     
데이터베이스 수준에서 스냅샷 옵션을 사용하도록 설정합니다. 이 옵션을 사용하면 트랜잭션에서 스냅샷 격리를 사용하지 않는 경우에도 DML 문에서 행 버전을 생성하기 시작합니다. 이 옵션을 사용하도록 설정하면 트랜잭션에서 SNAPSHOT 트랜잭션 격리 수준을 지정할 수 있습니다. 트랜잭션이 SNAPSHOT 격리 수준에서 실행되면 모든 문에서 트랜잭션 시작 시점의 상태로 데이터 스냅샷을 봅니다. SNAPSHOT 격리 수준에서 실행되는 트랜잭션이 여러 데이터베이스의 데이터에 액세스할 경우 모든 데이터베이스에서 ALLOW_SNAPSHOT_ISOLATION이 ON으로 설정되어 있어야 합니다. 그렇지 않고 ALLOW_SNAPSHOT_ISOLATION이 OFF로 설정된 경우에는 트랜잭션 내의 각 문에서는 FROM 절의 참조에서 데이터베이스의 테이블에 대한 잠금 힌트를 사용해야 합니다.

OFF     
데이터베이스 수준에서 스냅샷 옵션을 해제합니다. 트랜잭션을 SNAPSHOT 트랜잭션 격리 수준으로 지정할 수 없습니다.

ALLOW_SNAPSHOT_ISOLATION을 새 상태로 설정하는 경우(ON에서 OFF로 또는 OFF에서 ON으로) ALTER DATABASE는 데이터베이스 내의 기존 트랜잭션이 모두 커밋될 때까지 호출자에게 제어권을 반환하지 않습니다. 데이터베이스가 이미 ALTER DATABASE 문에 지정된 상태인 경우 제어권은 호출자에게 즉시 반환됩니다. ALTER DATABASE 문이 제어권을 빨리 반환하지 않는 경우 [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md)를 사용하여 장기 트랜잭션이 있는지 여부를 확인합니다. ALTER DATABASE 문을 취소하면 데이터베이스는 ALTER DATABASE가 시작된 시점의 상태로 남게 됩니다. [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰는 데이터베이스에 있는 스냅샷 격리 트랜잭션의 상태를 나타냅니다. **snapshot_isolation_state_desc** = IN_TRANSITION_TO_ON인 경우 ALTER DATABASE ALLOW_SNAPSHOT_ISOLATION을 OFF로 설정하는 작업은 6초간 일시 중지된 다음, 다시 시도됩니다.

데이터베이스가 OFFLINE인 경우 ALLOW_SNAPSHOT_ISOLATION의 상태를 변경할 수 없습니다.

READ_ONLY 데이터베이스에서 ALLOW_SNAPSHOT_ISOLATION을 설정하는 경우 데이터베이스가 이후에 READ_WRITE로 설정되어도 이 설정은 그대로 유지됩니다.

master, model, msdb 및 tempdb 데이터베이스에 대해 ALLOW_SNAPSHOT_ISOLATION 설정을 변경할 수 있습니다. tempdb에 대한 설정을 변경하면 이 설정은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 중지 후 다시 시작할 때마다 유지됩니다. model 데이터베이스에 대한 설정을 변경하면 이 설정은 새로 생성된 모든 데이터베이스(tempdb 제외)의 기본값이 됩니다.

master 및 msdb 데이터베이스에 대해 이 옵션은 기본적으로 ON입니다.

이 옵션의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `snapshot_isolation_state` 열을 검사하여 확인할 수 있습니다.

READ_COMMITTED_SNAPSHOT { ON | **OFF** }     
켜기     
데이터베이스 수준에서 Read-Committed Snapshot 옵션을 사용하도록 설정합니다. 이 옵션을 사용하면 트랜잭션에서 스냅샷 격리를 사용하지 않는 경우에도 DML 문에서 행 버전을 생성하기 시작합니다. 이 옵션을 사용하도록 설정하면 READ COMMITTED 스냅샷 격리 수준을 지정하는 트랜잭션에서는 잠금 대신 행 버전 관리를 사용합니다. 트랜잭션이 READ COMMITTED 격리 수준에서 실행되면, 모든 문에 문 시작 시의 데이터 스냅샷이 표시됩니다.

OFF     
데이터베이스 수준에서 Read-Committed Snapshot 옵션을 끕니다. READ COMMITTED 격리 수준을 지정하는 트랜잭션에서는 잠금을 사용합니다.

READ_COMMITTED_SNAPSHOT을 ON 또는 OFF로 설정하려면 ALTER DATABASE 명령을 실행하는 연결을 제외하고 데이터베이스에 대한 활성 상태의 연결이 없어야 합니다. 그러나 데이터베이스가 단일 사용자 모드에 있을 필요는 없습니다. 데이터베이스가 OFFLINE인 경우 이 옵션의 상태를 변경할 수 없습니다.

READ_ONLY 데이터베이스에서 READ_COMMITTED_SNAPSHOT을 설정하는 경우 데이터베이스가 이후에 READ_WRITE로 설정되어도 이 설정은 그대로 유지됩니다.

master, tempdb 또는 msdb 시스템 데이터베이스에 대해서는 READ_COMMITTED_SNAPSHOT을 ON으로 설정할 수 없습니다. model 데이터베이스에 대한 설정을 변경하면 이 설정은 새로 생성된 모든 데이터베이스(tempdb 제외)의 기본값이 됩니다.

이 옵션의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_read_committed_snapshot_on` 열을 검사하여 확인할 수 있습니다.

> [!WARNING]
> **DURABILITY = SCHEMA_ONLY**를 사용하여 테이블이 만들어지고 그 후에 **READ_COMMITTED_SNAPSHOT**이 **ALTER DATABASE**를 사용하여 변경되면 테이블의 데이터는 손실됩니다.

MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT { ON | **OFF** }     
켜기     
트랜잭션 격리 수준이 SNAPSHOT보다 낮은 격리 수준으로 설정된 경우 메모리 최적화 테이블에 대한 해석된 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업이 SNAPSHOT 격리로 실행됩니다. 스냅샷보다 낮은 격리 수준의 예는 READ COMMITTED 또는 READ UNCOMMITTED입니다. 이 작업은 세션 수준에서 트랜잭션 격리 수준이 명시적으로 설정되었거나 기본값이 암시적으로 사용되는지에 관계없이 실행됩니다.

OFF     
메모리 최적화 테이블에서 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업에 대해 트랜잭션 격리 수준을 승격하지 않습니다.

데이터베이스가 OFFLINE인 경우 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT의 상태를 변경할 수 없습니다.

기본값은 OFF입니다.

이 옵션의 현재 설정은 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_memory_optimized_elevate_to_snapshot_on` 열을 검사하여 확인할 수 있습니다.

**\<sql_option> ::=**      
ANSI 호환 옵션을 데이터베이스 수준에서 제어합니다.

ANSI_NULL_DEFAULT { ON | OFF }     
CREATE TABLE 또는 ALTER TABLE 문에서 Null 허용 여부가 명시적으로 정의되어 있지 않은 열 또는 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)에 대한 기본값(NULL 또는 NOT NULL)을 결정합니다. 제약 조건이 정의된 열은 이 설정이 무엇이든 관계없이 제약 조건 규칙을 따릅니다.

켜기     
기본값은 NULL입니다.

OFF     
기본값이 NOT NULL입니다.

SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_NULL_DEFAULT에 대한 기본 데이터베이스 수준 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 세션의 ANSI_NULL_DEFAULT를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET ANSI_NULL_DFLT_ON](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)을 참조하세요.

ANSI 호환성을 위해 ANSI_NULL_DEFAULT 데이터베이스 옵션을 ON으로 설정하면 데이터베이스의 기본값이 NULL로 변경됩니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_ansi_null_default_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAnsiNullDefault` 속성을 검사하여 상태를 확인할 수도 있습니다.

ANSI_NULLS { ON | OFF }     
켜기     
Null 값에 대한 모든 비교는 UNKNOWN으로 평가됩니다.

OFF     
Null 값에 대한 비-UNICODE 값 비교는 두 값이 모두 NULL인 경우 TRUE로 평가됩니다.

> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 ANSI_NULLS가 항상 ON으로 설정되므로 명시적으로 이 옵션을 OFF로 설정한 애플리케이션에서는 오류가 발생합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.

  SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_NULLS에 대한 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 세션의 ANSI_NULLS를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET ANSI_NULLS](../../t-sql/statements/set-ansi-nulls-transact-sql.md)를 참조하세요.

> [!IMPORTANT]
> 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경하는 경우에도 SET ANSI_NULLS를 ON으로 설정해야 합니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_ansi_nulls_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAnsiNullsEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

ANSI_PADDING { ON | **OFF** }     
켜기     
변환하기 전에 문자열이 동일한 길이만큼 채워집니다. 문자열을 동일한 길이만큼 채운 후에 **varchar** 또는 **nvarchar** 데이터 형식에 대해 삽입합니다.

OFF     
문자 값의 후행 공백을 **varchar** 또는 **nvarchar** 열에 삽입합니다. 또한 **varbinary** 열에 삽입된 이진 값에서 후행 0을 유지합니다. 값은 열의 크기만큼 오른쪽에 공백으로 채워집니다.

OFF로 지정하면 이 설정은 새 열의 정의에만 영향을 줍니다.

> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 ANSI_PADDING이 항상 ON으로 설정되므로 명시적으로 이 옵션을 OFF로 설정한 애플리케이션에서는 오류가 발생합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. ANSI_PADDING은 항상 ON으로 설정하는 것이 좋습니다. 계산 열이나 인덱싱된 뷰에서 인덱스를 만들거나 조작할 때는 ANSI_PADDING을 ON으로 설정해야 합니다.

ANSI_PADDING을 ON으로 설정하면 Null을 허용하는 **char(_n_)** 및 **binary(_n_)** 열이 열 길이만큼 채워집니다. ANSI_PADDING이 OFF이면 후행 공백과 0이 잘립니다. Null을 허용하지 않는 **char(_n_)** 및 **binary(_n_)** 열은 항상 열 길이만큼 채워집니다.

  SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_PADDING에 대한 기본 데이터베이스 수준 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 세션의 ANSI_PADDING을 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET ANSI_PADDING](../../t-sql/statements/set-ansi-padding-transact-sql.md)을 참조하세요.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_ansi_padding_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAnsiPaddingEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

ANSI_WARNINGS { ON | **OFF** }     
켜기     
0으로 나누기 등의 조건이 발생할 때 오류 또는 경고가 발생합니다. 집계 함수에 Null 값이 나타나는 경우에도 오류 또는 경고가 발생합니다.

OFF     
0으로 나누기와 같은 상황이 발생해도 아무런 경고도 발생하지 않으며 Null 값이 반환됩니다.

> [!IMPORTANT]
> 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경하는 경우 SET ANSI_WARNINGS를 ON으로 설정해야 합니다.

  SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_WARNINGS에 대한 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 세션의 ANSI_WARNINGS를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET ANSI_WARNINGS](../../t-sql/statements/set-ansi-warnings-transact-sql.md)를 참조하세요.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_ansi_warnings_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAnsiWarningsEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

ARITHABORT { ON | OFF }     
켜기     
쿼리 실행 중 오버플로 또는 0으로 나누기 오류가 발생하면 쿼리를 종료합니다.

OFF     
해당 오류 중 하나가 발생하면 경고 메시지가 표시됩니다. 경고 메시지가 표시되더라도 오류가 발생하지 않으면 쿼리, 일괄 처리 또는 트랜잭션이 계속 진행됩니다.

> [!IMPORTANT]
> 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때 SET ARITHABORT를 ON으로 설정해야 합니다.

  [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_arithabort_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsArithmeticAbortEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

COMPATIBILITY_LEVEL = { 150 \| 140 \| 130 \| 120 \| 110 \| 100 }     
자세한 내용은 [ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.

CONCAT_NULL_YIELDS_NULL { ON | **OFF** }     
켜기     
피연산자 중 하나가 NULL일 경우 연결 연산의 결과는 NULL입니다. 예를 들어 문자열 "This is"와 NULL을 연결하면 결과는 "This is"가 아니라 NULL이 됩니다.

OFF     
Null 값은 빈 문자열로 취급됩니다.

> [!IMPORTANT]
> 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때 SET CONCAT_NULL_YIELDS_NULL은 반드시 ON으로 설정되어야 합니다.
>
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 CONCAT_NULL_YIELDS_NULL이 항상 ON으로 설정되므로 명시적으로 이 옵션을 OFF로 설정한 애플리케이션에서는 오류가 발생합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.

SET 문을 사용하여 설정한 연결 수준의 설정은 CONCAT_NULL_YIELDS_NULL의 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 때 세션의 CONCAT_NULL_YIELDS_NULL을 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. 자세한 내용은 [SET CONCAT_NULL_YIELDS_NULL](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)을 참조하세요.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_concat_null_yields_null_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsNullConcat` 속성을 검사하여 상태를 확인할 수도 있습니다.

QUOTED_IDENTIFIER { ON | OFF }     
켜기     
큰따옴표는 구분 식별자를 묶을 때 사용할 수 있습니다.

큰따옴표로 구분되는 모든 문자열은 개체 식별자로 해석됩니다. 따옴표 붙은 식별자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자 규칙을 따르지 않아도 됩니다. 따옴표 붙은 식별자는 키워드일 수 있으며 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자에서 허용되지 않는 문자를 포함할 수 있습니다. 작은따옴표(')가 리터럴 문자열의 일부로 포함되면 큰따옴표(")로 나타낼 수 있습니다.

OFF     
식별자는 따옴표 안에 있을 수 없으며 식별자에 대한 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 규칙을 따라야 합니다. 리터럴은 작은따옴표 또는 큰따옴표로 구분할 수 있습니다.

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서도 식별자를 대괄호([ ])로 구분할 수 있습니다. 대괄호로 묶은 식별자는 QUOTED_IDENTIFIER의 설정이 무엇이든 관계없이 항상 사용할 수 있습니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.

  테이블이 생성될 때 QUOTED IDENTIFIER 옵션은 해당 테이블의 메타데이터에서 항상 ON으로 저장됩니다. 이 옵션은 테이블이 생성될 때 OFF로 설정되는 경우에도 저장됩니다.

SET 문을 사용하여 설정한 연결 수준의 설정은 QUOTED_IDENTIFIER의 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 QUOTED_IDENTIFIER를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하면 클라이언트에서 문을 실행합니다. 자세한 내용은 [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.

  [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_quoted_identifier_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsQuotedIdentifiersEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

NUMERIC_ROUNDABORT { ON | OFF }     
켜기     
식에서 전체 자릿수가 손실되면 오류가 발생합니다.

OFF     
정밀도가 손실되어도 오류 메시지가 생성되지 않으며, 결과를 저장하는 열 또는 변수의 정밀도로 결과가 반올림됩니다.

> [!IMPORTANT]
> 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때 NUMERIC_ROUNDABORT는 OFF로 설정되어야 합니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_numeric_roundabort_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsNumericRoundAbortEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

RECURSIVE_TRIGGERS { ON | OFF }     
켜기     
AFTER 트리거의 재귀적 실행이 허용됩니다.

OFF     
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_recursive_triggers_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsRecursiveTriggersEnabled` 속성을 검사하여 상태를 확인할 수도 있습니다.

> [!NOTE]
> RECURSIVE_TRIGGERS가 OFF로 설정되면 직접 재귀만 금지됩니다. 간접 재귀를 사용하지 않도록 하려면 nested triggers 서버 옵션을 0으로 설정해야 합니다.

이 옵션의 상태는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 `is_recursive_triggers_on` 열 또는 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsRecursiveTriggersEnabled` 속성을 검사하여 확인할 수 있습니다.

**\<target_recovery_time_option> ::=**      
데이터베이스 단위로 간접 검사점의 빈도를 지정합니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 새 데이터베이스의 기본값은 **1분**이며, 이 값은 데이터베이스에서 간접 검사점을 사용한다는 것을 나타냅니다. 이전 버전의 기본값 0은 데이터베이스가 자동 검사점을 사용함을 나타내며, 빈도는 서버 인스턴스의 복구 간격 설정에 따라 달라집니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서는 대부분의 시스템에 1분을 권장합니다.

TARGET_RECOVERY_TIME **=** _target_recovery_time_ { SECONDS | MINUTES }     
*target_recovery_time*     
충돌 시 지정된 데이터베이스를 복구하는 데 걸리는 최대 시간을 지정합니다.

SECONDS     
*target_recovery_time* 이 초 단위로 표현됨을 나타냅니다.

MINUTES     
*target_recovery_time* 이 분 단위로 표현됨을 나타냅니다.

간접 검사점에 대한 자세한 내용은 [데이터베이스 검사점](../../relational-databases/logs/database-checkpoints-sql-server.md)을 참조하세요.

ROLLBACK AFTER *integer* [SECONDS] | ROLLBACK IMMEDIATE     
지정한 시간(초)이 경과한 후 롤백할 것인지 또는 즉시 롤백할 것인지를 지정합니다.

NO_WAIT     
요청된 데이터베이스 상태 또는 옵션 변경을 즉시 완료할 수 없는 경우 요청이 실패하도록 지정합니다. 즉시 완료는 트랜잭션이 자체적으로 커밋되거나 롤백되기를 기다리지 않음을 의미합니다.

## <a name="setting-options"></a><a name="SettingOptions"></a> 옵션 설정
데이터베이스 옵션에 대한 현재 설정을 검색하려면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰 또는 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)를 사용합니다.

데이터베이스 옵션을 설정하면 새 설정이 즉시 적용됩니다.

새로 만드는 모든 데이터베이스에 대한 데이터베이스 옵션의 기본값을 변경할 수 있습니다. 이렇게 하려면 model 데이터베이스에서 해당 데이터베이스 옵션을 변경합니다.

## <a name="examples"></a>예제

### <a name="a-setting-the-database-to-read_only"></a>A. 데이터베이스를 READ_ONLY로 설정
데이터베이스 또는 파일 그룹의 상태를 READ_ONLY 또는 READ_WRITE로 변경하려면 데이터베이스에 대한 단독 액세스 권한이 필요합니다. 다음 예제에서는 데이터베이스를 `RESTRICTED_USER` 모드로 설정하여 액세스를 제한합니다. [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 상태를 `READ_ONLY` 로 설정한 후 데이터베이스 액세스를 모든 사용자에게 반환합니다.

```sql
USE master;
GO
ALTER DATABASE [database_name]
SET RESTRICTED_USER;
GO
ALTER DATABASE [database_name]
SET READ_ONLY
GO
ALTER DATABASE [database_name]
SET MULTI_USER;
GO
```

### <a name="b-enabling-snapshot-isolation-on-a-database"></a>B. 데이터베이스에서 스냅샷 격리 활성화
다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대해 스냅샷 격리 프레임워크 옵션을 활성화합니다.

```sql
USE [database_name];
USE master;
GO
ALTER DATABASE [database_name]
SET ALLOW_SNAPSHOT_ISOLATION ON;
GO
-- Check the state of the snapshot_isolation_framework
-- in the database.
SELECT name, snapshot_isolation_state,
    snapshot_isolation_state_desc AS description
FROM sys.databases
WHERE name = N'[database_name]';
GO
```

결과 집합은 스냅샷 격리 프레임워크가 활성화되었음을 보여 줍니다.

|name |snapshot_isolation_state |description|
|-------------------- |------------------------|----------|
|[database_name] |1| 켜기 |

### <a name="c-enabling-modifying-and-disabling-change-tracking"></a>C. 변경 내용 추적 설정, 수정 및 해제
다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대해 변경 내용 추적을 설정하고 보존 기간을 `2` 일로 설정합니다.

```sql
ALTER DATABASE [database_name]
SET CHANGE_TRACKING = ON
(AUTO_CLEANUP = ON, CHANGE_RETENTION = 2 DAYS);
```

다음 예에서는 보존 기간을 `3` 일로 바꾸는 방법을 보여 줍니다.

```sql
ALTER DATABASE [database_name]
SET CHANGE_TRACKING (CHANGE_RETENTION = 3 DAYS);
```

다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대한 변경 내용 추적을 해제하는 방법을 보여 줍니다.

```sql
ALTER DATABASE [database_name]
SET CHANGE_TRACKING = OFF;
```

### <a name="d-enabling-the-query-store"></a>D. 쿼리 저장소를 사용하도록 설정
다음 예제에서는 쿼리 저장소를 사용하도록 설정하고 쿼리 저장소 매개 변수를 구성합니다.

```sql
ALTER DATABASE [database_name]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1024,
      INTERVAL_LENGTH_MINUTES = 60
    );
```

### <a name="e-enabling-the-query-store-with-wait-statistics"></a>E. 대기 통계가 포함된 쿼리 저장소를 사용하도록 설정
다음 예제에서는 쿼리 저장소를 사용하도록 설정하고 쿼리 저장소와 매개 변수를 구성합니다.

```sql
ALTER DATABASE [database_name]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      MAX_STORAGE_SIZE_MB = 1024,
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO,
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
    );
```

### <a name="f-enabling-the-query-store-with-custom-capture-policy-options"></a>F. 사용자 지정 캡처 정책 옵션이 포함된 쿼리 저장소를 사용하도록 설정
다음 예제에서는 쿼리 저장소를 사용하도록 설정하고 쿼리 저장소와 매개 변수를 구성합니다.

```sql
ALTER DATABASE [database_name]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      MAX_STORAGE_SIZE_MB = 1024,
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO,
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
      QUERY_CAPTURE_MODE = CUSTOM,
      QUERY_CAPTURE_POLICY = (
        STALE_CAPTURE_POLICY_THRESHOLD = 24 HOURS,
        EXECUTION_COUNT = 30,
        TOTAL_COMPILE_CPU_TIME_MS = 1000,
        TOTAL_EXECUTION_CPU_TIME_MS = 100
      )
    );
```

## <a name="see-also"></a>참고 항목

- [ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)
- [ALTER DATABASE 데이터베이스 미러링](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)
- [통계](../../relational-databases/statistics/statistics.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=azuresqldb-mi-current)
- [변경 내용 추적 설정 및 해제](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [쿼리 저장소에 대한 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-database-transact-sql-set-options.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [SQL 데이터베이스](alter-database-transact-sql-set-options.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [SQL Database<br />Managed Instance](alter-database-transact-sql-set-options.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        **_\* Azure Synapse<br />Analytics \*_** &nbsp;
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-synapse-analytics"></a>Azure Synapse Analytics

## <a name="syntax"></a>구문

```syntaxsql
ALTER DATABASE { database_name }
SET
{
    <optionspec> [ ,...n ]
}
;

<option_spec>::=
{
    <auto_option>
  | <db_encryption_option>
  | <query_store_options>
  | <result_set_caching>
  | <snapshot_option>
}
;

<auto_option> ::=
{
    AUTO_CREATE_STATISTICS { OFF | ON }
}

<db_encryption_option> ::=
{
    ENCRYPTION { ON | OFF }
}

<query_store_option> ::=
{
    QUERY_STORE { OFF |  ON }
}

<result_set_caching_option> ::=
{
    RESULT_SET_CACHING {ON | OFF}
}

<snapshot_option> ::=
{
    READ_COMMITTED_SNAPSHOT {ON | OFF }
}

```

## <a name="arguments"></a>인수

*database_name*     
수정할 데이터베이스의 이름입니다.

**<auto_option> ::=**      
자동 옵션을 제어합니다.

AUTO_CREATE_STATISTICS { **ON** | OFF }     

켜기     
쿼리 최적화 프로그램에서 필요에 따라 쿼리 조건자의 단일 열에 대한 통계를 생성하여 쿼리 계획 및 쿼리 성능을 향상합니다. 쿼리 최적화 프로그램에서 쿼리를 컴파일할 때 이러한 단일 열 통계가 생성됩니다. 단일 열 통계는 기존 통계 개체의 첫 번째 열이 아닌 열에 대해서만 생성됩니다.

기본값은 ON입니다. 대부분의 데이터베이스의 경우 기본 설정을 사용하는 것이 좋습니다.

OFF     
쿼리 최적화 프로그램에서 쿼리를 컴파일할 때 쿼리 조건자의 단일 열에 대한 통계를 생성하지 않습니다. 이 옵션을 OFF로 설정하면 최적이 아닌 쿼리 계획을 사용하므로 쿼리 성능이 저하됩니다.

### <a name="remarks"></a>설명
이 명령은 사용자 데이터베이스에 연결된 동안 실행되어야 합니다.

[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 i`s_auto_create_stats_on` 열을 검사하여 이 옵션의 상태를 확인할 수 있습니다. [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 `IsAutoCreateStatistics` 속성을 검사하여 상태를 확인할 수도 있습니다.

자세한 내용은 통계에서 “데이터베이스 차원의 통계 옵션 사용” 섹션을 참조하세요.

**<db_encryption_option> ::=**      
데이터베이스 암호화 상태를 제어합니다.

ENCRYPTION { ON | OFF }     

켜기     
데이터베이스를 암호화하도록 설정합니다.

OFF     
데이터베이스를 암호화하지 않도록 설정합니다.

데이터베이스 암호화에 대한 자세한 내용은 투명한 데이터 암호화 및 Azure SQL Database를 사용한 투명한 데이터 암호화를 참조하세요.

데이터베이스 수준에서 암호화를 사용할 수 있으면 모든 파일 그룹이 암호화됩니다. 새로운 파일 그룹은 암호화된 속성을 상속합니다. 데이터베이스의 파일 그룹이 READ ONLY로 설정되면 데이터베이스 암호화 작업이 실패합니다.

sys.dm_database_encryption_keys 동적 관리 뷰를 사용하여 데이터베이스의 암호화 상태와 암호화 검사 상태를 확인할 수 있습니다.

**<query_store_option> ::=**      
이 데이터 웨어하우스에서 쿼리 저장소를 사용할 수 있는지 여부를 제어합니다.

QUERY_STORE { ON |  **OFF**  }     

켜기     
쿼리 저장소를 사용하도록 설정합니다.

OFF     
쿼리 저장소를 사용하지 않도록 합니다. OFF가 기본값입니다.

> [!NOTE]
> [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]의 경우 사용자 데이터베이스에서 `ALTER DATABASE SET QUERY_STORE`를 실행해야 합니다. 다른 데이터 웨어하우스 인스턴스에서는 문을 실행할 수 없습니다.

**<result_set_caching_option> ::=**      
**적용 대상**: Azure Synapse Analytics  

쿼리 결과를 데이터베이스에 캐시할지 여부를 제어합니다.

RESULT_SET_CACHING { ON | OFF}     

켜기     
이 데이터베이스에서 반환된 쿼리 결과 집합이 데이터베이스에 캐시되도록 지정합니다.

OFF     
이 데이터베이스에서 반환된 쿼리 결과 집합이 데이터베이스에 캐시되지 않도록 지정합니다.

### <a name="remarks"></a>설명

이 명령은 `master` 데이터베이스에 연결되어 있는 동안 실행되어야 합니다.  이 데이터베이스 설정 변경이 즉시 적용됩니다.  쿼리 집합 캐싱으로 스토리지 비용이 발생합니다. 데이터베이스의 결과 캐싱을 사용하지 않도록 설정하면 영구 결과 캐시가 즉시 Azure Synapse 스토리지에서 삭제됩니다.

이 명령을 실행하여 데이터베이스의 결과 집합 캐싱 구성을 확인합니다.  결과 집합 캐싱이 켜진 경우 is_result_set_caching_on이 1을 반환합니다.

```sql
SELECT name, is_result_set_caching_on FROM sys.databases
WHERE name = <'Your_Database_Name'>
```

이 명령을 실행하여 캐시된 결과로 쿼리를 실행했는지 확인합니다.  result_cache_hit 열은 캐시 적중 시 1을 반환하고, 캐시 누락 시 0을 반환하고, 결과 집합 캐싱이 사용되지 않은 이유에 대해 음수 값을 반환합니다.  자세한 내용은 [sys.dm_pdw_exec_requests](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql?view=aps-pdw-2016-au7)를 참조하세요.  

```sql
SELECT request_id, command, result_cache_hit FROM sys.dm_pdw_exec_requests
WHERE request_id = <'Your_Query_Request_ID'>
```

> [!IMPORTANT]
> 결과 집합 개시를 만들고 캐시에서 데이터를 검색하는 작업은 데이터 웨어하우스 인스턴스의 컨트롤 노드에서 수행됩니다. 결과 집합 캐싱이 켜져 있을 때 큰 결과 집합을 반환하는 쿼리(예: >100만개 행)를 실행하면 컨트롤 노드에서 CPU 사용량이 증가하고 인스턴스의 전체 쿼리 응답 속도가 느려질 수 있습니다. 이러한 쿼리는 일반적으로 데이터 탐색 또는 ETL 작업 중에 사용됩니다. 컨트롤 노드의 스트레스를 방지하고 성능 문제가 발생하는 것을 방지하려면 사용자는 해당 유형의 쿼리를 실행하기 전에 데이터베이스에서 결과 집합 캐싱을 해제해야 합니다.  

결과 집합 캐싱을 사용한 성능 조정에 대한 자세한 내용은 [성능 조정 지침](/azure/sql-data-warehouse/performance-tuning-result-set-caching)을 참조하세요.

### <a name="permissions"></a>사용 권한

RESULT_SET_CACHING 옵션을 설정하려면 사용자는 서버 수준 보안 주체 로그인(프로비저닝 프로세스에서 만든 로그인)가 있거나 `dbmanager` 데이터베이스 역할의 멤버여야 합니다.  

**<snapshot_option> ::=**      
**적용 대상**: Azure Synapse Analytics

데이터베이스의 트랜잭션 격리 수준을 제어합니다.

READ_COMMITTED_SNAPSHOT  { ON | **OFF** }     

켜기     
데이터베이스 수준에서 READ_COMMITTED_SNAPSHOT 옵션을 사용하도록 설정합니다.

OFF     
데이터베이스 수준에서 READ_COMMITTED_SNAPSHOT 옵션을 끕니다.

### <a name="remarks"></a>설명

이 명령은 `master` 데이터베이스에 연결되어 있는 동안 실행되어야 합니다. 사용자 데이터베이스에 대해 READ_COMMITTED_SNAPSHOT을 켜거나 끄면 이 데이터베이스에 열려 있는 모든 연결이 종료됩니다. 데이터베이스 유지 관리 기간에 이 내용을 변경하거나 ALTER DATABASE 명령을 실행하는 연결 이외의 활성화된 데이터베이스 연결이 없을 때까지 대기하는 것이 좋습니다.  데이터베이스가 단일 사용자 모드에 있을 필요는 없습니다. 세션 수준에서 READ_COMMITTED_SNAPSHOT 설정을 변경하는 것은 지원되지 않습니다.  데이터베이스에 대한이 설정을 확인하려면 is_read_committed_snapshot_on의 열을 확인합니다.

READ_COMMITTED_SNAPSHOT이 설정된 데이터베이스에서 여러 데이터 버전이 있는 경우 버전의 검사로 인해 쿼리 성능이 저하될 수 있습니다. 트랜잭션을 오래 열어두면 데이터베이스 크기도 증가할 수 있습니다. 이 문제는 트랜잭션의 데이터 변경 내용으로 인해 버전 정리가 차단되는 경우에 발생합니다.  

### <a name="permissions"></a>사용 권한

READ_COMMITTED_SNAPSHOT 옵션을 설정하려면 사용자에게 데이터베이스에 대한 ALTER 권한이 있어야 합니다.

## <a name="examples"></a>예제

### <a name="check-statistics-setting-for-a-database"></a>데이터베이스에 대한 통계 설정 확인

```sql
SELECT name, is_auto_create_stats_on FROM sys.databases
```

### <a name="enable-query-store-for-a-database"></a>데이터베이스에 대해 쿼리 저장소 사용

```sql
ALTER DATABASE [database_name]
SET QUERY_STORE = ON;
```

### <a name="enable-result-set-caching-for-a-database"></a>데이터베이스의 결과 집합 캐싱 사용 설정

```sql
-- Run this command when connecting to the MASTER database

ALTER DATABASE [database_name]
SET RESULT_SET_CACHING ON;
```

### <a name="check-result-set-caching-setting-for-a-database"></a>데이터베이스의 결과 집합 캐싱 설정 확인

```sql
SELECT name, is_result_set_caching_on
FROM sys.databases;
```

### <a name="enable-the-read_committed_snapshot-option-for-a-database"></a>데이터베이스에 대해 Read_Committed_Snapshot 옵션 사용

```sql
-- Run this command when connecting to the MASTER database

ALTER DATABASE MyDatabase
SET READ_COMMITTED_SNAPSHOT ON
```

## <a name="see-also"></a>참고 항목

- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [Azure Synapse Analytics 모범 사례](/azure/sql-data-warehouse/sql-data-warehouse-best-practices#maintain-statistics)
- [Azure Synapse Analytics의 테이블 디자인](/azure/sql-data-warehouse/sql-data-warehouse-tables-overview#statistics)
- [Azure Synapse Analytics 언어 요소](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-language-elements)

::: moniker-end
