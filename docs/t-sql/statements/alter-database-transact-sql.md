---
description: ALTER DATABASE(Transact-SQL)
title: ALTER DATABASE(Transact-SQL) | Microsoft Docs
ms.custom: references_regions
ms.date: 10/30/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_TSQL
- ALTER DATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- databases [SQL Server], modifying
- ALTER DATABASE statement
- databases [SQL Server], renaming
- renaming databases
- database modifications [SQL Server]
- ALTER DATABASE statement, syntax described
- database names [SQL Server], ALTER DATABASE
- modifying databases
- collations [SQL Server], modifying
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 15f8affd-8f39-4021-b092-0379fc6983da
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-current||=azuresqldb-mi-current||=azure-sqldw-latest||>=aps-pdw-2016'
ms.openlocfilehash: bacad46304c0795a5401238fec32a636426e56dd
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489923"
---
# <a name="alter-database-transact-sql"></a>ALTER DATABASE(Transact-SQL)

데이터베이스의 특정 구성 옵션을 수정합니다.

이 아티클에서는 원하는 SQL 제품에 대한 구문, 인수, 설명, 사용 권한 및 예제를 제공합니다.

구문 표기 규칙에 대한 자세한 내용은 [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)을 참조하십시오.

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [SQL 데이터베이스](alter-database-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [SQL Managed Instance](alter-database-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-database-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System(PDW)](alter-database-transact-sql.md?view=aps-pdw-2016-au7)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="overview-sql-server"></a>개요: SQL Server

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 문은 데이터베이스 또는 데이터베이스와 연관된 파일 및 파일 그룹을 수정합니다. 데이터베이스의 파일 및 파일 그룹 추가 또는 제거, 데이터베이스 또는 데이터베이스 내 파일 및 파일 그룹 특성 변경, 데이터베이스 데이터 정렬 변경 및 데이터베이스 옵션 설정을 수행합니다. 데이터베이스 스냅샷은 수정할 수 없습니다. 복제와 연관된 데이터베이스 옵션을 수정하려면 [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)을 사용하세요.

`ALTER DATABASE` 구문은 설명할 항목이 많기 때문에 여러 아티클로 구분하여 설명됩니다.

ALTER DATABASE   
현재 아티클은 데이터베이스의 이름 및 데이터 정렬 변경을 위한 구문 및 관련 정보를 제공합니다.

[ALTER DATABASE 파일 및 파일 그룹 옵션](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)   
데이터베이스의 파일과 파일 그룹을 추가 및 제거하고 파일과 파일 그룹의 특성을 변경하기 위한 구문 및 관련 정보를 제공합니다.

[ALTER DATABASE SET 옵션](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
ALTER DATABASE의 SET 옵션을 사용하여 데이터베이스의 특성을 변경하기 위한 구문 및 관련 정보를 제공합니다.

[ALTER DATABASE 데이터베이스 미러링](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
데이터베이스 미러링과 관련된 ALTER DATABASE의 SET 옵션에 대한 구문 및 관련 정보를 제공합니다.

[ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
Always On 가용성 그룹의 보조 복제본에서 보조 데이터베이스를 구성하기 위한 ALTER DATABASE의 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 옵션에 대한 구문 및 관련 정보를 제공합니다.

[ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
데이터베이스 호환성 수준과 관련된 ALTER DATABASE의 SET 옵션에 대한 구문 및 관련 정보를 제공합니다.

[데이터베이스 범위 구성 변경](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
쿼리 최적화 및 쿼리 실행 관련 동작과 같은 개별 데이터베이스 수준 설정에 사용되는 데이터베이스 범위 구성과 관련된 구문을 제공합니다.

## <a name="syntax"></a>구문

```syntaxsql
-- SQL Server Syntax
ALTER DATABASE { database_name | CURRENT }
{
    MODIFY NAME = new_database_name
  | COLLATE collation_name
  | <file_and_filegroup_options>
  | SET <option_spec> [ ,...n ] [ WITH <termination> ]
}
[;]

<file_and_filegroup_options>::=
  <add_or_modify_files>::=
  <filespec>::=
  <add_or_modify_filegroups>::=
  <filegroup_updatability_option>::=

<option_spec>::=
{
  | <auto_option>
  | <change_tracking_option>
  | <cursor_option>
  | <database_mirroring_option>
  | <date_correlation_optimization_option>
  | <db_encryption_option>
  | <db_state_option>
  | <db_update_option>
  | <db_user_access_option><delayed_durability_option>
  | <external_access_option>
  | <FILESTREAM_options>
  | <HADR_options>
  | <parameterization_option>
  | <query_store_options>
  | <recovery_option>
  | <service_broker_option>
  | <snapshot_option>
  | <sql_option>
  | <termination>
  | <temporal_history_retention>
  | <data_retention_policy>
  | <compatibility_level>
      { 150 | 140 | 130 | 120 | 110 | 100 | 90 }
}
```

## <a name="arguments"></a>인수

*database_name* 수정할 데이터베이스의 이름입니다.

> [!NOTE]
> 포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.

CURRENT   
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상

현재 사용 중인 데이터베이스를 변경하도록 지정합니다.

MODIFY NAME **=** _new_database_name_   
데이터베이스의 이름을 지정된 이름 *new_database_name* 으로 바꿉니다.

COLLATE *collation_name*   
데이터베이스에 대한 데이터 정렬을 지정합니다. *collation_name* 으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 이를 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 데이터 정렬이 지정됩니다.

> [!NOTE]
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 데이터베이스를 만든 후에는 데이터 정렬을 변경할 수 없습니다.

기본 데이터 정렬이 아닌 데이터 정렬로 데이터베이스를 만들 경우 데이터베이스의 데이터는 항상 지정된 데이터 정렬을 따릅니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 경우 포함된 데이터베이스를 만들 때 내부 카탈로그 정보는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 데이터 정렬인 **Latin1_General_100_CI_AS_WS_KS_SC** 를 통해 유지됩니다.

Windows 데이터 정렬 이름 및 SQL 데이터 정렬 이름에 대한 자세한 내용은 [COLLATE](~/t-sql/statements/collations.md)를 참조하세요.

**\<delayed_durability_option> ::=**    
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상

자세한 내용은 [ALTER DATABASE SET 옵션](../../t-sql/statements/alter-database-transact-sql-set-options.md) 및 [트랜잭션 내구성 제어](../../relational-databases/logs/control-transaction-durability.md)를 참조하세요.

**\<file_and_filegroup_options>::=**    
자세한 내용은 [ALTER DATABASE 파일 및 파일 그룹 옵션](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)을 참조하세요.

## <a name="remarks"></a>설명

데이터베이스를 제거하려면 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)를 사용합니다.

데이터베이스의 크기를 줄이려면 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)를 사용합니다.

`ALTER DATABASE` 문은 자동 커밋 모드(기본 트랜잭션 관리 모드)에서 실행되어야 하며 명시적 또는 암시적 트랜잭션에서는 허용되지 않습니다.

데이터베이스 파일의 상태(예: 온라인 또는 오프라인)는 데이터베이스의 상태와는 별도로 유지 관리됩니다. 자세한 내용은 [파일 상태](../../relational-databases/databases/file-states.md)를 참조하세요. 전체 파일 그룹의 가용성은 파일 그룹 내 파일의 상태에 따라 결정됩니다. 파일 그룹을 사용하려면 파일 그룹 내의 모든 파일이 온라인 상태여야 합니다. 파일 그룹이 오프라인 상태인 경우 SQL 문을 사용한 파일 그룹 액세스 시도는 오류가 발생하며 실패하게 됩니다. SELECT 문에 대한 쿼리 계획을 작성할 때 쿼리 최적화 프로그램은 오프라인 파일 그룹에 있는 비클러스터형 인덱스와 인덱싱된 뷰는 피함으로써 이러한 문이 성공하도록 합니다. 그러나 오프라인 파일 그룹에 대상 테이블의 힙이나 클러스터형 인덱스가 있는 경우 SELECT 문은 실패합니다. 또한 오프라인 파일 그룹에 인덱스를 가진 테이블을 수정하는 `INSERT`, `UPDATE` 또는 `DELETE` 문은 실패합니다.

데이터베이스가 RESTORING 상태에 있으면 `ALTER DATABASE` 문은 대부분 실패합니다. 단, 데이터베이스 미러링 옵션을 설정하는 경우는 예외입니다. 활성 복원 작업 중이나 데이터베이스 또는 로그 파일의 복원 작업이 손상된 백업 파일로 인해 실패할 경우 데이터베이스가 RESTORING 상태일 수 있습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 대한 계획 캐시는 다음 옵션 중 하나를 설정하여 삭제됩니다.

- COLLATE
- MODIFY FILEGROUP DEFAULT
- MODIFY FILEGROUP READ_ONLY
- MODIFY FILEGROUP READ_WRITE
- MODIFY_NAME
- OFFLINE
- ONLINE
- PAGE_VERIFY
- READ_ONLY
- READ_WRITE

계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. 계획 캐시의 삭제된 각 캐시스토어에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 `SQL Server has encountered %d occurrence(s) of cachestore flush for the '%s' cachestore (part of plan cache) due to some database maintenance or reconfigure operations`라는 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.

계획 캐시는 다음 시나리오에서도 플러시됩니다.

- 데이터베이스에서 `AUTO_CLOSE` 데이터베이스 옵션이 ON으로 설정되어 있습니다. 사용자 연결이 데이터베이스를 참조하거나 사용하지 않으면 백그라운드 작업에서 자동으로 데이터베이스를 닫고 종료하려고 합니다.
- 기본 옵션이 있는 데이터베이스에 대해 여러 가지 쿼리를 실행합니다. 그러면 데이터베이스가 삭제됩니다.
- 원본 데이터베이스에 대한 데이터베이스 스냅샷이 삭제됩니다.
- 데이터베이스에 대한 트랜잭션 로그를 성공적으로 다시 작성합니다.
- 데이터베이스 백업을 복원합니다.
- 데이터베이스를 분리합니다.

## <a name="changing-the-database-collation"></a>데이터베이스 데이터 정렬 변경

데이터베이스에 다른 데이터 정렬을 적용하기 전에 다음 조건이 충족되었는지 확인하세요.

- 현재 데이터베이스를 사용하고 있는 다른 사용자가 없습니다.
- 데이터베이스의 데이터 정렬에 종속된 스키마 바운드 개체가 없습니다.

데이터베이스 데이터 정렬에 종속되는 다음과 같은 개체가 데이터베이스에 있는 경우 ALTER DATABASE *database_name* COLLATE 문은 실패하게 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `ALTER` 동작을 차단하는 각 개체에 대해 오류 메시지를 반환합니다.

- SCHEMABINDING으로 생성된 사용자 정의 함수 및 뷰
- 계산 열
- CHECK 제약 조건
- 기본 데이터베이스 데이터 정렬에서 상속받은 데이터 정렬을 사용하는 문자 열이 있는 테이블을 반환하는 테이블 반환 함수
  
비스키마 바운드 엔터티에 대한 종속성 정보는 데이터베이스 데이터 정렬이 변경될 때 자동으로 업데이트됩니다.

데이터베이스 데이터 정렬을 변경해도 데이터베이스 개체에 대한 시스템 이름이 중복되는 경우는 발생하지 않습니다. 데이터 정렬 변경 시 중복 이름이 발생하면 다음 네임스페이스에서 데이터베이스 데이터 정렬 변경이 실패할 수 있습니다.

- 개체 이름(프로시저, 테이블, 트리거, 뷰 등)
- 스키마 이름
- 보안 주체(그룹, 역할, 사용자 등)
- 스칼라 유형 이름(시스템 및 사용자 정의 유형)
- 전체 텍스트 카탈로그 이름
- 개체 내의 열 또는 매개 변수 이름
- 테이블 내의 인덱스 이름

새로운 데이터 정렬로 중복 이름이 생성되는 경우 변경 동작은 실패하게 되며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 중복이 발견된 네임스페이스를 지정하는 오류 메시지를 반환합니다.

## <a name="viewing-database-information"></a>데이터베이스 정보 보기

카탈로그 뷰, 시스템 함수 및 시스템 저장 프로시저를 사용하여 데이터베이스, 파일 및 파일 그룹에 대한 정보를 반환할 수 있습니다.

## <a name="permissions"></a>사용 권한

데이터베이스에 대한 `ALTER` 권한이 필요합니다.

## <a name="examples"></a>예제

### <a name="a-changing-the-name-of-a-database"></a>A. 데이터베이스의 이름 변경

다음 예에서는 `AdventureWorks2012` 데이터베이스의 이름을 `Northwind`로 변경합니다.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
Modify Name = Northwind ;
GO
```

### <a name="b-changing-the-collation-of-a-database"></a>B. 데이터베이스 데이터 정렬 변경

다음 예에서는 `testdb`S 데이터 정렬을 사용하여 `SQL_Latin1_General_CP1_CI_A`라는 데이터베이스를 만든 다음 `testdb` 데이터베이스의 데이터 정렬을 `COLLATE French_CI_AI`로 변경합니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상

```sql
USE master;
GO

CREATE DATABASE testdb
COLLATE SQL_Latin1_General_CP1_CI_AS ;
GO

ALTER DATABASE testDB
COLLATE French_CI_AI ;
GO
```

## <a name="see-also"></a>참고 항목

- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [시스템 데이터베이스](../../relational-databases/databases/system-databases.md)

::: moniker-end
::: moniker range="=azuresqldb-current"

:::row:::
    :::column:::
        [SQL Server](alter-database-transact-sql.md?view=sql-server-ver15&preserve-view=true)
    :::column-end:::
    :::column:::
        **_\* SQL Database \*_** &nbsp;
    :::column-end:::
    :::column:::
        [SQL Managed Instance](alter-database-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-database-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System(PDW)](alter-database-transact-sql.md?view=aps-pdw-2016-au7)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="overview-sql-database"></a>개요: SQL Database

Azure SQL Database에서 이 문을 사용하여 데이터베이스를 수정합니다. 이 문을 사용하여 데이터베이스 이름을 변경하고, 데이터베이스의 버전 및 서비스 목표를 변경하고, 데이터베이스를 탄력적 풀에 연결하거나 탄력적 풀에서 제거하고, 데이터베이스 옵션을 설정하고, 데이터베이스를 지역 복제 관계의 보조로 추가 또는 제거하고, 데이터베이스 호환성 수준을 설정합니다.

`ALTER DATABASE` 구문은 설명할 항목이 많기 때문에 여러 아티클로 구분하여 설명됩니다.

ALTER DATABASE   
현재 아티클은 데이터베이스의 이름 및 데이터 정렬 변경을 위한 구문 및 관련 정보를 제공합니다.

[ALTER DATABASE SET 옵션](../../t-sql/statements/alter-database-transact-sql-set-options.md?view=azuresqldb-currentls)    
ALTER DATABASE의 SET 옵션을 사용하여 데이터베이스의 특성을 변경하기 위한 구문 및 관련 정보를 제공합니다.

[ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md?view=azuresqldb-currentls)   
데이터베이스 호환성 수준과 관련된 ALTER DATABASE의 SET 옵션에 대한 구문 및 관련 정보를 제공합니다.

## <a name="syntax"></a>구문

```syntaxsql
-- Azure SQL Database Syntax
ALTER DATABASE { database_name | CURRENT }
{
    MODIFY NAME = new_database_name
  | MODIFY ( <edition_options> [, ... n] )
  | MODIFY BACKUP_STORAGE_REDUNDANCY = { 'LOCAL' | 'ZONE' | 'GEO' }
  | SET { <option_spec> [ ,... n ] WITH <termination>}
  | ADD SECONDARY ON SERVER <partner_server_name>
    [WITH ( <add-secondary-option>::=[, ... n] ) ]
  | REMOVE SECONDARY ON SERVER <partner_server_name>
  | FAILOVER
  | FORCE_FAILOVER_ALLOW_DATA_LOSS
}
[;]

<edition_options> ::=
{

  MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 ... 1024 ... 4096 GB }
  | EDITION = { 'Basic' | 'Standard' | 'Premium' | 'GeneralPurpose' | 'BusinessCritical' | 'Hyperscale'}
  | SERVICE_OBJECTIVE =
       { <service-objective>
       | { ELASTIC_POOL (name = <elastic_pool_name>) }
       }
}

<add-secondary-option> ::=
   {
      ALLOW_CONNECTIONS = { ALL | NO }
     | SERVICE_OBJECTIVE =
       { <service-objective>
       | { ELASTIC_POOL ( name = <elastic_pool_name>) }
       }
   }

<service-objective> ::={ 'Basic' |'S0' | 'S1' | 'S2' | 'S3'| 'S4'| 'S6'| 'S7'| 'S9'| 'S12'
       | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'
      | 'GP_Gen4_1' | 'GP_Gen4_2' | 'GP_Gen4_3' | 'GP_Gen4_4' | 'GP_Gen4_5' | 'GP_Gen4_6'
      | 'GP_Gen4_7' | 'GP_Gen4_8' | 'GP_Gen4_9' | 'GP_Gen4_10' | 'GP_Gen4_16' | 'GP_Gen4_24'
      | 'GP_Gen5_2' | 'GP_Gen5_4' | 'GP_Gen5_6' | 'GP_Gen5_8' | 'GP_Gen5_10' | 'GP_Gen5_12' | 'GP_Gen5_14'
      | 'GP_Gen5_16' | 'GP_Gen5_18' | 'GP_Gen5_20' | 'GP_Gen5_24' | 'GP_Gen5_32' | 'GP_Gen5_40' | 'GP_Gen5_80'
      | 'GP_Fsv2_8' | 'GP_Fsv2_10' | 'GP_Fsv2_12' | 'GP_Fsv2_14' | 'GP_Fsv2_16' | 'GP_Fsv2_18'
      | 'GP_Fsv2_20' | 'GP_Fsv2_24' | 'GP_Fsv2_32' | 'GP_Fsv2_36' | 'GP_Fsv2_72'
      | 'GP_S_Gen5_1' | 'GP_S_Gen5_2' | 'GP_S_Gen5_4' | 'GP_S_Gen5_6' | 'GP_S_Gen5_8'
      | 'GP_S_Gen5_10' | 'GP_S_Gen5_12' | 'GP_S_Gen5_14' | 'GP_S_Gen5_16'
      | 'GP_S_Gen5_18' | 'GP_S_Gen5_20' | 'GP_S_Gen5_24' | 'GP_S_Gen5_32' | 'GP_S_Gen5_40'
      | 'BC_Gen4_1' | 'BC_Gen4_2' | 'BC_Gen4_3' | 'BC_Gen4_4' | 'BC_Gen4_5' | 'BC_Gen4_6'
      | 'BC_Gen4_7' | 'BC_Gen4_8' | 'BC_Gen4_9' | 'BC_Gen4_10' | 'BC_Gen4_16' | 'BC_Gen4_24'
      | 'BC_Gen5_2' | 'BC_Gen5_4' | 'BC_Gen5_6' | 'BC_Gen5_8' | 'BC_Gen5_10' | 'BC_Gen5_12' | 'BC_Gen5_14'
      | 'BC_Gen5_16' | 'BC_Gen5_18' | 'BC_Gen5_20' | 'BC_Gen5_24' | 'BC_Gen5_32' | 'BC_Gen5_40' | 'BC_Gen5_80'
      | 'BC_M_8' | 'BC_M_10' | 'BC_M_12' | 'BC_M_14' | 'BC_M_16' | 'BC_M_18'
      | 'BC_M_20' | 'BC_M_24' | 'BC_M_32' | 'BC_M_64' | 'BC_M_128'
      | 'HS_GEN4_1' | 'HS_GEN4_2' | 'HS_GEN4_4' | 'HS_GEN4_8' | 'HS_GEN4_16' | 'HS_GEN4_24'
      | 'HS_GEN5_2' | 'HS_GEN5_4' | 'HS_GEN5_8' | 'HS_GEN5_16' | 'HS_GEN5_24' | 'HS_GEN5_32' | 'HS_GEN5_48' | 'HS_GEN5_80'
      | { ELASTIC_POOL(name = <elastic_pool_name>) }
      }

<option_spec> ::=
{
    <auto_option>
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
  | <compatibility_level>
    { 150 | 140 | 130 | 120 | 110 | 100 | 90 }

}
```

## <a name="arguments"></a>인수

*database_name*   
수정할 데이터베이스의 이름입니다.

CURRENT   
현재 사용 중인 데이터베이스를 변경하도록 지정합니다.

MODIFY NAME **=** _new_database_name_   
데이터베이스의 이름을 지정된 이름 *new_database_name* 으로 바꿉니다. 다음 예에서는 `db1` 데이터베이스의 이름을 `db2`로 변경합니다.

```sql
ALTER DATABASE db1
    MODIFY Name = db2 ;
```

MODIFY (EDITION **=** ['Basic' \| 'Standard' \| 'Premium' \|'GeneralPurpose' \| 'BusinessCritical' \| 'Hyperscale'])   
데이터베이스의 서비스 계층을 변경합니다.

다음 예제에서는 버전을 `Premium`으로 변경합니다.

```sql
ALTER DATABASE current
    MODIFY (EDITION = 'Premium');
```

> [!IMPORTANT]
> 데이터베이스의 MAXSIZE 속성이 해당 버전에서 지원되는 유효 범위 밖의 값으로 설정되면 EDITION 변경이 실패합니다.

MODIFY (BACKUP_STORAGE_REDUNDANCY **=** ['LOCAL' \| 'ZONE' \| 'GEO'])   
데이터베이스의 특정 시점 복원 백업 및 장기 보존 백업(구성된 경우)의 스토리지 중복을 변경합니다. 변경 내용은 앞으로 수행되는 모든 백업에 적용됩니다. 기존 백업은 이전 설정을 계속 사용합니다. 

> [!IMPORTANT]
> Azure SQL Database에 대한 BACKUP_STORAGE_REDUNDANCY 옵션은 브라질 남부에서 퍼블릭 미리 보기로 이용할 수 있으며, 일반적으로 동남 아시아 Azure 지역에서만 이용할 수 있습니다.  

MODIFY (MAXSIZE **=** [100 MB \| 500 MB \| 1 \| 1024...4096] GB)   
데이터베이스의 최대 크기를 지정합니다. 최대 크기는 데이터베이스의 EDITION 속성에 대한 유효한 값 집합을 따라야 합니다. 데이터베이스의 최대 크기를 변경하면 데이터베이스 EDITION이 변경될 수 있습니다.

> [!NOTE]
> **MAXSIZE** 인수는 하이퍼스케일 서비스 계층의 단일 데이터베이스에 적용되지 않습니다. 하이퍼스케일 서비스 계층 데이터베이스는 필요에 따라 100TB까지 증가합니다. SQL Database 서비스는 스토리지를 자동으로 추가하므로 최대 크기를 설정할 필요가 없습니다.

**DTU 모델**

|**MAXSIZE**|**기본**|**S0-S2**|**S3-S12**|**P1-P6**|**P11-P15**|
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------|
|100MB|√|√|√|√|√|
|250MB|√|√|√|√|√|
|500MB|√|√|√|√|√|
|1 GB|√|√|√|√|√|
|2GB|√ (D)|√|√|√|√|
|5GB|해당 없음|√|√|√|√|
|10 GB|해당 없음|√|√|√|√|
|20GB|해당 없음|√|√|√|√|
|30GB|해당 없음|√|√|√|√|
|40GB|해당 없음|√|√|√|√|
|50GB|해당 없음|√|√|√|√|
|100GB|해당 없음|√|√|√|√|
|150GB|해당 없음|√|√|√|√|
|200GB|해당 없음|√|√|√|√|
|250GB|해당 없음|√ (D)|√ (D)|√|√|
|300GB|해당 없음|√|√|√|√|
|400GB|N/A|√|√|√|√|
|500GB|해당 없음|√|√|√ (D)|√|
|750GB|해당 없음|√|√|√|√|
|1024GB|해당 없음|√|√|√|√ (D)|
|1024GB에서 최대 4096GB(256 GB*로 증분)|해당 없음|해당 없음|해당 없음|해당 없음|√|

\* P11과 P15는 기본 크기인 1024를 사용하여 MAXSIZE를 최대 4TB까지 허용합니다. P11 및 P15는 추가 비용 없이 최대 4TB가 포함된 스토리지를 사용할 수 있습니다. 프리미엄 계층에서 1TB 초과 MAXSIZE는 현재 다음 지역에서 사용할 수 있습니다. 미국 동부2, 미국 서부, US Gov 버지니아, 서유럽, 독일 중부, 동남 아시아, 일본 동부, 오스트레일리아 동부, 캐나다 중부 및 캐나다 동부. DTU 모델에 대한 리소스 제한에 관한 자세한 내용은 [DTU 리소스 제한](/azure/sql-database/sql-database-dtu-resource-limits)을 참조하세요.

DTU 모델에 대한 MAXSIZE 값은 지정된 경우 지정된 서비스 계층에 대한 위의 표에 표시된 유효한 값이어야 합니다.

**vCore 모델**

**범용 - 프로비저닝된 컴퓨팅 - Gen4(1부)**

|MAXSIZE|GP_Gen4_1|GP_Gen4_2|GP_Gen4_3|GP_Gen4_4|GP_Gen4_5|GP_Gen4_6|
|:----- | ------: |-------: |-------: |-------: |-------: |--------:|
|최대 데이터 크기(GB)|1024|1024|1024|1536|1536|1536|

**범용 - 프로비저닝된 컴퓨팅 - Gen4(2부)**

|MAXSIZE|GP_Gen4_7|GP_Gen4_8|GP_Gen4_9|GP_Gen4_10|GP_Gen4_16|GP_Gen4_24
|:----- | ------: |-------: |-------: |-------: |-------: |--------:|
|최대 데이터 크기(GB)|1536|3072|3072|3072|4096|4096|

**범용 - 프로비저닝된 컴퓨팅 - Gen5(1부)**

|MAXSIZE|GP_Gen5_2|GP_Gen5_4|GP_Gen5_6|GP_Gen5_8|GP_Gen5_10|GP_Gen5_12|GP_Gen5_14|
|:----- | ------: |-------: |-------: |-------: |--------: |---------:|--------: |
|최대 데이터 크기(GB)|1024|1024|1024|1536|1536|1536|1536|

**범용 - 프로비저닝된 컴퓨팅 - Gen5(2부)**

|MAXSIZE|GP_Gen5_16|GP_Gen5_18|GP_Gen5_20|GP_Gen5_24|GP_Gen5_32|GP_Gen5_40|GP_Gen5_80|
|:----- | ------: |-------: |-------: |-------: |--------: |---------:|--------: |
|최대 데이터 크기(GB)|3072|3072|3072|4096|4096|4096|4096|

**범용 - 프로비저닝된 컴퓨팅 - Fsv2 시리즈(1부)**

|MAXSIZE|GP_Fsv2_8|GP_Fsv2_10|GP_Fsv2_12|GP_Fsv2_14|GP_Fsv2_16|GP_Fsv2_18|
|:----- | ------: | ------: | ------: | ------: | ------: | ------: |
|최대 데이터 크기(GB)|1024|1024|1024|1024|1536|1536|

**범용 - 프로비저닝된 컴퓨팅 - Fsv2 시리즈(2부)**

|MAXSIZE|GP_Fsv2_20|GP_Fsv2_24|GP_Fsv2_32|GP_Fsv2_36|GP_Fsv2_72|
|:----- | ------: | ------: | ------: | ------: | ------: |
|최대 데이터 크기(GB)|1536|1536|3072|3072|4096|

**범용 - 서버리스 컴퓨팅 - Gen5(1부)**

|MAXSIZE|GP_S_Gen5_1|GP_S_Gen5_2|GP_S_Gen5_4|GP_S_Gen5_6|GP_S_Gen5_8|
|:----- | ------: |-------: |-------: |-------: |--------: |
|최대 vCore 수|1|2|4|6|8|

**범용 - 서버리스 컴퓨팅 - Gen5(2부)**

|MAXSIZE|GP_S_Gen5_10|GP_S_Gen5_12|GP_S_Gen5_14|GP_S_Gen5_16|
|:----- | ------: |-------: |-------: |-------: |
|최대 vCore 수|10|12|14|16|

**범용 - 서버리스 컴퓨팅 - Gen5(3부)**

|MAXSIZE|GP_S_Gen5_18|GP_S_Gen5_20|GP_S_Gen5_24|GP_S_Gen5_32|GP_S_Gen5_40|
|:----- | ------: |-------: |-------: |-------: |--------: |
|최대 vCore 수|18|20|24|32|40|

**중요 비즈니스용 - 프로비저닝된 컴퓨팅 - Gen4(1부)**

|컴퓨팅 크기(서비스 목표)|BC_Gen4_1|BC_Gen4_2|BC_Gen4_3|BC_Gen4_4|BC_Gen4_5|BC_Gen4_6|
|:--------------- | ------: |-------: |-------: |-------: |-------: |-------: |
|최대 데이터 크기(GB)|1024|1024|1024|1024|1024|1024|

**중요 비즈니스용 - 프로비저닝된 컴퓨팅 - Gen4(2부)**

|컴퓨팅 크기(서비스 목표)|BC_Gen4_7|BC_Gen4_8|BC_Gen4_9|BC_Gen4_10|BC_Gen4_16|BC_Gen4_24|
|:--------------- | ------: |-------: |-------: |--------: |--------: |--------: |
|최대 데이터 크기(GB)|1024|1024|1024|1024|1024|1024|

**중요 비즈니스용 - 프로비저닝된 컴퓨팅 - Gen5(1부)**

|MAXSIZE|BC_Gen5_2|BC_Gen5_4|BC_Gen5_6|BC_Gen5_8|BC_Gen5_10|BC_Gen5_12|BC_Gen5_14|
|:----- | ------: |-------: |-------: |-------: |---------: |--------:|--------: |
|최대 데이터 크기(GB)|1024|1024|1024|1536|1536|1536|1536|

**중요 비즈니스용 - 프로비저닝된 컴퓨팅 - Gen5(2부)**

|MAXSIZE|BC_Gen5_16|BC_Gen5_18|BC_Gen5_20|BC_Gen5_24|BC_Gen5_32|BC_Gen5_40|BC_Gen5_80|
|:----- | -------: |--------: |--------: |--------: |--------: |---------:|--------: |
|최대 데이터 크기(GB)|3072|3072|3072|4096|4096|4096|4096|

**중요 비즈니스용 - 프로비저닝된 컴퓨팅 - M 시리즈(1부)**

|MAXSIZE|BC_M_8|BC_M_10|BC_M_12|BC_M_14|BC_M_16|BC_M_18|
|:----- | -------: | -------: | -------: | -------: | -------: | -------: |
|최대 데이터 크기(GB)|512|640|768|896|1024|1,152|

**중요 비즈니스용 - 프로비저닝된 컴퓨팅 - M 시리즈(2부)**

|MAXSIZE|BC_M_20|BC_M_24|BC_M_32|BC_M_64|BC_M_128|
|:----- | -------: | -------: | -------: | -------: | -------: |
|최대 데이터 크기(GB)|1280|1536|2048|4096|4096|

vCore 모델을 사용할 때 `MAXSIZE`값이 설정되지 않은 경우 기본값은 32GB입니다. vCore 모델에 대한 리소스 제한에 관한 자세한 내용은 [vCore 리소스 제한](/azure/sql-database/sql-database-dtu-resource-limits)을 참조하세요.

MAXSIZE 및 EDITION 인수에는 다음과 같은 규칙이 적용됩니다.

- EDITION이 지정되었지만 MAXSIZE가 지정되지 않은 경우 해당 버전에 대한 기본값이 사용됩니다. 예를 들어 EDITION이 Standard로 설정되었고 MAXSIZE가 지정되지 않았으면 MAXSIZE가 자동으로 250MB로 설정됩니다.
- MAXSIZE 또는 EDITION을 모두 지정하지 않으면 EDITION이 General Purpose로 설정되고, MAXSIZE는 32GB로 설정됩니다.

MODIFY (SERVICE_OBJECTIVE = \<service-objective>)   
컴퓨팅 크기(서비스 목표)를 지정합니다. 다음 예제에서는 프리미엄 데이터베이스의 서비스 목표를 `P6`으로 변경합니다.

```sql
ALTER DATABASE current
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```

SERVICE_OBJECTIVE   

- **단일 및 풀링된 데이터베이스**

  - 컴퓨팅 크기(서비스 목표)를 지정합니다. 서비스 목표의 사용 가능한 값은 `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_3`, `GP_GEN4_4`, `GP_GEN4_5`, `GP_GEN4_6`, `GP_GEN4_7`, `GP_GEN4_8`, `GP_GEN4_7`, `GP_GEN4_8`, `GP_GEN4_9`, `GP_GEN4_10`, `GP_GEN4_16`, `GP_GEN4_24`, `BC_GEN4_1`, `BC_GEN4_2`, `BC_GEN4_3`, `BC_GEN4_4`, `BC_GEN4_5`, `BC_GEN4_6`, `BC_GEN4_7`, `BC_GEN4_8`, `BC_GEN4_9`, `BC_GEN4_10`, `BC_GEN4_16`, `BC_GEN4_24`, `GP_Gen5_2`, `GP_Gen5_4`, `GP_Gen5_6`, `GP_Gen5_8`, `GP_Gen5_10`, `GP_Gen5_12`, `GP_Gen5_14`, `GP_Gen5_16`, `GP_Gen5_18`, `GP_Gen5_20`, `GP_Gen5_24`, `GP_Gen5_32`, `GP_Gen5_40`, `GP_Gen5_80`, `GP_Fsv2_8`, `GP_Fsv2_10`, `GP_Fsv2_12`, `GP_Fsv2_14`, `GP_Fsv2_16`, `GP_Fsv2_18`, `GP_Fsv2_20`, `GP_Fsv2_24`, `GP_Fsv2_32`, `GP_Fsv2_36`, `GP_Fsv2_72`, `BC_Gen5_2`, `BC_Gen5_4`, `BC_Gen5_6`, `BC_Gen5_8`, `BC_Gen5_10`, `BC_Gen5_12`, `BC_Gen5_14`, `BC_Gen5_16`, `BC_Gen5_18`, `BC_Gen5_20`, `BC_Gen5_24`, `BC_Gen5_32`,`BC_Gen5_40`, `BC_Gen5_80`, `BC_M_8`, `BC_M_10`, `BC_M_12`, `BC_M_14`, `BC_M_16`, `BC_M_18`, `BC_M_20`, `BC_M_24`, `BC_M_32`, `BC_M_64`, `BC_M_128`입니다.

- **서버리스 컴퓨팅 계층의 단일 데이터베이스**

  - 컴퓨팅 크기(서비스 목표)를 지정합니다. 서비스 목표의 사용 가능한 값은 `GP_S_Gen5_1`, `GP_S_Gen5_2`, `GP_S_Gen5_4`, `GP_S_Gen5_6`, `GP_S_Gen5_8`, `GP_S_Gen5_10`, `GP_S_Gen5_12`, `GP_S_Gen5_14`, `GP_S_Gen5_16`, `GP_S_Gen5_18`, `GP_S_Gen5_20`, `GP_S_Gen5_24`, `GP_S_Gen5_32`, `GP_S_Gen5_40`입니다.

- **하이퍼스케일 서비스 계층의 단일 데이터베이스인 경우**

  - 컴퓨팅 크기(서비스 목표)를 지정합니다. 서비스 목표의 사용 가능한 값은 `HS_GEN4_1` `HS_GEN4_2` `HS_GEN4_4` `HS_GEN4_8` `HS_GEN4_16`, `HS_GEN4_24`, `HS_Gen5_2`, `HS_Gen5_4`, `HS_Gen5_8`, `HS_Gen5_16`, `HS_Gen5_24`, `HS_Gen5_32`, `HS_Gen5_48`, `HS_Gen5_80`입니다.

서비스 목표 설명과 크기, 버전 및 서비스 목표 조합 등의 정보에 대한 자세한 내용은 [Azure SQL Database 서비스 계층 및 성능 수준](/azure/azure-sql/database/purchasing-models), [DTU 리소스 제한](/azure/sql-database/sql-database-dtu-resource-limits) 및 [vCore 리소스 제한](/azure/sql-database/sql-database-dtu-resource-limits)을 참조하세요. PRS 서비스 목표에 대한 지원이 제거되었습니다. 질문에 대해서는, 이메일 별칭(premium-rs@microsoft.com)을 사용하세요.

MODIFY (SERVICE_OBJECTIVE = ELASTIC\_POOL (name = \<elastic_pool_name>)   
탄력적 풀에 기존 데이터베이스를 추가하려면 데이터베이스의 SERVICE_OBJECTIVE를 ELASTIC_POOL로 설정하고 탄력적 풀의 이름을 입력합니다. 동일한 서버 내의 다른 탄력적 풀에 데이터베이스를 변경하려면 이 옵션을 사용할 수도 있습니다. 자세한 내용은 [SQL Database 탄력적 풀 만들기 및 관리](/azure/azure-sql/database/elastic-pool-overview)를 참조하세요. 탄력적 풀에서 데이터베이스를 제거하려면 ALTER DATABASE를 사용하여 SERVICE_OBJECTIVE를 단일 데이터베이스 컴퓨팅 크기(서비스 목표)로 설정합니다.

> [!NOTE]
> 하이퍼스케일 서비스 계층의 데이터베이스는 탄력적 풀에 추가할 수 없습니다.

ADD SECONDARY ON SERVER \<partner_server_name>   
파트너 서버에 동일한 이름의 지역 복제 보조 데이터베이스를 만들고, 지역 복제 주 데이터베이스에 로컬 데이터베이스를 만들고, 주 데이터베이스에서 새 보조 데이터베이스에 데이터를 비동기적으로 복제하기 시작합니다. 동일한 이름의 데이터베이스가 보조 데이터베이스에 이미 있으면 명령이 실패합니다. 이 명령은 주가 되는 로컬 데이터베이스를 호스팅하는 서버의 master 데이터베이스에서 실행됩니다.

> [!IMPORTANT]
> 하이퍼스케일 서비스 계층은 현재 지역에서 복제를 지원하지 않습니다.

> [!IMPORTANT]
> 기본적으로 보조 데이터베이스는 기본 데이터베이스 또는 원본 데이터베이스와 동일한 백업 스토리지 중복성을 사용하여 생성됩니다. 보조 데이터베이스를 만드는 동안 백업 스토리지 중복성을 변경하는 것은 T-SQL을 통해 지원되지 않습니다. 

WITH ALLOW_CONNECTIONS { **ALL** | NO }   
ALLOW_CONNECTIONS를 지정하지 않으면 기본적으로 ALL로 설정됩니다. ALL로 설정된 경우 연결할 적절한 권한이 있는 모든 로그인을 허용하는 읽기 전용 데이터베이스입니다.

WITH SERVICE_OBJECTIVE { `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_3`, `GP_GEN4_4`, `GP_GEN4_5`, `GP_GEN4_6`, `GP_GEN4_7`, `GP_GEN4_8`, `GP_GEN4_7`, `GP_GEN4_8`, `GP_GEN4_9`, `GP_GEN4_10`, `GP_GEN4_16`, `GP_GEN4_24`, `BC_GEN4_1`, `BC_GEN4_2`, `BC_GEN4_3`, `BC_GEN4_4`, `BC_GEN4_5`, `BC_GEN4_6`, `BC_GEN4_7`, `BC_GEN4_8`, `BC_GEN4_9`, `BC_GEN4_10`, `BC_GEN4_16`, `BC_GEN4_24`, `GP_Gen5_2`, `GP_Gen5_4`, `GP_Gen5_6`, `GP_Gen5_8`, `GP_Gen5_10`, `GP_Gen5_12`, `GP_Gen5_14`, `GP_Gen5_16`, `GP_Gen5_18`, `GP_Gen5_20`, `GP_Gen5_24`, `GP_Gen5_32`, `GP_Gen5_40`, `GP_Gen5_80`, `GP_Fsv2_8`, `GP_Fsv2_10`, `GP_Fsv2_12`, `GP_Fsv2_14`, `GP_Fsv2_16`, `GP_Fsv2_18`, `GP_Fsv2_20`, `GP_Fsv2_24`, `GP_Fsv2_32`, `GP_Fsv2_36`, `GP_Fsv2_72`, `GP_S_Gen5_1`, `GP_S_Gen5_2`, `GP_S_Gen5_4`, `GP_S_Gen5_6`, `GP_S_Gen5_8`, `GP_S_Gen5_10`, `GP_S_Gen5_12`, `GP_S_Gen5_14`, `GP_S_Gen5_16`, `GP_S_Gen5_18`, `GP_S_Gen5_20`, `GP_S_Gen5_24`, `GP_S_Gen5_32`, `GP_S_Gen5_40`, `BC_Gen5_2`, `BC_Gen5_4`, `BC_Gen5_6`, `BC_Gen5_8`, `BC_Gen5_10`, `BC_Gen5_12`, `BC_Gen5_14`, `BC_Gen5_16`, `BC_Gen5_18`, `BC_Gen5_20`, `BC_Gen5_24`, `BC_Gen5_32`,`BC_Gen5_40`, `BC_Gen5_80`, `BC_M_8`, `BC_M_10`, `BC_M_12`, `BC_M_14`, `BC_M_16`, `BC_M_18`, `BC_M_20`, `BC_M_24`, `BC_M_32`, `BC_M_64`, `BC_M_128` }

SERVICE_OBJECTIVE를 지정하지 않으면 보조 데이터베이스가 주 데이터베이스와 동일한 서비스 수준에서 생성됩니다. SERVICE_OBJECTIVE를 지정하면 보조 데이터베이스가 지정된 수준에서 생성됩니다. 이 옵션은 보다 저렴한 서비스 수준에서 지역 복제된 보조 데이터베이스를 만들도록 지원합니다. 지정된 SERVICE_OBJECTIVE를 소스와 동일한 버전 내에 있어야 합니다. 예를 들어 버전이 프리미엄인 경우 S0를 지정할 수 없습니다.

ELASTIC_POOL (name = \<elastic_pool_name>) ELASTIC_POOL을 지정하지 않으면 보조 데이터베이스는 탄력적 풀에서 생성되지 않습니다. ELASTIC_POOL을 지정하면 보조 데이터베이스는 탄력적인 풀에서 생성됩니다.

> [!IMPORTANT]
> ADD SECONDARY 명령을 실행하는 사용자는 주 서버에서 DBManager이고, 로컬 데이터베이스에서 db_owner 멤버 자격과 보조 서버에서 DBManager 멤버 자격이 있어야 합니다. 클라이언트 IP 주소를 주 서버와 보조 서버 모두에 대한 방화벽 규칙의 허용 목록에 추가해야 합니다. 다른 클라이언트 IP 주소를 사용할 경우 주 서버에 추가된 것과 동일한 클라이언트 IP 주소를 보조 서버에도 추가해야 합니다. 이는 지역 복제를 시작하기 위해 ADD SECONDARY 명령을 실행하기 전에 수행해야 하는 필수 단계입니다.

REMOVE SECONDARY ON SERVER \<partner_server_name> 지정된 서버에서 지정되고 지역 복제된 보조 데이터베이스를 제거합니다. 이 명령은 주 데이터베이스를 호스팅하는 서버의 master 데이터베이스에서 실행됩니다.

> [!IMPORTANT]
> REMOVE SECONDARY 명령을 실행하는 사용자는 주 서버에서 DBManager여야 합니다.

FAILOVER 지역 복제 파트너 자격에서 보조 데이터베이스를 승격합니다. 여기서 명령을 실행하여 주 데이터베이스가 되고 현재 주 데이터베이스를 새 보조 데이터베이스로 강등합니다. 이 과정의 일환으로 지역 복제 모드를 일시적으로 비동기 모드에서 동기 모드로 전환합니다. 장애 조치 과정 중:

1. 주 데이터베이스는 새 트랜잭션 사용을 중지합니다.
2. 모든 대기 중인 트랜잭션은 보조 데이터베이스에 플러시됩니다.
3. 보조 데이터베이스는 주 데이터베이스가 되고, 이전 주 데이터베이스/새 보조 데이터베이스에서 비동기 지역 복제를 시작합니다.

이 시퀀스는 데이터 손실이 발생하지 않게 합니다. 두 데이터베이스를 사용할 수 없는 기간은 역할이 전환되는 동안의 0~25초 순서입니다. 전체 작업은 1분 넘게 걸리지 않아야 합니다. 주 데이터베이스를 사용할 수 없는 경우 이 명령을 실행할 때 주 데이터베이스를 사용할 수 없다는 오류 메시지를 표시하며 명령이 실패합니다. 장애 조치 프로세스가 완료되지 않고 중단된 경우 강제 장애 조치 명령을 사용하여 데이터 손실을 허용할 수 있습니다. 그런 다음, 손실 데이터를 복구해야 하는 경우 DevOps(CSS)를 호출하여 손실 데이터를 복구합니다.

> [!IMPORTANT]
> FAILOVER 명령을 실행하는 사용자는 주 서버와 보조 서버 모두에서 DBManager여야 합니다.

FORCE_FAILOVER_ALLOW_DATA_LOSS 지역 복제 파트너 자격에서 보조 데이터베이스를 승격합니다. 여기서 명령을 실행하여 주 데이터베이스가 되고 현재 주 데이터베이스를 새 보조 데이터베이스로 강등합니다. 현재 주 데이터베이스를 더 이상 사용할 수 없는 경우에만 이 명령을 사용합니다. 가용성을 복원하는 것이 중요한 경우에 재해 복구 전용으로 설계되어 일부 데이터 손실을 허용 가능합니다.

강제 장애 조치(failover) 중:

1. 지정된 보조 데이터베이스는 즉시 주 데이터베이스가 되고 새 트랜잭션을 허용하기 시작합니다.
2. 원래 주 데이터베이스가 새 주 데이터베이스와 다시 연결될 수 있는 경우 원래 주 데이터베이스에서 증분 백업이 수행되고 원래 주 데이터베이스는 새 보조 데이터베이스가 됩니다.
3. 이전 주 데이터베이스의 이 증분 백업으로부터 데이터를 복구하기 위해 사용자는 DevOps/CSS를 사용합니다.
4. 추가 보조 데이터베이스가 있는 경우 새 주 데이터베이스의 보조 데이터베이스가 되도록 자동으로 재구성됩니다. 이 프로세스는 비동기적이며 이 프로세스가 완료될 때까지 지연될 수 있습니다. 재구성이 완료될 때까지 보조 데이터베이스는 여전히 이전 기본 데이터베이스의 보조 데이터베이스입니다.

> [!IMPORTANT]
> `FORCE_FAILOVER_ALLOW_DATA_LOSS` 명령을 실행하는 사용자는 주 서버와 보조 서버 모두에서 `dbmanager` 역할에 속해야 합니다.

## <a name="remarks"></a>설명

데이터베이스를 제거하려면 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)를 사용합니다.
데이터베이스의 크기를 줄이려면 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)를 사용합니다.

`ALTER DATABASE` 문은 자동 커밋 모드(기본 트랜잭션 관리 모드)에서 실행되어야 하며 명시적 또는 암시적 트랜잭션에서는 허용되지 않습니다.

계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. 계획 캐시의 삭제된 각 캐시스토어에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 `SQL Server has encountered %d occurrence(s) of cachestore flush for the '%s' cachestore (part of plan cache) due to some database maintenance or reconfigure operations`라는 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.

프로시저 캐시는 다음 시나리오에도 플러시됩니다. 기본 옵션이 있는 데이터베이스에 대해 여러 가지 쿼리를 실행합니다. 그러면 데이터베이스가 삭제됩니다.

## <a name="viewing-database-information"></a>데이터베이스 정보 보기

카탈로그 뷰, 시스템 함수 및 시스템 저장 프로시저를 사용하여 데이터베이스, 파일 및 파일 그룹에 대한 정보를 반환할 수 있습니다.

## <a name="permissions"></a>사용 권한

데이터베이스를 변경하려면 로그인이 서버 수준 보안 주체 로그인(프로비저닝 프로세스에서 생성됨), 마스터의 `dbmanager` 데이터베이스 역할의 멤버, 현재 데이터베이스의 `db_owner` 데이터베이스 역할 또는 데이터베이스의 `dbo` 중 하나여야 합니다.

## <a name="examples"></a>예제

### <a name="a-check-the-edition-options-and-change-them"></a>A. 버전 옵션 확인 및 변경

db1 데이터베이스의 버전과 최대 크기를 설정합니다.

```sql
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>B. 다른 탄력적 풀에 데이터베이스 이동

기존 데이터베이스를 pool1이라는 풀로 이동합니다.

```sql
ALTER DATABASE db1
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;
```

### <a name="c-add-a-geo-replication-secondary"></a>C. 지역 복제 보조 데이터베이스 추가

로컬 서버에 있는 db1의 `secondaryserver` 서버에서 읽기 가능한 보조 데이터베이스 db1을 만듭니다.

```sql
ALTER DATABASE db1
ADD SECONDARY ON SERVER secondaryserver
WITH ( ALLOW_CONNECTIONS = ALL )
```

### <a name="d-remove-a-geo-replication-secondary"></a>D. 지역 복제 보조 데이터베이스 제거

`secondaryserver` 서버에서 보조 데이터베이스 db1을 제거합니다.

```sql
ALTER DATABASE db1
REMOVE SECONDARY ON SERVER testsecondaryserver
```

### <a name="e-failover-to-a-geo-replication-secondary"></a>E. 지역 복제 보조 데이터베이스로 장애 조치

`secondaryserver` 서버에서 실행될 때 `secondaryserver` 서버에서 보조 데이터베이스 db1을 승격하여 새로운 주 데이터베이스를 만듭니다.

```sql
ALTER DATABASE db1 FAILOVER
```

### <a name="e-force-failover-to-a-geo-replication-secondary-with-data-loss"></a>E. 데이터 손실이 있는 지역 복제 보조 데이터베이스로 강제 장애 조치(failover)

주 서버를 사용할 수 없는 경우 `secondaryserver` 서버에서 실행될 때 `secondaryserver` 서버에서 보조 데이터베이스 db1을 새로운 주 데이터베이스가 되도록 합니다. 이 옵션은 데이터 손실이 발생할 수 있습니다.

```sql
ALTER DATABASE db1 FORCE_FAILOVER_ALLOW_DATA_LOSS
```

### <a name="g-update-a-single-database-to-service-tier-s0-standard-edition-performance-level-0"></a>G. 단일 데이터베이스를 서비스 계층 S0(Standard Edition, 성능 수준 0)으로 업데이트

단일 데이터베이스를 컴퓨팅 크기(서비스 목표)가 S0이고 최대 크기가 250GB인 Standard Edition(서비스 계층)으로 업데이트합니다.

```sql
ALTER DATABASE [db1] MODIFY (EDITION = 'Standard', MAXSIZE = 250 GB, SERVICE_OBJECTIVE = 'S0');
```

### <a name="h-update-the-backup-storage-redundancy-of-a-database"></a>H. 데이터베이스의 백업 스토리지 중복성 업데이트

데이터베이스의 백업 스토리지 중복성을 영역 중복으로 업데이트합니다. 이 데이터베이스의 이후 모든 백업에는 새 설정을 사용합니다. 여기에는 특정 시점 복원 백업 및 장기 보존 백업(구성된 경우)이 포함됩니다. 

```sql
ALTER DATABASE db1 MODIFY BACKUP_STORAGE_REDUNDANCY = 'ZONE'
```

## <a name="see-also"></a>참고 항목

- [CREATE DATABASE - Azure SQL Database](../../t-sql/statements/create-database-transact-sql.md?view=azuresqldb-currentls)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [시스템 데이터베이스](../../relational-databases/databases/system-databases.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current"

:::row:::
    :::column:::
        [SQL Server](alter-database-transact-sql.md?view=sql-server-ver15&preserve-view=true)
    :::column-end:::
    :::column:::
        [SQL 데이터베이스](alter-database-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        **_\* SQL Managed Instance \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-database-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System(PDW)](alter-database-transact-sql.md?view=aps-pdw-2016-au7)
    :::column-end:::
:::row-end:::



&nbsp;

## <a name="overview-azure-sql-managed-instance"></a>개요: Azure SQL Managed Instance

[!INCLUDE[ssSDSMIfull](../../includes/sssdsmifull-md.md)]에서 이 문을 사용하여 데이터베이스 옵션을 설정합니다.

`ALTER DATABASE` 구문은 설명할 항목이 많기 때문에 여러 아티클로 구분하여 설명됩니다.

ALTER DATABASE   
현재 아티클에서는 파일 및 파일 그룹 옵션, 데이터베이스 옵션 및 데이터베이스 호환성 수준을 설정하기 위한 구문과 관련 정보를 제공합니다.  
  
[ALTER DATABASE 파일 및 파일 그룹 옵션](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md?&tabs=sqldbmi)   
데이터베이스의 파일과 파일 그룹을 추가 및 제거하고 파일과 파일 그룹의 특성을 변경하기 위한 구문 및 관련 정보를 제공합니다.  
  
[ALTER DATABASE SET 옵션](../../t-sql/statements/alter-database-transact-sql-set-options.md?&tabs=sqldbmi)   
ALTER DATABASE의 SET 옵션을 사용하여 데이터베이스의 특성을 변경하기 위한 구문 및 관련 정보를 제공합니다.  
  
[ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md?&tabs=sqldbmi)   
데이터베이스 호환성 수준과 관련된 ALTER DATABASE의 SET 옵션에 대한 구문 및 관련 정보를 제공합니다.  

## <a name="syntax"></a>구문

```syntaxsql
-- Azure SQL Database Syntax  
ALTER DATABASE { database_name | CURRENT }  
{
    MODIFY NAME = new_database_name
  | COLLATE collation_name
  | <file_and_filegroup_options>  
  | SET <option_spec> [ ,...n ]  
}  
[;]

<file_and_filegroup_options>::=  
  <add_or_modify_files>::=  
  <filespec>::=
  <add_or_modify_filegroups>::=  
  <filegroup_updatability_option>::=  

<option_spec> ::=
{
    <auto_option>
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
  | <temporal_history_retention>
  | <compatibility_level>
      { 150 | 140 | 130 | 120 | 110 | 100 | 90 }

}  

```

## <a name="arguments"></a>인수

*database_name*   
수정할 데이터베이스의 이름입니다.

CURRENT   
현재 사용 중인 데이터베이스를 변경하도록 지정합니다.

## <a name="remarks"></a>설명

데이터베이스를 제거하려면 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)를 사용합니다.
데이터베이스의 크기를 줄이려면 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)를 사용합니다.

`ALTER DATABASE` 문은 자동 커밋 모드(기본 트랜잭션 관리 모드)에서 실행되어야 하며 명시적 또는 암시적 트랜잭션에서는 허용되지 않습니다.

계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. 계획 캐시의 삭제된 각 캐시스토어에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 "데이터베이스 유지 관리 또는 재구성 작업으로 인해 '%s' 캐시스토어(계획 캐시의 일부)에 대한 캐시스토어 플러시가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 %d번 발견되었습니다"라는 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.

계획 캐시는 기본 옵션이 있는 데이터베이스에 대해 여러 개의 쿼리가 실행될 때에도 플러시됩니다. 그러면 데이터베이스가 삭제됩니다.

## <a name="viewing-database-information"></a>데이터베이스 정보 보기

카탈로그 뷰, 시스템 함수 및 시스템 저장 프로시저를 사용하여 데이터베이스, 파일 및 파일 그룹에 대한 정보를 반환할 수 있습니다.

## <a name="permissions"></a>사용 권한

프로비전 프로세스를 통해 만들어진 서버 수준의 보안 주체 로그인 또는 `dbcreator` 데이터베이스 역할의 구성원만 데이터베이스를 변경할 수 있습니다.

> [!IMPORTANT]
> 데이터베이스의 소유자가 `dbcreator` 역할의 구성원인 경우 데이터베이스를 변경할 수 있습니다.

## <a name="examples"></a>예제

다음 예제에서는 자동 튜닝을 설정하는 방법 및 관리되는 인스턴스에서 파일을 추가하는 방법을 보여줍니다.

```sql
ALTER DATABASE WideWorldImporters
  SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON)

ALTER DATABASE WideWorldImporters
  ADD FILE (NAME = 'data_17')
```

## <a name="see-also"></a>참고 항목

- [CREATE DATABASE - Azure SQL Database](../../t-sql/statements/create-database-transact-sql.md?view=azuresqldb-mi-current)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)[sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [시스템 데이터베이스](../../relational-databases/databases/system-databases.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest"

:::row:::
    :::column:::
        [SQL Server](alter-database-transact-sql.md?view=sql-server-ver15&preserve-view=true)
    :::column-end:::
    :::column:::
        [SQL 데이터베이스](alter-database-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [SQL Managed Instance](alter-database-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        **_\* Azure Synapse<br />Analytics \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System(PDW)](alter-database-transact-sql.md?view=aps-pdw-2016-au7)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="overview-azure-synapse-analytics"></a>개요: Azure Synapse Analytics

Azure Synapse에서 `ALTER DATABASE`는 데이터베이스의 이름, 최대 크기 또는 서비스 목표를 수정합니다.

`ALTER DATABASE` 구문은 설명할 항목이 많기 때문에 여러 아티클로 구분하여 설명됩니다.

[ALTER DATABASE SET 옵션](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
ALTER DATABASE의 SET 옵션을 사용하여 데이터베이스의 특성을 변경하기 위한 구문 및 관련 정보를 제공합니다.

## <a name="syntax"></a>구문

### <a name="dedicated-sql-pool"></a>[전용 SQL 풀](#tab/sqlpool)
```syntaxsql
ALTER DATABASE { database_name | CURRENT }
{
  MODIFY NAME = new_database_name
| MODIFY ( <edition_option> [, ... n] )
| SET <option_spec> [ ,...n ] [ WITH <termination> ]
}
[;]

<edition_option> ::=
      MAXSIZE = {
            250 | 500 | 750 | 1024 | 5120 | 10240 | 20480
          | 30720 | 40960 | 51200 | 61440 | 71680 | 81920
          | 92160 | 102400 | 153600 | 204800 | 245760
      } GB
      | SERVICE_OBJECTIVE = {
            'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500'
          | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000'
          | 'DW3000' | 'DW6000' | 'DW500c' | 'DW1000c' | 'DW1500c'
          | 'DW2000c' | 'DW2500c' | 'DW3000c' | 'DW5000c' | 'DW6000c'
          | 'DW7500c' | 'DW10000c' | 'DW15000c' | 'DW30000c'
      }
```
### <a name="serverless-sql-pool"></a>[서버리스 SQL 풀](#tab/sqlod)
```syntaxsql
ALTER DATABASE { database_name | Current } 
{ 
    COLLATE collation_name 
  | SET { <optionspec> [ ,...n ] } 
} 
[;] 

<optionspec> ::= 
{ 
    <auto_option> 
  | <sql_option> 
}  

<auto_option> ::= 
{ 
    AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] } 
  | AUTO_UPDATE_STATISTICS { ON | OFF } 
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF } 
} 

<sql_option> ::= 
{ 
    ANSI_NULL_DEFAULT { ON | OFF } 
  | ANSI_NULLS { ON | OFF } 
  | ANSI_PADDING { ON | OFF } 
  | ANSI_WARNINGS { ON | OFF } 
  | ARITHABORT { ON | OFF } 
  | COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 } 
  | CONCAT_NULL_YIELDS_NULL { ON | OFF } 
  | NUMERIC_ROUNDABORT { ON | OFF } 
  | QUOTED_IDENTIFIER { ON | OFF } 
} 
```
---

## <a name="arguments"></a>인수

*database_name*   
수정할 데이터베이스의 이름을 지정합니다.

MODIFY NAME = *new_database_name*   
데이터베이스의 이름을 지정된 이름 *new_database_name* 으로 바꿉니다.

MAXSIZE   
기본값은 245,760GB(240TB)입니다.

**적용 대상:** Compute Gen1에 최적화됨

데이터베이스의 최대 허용 크기입니다. 데이터베이스는 MAXSIZE 이상으로 커질 수 없습니다.

**적용 대상:** Compute Gen2에 최적화됨

데이터베이스의 rowstore 데이터에 허용되는 최대 크기입니다. Rowstore 테이블, columnstore 인덱스의 deltastore 또는 클러스터된 columnstore 인덱스의 비클러스터된 인덱스에 저장된 데이터는 MAXSIZE 보다 커질 수 없습니다. columnstore 형식으로 압축된 데이터에는 크기 제한이 없으며 MAXSIZE에 의해 제한되지 않습니다.

SERVICE_OBJECTIVE   
컴퓨팅 크기(서비스 목표)를 지정합니다. Azure Synapse의 서비스 목표에 대한 자세한 내용은 [DWU(데이터 웨어하우스 단위)](/azure/sql-data-warehouse/what-is-a-data-warehouse-unit-dwu-cdwu)를 참조하세요.

## <a name="permissions"></a>사용 권한

다음과 같은 사용 권한이 필요합니다.

- 서버 수준 보안 주체 로그인(프로비전 프로세스에 의해 생성됨) 또는
- `dbmanager` 데이터 베이스 역할의 멤버

데이터베이스의 소유자가 `dbmanager` 역할의 멤버가 아니면 데이터베이스를 변경할 수 있습니다.

## <a name="general-remarks"></a>일반적인 주의 사항

현재 데이터베이스는 변경된 것과 다른 데이터베이스여야 합니다. 따라서 **ALTER는 master 데이터베이스에 연결되어 있는 동안 실행되어야 합니다**.

SQL Analytics의 COMPATIBILITY_LEVEL은 기본적으로 130으로 설정되며 변경할 수 없습니다. 자세한 내용은 [Azure SQL Database의 호환성 수준 130으로 향상된 쿼리 성능](./alter-database-transact-sql-compatibility-level.md)을 참조하세요.

> [!NOTE]
> COMPATIBILITY_LEVEL은 프로비전된 리소스(풀)에만 적용됩니다.

## <a name="limitations-and-restrictions"></a>제한 사항

`ALTER DATABASE`를 실행하려면 데이터베이스가 온라인이어야 하며 일시 중지된 상태일 수 없습니다.

`ALTER DATABASE` 문은 기본 트랜잭션 관리 모드인 자동 커밋 모드에서 실행해야 합니다. 이 항목은 연결 설정에서 설정됩니다.

`ALTER DATABASE` 문은 사용자 정의 트랜잭션에 포함될 수 없습니다.

데이터베이스 데이터 정렬을 변경할 수 없습니다.

## <a name="examples"></a>예제

이러한 예제를 실행하기 전에 변경하는 데이터베이스가 현재 데이터베이스가 아닌지 확인합니다. 현재 데이터베이스는 변경된 것과 다른 데이터베이스여야 합니다. 따라서 **ALTER는 master 데이터베이스에 연결되어 있는 동안 실행되어야 합니다**.

### <a name="a-change-the-name-of-the-database"></a>A. 데이터베이스의 이름을 변경합니다.

```sql
ALTER DATABASE AdventureWorks2012
MODIFY NAME = Northwind;
```

### <a name="b-change-max-size-for-the-database"></a>B. 데이터베이스의 최대 크기를 변경합니다.

```sql
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB );
```

### <a name="c-change-the-compute-size-service-objective"></a>C. 컴퓨팅 크기(서비스 목표)를 변경합니다.

```sql
ALTER DATABASE dw1 MODIFY ( SERVICE_OBJECTIVE= 'DW1200' );
```

### <a name="d-change-the-max-size-and-the-compute-size-service-objective"></a>D. 최대 크기 및 컴퓨팅 크기(서비스 목표)를 변경합니다.

```sql
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB, SERVICE_OBJECTIVE= 'DW1200' );
```

## <a name="see-also"></a>참고 항목

- [CREATE DATABASE(Azure Synapse Analytics)](../../t-sql/statements/create-database-transact-sql.md?view=aps-pdw-2016-au7)
- [Azure Synapse Analytics 참조 문서 목록](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-reference-tsql-language-elements)

::: moniker-end
::: moniker range=">=aps-pdw-2016"

:::row:::
    :::column:::
        [SQL Server](alter-database-transact-sql.md?view=sql-server-ver15&preserve-view=true)
    :::column-end:::
    :::column:::
        [SQL 데이터베이스](alter-database-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [SQL Managed Instance](alter-database-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-database-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        **_\* Analytics<br />Platform System(PDW) \*_** &nbsp;
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="overview-analytics-platform-system"></a>개요: 분석 플랫폼 시스템

복제된 테이블, 분산된 테이블 및 트랜잭션 로그인 PDW에 대한 최대 데이터베이스 크기 옵션을 수정합니다. 이 문을 사용하여 크기의 축소나 확대에 따라 데이터베이스에 대한 디스크 공간 할당을 관리합니다. 이 아티클은 PDW에서 데이터베이스 옵션 설정과 관련된 구문을 설명합니다.

## <a name="syntax"></a>구문

```syntaxsql
-- Analytics Platform System
ALTER DATABASE database_name
    SET ( <set_database_options> | <db_encryption_option> )
[;]

<set_database_options> ::=
{
    AUTOGROW = { ON | OFF }
    | REPLICATED_SIZE = size [GB]
    | DISTRIBUTED_SIZE = size [GB]
    | LOG_SIZE = size [GB]
    | SET AUTO_CREATE_STATISTICS { ON | OFF }
    | SET AUTO_UPDATE_STATISTICS { ON | OFF }
    | SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }
}

<db_encryption_option> ::=
    ENCRYPTION { ON | OFF }
```

## <a name="arguments"></a>인수

*database_name*   
수정할 데이터베이스의 이름입니다. 데이터베이스 목록을 어플라이언스에 표시하려면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)를 사용합니다.

AUTOGROW = { ON | OFF }   
AUTOGROW 옵션을 업데이트합니다. AUTOGROW가 켜진 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]이 스토리지 요구 사항의 증가를 수용할 필요에 따라 복제된 테이블, 분산된 테이블 및 트랜잭션 로그에 대해 할당된 공간을 자동으로 증가시킵니다. AUTOGROW가 꺼진 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 복제된 테이블이나 분산된 테이블 또는 트랜잭션 로그가 최대 크기 설정을 초과한 경우 오류를 반환합니다.

REPLICATED_SIZE = *size* [GB]   
변경되는 데이터베이스에 모든 복제된 테이블을 저장하기 위해 컴퓨팅 노드당 최대 기가바이트를 새로 지정합니다. 어플라이언스 스토리지 공간을 계획하는 경우 어플라이언스에서 REPLICATED_SIZE에 컴퓨팅 노드 수를 곱해야 합니다.

DISTRIBUTED_SIZE = *size* [GB]   
변경되는 데이터베이스에 모든 분산된 테이블을 저장하기 위해 데이터베이스당 최대 기가바이트를 새로 지정합니다. 해당 크기는 어플라이언스의 모든 컴퓨팅 노드에 분산됩니다.

LOG_SIZE = *size* [GB]   
변경되는 데이터베이스에 모든 트랜잭션 로그를 저장하기 위해 데이터베이스당 최대 기가바이트를 새로 지정합니다. 해당 크기는 어플라이언스의 모든 컴퓨팅 노드에 분산됩니다.

ENCRYPTION { ON | OFF }   
데이터베이스를 암호화하거나(ON) 암호화하지 않도록(OFF) 설정합니다. [sp_pdw_database_encryption](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)이 **1** 로 설정된 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 대한 암호화를 구성할 수 있습니다. 투명한 데이터 암호화를 구성하기 전에 데이터베이스 암호화 키를 만들어야 합니다. 데이터 암호화에 대한 자세한 내용은 [TDE(투명한 데이터 암호화)](../../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하세요.

SET AUTO_CREATE_STATISTICS { ON | OFF }   
자동 통계 작성 옵션인 AUTO_CREATE_STATISTICS가 ON으로 설정된 경우 쿼리 최적화 프로그램은 필요에 따라 쿼리 조건자의 개별 열에 대한 통계를 작성하므로 쿼리 계획에 대한 카디널리티 예상치의 정확도가 높아집니다. 이러한 단일 열 통계는 기존 통계 개체에 히스토그램이 없는 열에 대해 작성됩니다.

기본값은 AU7로 업그레이드한 후 생성된 새 데이터베이스에 대해 ON입니다. 기본값은 업그레이드 이전에 생성된 데이터베이스에 대해 OFF입니다.

통계에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md) 참조

SET AUTO_UPDATE_STATISTICS { ON | OFF }   
자동 통계 업데이트 옵션인 AUTO_UPDATE_STATISTICS가 ON으로 설정되면 쿼리 최적화 프로그램은 통계가 최신이 아닌 통계가 되는 시점을 확인한 다음, 쿼리에서 사용될 때 이를 업데이트합니다. 작업 삽입, 업데이트, 삭제 또는 병합을 통해 테이블이나 인덱싱된 뷰의 데이터 분포가 변경되면 통계 내용이 더 이상 최신이 아니게 됩니다. 쿼리 최적화 프로그램은 마지막 통계 업데이트 이후 데이터 수정 개수를 계산한 다음 이 수를 임계값과 비교하여 통계가 최신이 아니게 된 시점을 결정합니다. 임계값은 테이블 또는 인덱싱된 뷰의 행 수를 기준으로 합니다.

기본값은 AU7로 업그레이드한 후 생성된 새 데이터베이스에 대해 ON입니다. 기본값은 업그레이드 이전에 생성된 데이터베이스에 대해 OFF입니다.

통계에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.

SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }   
비동기 통계 업데이트 옵션인 AUTO_UPDATE_STATISTICS_ASYNC는 쿼리 최적화 프로그램이 동기 또는 비동기 통계 업데이트를 사용하는지를 결정합니다. AUTO_UPDATE_STATISTICS_ASYNC 옵션은 인덱스에 대해 작성된 통계 개체, 쿼리 조건자의 단일 열 및 CREATE STATISTICS 문으로 작성된 통계에 적용됩니다.

기본값은 AU7로 업그레이드한 후 생성된 새 데이터베이스에 대해 ON입니다. 기본값은 업그레이드 이전에 생성된 데이터베이스에 대해 OFF입니다.

통계에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.

## <a name="permissions"></a>사용 권한

데이터베이스에 대한 `ALTER` 권한이 필요합니다.

## <a name="error-messages"></a>오류 메시지

자동 통계를 사용하지 않고 통계 설정을 변경하려는 경우 PDW는 `This option is not supported in PDW`라는 오류를 출력합니다. 시스템 관리자는 기능 스위치[AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md)를 사용하여 자동 통계를 사용할 수 있습니다.

## <a name="general-remarks"></a>일반적인 주의 사항

`REPLICATED_SIZE`, `DISTRIBUTED_SIZE` 및 `LOG_SIZE`에 대한 값이 데이터베이스에 대한 현재 값보다 크거나 작거나 같을 수 있습니다.

## <a name="limitations-and-restrictions"></a>제한 사항

확장 및 축소 작업은 근사치입니다. 결과로 생성된 실제 크기는 매개 변수에 따라 다를 수 있습니다.

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 원자 조작으로서 ALTER DATABASE 문을 수행 하지 않습니다. 실행 동안 이 문이 중단되는 경우 이미 발생한 변경 내용은 유지됩니다.

통계 설정은 관리자가 자동 통계를 사용하는 경우에만 작동합니다. 사용자가 관리자인 경우 기능 스위치[AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md)를 사용하여 자동 통계를 사용하거나 사용하지 않도록 설정합니다.

## <a name="locking-behavior"></a>잠금 동작

DATABASE 개체에 대한 공유 잠금을 사용합니다. 읽기 또는 쓰기를 위해 다른 사용자가 사용 중인 데이터베이스는 변경할 수 없습니다. 여기에는 해당 데이터베이스에서 [USE](../language-elements/use-transact-sql.md) 문을 발급한 세션이 포함됩니다.

## <a name="performance"></a>성능

데이터베이스 축소는 해당 데이터베이스 내의 실제 데이터의 크기와 디스크의 조각화 양에 따라 많은 시간 및 시스템 리소스가 필요할 수 있습니다. 예를 들어 데이터베이스를 축소하면 여러 시간 이상이 걸릴 수 있습니다.

## <a name="determining-encryption-progress"></a>암호화 진행률 결정

다음 쿼리를 사용하여 데이터베이스 TDE(투명한 데이터 암호화) 진행률을 백분율로 확인하십시오.

```sql
WITH
database_dek AS (
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id,
        dek.encryption_state, dek.percent_complete,
        dek.key_algorithm, dek.key_length, dek.encryptor_thumbprint,
        type
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek
    INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map
        ON dek.database_id = node_db_map.database_id
        AND dek.pdw_node_id = node_db_map.pdw_node_id
    LEFT JOIN sys.pdw_database_mappings AS db_map
        ON node_db_map .physical_name = db_map.physical_name
    INNER JOIN sys.dm_pdw_nodes nodes
        ON nodes.pdw_node_id = dek.pdw_node_id
    WHERE dek.encryptor_thumbprint <> 0x
),
dek_percent_complete AS (
    SELECT database_dek.database_id, AVG(database_dek.percent_complete) AS percent_complete
    FROM database_dek
    WHERE type = 'COMPUTE'
    GROUP BY database_dek.database_id
)
SELECT DB_NAME( database_dek.database_id ) AS name,
    database_dek.database_id,
    ISNULL(
       (SELECT TOP 1 dek_encryption_state.encryption_state
        FROM database_dek AS dek_encryption_state
        WHERE dek_encryption_state.database_id = database_dek.database_id
        ORDER BY (CASE encryption_state
            WHEN 3 THEN -1
            ELSE encryption_state
            END) DESC), 0)
        AS encryption_state,
dek_percent_complete.percent_complete,
database_dek.key_algorithm, database_dek.key_length, database_dek.encryptor_thumbprint
FROM database_dek
INNER JOIN dek_percent_complete
    ON dek_percent_complete.database_id = database_dek.database_id
WHERE type = 'CONTROL';
```

TDE를 구현하는 모든 단계를 보여주는 포괄적인 예제는 [TDE(투명한 데이터 암호화)](../../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하세요.

## <a name="examples-sspdw"></a>예제: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

### <a name="a-altering-the-autogrow-setting"></a>A. AUTOGROW 설정 변경

데이터베이스에 대해 AUTOGROW를 ON으로 설정합니다 `CustomerSales`.

```sql
ALTER DATABASE CustomerSales
    SET ( AUTOGROW = ON );
```

### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. 복제된 테이블에 대해 최대 스토리지 변경

다음 예제에서는 데이터베이스 `CustomerSales`에 대해 복제된 테이블 스토리지 용량 한도를 1GB로 설정. 컴퓨팅 노드당 스토리지 용량 한도입니다.

```sql
ALTER DATABASE CustomerSales
    SET ( REPLICATED_SIZE = 1 GB );
```

### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. 분산된 테이블에 대해 최대 스토리지 변경

 다음 예제에서는 데이터베이스 `CustomerSales`에 대해 분산된 테이블 스토리지 용량 한도를 1000GB(1테라바이트)로 설정합니다. 컴퓨팅 노드당 스토리지 용량 한도가 아닌 모든 컴퓨팅 노드에 대해 어플라이언스에서 결합된 스토리지 용량 한도입니다.

```sql
ALTER DATABASE CustomerSales
    SET ( DISTRIBUTED_SIZE = 1000 GB );
```

### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. 트랜잭션 로그에 대해 최대 스토리지 변경

 다음 예제에서는 어플라이언스에 대해 10GB의 트랜잭션 로그 크기가 최대값[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 갖도록 데이터베이스 `CustomerSales`를 업데이트합니다.

```sql
ALTER DATABASE CustomerSales
    SET ( LOG_SIZE = 10 GB );
```

### <a name="e-check-for-current-statistics-values"></a>E. 현재 통계 값에 대한 확인

다음 쿼리는 모든 데이터베이스에 대해 현재 통계 값을 반환합니다. 값이 1이면 기능이 켜져있고 0이면 기능이 꺼져있다는 의미입니다.

```sql
SELECT NAME,
    is_auto_create_stats_on,
    is_auto_update_stats_on,
    is_auto_update_stats_async_on
FROM sys.databases;
```

### <a name="f-enable-auto-create-and-auto-update-stats-for-a-database"></a>F. 데이터베이스에 대한 통계 자동 작성 및 자동 업데이트 사용

다음 명령문을 사용하여 CustomerSales 데이터베이스에 대한 통계를 자동 및 비동기적으로 만들고 업데이트할 수 있습니다. 이렇게 하면 고품질의 쿼리 계획을 만들기 위한 필요에 따라 단일 열 통계를 만들고 업데이트합니다.

```sql
ALTER DATABASE CustomerSales
    SET AUTO_CREATE_STATISTICS ON;
ALTER DATABASE CustomerSales
    SET AUTO_UPDATE_STATISTICS ON;
ALTER DATABASE
    SET AUTO_UPDATE_STATISTICS_ASYNC ON;
```

## <a name="see-also"></a>참고 항목

- [CREATE DATABASE - Analytics Platform System](../../t-sql/statements/create-database-transact-sql.md?view=aps-pdw-2016-au7)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)

::: moniker-end
