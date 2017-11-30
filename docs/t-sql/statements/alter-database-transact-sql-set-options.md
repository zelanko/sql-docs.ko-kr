---
title: "ALTER DATABASE SET 옵션 (Transact SQL) | Microsoft Docs"
description: "자동 튜닝, 암호화, SQL Server 및 Azure SQL 데이터베이스에서 쿼리 저장소와 같은 데이터베이스 옵션을 설정 하는 방법에 알아보기"
ms.custom: 
ms.date: 11/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
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
- automatic tuning
- SQL plan regression correction
- auto_create_statistics
- auto_update_statistics
ms.assetid: f76fbd84-df59-4404-806b-8ecb4497c9cc
caps.latest.revision: "159"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: d73118014577a947037bd25fd2fb3959a56a4e47
ms.sourcegitcommit: 28cccac53767db70763e5e705b8cc59a83c77317
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2017
---
# <a name="alter-database-set-options-transact-sql"></a>ALTER DATABASE SET 옵션(Transact-SQL) 
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스 옵션 설정과 관련된 ALTER DATABASE 구문을 제공합니다. 다른 ALTER DATABASE 구문은 다음 항목을 참조 하십시오.  
  
-   [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  

-   [ALTER database&#40; Azure SQL 데이터베이스 &#41;](alter-database-azure-sql-database.md) 

-   [ALTER database&#40; Azure SQL 데이터 웨어하우스 &#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)  
  
-   [ALTER database&#40; 병렬 데이터 웨어하우스 &#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)  
  
데이터베이스 미러링 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], 호환성 수준은 및 `SET` 옵션 이지만에 설명 되어 별도 항목으로 합니다. 자세한 내용은 참조 [ALTER 데이터베이스 데이터베이스 미러링 &#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md), [ALTER DATABASE SET hadr&#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-hadr.md), 및 [ALTER DATABASE 호환성 수준 &#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
> [!NOTE]  
> 사용 하 여 현재 세션에 대 한 많은 데이터베이스 설정 옵션을 구성할 수 있습니다 [SET 문 &#40; Transact SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md) 연결할 때 응용 프로그램에서 자주 구성 됩니다. 세션 수준 설정 옵션은 **ALTER DATABASE SET** 값을 재정의합니다. 아래에 설명된 데이터베이스 옵션은 다른 설정 옵션 값을 명시적으로 제공하지 않는 세션에 대해 설정할 수 있는 값입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER DATABASE { database_name  | CURRENT }  
SET   
{  
    <optionspec> [ ,...n ] [ WITH <termination> ]   
}  
  
<optionspec> ::=   
{  
    <auto_option>   
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
    ENCRYPTION { ON | OFF }  
  
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
          = OFF   
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
    | SIZE_BASED_CLEANUP_MODE = [ AUTO | OFF ]  
    | QUERY_CAPTURE_MODE = [ ALL | AUTO | NONE ]  
    | MAX_PLANS_PER_QUERY = number
    | WAIT_STATS_CAPTURE_MODE = [ ON | OFF ]
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
                  {   CREDENTIAL = <db_scoped_credential_name>  
                     | FEDERATED_SERVICE_ACCOUNT =  ON | OFF   
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
  | READ_COMMITTED_SNAPSHOT {ON | OFF }  
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = {ON | OFF }  
}  
<sql_option> ::=   
{  
    ANSI_NULL_DEFAULT { ON | OFF }   
  | ANSI_NULLS { ON | OFF }   
  | ANSI_PADDING { ON | OFF }   
  | ANSI_WARNINGS { ON | OFF }   
  | ARITHABORT { ON | OFF }   
  | COMPATIBILITY_LEVEL = { 90 | 100 | 110 | 120}  
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }   
  | NUMERIC_ROUNDABORT { ON | OFF }   
  | QUOTED_IDENTIFIER { ON | OFF }   
  | RECURSIVE_TRIGGERS { ON | OFF }   
}  
  
<target_recovery_time_option> ::=  
    TARGET_RECOVERY_TIME = target_recovery_time { SECONDS | MINUTES }  
  
<termination>  ::=   
{  
    ROLLBACK AFTER integer [ SECONDS ]   
  | ROLLBACK IMMEDIATE   
  | NO_WAIT  
}  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 수정할 데이터베이스의 이름입니다.  
  
 CURRENT  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 `CURRENT`현재 데이터베이스에서 작업을 수행 합니다. `CURRENT`모든 컨텍스트의 모든 옵션에 대해 지원 되지 않습니다. 경우 `CURRENT` 실패 하면 데이터베이스 이름을 제공 합니다.  
  
 **\<auto_option >:: =**  
  
 자동 옵션을 제어합니다.  
 <a name="auto_close"></a>AUTO_CLOSE {ON | OFF}  
 ON  
 마지막 사용자가 사용을 끝낸 후 데이터베이스가 종료되고 해당 리소스가 해제됩니다.  
  
 사용자가 데이터베이스를 다시 사용하려고 하면(예: 실행 하 여 예를 들어 한 `USE database_name` 문. AUTO_CLOSE가 ON으로 설정되어 있는 상태에서 데이터베이스가 완전히 종료된 경우 다음 번에 사용자가 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 다시 시작하고 데이터베이스 사용을 시도할 때까지 데이터베이스는 다시 열리지 않습니다.  
  
 OFF  
 마지막 사용자가 사용을 끝낸 후에도 데이터베이스는 열려 있는 상태가 됩니다.  
  
 AUTO_CLOSE 옵션을 사용하면 데이터베이스 파일을 일반 파일처럼 다룰 수 있기 때문에 데스크톱 데이터베이스에서 유용합니다. 데이터베이스 파일을 이동하거나 복사하여 백업을 만들 수도 있고 다른 사용자에게 전자 메일로 보낼 수도 있습니다. AUTO_CLOSE 프로세스는 비동기 프로세스이므로 데이터베이스를 반복적으로 열고 닫아도 성능이 저하되지 않습니다.  
  
> [!NOTE]  
>  AUTO_CLOSE 옵션 또는에 포함 된 데이터베이스에서 사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_auto_close_on 열 또는 DATABASEPROPERTYEX 함수의 IsAutoClose 속성을 검사하여 확인할 수 있습니다.  
  
> [!NOTE]  
>  AUTO_CLOSE가 ON으로 설정되어 있으면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 일부 열과 DATABASEPROPERTYEX 함수는 데이터베이스에서 데이터를 검색할 수 없는 경우 NULL을 반환합니다. 이 문제를 해결하려면 USE 문을 실행하여 데이터베이스를 엽니다.  
  
> [!NOTE]  
>  데이터베이스 미러링을 위해서는 AUTO_CLOSE가 OFF로 설정되어 있어야 합니다.  
  
 데이터베이스가 AUTOCLOSE = ON으로 설정되어 있으면 자동 데이터베이스 종료를 시작하는 작업이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 계획 캐시를 삭제합니다. 계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 서비스 팩 2 이상에서는 계획 캐시의 삭제된 각 캐시스토어에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 "데이터베이스 유지 관리 또는 재구성 작업으로 인해 '%s' 캐시스토어(계획 캐시의 일부)에 대한 캐시스토어 플러시가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 %d번 발견되었습니다"라는 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.  
 
 <a name="auto_create_statistics"></a>AUTO_CREATE_STATISTICS {ON | OFF}  
 ON  
 쿼리 최적화 프로그램에서 필요에 따라 쿼리 조건자의 단일 열에 대한 통계를 생성하여 쿼리 계획 및 쿼리 성능을 향상시킵니다. 쿼리 최적화 프로그램에서 쿼리를 컴파일할 때 이러한 단일 열 통계가 생성됩니다. 단일 열 통계는 기존 통계 개체의 첫 번째 열이 아닌 열에 대해서만 생성됩니다.  
  
 기본값은 ON입니다. 대부분의 데이터베이스의 경우 기본 설정을 사용하는 것이 좋습니다.  
  
 OFF  
 쿼리 최적화 프로그램에서 쿼리를 컴파일할 때 쿼리 조건자의 단일 열에 대한 통계를 생성하지 않습니다. 이 옵션을 OFF로 설정하면 최적이 아닌 쿼리 계획을 사용하므로 쿼리 성능이 저하됩니다.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_auto_create_stats_on 열 또는 DATABASEPROPERTYEX 함수의 IsAutoCreateStatistics 속성을 검사하여 확인할 수 있습니다.  
  
 자세한 내용은 "데이터베이스 차원의 통계 옵션 사용" 섹션을 참조 [통계](../../relational-databases/statistics/statistics.md)합니다.  
  
 INCREMENTAL = ON | OFF  
 AUTO_CREATE_STATISTICS가 ON이고 INCREMENTAL이 ON으로 설정되면, 자동으로 생성되는 통계가 증분 통계가 지원될 때마다 증분으로 생성됩니다. 기본값은 OFF입니다. 자세한 내용은 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)를 참조하세요.  
  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 <a name="auto_shrink"></a>AUTO_SHRINK {ON | OFF}  
 ON  
 데이터베이스 파일이 주기적인 축소의 후보가 됩니다.  
  
 데이터 파일과 로그 파일 모두 자동으로 축소될 수 있습니다. AUTO_SHRINK는 데이터베이스가 단순 복구 모델로 설정되거나 로그가 백업된 경우에만 트랜잭션 로그의 크기를 축소합니다. 이 옵션이 OFF로 설정되면 사용되지 않는 공간을 정기적으로 검사하는 동안 데이터베이스 파일을 자동으로 축소하지 않습니다.  
  
 AUTO_SHRINK 옵션은 파일에서 사용되지 않는 공간이 25% 이상일 때 파일을 축소합니다. 파일은 파일의 25%가 사용되지 않을 때의 크기 또는 파일이 만들어졌을 때의 크기 중 더 큰 크기로 축소됩니다.  
  
 읽기 전용 데이터베이스는 축소할 수 없습니다.  
  
 OFF  
 사용되지 않는 공간을 정기적으로 검사하는 동안에는 데이터베이스 파일을 자동으로 축소하지 않습니다.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_auto_shrink_on 열 또는 DATABASEPROPERTYEX 함수의 IsAutoShrink 속성을 검사하여 확인할 수 있습니다.  
  
> [!NOTE]  
> 포함된 데이터베이스에서는 AUTO_SHRINK 옵션을 사용할 수 없습니다.  
  
 <a name="auto_update_statistics"></a>AUTO_UPDATE_STATISTICS {ON | OFF}  
 ON  
 쿼리에서 통계를 사용하거나 통계가 최신이 아닐 때 쿼리 최적화 프로그램에서 통계를 업데이트하도록 지정합니다. 삽입, 업데이트, 삭제 또는 병합 작업을 통해 테이블이나 인덱싱된 뷰의 데이터 분포가 변경되면 통계 내용이 더 이상 최신이 아니게 됩니다. 쿼리 최적화 프로그램은 마지막 통계 업데이트 이후 데이터 수정 개수를 계산한 다음 이 수를 임계값과 비교하여 통계가 최신이 아니게 된 시점을 결정합니다. 임계값은 테이블 또는 인덱싱된 뷰의 행 수를 기준으로 합니다.  
  
 쿼리 최적화 프로그램은 쿼리를 컴파일하기 전과 캐시된 쿼리 계획을 실행하기 전에 최신이 아닌 통계가 있는지를 확인합니다. 쿼리 최적화 프로그램은 쿼리를 컴파일하기 전에 쿼리 조건자의 열, 테이블 및 인덱싱된 뷰를 사용하여 어떤 통계가 최신이 아닌지 결정합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 캐시된 쿼리 계획을 실행하기 전에 쿼리 계획에서 최신 통계가 참조되는지 확인합니다.  
  
 AUTO_UPDATE_STATISTICS 옵션은 인덱스에 대해 생성된 통계, 쿼리 조건자의 단일 열 및 CREATE STATISTICS 문을 사용하여 생성된 통계에 적용됩니다. 이 옵션은 또한 필터링된 통계에도 적용됩니다.  
  
 기본값은 ON입니다. 대부분의 데이터베이스의 경우 기본 설정을 사용하는 것이 좋습니다.  
  
 AUTO_UPDATE_STATISTICS_ASYNC 옵션을 사용하여 통계를 동기적으로 업데이트할지 또는 비동기적으로 업데이트할지를 지정합니다.  
  
 OFF  
 쿼리에서 통계를 사용하거나 통계가 최신이 아닐 때 쿼리 최적화 프로그램에서 통계를 업데이트하지 않도록 지정합니다. 이 옵션을 OFF로 설정하면 최적이 아닌 쿼리 계획을 사용하므로 쿼리 성능이 저하됩니다.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_auto_update_stats_on 열 또는 DATABASEPROPERTYEX 함수의 IsAutoUpdateStatistics 속성을 검사하여 확인할 수 있습니다.  
  
 자세한 내용은 "데이터베이스 차원의 통계 옵션 사용" 섹션을 참조 [통계](../../relational-databases/statistics/statistics.md)합니다.  
  
 <a name="auto_update_statistics_async"></a>AUTO_UPDATE_STATISTICS_ASYNC {ON | OFF}  
 ON  
 AUTO_UPDATE_STATISTICS 옵션에 대한 통계 업데이트를 비동기로 지정합니다. 쿼리 최적화 프로그램은 쿼리를 컴파일하기 전에 통계 업데이트가 완료될 때까지 기다리지 않습니다.  
  
 이 옵션을 ON으로 설정해도 AUTO_UPDATE_STATISTICS가 ON으로 설정되어 있지 않으면 영향을 주지 않습니다.  
  
 기본적으로 AUTO_UPDATE_STATISTICS_ASYNC 옵션은 OFF로 설정되므로 쿼리 최적화 프로그램은 통계를 동기적으로 업데이트합니다.  
  
 OFF  
 AUTO_UPDATE_STATISTICS 옵션에 대한 통계 업데이트를 동기로 지정합니다. 쿼리 최적화 프로그램은 쿼리를 컴파일하기 전에 통계 업데이트가 완료될 때까지 기다립니다.  
  
 이 옵션을 OFF로 설정해도 AUTO_UPDATE_STATISTICS가 ON으로 설정되어 있지 않으면 영향을 주지 않습니다.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_auto_update_stats_async_on 열을 검사하여 확인할 수 있습니다.  
  
 동기 또는 비동기 통계 업데이트를 사용 하는 경우를 설명 하는 자세한 내용은 "데이터베이스 차원의 통계 옵션 사용" 섹션을 참조 [통계](../../relational-databases/statistics/statistics.md)합니다.  
  
 <a name="auto_tuning"></a> **\<automatic_tuning_option >:: =**  
 **적용 대상**: [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  

 설정 하거나 해제 `FORCE_LAST_GOOD_PLAN` [자동 튜닝](../../relational-databases/automatic-tuning/automatic-tuning.md) 옵션입니다.  
  
 FORCE_LAST_GOOD_PLAN = {ON | OFF}  
 ON  
 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 에서 마지막 알려진된 좋은 계획을 자동으로 강제는 [!INCLUDE[tsql_md](../../includes/tsql_md.md)] 새 SQL 계획 한 성능 저하가 발생 하는 위치 쿼리 합니다. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 계속 해 서의 쿼리 성능을 모니터링 하는 [!INCLUDE[tsql_md](../../includes/tsql_md.md)] 강제 계획을 사용 하 여 쿼리 합니다. 성능 향상이 없으면는 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 는 마지막 알려진된 좋은 계획에 사용 하 여 계속 합니다. 성능 향상, 검색 되지 않는 경우는 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 새 SQL 계획을 생성 합니다. 쿼리 저장소를 사용 하지 않는 경우 또는 없는 경우 문이 실패 합니다 *읽기 / 쓰기* 모드입니다.   

 OFF  
 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 에 SQL 계획 변경으로 인 한 잠재적 쿼리 성능 저하 보고 [sys.dm_db_tuning_recommendations](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) 보기. 그러나 이러한 권장 사항은 자동으로 적용 되지 않습니다. 사용자에 적용 하 여 활성 권장 사항 및 문제를 식별 하는 해결을 모니터링할 수 [!INCLUDE[tsql_md](../../includes/tsql_md.md)] 보기에 표시 되는 스크립트입니다. 이 값은 기본값입니다.

 **\<change_tracking_option >:: =**  
  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 변경 내용 추적 옵션을 제어합니다. 변경 내용 추적을 설정 또는 해제하고 옵션을 설정 또는 변경할 수 있습니다. 예를 보려면 이 항목의 뒤 부분에 나오는 예 섹션을 참조하십시오.  
  
 ON  
 데이터베이스에 변경 내용 추적을 설정합니다. 변경 내용 추적을 설정하면 AUTO CLEANUP 및 CHANGE RETENTION 옵션도 설정할 수 있습니다.  
  
 AUTO_CLEANUP = { ON | OFF }  
 ON  
 지정된 보존 기간 후에 변경 내용 추적 정보가 자동으로 제거됩니다.  
  
 OFF  
 변경 내용 추적 데이터가 데이터베이스에서 제거되지 않습니다.  
  
 CHANGE_RETENTION =*retention_period* {일 | 시간 | 시간 (분)를 (를)  
 데이터베이스에 변경 내용 추적 정보를 보존하는 최소 기간을 지정합니다. 데이터는 AUTO_CLEANUP 값이 ON일 때만 제거됩니다.  
  
 *retention_period* 보존 기간의 숫자 부분을 지정 하는 정수입니다.  
  
 기본 보존 기간은 2일입니다. 최소 보존 기간은 1분입니다. 기본 보존 유형 (일)입니다.  
  
 OFF  
 데이터베이스에서 변경 내용 추적을 해제합니다. 데이터베이스에서 변경 내용 추적을 해제하려면 모든 테이블에서 변경 내용 추적을 해제해야 합니다.  
  
 **\<containment_option >:: =**  
  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 데이터베이스 포함 옵션을 제어합니다.  
  
 CONTAINMENT = {NONE | (를) 부분  
 없음  
 데이터베이스가 포함된 데이터베이스가 아닙니다.  
  
 PARTIAL  
 데이터베이스가 포함된 데이터베이스입니다. 데이터베이스에 복제, 변경 데이터 캡처 또는 변경 내용 추적을 사용하도록 설정되어 있는 경우 데이터베이스를 부분적으로 포함된 데이터베이스로 설정하면 실패합니다. 실패 후에는 오류 검사가 중지됩니다. 포함된 데이터베이스에 대한 자세한 내용은 [Contained Databases](../../relational-databases/databases/contained-databases.md)를 참조하십시오.  
  
> [!NOTE]  
> Containment에서 구성할 수 없는 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다. 포함을 명시적으로 지정 하지 않을 하지만 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 데이터베이스 사용자와 같은 포함 된 포함 된 기능을 사용할 수 있습니다.  
  
 **\<cursor_option >:: =**  
  
 커서 옵션을 제어합니다.  
  
 CURSOR_CLOSE_ON_COMMIT { ON | OFF }  
 ON  
 트랜잭션이 커밋되거나 롤백될 때 열린 모든 커서가 닫힙니다.  
  
 OFF  
 트랜잭션 커밋 시에는 커서가 그대로 열려 있으나 트랜잭션 롤백 시에는 INSENSITIVE 또는 STATIC으로 정의된 것을 제외한 모든 커서가 닫힙니다.  
  
 SET 문을 사용하여 설정한 연결 수준 설정은 CURSOR_CLOSE_ON_COMMIT의 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 때 세션의 CURSOR_CLOSE_ON_COMMIT을 OFF로 설정하여 연결 수준의 SET 문을 실행합니다. 자세한 내용은 [SET CURSOR_CLOSE_ON_COMMIT&#40;Transact-SQL&#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)을 참조하세요.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_cursor_close_on_commit_on 열 또는 DATABASEPROPERTYEX 함수의 IsCloseCursorsOnCommitEnabled 속성을 검사하여 확인할 수 있습니다.  
  
 CURSOR_DEFAULT { LOCAL | GLOBAL }  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 커서 범위가 LOCAL인지 GLOBAL인지 여부를 제어합니다.  
  
 LOCAL  
 LOCAL을 지정하고 커서를 만들 때 GLOBAL로 정의하지 않은 경우 커서의 범위는 커서가 생성된 일괄 처리, 저장 프로시저 또는 트리거에 로컬로 적용됩니다. 커서 이름은 그 범위 내에서만 유효합니다. 일괄 처리, 저장 프로시저, 트리거의 로컬 커서 변수 또는 저장 프로시저의 OUTPUT 매개 변수에서 커서를 참조할 수 있습니다. 커서는 OUTPUT 매개 변수에서 다시 전달되지 않는 한 일괄 처리, 저장 프로시저 또는 트리거가 종료될 때 암시적으로 할당이 취소됩니다. OUTPUT 매개 변수에서 커서가 다시 전달되면 커서를 참조하는 마지막 변수의 할당이 취소되거나 범위를 벗어날 때 커서의 할당이 취소됩니다.  
  
 GLOBAL  
 GLOBAL을 지정하고 커서를 만들 때 LOCAL로 정의하지 않은 경우 커서의 범위는 연결에 대해 전역으로 적용됩니다. 연결되어 실행하는 모든 저장 프로시저 또는 일괄 처리에서 커서 이름을 참조할 수 있습니다.  
  
 커서는 연결이 끊어질 때만 암시적으로 할당이 취소됩니다. 자세한 내용은 참조 [DECLARE CURSOR &#40; Transact SQL &#41; ](../../t-sql/language-elements/declare-cursor-transact-sql.md).  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_local_cursor_default 열 또는 DATABASEPROPERTYEX 함수의 IsLocalCursorsDefault 속성을 검사하여 확인할 수 있습니다.  
  
 **\<database_mirroring >**  
  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 인수 설명에 대 한 참조 [ALTER 데이터베이스 데이터베이스 미러링 &#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md).  
  
 **\<date_correlation_optimization_option >:: =**  
  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 date_correlation_optimization 옵션을 제어합니다.  
  
 DATE_CORRELATION_OPTIMIZATION { ON | OFF }  
 ON  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]FOREIGN KEY 제약 조건으로 연결 되 고 있는 데이터베이스에 두 테이블 간의 상관 관계 통계를 유지 관리 **datetime** 열입니다.  
  
 OFF  
 상관 관계 통계를 유지하지 않습니다.  
  
 DATE_CORRELATION_OPTIMIZATION을 ON으로 설정하려면 ALTER DATABASE 문을 실행하는 연결을 제외하고 데이터베이스에 대한 활성 연결이 없어야 합니다. 그런 후에는 여러 개의 연결이 지원됩니다.  
  
 이 옵션의 현재 설정은 sys.databases 카탈로그 뷰의 is_date_correlation_on 열을 검사하여 확인할 수 있습니다.  
  
 **\<db_encryption_option >:: =**  
  
 데이터베이스 암호화 상태를 제어합니다.  
  
 ENCRYPTION {ON | OFF}  
 데이터베이스를 암호화하거나(ON) 암호화하지 않도록(OFF) 설정합니다. 데이터베이스 암호화에 대 한 자세한 내용은 참조 [투명 한 데이터 암호화 &#40; Tde&#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md), 및 [Azure SQL 데이터베이스를 사용한 투명 한 데이터 암호화](../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)합니다.  
  
 데이터베이스 수준에서 암호화가 설정되면 모든 파일 그룹이 암호화됩니다. 새로운 파일 그룹은 암호화된 속성을 상속합니다. 데이터베이스의 파일 그룹이 **READ ONLY**로 설정되면 데이터베이스 암호화 작업이 실패합니다.  
  
 사용 하 여 데이터베이스의 암호화 상태를 볼 수는 [sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 동적 관리 뷰.  
  
 **\<db_state_option >:: =**  
  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 데이터베이스의 상태를 제어합니다.  
  
 OFFLINE  
 데이터베이스가 닫히고 완전히 종료되어 오프라인 상태로 표시됩니다. 데이터베이스가 오프라인 상태인 동안에는 데이터베이스를 수정할 수 없습니다.  
  
 ONLINE  
 데이터베이스가 열려 사용할 수 있게 됩니다.  
  
 EMERGENCY  
 데이터베이스가 READ_ONLY로 표시되고 로깅이 비활성화되며 sysadmin 고정 서버 역할의 멤버로 액세스가 제한됩니다. EMERGENCY는 주로 문제 해결을 위해 사용됩니다. 예를 들어 손상된 로그 파일로 인해 주의 대상으로 표시된 데이터베이스를 EMERGENCY 상태로 설정할 수 있습니다. 이 경우 시스템 관리자는 읽기 전용으로 데이터베이스에 액세스할 수 있습니다. sysadmin 고정 서버 역할의 멤버만 데이터베이스를 EMERGENCY 상태로 설정할 수 있습니다.  
  
> [!NOTE]  
> **사용 권한:** 데이터베이스를 오프 라인 또는 응급 상태로 변경 하려면 주제 데이터베이스에 대 한 ALTER DATABASE 권한이 필요 합니다. 데이터베이스를 오프라인 상태에서 온라인 상태로 전환하려면 서버 수준 ALTER ANY DATABASE 권한이 필요합니다.  
  
 상태 및 state_desc 열을 검사 하 여이 옵션의 상태를 확인할 수 있습니다는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰 또는의 Status 속성은 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수입니다. 자세한 내용은 [Database States](../../relational-databases/databases/database-states.md)을 참조하세요.  
  
 RESTORING으로 표시된 데이터베이스는 OFFLINE, ONLINE 또는 EMERGENCY로 설정할 수 없습니다. 활성 복원 작업 중이나 데이터베이스 또는 로그 파일의 복원 작업이 손상된 백업 파일로 인해 실패할 경우 데이터베이스가 RESTORING 상태일 수 있습니다.  
  
 **\<db_update_option >:: =**  
  
 데이터베이스에 대한 업데이트 허용 여부를 제어합니다.  
  
 READ_ONLY  
 사용자는 데이터베이스에서 데이터를 읽을 수 있지만 수정은 할 수 없습니다.  
  
> [!NOTE]  
>  쿼리 성능을 향상시키려면 데이터베이스를 READ_ONLY로 설정하기 전에 통계를 업데이트하십시오. 데이터베이스를 READ_ONLY로 설정한 후에 추가 통계가 필요한 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 tempdb에 통계를 만듭니다. 읽기 전용 데이터베이스에 대 한 통계에 대 한 자세한 내용은 참조 [통계](../../relational-databases/statistics/statistics.md)합니다.  
  
 READ_WRITE  
 데이터베이스에서 읽기와 쓰기 작업을 할 수 있습니다.  
  
 이 상태를 변경하려면 데이터베이스에 대해 배타적 액세스 권한이 있어야 합니다. 자세한 내용은 SINGLE_USER 절을 참조하십시오.  
  
> [!NOTE]  
> [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 연결된 데이터베이스에서 SET { READ_ONLY | READ_WRITE }는 해제됩니다.  
  
 **\<db_user_access_option >:: =**  
  
 데이터베이스에 대한 사용자 액세스를 제어합니다.  
  
 SINGLE_USER  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 한 번에 한 사용자만 데이터베이스에 액세스할 수 있도록 지정합니다. SINGLE_USER가 지정된 상태에서 다른 사용자들이 데이터베이스에 연결되어 있는 경우 모든 사용자가 지정된 데이터베이스와의 연결을 끊을 때까지 ALTER DATABASE 문이 차단됩니다. 이 동작을 재정의 하려면 참조는 WITH \<종료 > 절.  
  
 옵션을 설정한 사용자가 로그오프해도 데이터베이스는 SINGLE_USER 모드로 유지됩니다. 이때 다른 한 명의 사용자만 데이터베이스에 연결할 수 있습니다.  
  
 데이터베이스를 SINGLE_USER로 설정하기 전에 AUTO_UPDATE_STATISTICS_ASYNC 옵션이 OFF로 설정되어 있는지 확인합니다. 이 옵션이 ON으로 설정되면 통계 업데이트에 사용되는 백그라운드 스레드가 데이터베이스에 대한 연결을 점유하므로 사용자는 단일 사용자 모드로 데이터베이스에 액세스할 수 없습니다. 이 옵션의 상태를 보려면 is_auto_update_stats_async_on 열을 쿼리는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰에 있습니다. 옵션이 ON으로 설정되어 있으면 다음 태스크를 수행합니다.  
  
1.  AUTO_UPDATE_STATISTICS_ASYNC를 OFF로 설정합니다.  
  
2.  쿼리하여 활성 비동기 통계 작업에 대 한 확인은 [sys.dm_exec_background_job_queue](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md) 동적 관리 뷰.  
  
 활성 작업이 있을 경우 작업을 완료 하거나, 사용 하 여이 수동으로 종료를 허용 하거나 [KILL STATS JOB](../../t-sql/language-elements/kill-stats-job-transact-sql.md)합니다.  
  
RESTRICTED_USER  
 RESTRICTED_USER는 db_owner 고정 데이터베이스 역할 및 dbcreator와 sysadmin 고정 서버 역할의 멤버만 데이터베이스로의 연결을 허용하지만 연결되는 수는 제한하지 않습니다. 데이터베이스에 대한 모든 연결은 ALTER DATABASE 문의 termination 절에 지정된 시간대에 끊어집니다. 데이터베이스가 RESTRICTED_USER 상태로 바뀐 후 자격이 없는 사용자의 연결 시도는 거부됩니다.  
  
MULTI_USER  
 데이터베이스에 연결할 수 있는 적절한 권한이 있는 모든 사용자의 연결을 허용합니다.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 user_access 열 또는 DATABASEPROPERTYEX 함수의 UserAccess 속성을 검사하여 확인할 수 있습니다.  
  
 **\<delayed_durability_option >:: =**  
  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 트랜잭션이 완전한 내구성이 있게 커밋될지 아니면 지연된 내구성이 있게 커밋될지 제어합니다.  
  
 DISABLED  
 SET DISABLED 다음의 모든 트랜잭션은 완전한 내구성이 있습니다. ATOMIC 블록이나 COMMIT 문에 설정된 내구성 옵션은 무시됩니다.  
  
 ALLOWED  
 SET ALLOWED 다음의 모든 트랜잭션은 ATOMIC 블록이나 COMMIT 문에 설정된 내구성 옵션에 따라 완전한 내구성이 있거나 지연된 내구성이 있습니다.  
  
 FORCED  
 SET FORCED 다음의 모든 트랜잭션은 지연된 내구성이 있습니다. ATOMIC 블록이나 COMMIT 문에 설정된 내구성 옵션은 무시됩니다.  
  
 **\<external_access_option >:: =**  
  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 다른 데이터베이스의 개체와 같은 외부 리소스에서 데이터베이스에 액세스할 수 있는지 여부를 제어합니다.  
  
 DB_CHAINING { ON | OFF }  
 ON  
 데이터베이스가 데이터베이스 간 소유권 체인의 원본이나 대상이 될 수 있습니다.  
  
 OFF  
 데이터베이스가 데이터베이스 간 소유권 체인에 참여할 수 없습니다.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 cross db ownership chaining 서버 옵션이 0(OFF)일 때 이 설정을 인식할 수 있습니다. cross db ownership chaining이 1(ON)이면 모든 사용자 데이터베이스는 이 옵션 값에 관계없이 데이터베이스 간 소유권 체인에 참여할 수 있습니다. 이 옵션을 사용 하 여 설정 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)합니다.  
  
 이 옵션을 설정 하려면 데이터베이스에 대 한 CONTROL SERVER 권한이 필요 합니다.  
  
 DB_CHAINING 옵션은 master, model 및 tempdb 시스템 데이터베이스에서는 설정할 수 없습니다.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_db_chaining_on 열을 검사하여 확인할 수 있습니다.  
  
 TRUSTWORTHY { ON | OFF }  
 ON  
 가장 컨텍스트를 사용하는 데이터베이스 모듈(예: 사용자 정의 함수 또는 저장 프로시저)이 데이터베이스 외부의 리소스에 액세스할 수 있습니다.  
  
 OFF  
 가장 컨텍스트의 데이터베이스 모듈이 데이터베이스 외부 리소스에 액세스할 수 없습니다.  
  
 TRUSTWORTHY는 데이터베이스가 연결될 때마다 OFF로 설정됩니다.  
  
 기본적으로 msdb 데이터베이스를 제외한 모든 시스템 데이터베이스는 TRUSTWORTHY가 OFF로 설정되어 있습니다. model 및 tempdb 데이터베이스에 대해서는 이 값을 변경할 수 없습니다. master 데이터베이스의 경우 TRUSTWORTHY 옵션을 ON으로 설정하지 않는 것이 좋습니다.  
  
 이 옵션을 설정 하려면 데이터베이스에 대 한 CONTROL SERVER 권한이 필요 합니다.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_trustworthy_on 열을 검사하여 확인할 수 있습니다.  
  
 DEFAULT_FULLTEXT_LANGUAGE  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 전체 텍스트 인덱싱된 열에 대한 기본 언어 값을 지정합니다.  
  
> [!IMPORTANT]  
>  이 옵션은 CONTAINMENT가 PARTIAL로 설정된 경우에만 사용할 수 있습니다. CONTAINMENT가 NONE으로 설정되어 있으면 오류가 발생합니다.  
  
 DEFAULT_LANGUAGE  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 새로 생성된 모든 로그인에 대한 기본 언어를 지정합니다. LCID(로캘 ID), 언어 이름 또는 언어 별칭을 제공하여 언어를 지정할 수 있습니다. 가능한 언어 이름 및 별칭의 목록에 대 한 참조 [sys.syslanguages&#40; Transact SQL &#41; ](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md). 이 옵션은 CONTAINMENT가 PARTIAL로 설정된 경우에만 사용할 수 있습니다. CONTAINMENT가 NONE으로 설정되어 있으면 오류가 발생합니다.  
  
 NESTED_TRIGGERS  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 AFTER 트리거의 중첩(한 트리거가 다른 트리거를 시작하는 과정이 반복되는 동작) 여부를 지정합니다. 이 옵션은 CONTAINMENT가 PARTIAL로 설정된 경우에만 사용할 수 있습니다. CONTAINMENT가 NONE으로 설정되어 있으면 오류가 발생합니다.  
  
 TRANSFORM_NOISE_WORDS  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 의미 없는 단어 또는 중지 단어로 인해 전체 텍스트 쿼리에 대한 부울 연산이 실패할 경우 오류 메시지를 표시하지 않는 데 사용됩니다. 이 옵션은 CONTAINMENT가 PARTIAL로 설정된 경우에만 사용할 수 있습니다. CONTAINMENT가 NONE으로 설정되어 있으면 오류가 발생합니다.  
  
 TWO_DIGIT_YEAR_CUTOFF  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 두 자리 연도를 네 자리 연도로 해석하기 위한 구분 연도를 나타내는 1753에서 9999까지의 정수를 지정합니다. 이 옵션은 CONTAINMENT가 PARTIAL로 설정된 경우에만 사용할 수 있습니다. CONTAINMENT가 NONE으로 설정되어 있으면 오류가 발생합니다.  
  
 **\<FILESTREAM_option >:: =**  
  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 FileTable에 대한 설정을 제어합니다.  
  
 NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL }  
 OFF  
 FileTable 데이터에 대한 비트랜잭션 액세스를 사용하지 않도록 설정합니다.  
  
 READ_ONLY  
 비트랜잭션 프로세스에서 이 데이터베이스의 FileTable에 있는 FILESTREAM 데이터를 읽을 수 있습니다.  
  
 FULL  
 FileTabl의 FILESTREAM 데이터에 대한 전체 비트랜잭션 액세스를 사용할 수 있습니다.  
  
 DIRECTORY_NAME =  *\<directory_name >*  
 Windows 호환 디렉터리 이름입니다. 이 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 데이터베이스 수준 디렉터리 이름 중에서 고유해야 합니다. 고유성을 비교할 때는 데이터 정렬 설정과 관계없이 대/소문자가 구분되지 않습니다. 데이터베이스에 FileTable을 만들기 전에 이 옵션을 설정해야 합니다.  
  
 **\<HADR_options >:: =**  
  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 참조 [ALTER DATABASE SET hadr&#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-hadr.md).  
  
 **\<mixed_page_allocation_option >:: =**  
  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)). 사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 MIXED_PAGE_ALLOCATION {OFF | 여부} 컨트롤에 데이터베이스 혼합된 익스텐트를 사용 하 여 테이블이 나 인덱스의 첫 8 페이지에 대 한 초기 페이지 만들 수 있습니다.  
  
 OFF  
 데이터베이스는 항상 단일 익스텐트를 사용 하 여 초기 페이지를 만듭니다. 이 값은 기본값입니다.  
  
 ON  
 데이터베이스 혼합된 익스텐트를 사용 하 여 초기 페이지를 만들 수 있습니다.  
  
 이 설정은 모든 시스템 데이터베이스에 대해 ON입니다. **tempdb** OFF를 지 원하는 유일한 시스템 데이터베이스입니다.  
  
 **\<PARAMETERIZATION_option >:: =**  
  
 매개 변수화 옵션을 제어합니다.  
  
 PARAMETERIZATION { SIMPLE | FORCED }  
 SIMPLE  
 데이터베이스의 기본 동작에 따라 쿼리를 매개 변수화합니다.  
  
 FORCED  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스의 모든 쿼리를 매개 변수화합니다.  
  
 이 옵션의 현재 설정은 sys.databases 카탈로그 뷰의 is_parameterization_forced 열을 검사하여 확인할 수 있습니다.  
  
 **\<query_store_options >:: =**  
  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.  
  
 ON | OFF | CLEAR [ ALL ]  
 이 데이터베이스에서 쿼리 저장소를 사용 여부를 제어하고 쿼리 저장소의 내용 제거를 제어합니다.  
  
ON  
 쿼리 저장소를 사용 하도록 설정 합니다.  
  
OFF  
 쿼리 저장소를 사용 하지 않도록 설정 합니다.  이 값은 기본값입니다.   
  
CLEAR  
 쿼리 저장소의 콘텐츠를 제거 합니다.  
  
OPERATION_MODE  
 쿼리 저장소의 작업 모드를 설명합니다. 유효한 값은 READ_ONLY 및 READ_WRITE입니다. READ_WRITE 모드에서 쿼리 저장소는  쿼리 계획 및 런타임 실행 통계 정보를 수집하고 유지합니다. READ_ONLY 모드에서는 쿼리 저장소에서 정보를 읽을 수 있지만 새 정보는 추가되지 않습니다. 쿼리 저장소의 최대 할당 공간이 최대값에 도달하면 쿼리 저장소는 작업 모드를 READ_ONLY로 변경합니다.  
  
 CLEANUP_POLICY  
 쿼리 저장소의 데이터 보존 정책을 설명합니다. STALE_QUERY_THRESHOLD_DAYS는 쿼리에 대 한 정보는 쿼리 저장소에 보존할 일 수를 결정 합니다. STALE_QUERY_THRESHOLD_DAYS 형식이 **bigint**합니다.  
  
 DATA_FLUSH_INTERVAL_SECONDS  
 쿼리 저장소에 기록된 데이터가 디스크에 유지되는 빈도를 결정합니다. 성능 최적화를 위해 쿼리 저장소에서 수집한 데이터는 디스크에 비동기적으로 기록됩니다. 비동기 전송이 발생하는 빈도는 DATA_FLUSH_INTERVAL_SECONDS 인수를 사용하여 구성됩니다. DATA_FLUSH_INTERVAL_SECONDS 형식이 **bigint**합니다.  
  
 MAX_STORAGE_SIZE_MB  
 쿼리 저장소에 할당되는 공간을 결정합니다. MAX_STORAGE_SIZE_MB 형식이 **bigint**합니다.  
  
 INTERVAL_LENGTH_MINUTES  
 런타임 실행 통계 데이터가 쿼리 저장소로 집계되는 간격을 결정합니다. 공간 사용을 최적화하기 위해 런타임 통계 저장소의 런타임 실행 통계는 고정된 시간 창을 통해 집계됩니다. 고정된 시간 창은 INTERVAL_LENGTH_MINUTES 인수를 사용하여 구성됩니다. INTERVAL_LENGTH_MINUTES 형식이 **bigint**합니다.  
  
 SIZE_BASED_CLEANUP_MODE  
 여부 정리를 자동으로 활성화할지 총 데이터 양이 최대 크기에 가까워 하는 경우를 제어 합니다.  
  
 OFF  
 크기 기반 정리를 자동으로 활성화 되지 않습니다. 
  
 AUTO  
 크기 기반된 정리를 자동으로 활성화할지 때 디스크에 크기가의 90%에 도달 하면 **max_storage_size_mb**합니다. 크기 기반 정리 가장 비용이 많이 드는 주문과 가장 오래 된 쿼리를 먼저 제거합니다. 약 80%에서 멈춥니다 **max_storage_size_mb**합니다.  이것이 기본 구성 값입니다.  
  
 SIZE_BASED_CLEANUP_MODE 형식이 **nvarchar**합니다.  
  
 QUERY_CAPTURE_MODE  
 현재 활성 쿼리 캡처 모드를 지정 합니다.  
  
 모든 모든 쿼리가 캡처됩니다. 이것이 기본 구성 값입니다.  에 대 한 기본 구성 값입니다.[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]
  
 AUTO 캡처 관련 쿼리 실행 횟수 및 리소스 소비량에 따른 합니다.  에 대 한 기본 구성 값입니다.[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 NONE 새 쿼리 캡처가 중지 합니다. 쿼리 저장소는 이미 캡처된 쿼리에 대 한 컴파일 및 런타임 통계를 수집 하도록 계속 됩니다. 중요 한 쿼리 캡처를 놓칠 수 있으므로 주의 해 서이 구성을 사용 합니다.  
  
 QUERY_CAPTURE_MODE 형식이 **nvarchar**합니다.  
  
 max_plans_per_query  
 각 쿼리에 대하여 유지되는 계획의 수를 나타내는 정수입니다. 기본값은 200입니다.  
  
 **\<recovery_option >:: =**  
  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 데이터베이스 복구 옵션과 디스크 I/O 오류 검사를 제어합니다.  
  
 FULL  
 미디어 오류가 발생한 후에는 트랜잭션 로그 백업을 사용하여 전체 복구를 제공합니다. 데이터 파일이 손상된 경우 미디어 복구 기능을 통해 모든 커밋된 트랜잭션을 복원할 수 있습니다. 자세한 내용은 [복구 모델&#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)을 참조하세요.  
  
 BULK_LOGGED  
 미디어 오류가 발생한 후에 일부 대량 작업에 대해 성능은 좋고 로그 공간 사용량은 적은 방법으로 복구를 제공합니다. 어떤 수 최소 로깅 가능한 작업에 대 한 정보를 참조 하십시오. [트랜잭션 로그 &#40; SQL Server &#41; ](../../relational-databases/logs/the-transaction-log-sql-server.md). BULK_LOGGED 복구 모델에서는 이러한 작업에 대해서 최소 로깅이 사용됩니다. 자세한 내용은 [복구 모델&#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)을 참조하세요.  
  
 SIMPLE  
 최소 로그 공간을 사용하는 단순 백업 전략을 제공합니다. 서버 오류 복구에 더 이상 필요 없는 로그 공간은 자동으로 재사용됩니다. 자세한 내용은 [복구 모델&#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)을 참조하세요.  
  
> [!IMPORTANT]  
> 단순 복구 모델은 다른 두 모델보다 관리하기는 쉽지만 데이터 파일이 손상된 경우 데이터 손실 위험은 더 큽니다. 최신 데이터베이스 또는 차등 데이터베이스 백업이 손실된 이후의 변경 사항은 모두 수동으로 다시 입력해야 합니다.  
  
 기본 복구 모델은 **model** 데이터베이스의 복구 모델에 의해 결정됩니다. 적절 한 복구 모델을 선택 하는 방법에 대 한 자세한 내용은 참조 [복구 모델 &#40; SQL Server &#41; ](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
 검사 하 여이 옵션의 상태를 확인할 수 있습니다는 **recovery_model** 및 **recovery_model_desc** 열 sys.databases 카탈로그 뷰 또는 DATABASEPROPERTYEX의 복구 속성 함수입니다.  
  
 TORN_PAGE_DETECTION { ON | OFF }  
 ON  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 완료되지 않은 페이지를 검색할 수 있습니다.  
  
 OFF  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 완료되지 않은 페이지를 검색할 수 없습니다.  
  
> [!IMPORTANT]  
> TORN_PAGE_DETECTION ON | OFF 구문 구조는 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 제거될 예정입니다. 새 개발 작업에서는 이 구문 구조를 사용하지 않도록 하고 현재 이 구문 구조를 사용하는 응용 프로그램은 수정하십시오. 대신 PAGE_VERIFY 옵션을 사용하십시오.  
  
<a name="page_verify"></a>PAGE_VERIFY {체크섬 | TORN_PAGE_DETECTION | NONE}  
 디스크 I/O 경로 오류로 인해 손상된 데이터베이스 페이지를 찾습니다. 디스크 I/O 경로 오류는 일반적으로 페이지를 디스크에 쓸 때 전원 오류나 디스크 하드웨어 오류로 인해 발생하며 데이터베이스 손상 문제를 일으킬 수 있습니다.  
  
 CHECKSUM  
 페이지를 디스크에 쓸 때 전체 페이지의 내용에 대한 체크섬을 계산하고 이 값을 페이지 헤더에 저장합니다. 디스크에서 페이지를 읽으면 체크섬이 다시 계산되어 페이지 헤더에 저장된 체크섬 값과 비교됩니다. 두 값이 일치하지 않으면 체크섬 오류를 나타내는 824 오류 메시지가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 Windows 이벤트 로그에 보고됩니다. 체크섬 오류는 I/O 경로 문제를 나타냅니다. 오류에 대한 근본 원인을 확인하려면 하드웨어, 펌웨어 드라이버, BIOS, 필터 드라이버(예: 바이러스 소프트웨어) 및 기타 I/O 경로 구성 요소를 조사해야 합니다.  
  
 TORN_PAGE_DETECTION  
 페이지를 디스크에 쓸 때 8KB 데이터베이스 페이지의 각 512바이트 섹터에 대해 특정 2비트 패턴을 데이터베이스 페이지 헤더에 저장합니다. 디스크에서 페이지를 읽으면 페이지 헤더에 저장된 조각난 비트가 실제 페이지 섹터 정보와 비교됩니다. 값이 일치하지 않으면 페이지의 일부분만 디스크에 쓰여졌음을 의미합니다. 이 경우 조각난 페이지 오류를 나타내는 824 오류 메시지가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 Windows 이벤트 로그에 보고됩니다. 조각난 페이지가 실제로 쓰기가 완료되지 않은 페이지인 경우 조각난 페이지는 보통 데이터베이스 복구에서 검색됩니다. 그러나 다른 I/O 경로 오류도 언제든 조각난 페이지의 원인이 될 수 있습니다.  
  
 없음  
 데이터베이스 페이지 쓰기에서 CHECKSUM 또는 TORN_PAGE_DETECTION 값이 생성되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 페이지 헤더에 CHECKSUM 또는 TORN_PAGE_DETECTION 값이 있는 경우에도 읽기 중 체크섬이나 조각난 페이지를 확인하지 않습니다.  
  
 PAGE_VERIFY 옵션을 사용하는 경우 다음 중요 사항을 고려하십시오.  
  
-   기본값은 CHECKSUM입니다.  
  
-   사용자 또는 시스템 데이터베이스를 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전으로 업그레이드하는 경우 PAGE_VERIFY 값(NONE 또는 TORN_PAGE_DETECTION)이 유지됩니다. CHECKSUM을 사용하는 것이 좋습니다.  
  
    > [!NOTE]  
    > 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 tempdb 데이터베이스의 PAGE_VERIFY 데이터베이스 옵션이 NONE으로 설정되며 수정할 수 없습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서는 tempdb 데이터베이스에 대 한 기본값은 CHECKSUM을 새로 설치 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치를 업그레이드하면 기본값이 NONE으로 유지됩니다. 이 옵션은 수정할 수 없습니다. tempdb 데이터베이스에는 CHECKSUM을 사용하는 것이 좋습니다.  
  
-   TORN_PAGE_DETECTION은 리소스는 덜 사용하지만 CHECKSUM 보호를 최소한으로 제공합니다.  
  
-   PAGE_VERIFY는 데이터베이스를 잠그거나 오프라인으로 설정하지 않고 즉, 데이터베이스의 동시성을 방해하지 않고 설정할 수 있습니다.  
  
-   CHECKSUM과 TORN_PAGE_DETECTION은 상호 배타적이므로 두 옵션을 동시에 사용할 수 없습니다.  
  
 조각난 페이지나 체크섬 오류가 검색되면 데이터를 복원하거나 오류가 인덱스 페이지에만 해당되는 경우 인덱스를 다시 작성하여 복구할 수 있습니다. 체크섬 오류가 발생하면 DBCC CHECKDB를 실행하여 이 오류의 영향을 받는 데이터베이스 페이지의 형식 또는 페이지를 확인할 수 있습니다. 복원 옵션에 대 한 자세한 내용은 참조 하세요. [RESTORE 인수 &#40; Transact SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md). 데이터를 복원하면 데이터 손상 문제를 해결할 수 있지만 오류가 계속 발생하지 않도록 하려면 하드웨어 오류 등의 근본 원인을 진단하여 수정해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 체크섬, 조각난 페이지 또는 기타 I/O 오류로 읽기가 실패할 경우 4번 다시 시도합니다. 다시 시도 중에 한 번이라도 읽기가 성공하면 오류 로그에 메시지가 기록되고 해당 읽기를 트리거한 명령이 계속 수행됩니다. 다시 시도가 실패하면 824 오류 메시지와 함께 명령이 실패합니다.  
  
 오류 메시지 823, 824 및 825에 대 한 자세한 내용은 참조 [SQL Server에서 메시지 823 오류 문제를 해결 하는 방법을](http://support.microsoft.com/help/2015755), [SQL Server에서 메시지 824 문제를 해결 하는 방법을](http://support.microsoft.com/help/2015756) 및 [메시지 825를 해결 하는 방법 &#40; 읽기 다시 시도 &#41; SQL Server에서](http://support.microsoft.com/help/2015757)합니다.
  
 이 옵션의 현재 설정을 검사 하 여 확인할 수 있습니다는 *page_verify_option* 열에는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰 또는 *IsTornPageDetectionEnabled*의 속성은 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 함수입니다.  
  
**\<remote_data_archive_option >:: =**  
  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 데이터베이스에 대 한 스트레치 데이터베이스를 사용 하지 않도록 설정 하거나 사용 합니다. 자세한 내용은 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하십시오.  
  
REMOTE_DATA_ARCHIVE = {ON (SERVER = \<서버 _ 이름 >, {자격 증명 = \<db_scoped_credential_name > | FEDERATED_SERVICE_ACCOUNT = ON | OFF}) | ON 해제  
 데이터베이스에 대 한 스트레치 데이터베이스를 수 있습니다. 추가 필수 구성 요소를 포함 하 여 자세한 정보를 참조 하십시오. [데이터베이스에서 스트레치 데이터베이스 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)합니다.  
  
 **사용 권한**. 데이터베이스 또는 테이블에 대 한 스트레치 데이터베이스를 활성화 하려면 db_owner 권한이 필요 합니다. 데이터베이스에 대 한 스트레치 데이터베이스를 활성화 하면 CONTROL DATABASE 사용 권한도 있어야 합니다.  
  
SERVER = \<서버 _ 이름 >  
 Azure 서버 주소를 지정합니다. 포함 된 `.database.windows.net` 이름의 부분입니다. `MyStretchDatabaseServer.database.windows.net`)을 입력합니다.  
  
자격 증명 = \<db_scoped_credential_name >  
 데이터베이스 범위 자격 증명을 하는 지정 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure 서버에 연결 하기 위해 사용 합니다. 이 명령을 실행 하기 전에 자격 증명이 있는지 확인 합니다. 자세한 내용은 참조 하세요. [데이터베이스 범위 자격 증명 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
FEDERATED_SERVICE_ACCOUNT = ON | 해제  
 다음 조건이 모두 참인 경우 원격 Azure 서버와 통신 하는 온-프레미스 SQL Server에 대 한 페더레이션된 서비스 계정을 사용할 수 있습니다.  
  
-   SQL Server 인스턴스를 실행하는 서비스 계정은 도메인 계정입니다.  
  
-   이 도메인 계정은 Active Directory가 Azure Active Directory와 페더레이션된 도메인에 속합니다.  
  
-   원격 Azure 서버는 Azure Active Directory 인증을 지원하도록 구성됩니다.  
  
-   SQL Server 인스턴스를 실행하는 서비스 계정은 원격 Azure 서버에서 dbmanager 또는 sysadmin 계정으로 구성되어야 합니다.  
  
 ON을 지정 하는 경우 CREDENTIAL 인수를 지정할 수 없습니다. OFF를 지정 하면 CREDENTIAL 인수를 제공 해야 합니다.  
  
 OFF  
 데이터베이스에 대 한 스트레치 데이터베이스를 사용 하지 않도록 설정 합니다. 자세한 내용은 [Stretch Database 비활성화 및 원격 데이터 다시 가져오기](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)를 사용하세요.  
  
 스트레치 데이터베이스에 대해 설정 된 테이블이 데이터베이스에 더 이상 포함 되어 후 스트레치 데이터베이스는 데이터베이스에 대해 비활성화할 수 없습니다. 스트레치 데이터베이스를 비활성화 하면 데이터 마이그레이션이 중단 되 고 쿼리 결과 더 이상 원격 테이블의 결과가 포함 합니다.  
  
 스트레치를 비활성화 하면 원격 데이터베이스는 제거 되지 않습니다. 원격 데이터베이스를 삭제하려면 Azure 관리 포털을 사용하여 삭제해야 합니다.  
  
**\<다음과 >:: =**  
  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 제어 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 옵션: 사용 또는 메시지 배달 비활성화, 새 설정 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자 또는 설정 대화 우선 순위를 ON 또는 OFF입니다.  
  
 ENABLE_BROKER  
 지정된 데이터베이스에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용할 수 있도록 지정합니다. 메시지 배달이 시작되고 sys.databases 카탈로그 뷰에서 is_broker_enabled 플래그가 true로 설정됩니다. 데이터베이스에 기존 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자가 유지됩니다. 데이터베이스가 데이터베이스 미러링 구성에서 보안 주체인 경우에는 Service Broker를 사용할 수 없습니다.  
  
> [!NOTE]  
>  ENABLE_BROKER를 사용하려면 배타적 데이터베이스 잠금이 필요합니다. 다른 세션이 데이터베이스의 리소스를 잠근 경우 ENABLE_BROKER는 다른 세션이 해당 잠금을 해제할 때까지 기다립니다. 사용자 데이터베이스에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용하도록 설정하려면 데이터베이스를 단일 사용자 모드로 설정하는 등의 방법으로 데이터베이스가 다른 세션에 의해 사용되지 않도록 한 다음 ALTER DATABASE SET ENABLE_BROKER 문을 실행합니다. msdb 데이터베이스에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용하도록 설정하려면 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 중지하여 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서 필요한 잠금을 획득할 수 있도록 합니다.  
  
 DISABLE_BROKER  
 지정된 데이터베이스에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용하지 않도록 지정합니다. 메시지 배달이 중지되고 sys.databases 카탈로그 뷰에서 is_broker_enabled 플래그가 false로 설정됩니다. 데이터베이스에 기존 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자가 유지됩니다.  
  
 NEW_BROKER  
 데이터베이스가 새 Broker 식별자를 받도록 지정합니다. 데이터베이스는 새 Service Broker가 될 것으로 간주되기 때문에 데이터베이스 내의 모든 기존 대화는 종료 대화 메시지 없이 즉시 제거됩니다. 이전 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자를 참조하는 경로는 새 식별자로 다시 만들어야 합니다.  
  
 ERROR_BROKER_CONVERSATIONS  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 배달을 사용하도록 지정합니다. 이렇게 하면 기존 유지할 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 데이터베이스에 대 한 식별자입니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 오류가 있는 데이터베이스의 모든 대화를 종료합니다. 또한 응용 프로그램에서 기존 대화에 대해 일반적인 정리 작업을 수행할 수 있습니다.  
  
 HONOR_BROKER_PRIORITY {ON | OFF}  
 ON  
 보내기 작업에서 대화에 할당된 우선 순위 수준을 고려합니다. 우선 순위 수준이 높은 대화의 메시지는 우선 순위 수준이 낮은 대화의 메시지보다 먼저 전송됩니다.  
  
 OFF  
 모든 대화에 기본 우선 순위 수준이 할당된 것으로 간주하고 보내기 작업이 실행됩니다.  
  
 HONOR_BROKER_PRIORITY 옵션의 변경 내용은 전송 대기 중인 메시지가 없는 대화 또는 새 대화에 즉시 적용됩니다. ALTER DATABASE가 실행될 때 대화에 전송 대기 중인 메시지가 있는 경우에는 대화의 해당 메시지가 전송되기 전까지 새 설정이 적용되지 않습니다. 모든 대화에 새 설정이 적용되는 데 걸리는 시간은 상황에 따라 크게 다를 수 있습니다.  
  
 이 속성의 현재 설정을 is_broker_priority_honored 열에 보고 되는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰.  
  
 **\<snapshot_option >:: =**  
  
 트랜잭션 격리 수준을 결정합니다.  
  
 ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
 ON  
 데이터베이스 수준에서 스냅숏 옵션을 사용하도록 설정합니다. 이 옵션을 사용하면 트랜잭션에서 스냅숏 격리를 사용하지 않는 경우에도 DML 문에서 행 버전을 생성하기 시작합니다. 이 옵션을 사용하도록 설정하면 트랜잭션에서 SNAPSHOT 트랜잭션 격리 수준을 지정할 수 있습니다. 트랜잭션이 SNAPSHOT 격리 수준에서 실행되면 모든 문에서 트랜잭션 시작 시점의 상태로 데이터 스냅숏을 봅니다. SNAPSHOT 격리 수준에서 실행되는 트랜잭션이 여러 데이터베이스의 데이터에 액세스할 경우 모든 데이터베이스에서 ALLOW_SNAPSHOT_ISOLATION이 ON으로 설정되어 있어야 합니다. 그렇지 않고 ALLOW_SNAPSHOT_ISOLATION이 OFF로 설정된 경우에는 트랜잭션 내의 각 문에서는 FROM 절의 참조에서 데이터베이스의 테이블에 대한 잠금 힌트를 사용해야 합니다.  
  
 OFF  
 데이터베이스 수준에서 스냅숏 옵션을 해제합니다. 트랜잭션에서는 SNAPSHOT 트랜잭션 격리 수준을 지정할 수 없습니다.  
  
 ALLOW_SNAPSHOT_ISOLATION을 새 상태로 설정하는 경우(ON에서 OFF로 또는 OFF에서 ON으로) ALTER DATABASE는 데이터베이스 내의 기존 트랜잭션이 모두 커밋될 때까지 호출자에게 제어권을 반환하지 않습니다. 데이터베이스가 이미 ALTER DATABASE 문에 지정된 상태인 경우 제어권은 호출자에게 즉시 반환됩니다. ALTER DATABASE 문이 빨리 반환 하지 않는 경우 사용 하 여 [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) 장기 실행 트랜잭션이 있는지 확인할 수 있습니다. ALTER DATABASE 문을 취소하면 데이터베이스는 ALTER DATABASE가 시작된 시점의 상태로 남게 됩니다. [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰는 데이터베이스에서 스냅숏 격리 트랜잭션의 상태를 나타냅니다. 경우 **snapshot_isolation_state_desc** = IN_TRANSITION_TO_ON, ALTER DATABASE ALLOW_SNAPSHOT_ISOLATION OFF은 6 초간 일시 중지 하 고 작업을 다시 시도 합니다.  
  
 데이터베이스가 OFFLINE인 경우 ALLOW_SNAPSHOT_ISOLATION의 상태를 변경할 수 없습니다.  
  
 READ_ONLY 데이터베이스에서 ALLOW_SNAPSHOT_ISOLATION을 설정하는 경우 데이터베이스가 이후에 READ_WRITE로 설정되어도 이 설정은 그대로 유지됩니다.  
  
 master, model, msdb 및 tempdb 데이터베이스에 대해 ALLOW_SNAPSHOT_ISOLATION 설정을 변경할 수 있습니다. tempdb에 대한 설정을 변경하면 이 설정은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 중지 후 다시 시작할 때마다 유지됩니다. model 데이터베이스에 대한 설정을 변경하면 이 설정은 새로 생성된 모든 데이터베이스(tempdb 제외)의 기본값이 됩니다.  
  
 master 및 msdb 데이터베이스에 대해 이 옵션은 기본적으로 ON입니다.  
  
 이 옵션의 현재 설정은 sys.databases 카탈로그 뷰의 snapshot_isolation_state 열을 검사하여 확인할 수 있습니다.  
  
 READ_COMMITTED_SNAPSHOT { ON | OFF }  
 ON  
 데이터베이스 수준에서 커밋된 읽기 스냅숏 옵션을 사용하도록 설정합니다. 이 옵션을 사용하면 트랜잭션에서 스냅숏 격리를 사용하지 않는 경우에도 DML 문에서 행 버전을 생성하기 시작합니다. 이 옵션을 사용하도록 설정하면 커밋된 읽기 스냅숏 격리 수준을 지정하는 트랜잭션에서는 잠금 대신 행 버전 관리를 사용합니다. 트랜잭션이 커밋된 읽기 격리 수준에서 실행되면 모든 문에서는 해당 문이 시작되던 때의 상태로 데이터 스냅숏을 봅니다.  
  
 OFF  
 데이터베이스 수준에서 커밋된 읽기 스냅숏 옵션을 해제합니다. READ COMMITTED 격리 수준을 지정하는 트랜잭션에서는 잠금을 사용합니다.  
  
 READ_COMMITTED_SNAPSHOT을 ON 또는 OFF로 설정하려면 ALTER DATABASE 명령을 실행하는 연결을 제외하고 데이터베이스에 대한 활성 상태의 연결이 없어야 합니다. 그러나 데이터베이스가 단일 사용자 모드에 있을 필요는 없습니다. 데이터베이스가 OFFLINE인 경우 이 옵션의 상태를 변경할 수 없습니다.  
  
 READ_ONLY 데이터베이스에서 READ_COMMITTED_SNAPSHOT을 설정하는 경우 데이터베이스가 이후에 READ_WRITE로 설정되어도 이 설정은 그대로 유지됩니다.  
  
 master, tempdb 또는 msdb 시스템 데이터베이스에 대해서는 READ_COMMITTED_SNAPSHOT을 ON으로 설정할 수 없습니다. model 데이터베이스에 대한 설정을 변경하면 이 설정은 새로 생성된 모든 데이터베이스(tempdb 제외)의 기본값이 됩니다.  
  
 이 옵션의 현재 설정은 sys.databases 카탈로그 뷰의 is_read_committed_snapshot_on 열을 검사하여 확인할 수 있습니다.  
  
> [!WARNING]  
>  와 테이블을 만들면 **DURABILITY = SCHEMA_ONLY**, 및 **READ_COMMITTED_SNAPSHOT** 를 사용 하 여 변경 이후에 **ALTER DATABASE**, 테이블의 데이터는 손실 됩니다.  
  
 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT { ON | OFF }  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 ON  
 트랜잭션 격리 수준이 SNAPSHOT보다 낮은 격리 수준(예: READ COMMITTED 또는 READ UNCOMMITTED)으로 설정된 경우 메모리 최적화 테이블에 대한 해석된 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업이 SNAPSHOT 격리로 수행됩니다. 이 작업은 세션 수준에서 트랜잭션 격리 수준이 명시적으로 설정되었거나 기본값이 암시적으로 사용되었는지에 관계없이 수행됩니다.  
  
 OFF  
 메모리 최적화 테이블에서 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업에 대해 트랜잭션 격리 수준을 승격하지 않습니다.  
  
 데이터베이스가 OFFLINE인 경우 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT의 상태를 변경할 수 없습니다.  
  
 이 옵션은 기본적으로 OFF입니다.  
  
 이 옵션의 현재 설정을 검사 하 여 확인할 수 있습니다는 **is_memory_optimized_elevate_to_snapshot_on** 열에는 [sys.databases&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
 **\<sql_option >:: =**  
  
 ANSI 호환 옵션을 데이터베이스 수준에서 제어합니다.  
  
 ANSI_NULL_DEFAULT { ON | OFF }  
 기본값 NULL 또는 NOT NULL 결정, 열 또는 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) null 허용 여부 정의 되지 않은 명시적으로 CREATE TABLE 또는 ALTER TABLE 문에 대 한 합니다. 제약 조건이 정의된 열은 이 설정에 상관 없이 제약 조건 규칙을 따릅니다.  
  
 ON  
 기본값은 NULL입니다.  
  
 OFF  
 기본값이 NOT NULL입니다.  
  
 SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_NULL_DEFAULT에 대한 기본 데이터베이스 수준 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 때 세션의 ANSI_NULL_DEFAULT를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. 자세한 내용은 참조 [SET ansi_null_dflt_on&#40; Transact SQL &#41; ](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md).  
  
 ANSI 호환성을 위해 ANSI_NULL_DEFAULT 데이터베이스 옵션을 ON으로 설정하면 데이터베이스의 기본값이 NULL로 변경됩니다.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_ansi_null_default_on 열 또는 DATABASEPROPERTYEX 함수의 IsAnsiNullDefault 속성을 검사하여 확인할 수 있습니다.  
  
 ANSI_NULLS { ON | OFF }  
 ON  
 Null 값에 대한 모든 비교는 UNKNOWN으로 평가됩니다.  
  
 OFF  
 Null 값에 대한 비-UNICODE 값 비교는 두 값이 모두 NULL인 경우 TRUE로 평가됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 ANSI_NULLS가 항상 ON으로 설정되므로 명시적으로 이 옵션을 OFF로 설정한 응용 프로그램에서는 오류가 발생합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.  
  
 SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_NULLS에 대한 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 때 세션의 ANSI_NULLS를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. 자세한 내용은 [SET ANSI_NULLS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)를 참조하세요.  
  
 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경하는 경우에도 SET ANSI_NULLS를 ON으로 설정해야 합니다.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_ansi_nulls_on 열 또는 DATABASEPROPERTYEX 함수의 IsAnsiNullsEnabled 속성을 검사하여 확인할 수 있습니다.  
  
 ANSI_PADDING { ON | OFF }  
 ON  
 으로 변환 또는 삽입 하기 전에 문자열이 동일한 길이 만큼 채워집니다는 **varchar** 또는 **nvarchar** 데이터 형식입니다.  
  
 **varchar** 또는 **nvarchar** 열에 삽입된 문자 값의 후행 공백과 **varbinary** 열에 삽입된 이진 값의 후행 0이 잘리지 않습니다. 값은 열의 크기만큼 오른쪽에 공백으로 채워집니다.  
  
 OFF  
 후행 공백과 **varchar** 또는 **nvarchar** 0 **varbinary** 잘립니다.  
  
 OFF로 지정하면 이 설정은 새 열의 정의에만 영향을 줍니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 ANSI_PADDING이 항상 ON으로 설정되므로 명시적으로 이 옵션을 OFF로 설정한 응용 프로그램에서는 오류가 발생합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. ANSI_PADDING은 항상 ON으로 설정하는 것이 좋습니다. 계산 열이나 인덱싱된 뷰에서 인덱스를 만들거나 조작할 때는 ANSI_PADDING을 ON으로 설정해야 합니다.  
  
 **char(*n*)** 및 **이진(*n*)** null ANSI_PADDING이 설정 된 경우 열의 길이로 패딩 됩니다에 대 한 허용 하는 열 on으로 하지만 후행 공백 및 0이 잘립니다 ANSI_PADDING이 OFF입니다. **char(*n*)** 및 **이진(*n*)** null을 허용 하지 않는 열은 항상 열 길이 채워집니다.  
  
 SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_PADDING에 대한 기본 데이터베이스 수준 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 때 세션의 ANSI_PADDING을 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. 자세한 내용은 [SET ANSI_PADDING&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)을 참조하세요.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_ansi_padding_on 열 또는 DATABASEPROPERTYEX 함수의 IsAnsiPaddingEnabled 속성을 검사하여 확인할 수 있습니다.  
  
 ANSI_WARNINGS { ON | OFF }  
 ON  
 0으로 나누기 또는 집계 함수에 Null 값이 나타나는 등의 상황에서 오류 또는 경고가 발생합니다.  
  
 OFF  
 0으로 나누기와 같은 상황이 발생해도 아무런 경고도 발생하지 않으며 Null 값이 반환됩니다.  
  
 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경하는 경우 SET ANSI_WARNINGS를 ON으로 설정해야 합니다.  
  
 SET 문을 사용하여 설정한 연결 수준의 설정은 ANSI_WARNINGS에 대한 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 때 세션의 ANSI_WARNINGS를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. 자세한 내용은 [SET ANSI_WARNINGS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)를 참조하세요.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_ansi_warnings_on 열 또는 DATABASEPROPERTYEX 함수의 IsAnsiWarningsEnabled 속성을 검사하여 확인할 수 있습니다.  
  
 ARITHABORT { ON | OFF }  
 ON  
 쿼리 실행 중 오버플로 또는 0으로 나누기 오류가 발생하면 쿼리를 종료합니다.  
  
 OFF  
 이러한 오류 중 하나가 발생할 경우 경고 메시지가 표시되지만 쿼리, 일괄 처리 또는 트랜잭션은 오류가 발생하지 않은 것처럼 계속 처리됩니다.  
  
 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때 SET ARITHABORT를 ON으로 설정해야 합니다.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_arithabort_on 열 또는 DATABASEPROPERTYEX 함수의 IsArithmeticAbortEnabled 속성을 검사하여 확인할 수 있습니다.  
  
 COMPATIBILITY_LEVEL { 90 | 100 | 110 | 120}  
 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  
  
 CONCAT_NULL_YIELDS_NULL { ON | OFF }  
 ON  
 피연산자 중 하나가 NULL일 경우 연결 연산의 결과는 NULL입니다. 예를 들어 문자열 "This is"와 NULL을 연결하면 결과는 "This is"가 아니라 NULL이 됩니다.  
  
 OFF  
 Null 값은 빈 문자열로 취급됩니다.  
  
 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때 SET CONCAT_NULL_YIELDS_NULL은 반드시 ON으로 설정되어야 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 CONCAT_NULL_YIELDS_NULL이 항상 ON으로 설정되므로 명시적으로 이 옵션을 OFF로 설정한 응용 프로그램에서는 오류가 발생합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.  
  
 SET 문을 사용하여 설정한 연결 수준의 설정은 CONCAT_NULL_YIELDS_NULL의 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 때 세션의 CONCAT_NULL_YIELDS_NULL을 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. 자세한 내용은 [SET CONCAT_NULL_YIELDS_NULL&#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)을 참조하세요.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_concat_null_yields_null_on 열 또는 DATABASEPROPERTYEX 함수의 IsNullConcat 속성을 검사하여 확인할 수 있습니다.  
  
 QUOTED_IDENTIFIER { ON | OFF }  
 ON  
 큰따옴표는 구분 식별자를 묶을 때 사용할 수 있습니다.  
  
 큰따옴표로 구분되는 모든 문자열은 개체 식별자로 해석됩니다. 따옴표 붙은 식별자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자 규칙을 따르지 않아도 됩니다. 따옴표 붙은 식별자는 키워드일 수 있으며 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자에서 일반적으로 허용되지 않는 문자를 포함할 수 있습니다. 작은따옴표(')가 리터럴 문자열의 일부로 포함되면 큰따옴표(")로 나타낼 수 있습니다.  
  
 OFF  
 식별자는 따옴표 안에 있을 수 없으며 식별자에 대한 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 규칙을 따라야 합니다. 리터럴은 작은따옴표 또는 큰따옴표로 구분할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서도 식별자를 대괄호([ ])로 구분할 수 있습니다. 대괄호로 묶은 식별자는 QUOTED_IDENTIFIER의 설정에 관계없이 항상 사용할 수 있습니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
 테이블이 생성될 때 QUOTED IDENTIFIER 옵션이 OFF로 설정된 경우에도 해당 테이블의 메타데이터에는 항상 ON으로 저장됩니다.  
  
 SET 문을 사용하여 설정한 연결 수준의 설정은 QUOTED_IDENTIFIER의 기본 데이터베이스 설정보다 우선적으로 적용됩니다. 기본적으로 ODBC 및 OLE DB 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 때 QUOTED_IDENTIFIER를 ON으로 설정하여 연결 수준의 SET 문을 실행합니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_quoted_identifier_on 열 또는 DATABASEPROPERTYEX 함수의 IsQuotedIdentifiersEnabled 속성을 검사하여 확인할 수 있습니다.  
  
 NUMERIC_ROUNDABORT { ON | OFF }  
 ON  
 식에서 전체 자릿수가 손실되면 오류가 발생합니다.  
  
 OFF  
 전체 자릿수가 손실되어도 오류 메시지가 생성되지 않으며 결과를 저장하는 열 또는 변수의 전체 자릿수로 결과가 반올림됩니다.  
  
 계산 열 또는 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때 NUMERIC_ROUNDABORT는 OFF로 설정되어야 합니다.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_numeric_roundabort_on 열 또는 DATABASEPROPERTYEX 함수의 IsNumericRoundAbortEnabled 속성을 검사하여 확인할 수 있습니다.  
  
 RECURSIVE_TRIGGERS { ON | OFF }  
 ON  
 AFTER 트리거의 재귀적 실행이 허용됩니다.  
  
 OFF  
 AFTER 트리거의 직접 재귀적 실행이 허용되지 않습니다. 또한 AFTER 트리거의 간접 재귀를 해제 하려면 nested triggers 서버 옵션을 설정 **0** 를 사용 하 여 **sp_configure**합니다.  
  
> [!NOTE]  
>  RECURSIVE_TRIGGERS가 OFF로 설정되면 직접 재귀만 금지됩니다. 간접 재귀를 사용하지 않도록 하려면 nested triggers 서버 옵션을 0으로 설정해야 합니다.  
  
 이 옵션의 상태는 sys.databases 카탈로그 뷰의 is_recursive_triggers_on 열 또는 DATABASEPROPERTYEX 함수의 IsRecursiveTriggersEnabled 속성을 검사하여 확인할 수 있습니다.  
  
 **\<target_recovery_time_option >:: =**  
  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 사용할 수 없는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 데이터베이스 단위로 간접 검사점의 빈도를 지정합니다. 부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 새 데이터베이스에 대 한 기본값은 1 분, 데이터베이스에서 간접 검사점을 사용 하는 것을 나타냅니다. 이전 버전에 대 한 기본값은 0으로, 데이터베이스를 빈도 서버 인스턴스의 복구 간격 설정에 따라 달라 집니다 자동 검사점을 사용 함을 나타냅니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)]대부분의 시스템에 1 분을 권장합니다.  
  
 TARGET_RECOVERY_TIME **=***target_recovery_time* { SECONDS | MINUTES }  
 *target_recovery_time*  
 충돌 시 지정된 데이터베이스를 복구하는 데 걸리는 최대 시간을 지정합니다.  
  
 SECONDS  
 *target_recovery_time* 이 초 단위로 표현됨을 나타냅니다.  
  
 MINUTES  
 *target_recovery_time* 이 분 단위로 표현됨을 나타냅니다.  
  
 간접 검사점에 대 한 자세한 내용은 참조 [데이터베이스 검사점 &#40; SQL Server &#41; ](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 **와 \<종료 >:: =**  
  
 데이터베이스가 다른 상태로 바뀔 때 완료되지 않은 트랜잭션을 롤백할 시점을 지정합니다. termination 절을 생략하면 데이터베이스에 잠금이 있는 경우 ALTER DATABASE 문이 무기한 대기합니다. termination 절은 SET 절 다음에 한 번만 지정할 수 있습니다.  
  
> [!NOTE]  
>  WITH를 사용 하는 일부 데이터베이스 옵션 \<종료 > 절. 자세한 내용은 이 항목에 있는 "주의 섹션"의 "[옵션 설정](#SettingOptions) " 아래에 있는 표를 참조하십시오.  
  
 롤백 후 *정수* [SECONDS] | 즉시 롤백  
 지정한 시간(초)이 경과한 후 롤백할 것인지 또는 즉시 롤백할 것인지를 지정합니다.  
  
 NO_WAIT  
 트랜잭션이 자체적으로 커밋되거나 롤백되기를 기다리지 않고 요청된 데이터베이스 상태 또는 옵션 변경을 즉시 완료할 수 없는 경우에 요청이 실패하도록 지정합니다.  
  
##  <a name="SettingOptions"></a>옵션 설정  
 데이터베이스 옵션에 대 한 현재 설정을 검색 하려면는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰 또는 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)  
  
 데이터베이스 옵션을 설정하면 수정 사항이 즉시 반영됩니다.  
  
 새로 만든 모든 데이터베이스에 대한 데이터베이스 옵션의 기본값을 바꾸려면 model 데이터베이스에서 해당 데이터베이스 옵션을 변경하십시오.  
  
 WITH를 사용 하는 일부 데이터베이스 옵션 \<종료 > 절 또는 다른 옵션과 함께에서 지정할 수 있습니다. 다음 표에서는 이러한 옵션 및 이들의 옵션과 종료 상태를 나열합니다.  
  
|옵션 범주|다른 옵션과 함께 지정할 수 있음|WITH צ ְ ײ \<종료 > 절|  
|----------------------|-----------------------------------------|---------------------------------------------|  
|\<db_state_option >|예|예|  
|\<db_user_access_option >|예|예|  
|\<db_update_option >|예|예|  
|\<delayed_durability_option >|예|예|  
|\<external_access_option >|예|아니요|  
|\<cursor_option >|예|아니요|  
|\<auto_option >|예|아니요|  
|\<sql_option >|예|아니요|  
|\<recovery_option >|예|아니요|  
|\<target_recovery_time_option >|아니요|예|  
|\<문당 >|아니요|아니요|  
|ALLOW_SNAPSHOT_ISOLATION|아니요|아니요|  
|READ_COMMITTED_SNAPSHOT|아니요|예|  
|MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT|예|예|  
|\<다음과 >|예|아니요|  
|DATE_CORRELATION_OPTIMIZATION|예|예|  
|\<parameterization_option >|예|예|  
|\<change_tracking_option >|예|예|  
|\<db_encryption >|예|아니요|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 대한 계획 캐시는 다음 옵션 중 하나를 설정하여 삭제됩니다.  
  
|||  
|-|-|  
|OFFLINE|READ_WRITE|  
|ONLINE|MODIFY FILEGROUP DEFAULT|  
|MODIFY_NAME|MODIFY FILEGROUP READ_WRITE|  
|COLLATE|MODIFY FILEGROUP READ_ONLY|  
|READ_ONLY||  
  
 프로시저 캐시는 다음 시나리오에도 플러시됩니다.  
  
-   데이터베이스에서 AUTO_CLOSE 데이터베이스 옵션이 ON으로 설정되어 있습니다. 사용자 연결이 데이터베이스를 참조하거나 사용하지 않으면 백그라운드 작업에서 자동으로 데이터베이스를 닫고 종료하려고 합니다.  
  
-   기본 옵션이 있는 데이터베이스에 대해 여러 가지 쿼리를 실행합니다. 그러면 데이터베이스가 삭제됩니다.  
  
-   원본 데이터베이스에 대한 데이터베이스 스냅숏이 삭제됩니다.  
  
-   데이터베이스에 대한 트랜잭션 로그를 성공적으로 다시 작성합니다.  
  
-   데이터베이스 백업을 복원합니다.  
  
-   데이터베이스를 분리합니다.  
  
 계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. 계획 캐시의 삭제된 각 캐시스토어에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 "데이터베이스 유지 관리 또는 재구성 작업으로 인해 '%s' 캐시스토어(계획 캐시의 일부)에 대한 캐시스토어 플러시가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 %d번 발견되었습니다"라는 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-setting-options-on-a-database"></a>1. 데이터베이스 옵션 설정  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스에 대해 복구 모델 및 데이터 페이지 확인 옵션을 설정합니다.  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL PAGE_VERIFY CHECKSUM;  
GO  
  
```  
  
### <a name="b-setting-the-database-to-readonly"></a>2. 데이터베이스를 READ_ONLY로 설정  
 데이터베이스 또는 파일 그룹의 상태를 READ_ONLY 또는 READ_WRITE로 변경하려면 데이터베이스에 대한 배타적 액세스가 필요합니다. 다음 예에서는 데이터베이스를 `SINGLE_USER` 모드로 설정하여 배타적 액세스 권한을 확보한 다음 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 상태를 `READ_ONLY`로 설정한 후 데이터베이스 액세스를 모든 사용자에게 반환합니다.  
  
> [!NOTE]  
>  이 예에서는 첫 번째 `WITH ROLLBACK IMMEDIATE` 문에서 `ALTER DATABASE` 종료 옵션을 사용합니다. 완료되지 않은 트랜잭션은 모두 롤백되며 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대한 다른 모든 연결은 즉시 끊어집니다.  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER  
WITH ROLLBACK IMMEDIATE;  
GO  
ALTER DATABASE AdventureWorks2012  
SET READ_ONLY  
GO  
ALTER DATABASE AdventureWorks2012  
SET MULTI_USER;  
GO  
  
```  
  
### <a name="c-enabling-snapshot-isolation-on-a-database"></a>3. 데이터베이스에서 스냅숏 격리 활성화  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대해 스냅숏 격리 프레임워크 옵션을 활성화합니다.  
  
```  
USE AdventureWorks2012;  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET ALLOW_SNAPSHOT_ISOLATION ON;  
GO  
-- Check the state of the snapshot_isolation_framework  
-- in the database.  
SELECT name, snapshot_isolation_state,   
    snapshot_isolation_state_desc AS description  
FROM sys.databases  
WHERE name = N'AdventureWorks2012';  
GO  
  
```  
  
 결과 집합은 스냅숏 격리 프레임워크가 활성화되었음을 보여 줍니다.  
  
 |name |snapshot_isolation_state |description|  
 |-------------------- |------------------------  |----------|  
 |AdventureWorks2012   |1.                        | ON |  
  
### <a name="d-enabling-modifying-and-disabling-change-tracking"></a>4. 변경 내용 추적 설정, 수정 및 해제  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대해 변경 내용 추적을 설정하고 보존 기간을 `2`일로 설정합니다.  
  
```  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = ON  
(AUTO_CLEANUP = ON, CHANGE_RETENTION = 2 DAYS);  
```  
  
 다음 예에서는 보존 기간을 `3` 일로 바꾸는 방법을 보여 줍니다.  
  
```  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING (CHANGE_RETENTION = 3 DAYS);  
```  
  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대한 변경 내용 추적을 해제하는 방법을 보여 줍니다.  
  
```  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = OFF;  
```  
  
### <a name="e-enabling-the-query-store"></a>5. 쿼리 저장소를 사용하도록 설정  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 다음 예제에서는 쿼리 저장소를 사용하도록 설정하고 쿼리 저장소 매개 변수를 구성합니다.  
  
```  
ALTER DATABASE AdventureWorks2012  
SET QUERY_STORE = ON   
    (  
      OPERATION_MODE = READ_WRITE   
    , CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 )  
    , DATA_FLUSH_INTERVAL_SECONDS = 900   
    , MAX_STORAGE_SIZE_MB = 1024   
    , INTERVAL_LENGTH_MINUTES = 60   
    );  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [ALTER DATABASE 데이터베이스 미러링&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [ALTER DATABASE SET HADR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [통계](../../relational-databases/statistics/statistics.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [변경 내용 추적 설정 및 해제&#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)   
 [DATABASEPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION level&#40; Transact SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.data_spaces &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [쿼리 저장소에 대한 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md) 
  
