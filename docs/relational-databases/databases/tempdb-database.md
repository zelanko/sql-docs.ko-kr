---
title: tempdb 데이터베이스 | Microsoft Docs
description: 이 항목에서는 SQL Server 및 Azure SQL Database의 구성과 사용에 관한 세부 정보를 제공합니다.
ms.custom: P360
ms.date: 09/16/2020
ms.prod: sql
ms.prod_service: database-engine
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c49e89d9ed81950d0c8781d39c57eef3e408482b
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195561"
---
# <a name="tempdb-database"></a>tempdb 데이터베이스

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

`tempdb` 시스템 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스 또는 Azure SQL Database에 연결된 모든 사용자가 사용할 수 있는 전역 리소스입니다. `tempdb`에 보관되는 내용은 다음과 같습니다.  
  
- 명시적으로 생성되는 임시 사용자 개체. 여기에는 전역 또는 로컬 임시 테이블과 인덱스, 임시 저장 프로시저, 테이블 변수, 테이블 반환 함수에서 반환된 테이블, 커서 등이 포함됩니다.  
- 데이터베이스 엔진에서 만든 내부 개체 다음과 같은 변경 내용이 해당됩니다.
  - 스풀, 커서, 정렬 및 임시 LOB(Large Object) 스토리지에 대한 중간 결과를 저장할 작업 테이블
  - 해시 조인 또는 해시 집계 작업에 대한 작업 파일
  - 인덱스 생성 또는 다시 작성(`SORT_IN_TEMPDB`가 지정된 경우), 특정 `GROUP BY`, `ORDER BY`, `UNION` 쿼리 같은 작업의 중간 정렬 결과

  각 내부 개체는 IAM 페이지와 8페이지 익스텐트를 포함하여 최소 9페이지를 사용합니다. 페이지 및 익스텐트에 대한 자세한 내용은 [페이지 및 익스텐트](../../relational-databases/pages-and-extents-architecture-guide.md#pages-and-extents)를 참조하세요.

  > [!IMPORTANT]
  > Azure SQL Database 단일 데이터베이스 및 탄력적 풀은 `tempdb`에 저장되고 데이터베이스 수준을 범위로 하는 전역 임시 테이블 및 전역 임시 저장 프로시저를 지원합니다. 
  >
  > 글로벌 임시 테이블 및 글로벌 임시 저장 프로시저는 동일한 SQL 데이터베이스 내의 모든 사용자 세션에 대해 공유됩니다. 다른 SQL 데이터베이스의 사용자 세션은 전역 임시 테이블에 액세스할 수 없습니다. 자세한 내용은 [데이터베이스 범위 전역 임시 테이블(Azure SQL Database)](../../t-sql/statements/create-table-transact-sql.md#database-scoped-global-temporary-tables-azure-sql-database)을 참조하세요. [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)는 SQL Server에서 지원하는 것과 동일한 임시 개체를 지원합니다.
  >
  > Azure SQL Database 단일 데이터베이스와 탄력적 풀의 경우 master 데이터베이스 및 `tempdb` 데이터베이스만 적용됩니다. 자세한 내용은 [Azure SQL Database 서버란?](/azure/sql-database/sql-database-servers-databases#what-is-an-azure-sql-database-server)을 참조하세요. Azure SQL Database 단일 데이터베이스와 탄력적 풀의 컨텍스트에서 `tempdb`의 설명은 [Azure SQL Database 단일 데이터베이스와 탄력적 풀의 tempdb 데이터베이스](#tempdb-database-in-sql-database)를 참조하세요. 
  >
  > Azure SQL Managed Instance의 경우 모든 시스템 데이터베이스가 적용됩니다.

- 버전 저장소는 행 버전 관리 기능을 지원하는 데이터 행이 보관된 데이터 페이지 모음입니다. 일반 버전 저장소와 온라인 인덱스 작성 버전 저장소의 두 가지 유형이 있습니다. 버전 저장소에는 다음 정보가 포함됩니다.
  - 행 버전 관리 격리 또는 스냅샷 격리 트랜잭션을 통해 `READ COMMITTED`를 사용하는 데이터베이스의 데이터 수정 트랜잭션에서 생성된 행 버전  
  - 온라인 인덱스 작업, MARS(Multiple Active Result Sets) 및 `AFTER` 트리거 같은 기능에 대한 데이터 수정 트랜잭션에서 생성된 행 버전  
  
트랜잭션을 롤백할 수 있도록 `tempdb` 내의 작업은 최소한으로 로깅됩니다. 시스템이 항상 깨끗한 데이터베이스 복사본으로 시작되도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 시작할 때마다 `tempdb`가 다시 생성됩니다. 연결이 끊길 때 임시 테이블 및 저장 프로시저는 자동으로 제거되고 시스템이 종료될 때 활성 상태인 연결이 없습니다. 

`tempdb`에 있는 어떠한 내용도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 한 세션에서 다른 세션으로 저장되지 않습니다. `tempdb`에서는 백업 및 복원 작업이 허용되지 않습니다.  

## <a name="physical-properties-of-tempdb-in-sql-server"></a>SQL Server에서 tempdb의 물리적 속성

다음 표에는 SQL Server의 `tempdb` 데이터 및 로그 파일의 초기 구성 값이 나열되어 있습니다. 값은 `model` 데이터베이스의 기본값을 기준으로 합니다. 이러한 파일의 크기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 따라 조금씩 다를 수 있습니다.  
  
|파일|논리적 이름|물리적 이름|처음 크기|파일 증가|  
|----------|------------------|-------------------|------------------|-----------------|  
|주 데이터|tempdev|tempdb.mdf|8MB|디스크가 꽉 찰 때까지 64MB씩 자동 증가|  
|보조 데이터 파일|temp#|tempdb_mssql_#.ndf|8MB|디스크가 꽉 찰 때까지 64MB씩 자동 증가|  
|로그|templog|templog.ldf|8MB|최대 2TB까지 64MB씩 자동 증가|  
  
보조 데이터 파일의 수는 컴퓨터의 논리 프로세서 수에 따라 달라집니다. 일반적으로 논리 프로세서의 수가 8 이하인 경우 논리 프로세서와 같은 수의 데이터 파일을 사용합니다. 논리 프로세서 수가 8보다 크면 8개의 데이터 파일을 사용합니다. 그런 다음에도 경합이 계속될 경우 경합이 허용 가능한 수준으로 감소할 때까지 데이터 파일의 수를 4의 배수로 늘리거나 작업/코드를 변경합니다.

> [!NOTE]
> 데이터 파일 수의 기본값은 [KB 2154845](https://support.microsoft.com/kb/2154845/)의 일반 지침을 기준으로 합니다.  
  
### <a name="moving-the-tempdb-data-and-log-files-in-sql-server"></a>SQL Server에서 tempdb 데이터 및 로그 파일 이동

`tempdb` 데이터 및 로그 파일을 이동하려면 [시스템 데이터베이스 이동](../../relational-databases/databases/move-system-databases.md)을 참조하세요.  
  
### <a name="database-options-for-tempdb-in-sql-server"></a>SQL Server에서 tempdb에 대한 데이터베이스 옵션

다음 표에서는 `tempdb` 데이터베이스의 각 데이터베이스 옵션에 대한 기본값과 수정 가능 여부를 나열합니다. 이러한 옵션의 현재 설정을 보려면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰를 사용하세요.  
  
|데이터베이스 옵션|기본값|수정 가능|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|예|  
|ANSI_NULL_DEFAULT|OFF|예|  
|ANSI_NULLS|OFF|예|  
|ANSI_PADDING|OFF|예|  
|ANSI_WARNINGS|OFF|예|  
|ARITHABORT|OFF|예|  
|AUTO_CLOSE|OFF|예|  
|AUTO_CREATE_STATISTICS|켜기|예|  
|AUTO_SHRINK|OFF|예|  
|AUTO_UPDATE_STATISTICS|켜기|예|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|예|  
|CHANGE_TRACKING|OFF|예|  
|CONCAT_NULL_YIELDS_NULL|OFF|예|  
|CURSOR_CLOSE_ON_COMMIT|OFF|예|  
|CURSOR_DEFAULT|GLOBAL|예|  
|데이터베이스 가용성 옵션|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|예<br /><br /> 예<br /><br /> 예|  
|DATE_CORRELATION_OPTIMIZATION|OFF|예|  
|DB_CHAINING|켜기|예|  
|ENCRYPTION|OFF|예|  
|MIXED_PAGE_ALLOCATION|OFF|예|  
|NUMERIC_ROUNDABORT|OFF|예|  
|PAGE_VERIFY|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 새 설치의 경우 CHECKSUM입니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업그레이드의 경우 NONE입니다.|예|  
|PARAMETERIZATION|SIMPLE|예|  
|QUOTED_IDENTIFIER|OFF|예|  
|READ_COMMITTED_SNAPSHOT|OFF|예|  
|RECOVERY|SIMPLE|예|  
|RECURSIVE_TRIGGERS|OFF|예|  
|Service Broker 옵션|ENABLE_BROKER|예|  
|TRUSTWORTHY|OFF|예|  
  
이러한 데이터베이스 옵션에 대한 자세한 내용은 [ALTER DATABASE SET 옵션(Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.  
  
## <a name="tempdb-database-in-sql-database"></a>SQL Database의 tempdb 데이터베이스

### <a name="tempdb-sizes-for-dtu-based-service-tiers"></a>DTU 기반 서비스 계층에 대한 tempdb 크기

<!-- tempdb being larger for Basic and 50 eDTU pools than for 100-400 eDTU pools reflects actual config (historical reasons) --> 

|서비스 수준 목표|`tempdb` 데이터 파일 최대 크기(GB)|`tempdb` 데이터 파일 수|`tempdb` 데이터 최대 크기(GB)|
|---|---:|---:|---:|
|Basic|13.9|1|13.9|
|S0|13.9|1|13.9|
|S1|13.9|1|13.9|
|S2|13.9|1|13.9|
|S3|32|1|32
|S4|32|2|64|
|S6|32|3|96|
|S7|32|6|192|
|S9|32|12|384|
|S12|32|12|384|
|P1|13.9|12|166.7|
|P2|13.9|12|166.7|
|P4|13.9|12|166.7|
|P6|13.9|12|166.7|
|P11|13.9|12|166.7|
|P15|13.9|12|166.7|
|기본 탄력적 풀(모든 DTU 구성)|13.9|12|166.7|
|표준 탄력적 풀(50 eDTU)|13.9|12|166.7|
|표준 탄력적 풀(100 eDTU)|32|1|32|
|표준 탄력적 풀(200 eDTU)|32|2|64|
|표준 탄력적 풀(300 eDTU)|32|3|96|
|표준 탄력적 풀(400 eDTU)|32|3|96|
|표준 탄력적 풀(800 eDTU)|32|6|192|
|표준 탄력적 풀(1200 eDTU)|32|10|320|
|표준 탄력적 풀(1600-3000 eDTU)|32|12|384|
|프리미엄 탄력적 풀(모든 DTU 구성)|13.9|12|166.7|
||||

### <a name="tempdb-sizes-for-vcore-based-service-tiers"></a>vCore 기반 서비스 계층에 대한 tempdb 크기

[vCore 기반 리소스 제한](/azure/sql-database/sql-database-vcore-resource-limits) 참조

## <a name="restrictions"></a>제한 사항

`tempdb` 데이터베이스에서는 다음 작업을 수행할 수 없습니다.  
  
- 파일 그룹 추가
- 데이터베이스 백업 또는 복원
- 데이터 정렬 변경. 기본 데이터 정렬은 서버 데이터 정렬입니다.
- 데이터베이스 소유자 변경. `tempdb`는 *sa*가 소유합니다.
- 데이터베이스 스냅샷 만들기
- 데이터베이스 삭제
- 데이터베이스에서 *guest* 사용자 삭제
- 변경 데이터 캡처 사용
- 데이터베이스 미러링 참여
- 주 파일 그룹, 주 데이터 파일 또는 로그 파일 제거
- 데이터베이스 또는 주 파일 그룹 이름 바꾸기
- `DBCC CHECKALLOC`을 실행하고 있습니다.
- `DBCC CHECKCATALOG`를 실행하고 있습니다.
- 데이터베이스를 `OFFLINE`으로 설정합니다.
- 데이터베이스 또는 주 파일 그룹 이름을 `READ_ONLY`로 바꿉니다.
  
## <a name="permissions"></a>사용 권한

모든 사용자가 `tempdb`에 임시 개체를 만들 수 있습니다. 사용자가 추가 사용 권한을 받는 경우를 제외하고 자신의 고유 개체에만 액세스할 수 있습니다. `tempdb`에 대한 연결 권한을 철회하여 사용자가 `tempdb`를 사용하지 못하게 할 수 있습니다. 일부 루틴 작업은 `tempdb`를 사용해야 하기 때문에 권장하지 않습니다.  

## <a name="optimizing-tempdb-performance-in-sql-server"></a>SQL Server에서 tempdb 성능 최적화
`tempdb` 데이터베이스의 크기와 물리적인 배치는 시스템 성능에 영향을 줄 수 있습니다. 예를 들어 `tempdb`에 대해 정의된 크기가 너무 작으면 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작할 때마다 시스템의 처리 로드 중 일부가 작업을 지원하는 데 필요한 크기로 `tempdb`를 자동 증가시키기 위해 소모될 수 있습니다.

가능하면 데이터 파일 증가 작업의 성능을 향상시키기 위해 [인스턴트 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)를 사용하세요.

환경의 일반적인 작업량을 수용할 수 있는 값으로 파일 크기를 설정하여 모든 `tempdb` 파일에 충분한 공간을 미리 할당합니다. 미리 할당하면 `tempdb`가 너무 자주 확장되어 성능에 영향을 주는 것을 방지할 수 있습니다. `tempdb` 데이터베이스는 예기치 않은 예외 발생 시 디스크 공간을 늘리기 위해 자동 증가하도록 설정해야 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 여유 공간이 더 많은 파일에 할당을 선호하는 비례 채우기 알고리즘을 사용하기 때문에 데이터 파일은 각 [파일 그룹](../../relational-databases/databases/database-files-and-filegroups.md#filegroups) 내에서 동일한 크기여야 합니다. `tempdb`를 동일한 크기의 여러 데이터 파일로 나누면 `tempdb`를 사용하는 작업에서 높은 수준의 병렬 효율성을 얻을 수 있습니다.

파일 증가분을 적정 크기로 설정하여 `tempdb` 데이터베이스 파일 증가 단위가 너무 작지 않게 합니다. `tempdb`에 기록되는 데이터 양에 비해 파일 증가 단위가 너무 작으면 `tempdb`가 지속적으로 확장되어 성능에 영향을 줍니다.

현재 `tempdb` 크기 및 성장 매개 변수를 확인하려면 다음 쿼리를 사용합니다.

```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeInMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
        ELSE 'Log file grows to a maximum size of 2 TB.'
    END,
    growth AS 'GrowthValue',
    'GrowthIncrement' =
        CASE
            WHEN growth = 0 THEN 'Size is fixed.'
            WHEN growth > 0 AND is_percent_growth = 0
                THEN 'Growth value is in 8-KB pages.'
            ELSE 'Growth value is a percentage.'
        END
FROM tempdb.sys.database_files;
GO
```

`tempdb` 데이터베이스를 고속 I/O 하위 시스템에 배치합니다. 직접 연결되어 있는 디스크가 많으면 디스크 스트라이프를 사용합니다. `tempdb` 데이터 파일의 개별 또는 그룹은 I/O 병목 상태가 발생하지 않는 한, 다른 디스크나 스핀들에 있을 필요가 없습니다.

사용자 데이터베이스에 사용되는 디스크와는 다른 디스크에 `tempdb` 데이터베이스를 배치합니다.

## <a name="performance-improvements-in-tempdb-for-sql-server"></a>SQL Server tempdb의 성능 향상
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터, `tempdb` 성능은 다음과 같은 방법으로 더욱 최적화되었습니다.  
  
- 임시 테이블과 테이블 변수가 캐시됩니다. 캐싱을 사용하면 임시 개체를 삭제하고 만드는 작업이 매우 신속하게 실행됩니다. 캐싱은 페이지 할당과 메타데이터 경합을 줄입니다.  
- 사용되는 `UP`(업데이트) 래치 수가 감소하도록 할당 페이지 래치 프로토콜이 개선되었습니다.  
- `tempdb` 로그 파일의 디스크 I/O 대역폭 사용량을 줄일 수 있도록 `tempdb`의 로깅 오버헤드가 감소했습니다.  
- 설치 시에는 새 인스턴스를 설치하는 동안 `tempdb` 데이터 파일이 여러 개 추가됩니다. **데이터베이스 엔진 구성** 섹션의 새 UI 입력 컨트롤과 명령줄 매개 변수 `/SQLTEMPDBFILECOUNT`를 사용하여 이 작업을 수행할 수 있습니다. 설치 시에는 기본적으로 논리 프로세서 수나 8 중에서 더 적은 숫자에 해당하는 만큼의 `tempdb` 데이터 파일이 추가됩니다.  
- `tempdb` 데이터 파일이 여러 개이면 모든 파일은 증가 설정에 따라 동시에 같은 크기만큼 증가합니다. [추적 플래그 1117](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)이 더 이상 필요하지 않습니다.  
- `tempdb`의 모든 할당에는 단일 범위가 사용됩니다. [추적 플래그 1118](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)은 더 이상 필요하지 않습니다.  
- 주 파일 그룹의 경우 `AUTOGROW_ALL_FILES` 속성이 설정되며 수정할 수 없습니다.

`tempdb`의 성능 개선에 대한 자세한 내용은 블로그 게시물 [TEMPDB - Files and Trace Flags and Updates, Oh My!](/archive/blogs/sql_server_team/tempdb-files-and-trace-flags-and-updates-oh-my)를 참조하세요.

## <a name="memory-optimized-tempdb-metadata"></a>메모리 최적화 tempdb 메타데이터
`tempdb`의 메타데이터 경합으로 인해 기존에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행하는 많은 워크로드의 확장성에 병목 상태가 발생했습니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에는 [메모리 내 데이터베이스](../in-memory-database.md) 기능 제품군에 속하는 새로운 기능인 메모리 액세스에 최적화된 tempdb 메타데이터가 도입되었습니다. 

이 기능은 이러한 병목 현상을 효과적으로 제거하고 tempdb가 많은 워크로드에 대해 새로운 수준의 확장성을 발휘할 수 있도록 합니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에서 임시 테이블 메타데이터 관리에 필요한 시스템 테이블은 래치가 없는 비내구성 메모리 최적화 테이블로 이동할 수 있습니다.

메모리 최적화 tempdb 메타데이터를 사용하는 방법과 시기에 대한 개요는 7분 분량의 다음 동영상을 시청하세요.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/How-and-When-To-Memory-Optimized-TempDB-Metadata/player?WT.mc_id=dataexposed-c9-niner]


### <a name="configuring-and-using-memory-optimized-tempdb-metadata"></a>메모리 최적화 tempdb 메타데이터 구성 및 사용

해당 새 기능으로 옵트인하려면 다음 스크립트를 사용합니다.

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON;
```

이 구성 변경이 적용되려면 서비스를 다시 시작해야 합니다.

다음 T-SQL 명령을 사용하여 `tempdb`가 메모리 최적화인지 여부를 확인할 수 있습니다.

```sql
SELECT SERVERPROPERTY('IsTempdbMetadataMemoryOptimized');
```

메모리 최적화 `tempdb` 메타데이터를 사용하도록 설정한 후 어떤 이유로든 서버를 시작할 수 없는 경우, **-f** 시작 옵션을 통해 [minimal 구성](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md)으로 SQL Server 인스턴스를 시작하여 기능을 무시할 수 있습니다. 이후 기능을 사용하지 않도록 설정한 다음 표준 모드로 SQL Server를 다시 시작할 수 있습니다.

서버 메모리 부족을 방지하기 위해 `tempdb`를 [리소스 풀](../in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)에 바인딩할 수 있습니다. 이 작업은 리소스 풀을 데이터베이스에 바인딩하기 위해 일반적으로 수행하는 단계가 아니라 [`ALTER SERVER`](../../t-sql/statements/alter-server-configuration-transact-sql.md) 명령을 통해 수행됩니다.

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON (RESOURCE_POOL = 'pool_name');
```

메모리 최적화 tempdb 메타데이터를 이미 사용하도록 설정한 경우에도 이 변경을 적용하려면 다시 시작해야 합니다.

### <a name="memory-optimized-tempdb-limitations"></a>메모리 최적화 tempdb 제한 사항

- 기능 설정 및 해제가 동적으로 이루어지지 않습니다. `tempdb`의 구조를 변경해야 하는 고유한 사항 때문에 이 기능을 설정하거나 해제하려면 다시 시작해야 합니다.

- 단일 트랜잭션이 둘 이상의 데이터베이스에서는 메모리 최적화 테이블에 액세스할 수 없습니다. 사용자 데이터베이스에 메모리 최적화 테이블을 포함하는 트랜잭션은 동일한 트랜잭션에서 `tempdb` 시스템 보기에 액세스할 수 없습니다. 사용자 데이터베이스의 메모리 최적화 테이블과 동일한 트랜잭션에서 `tempdb` 시스템 보기에 액세스를 시도하면 다음과 같은 오류가 발생합니다.
    
  ```
  A user transaction that accesses memory optimized tables or natively compiled modules cannot access more than one user database or databases model and msdb, and it cannot write to master.
  ```
    
  예:
    
  ```sql
  BEGIN TRAN;
  
  SELECT *
  FROM tempdb.sys.tables;  -----> Creates a user in-memory OLTP transaction in tempdb
  
  INSERT INTO <user database>.<schema>.<mem-optimized table>
  VALUES (1); ----> Tries to create a user in-memory OLTP transaction in the user database but will fail
  
  COMMIT TRAN;
  ```
    
- 메모리 최적화 테이블에 대한 쿼리가 잠금 및 분리 힌트를 지원하지 않으므로, 메모리 최적화 `tempdb` 카탈로그 보기에 대한 쿼리는 잠금 및 분리 힌트를 유지하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 시스템 카탈로그 보기와 마찬가지로 시스템 보기에 대한 모든 트랜잭션은 `READ COMMITTED`(또는 이 경우 `READ COMMITTED SNAPSHOT`) 분리 내에 있습니다.

- 메모리 최적화 `tempdb` 메타데이터가 사용하도록 설정된 경우에는 임시 테이블에 [columnstore 인덱스](../indexes/columnstore-indexes-overview.md)를 만들 수 없습니다.

- columnstore 인덱스에 대한 제한으로 인해, 메모리 최적화 `tempdb` 메타데이터가 사용하도록 설정된 경우 `COLUMNSTORE` 또는 `COLUMNSTORE_ARCHIVE` 데이터 압축 매개 변수와 함께 `sp_estimate_data_compression_savings` 시스템 저장 프로시저를 사용할 수 없습니다.

> [!NOTE] 
> 이러한 제한 사항은 `tempdb` 시스템 보기를 참조하는 경우에만 적용됩니다. 원하는 경우 사용자 데이터베이스에서 메모리 최적화 테이블에 액세스할 때와 동일한 트랜잭션에서 임시 테이블을 만들 수 있습니다.

## <a name="capacity-planning-for-tempdb-in-sql-server"></a>SQL Server의 tempdb 용량 계획
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로덕션 환경에서 `tempdb`의 적절한 크기는 많은 요인에 따라 결정됩니다. 앞서 설명한 것처럼 기존 작업, 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 등이 이러한 요인에 포함됩니다. SQL Server 테스트 환경에서 다음 태스크를 수행하여 기존 작업을 분석하는 것이 좋습니다.

- `tempdb`에 대해 자동 증가를 설정합니다.
- 개별 쿼리 또는 워크로드 추적 파일을 실행하고 `tempdb` 공간 사용을 모니터링합니다.
- 인덱스 다시 작성 및 `tempdb` 공간 모니터링 같은 인덱스 유지 관리 작업을 실행합니다.
- 이전 단계의 공간 사용 값을 사용하여 총 워크로드 사용량을 예측합니다. 예상되는 동시 작업에 맞춰 이 값을 조정한 다음 `tempdb` 크기를 적절하게 설정합니다.

## <a name="monitoring-tempdb-use"></a>tempdb 사용 모니터링
`tempdb`의 디스크 공간이 부족하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로덕션 환경에서 심각한 중단이 발생할 수 있습니다. 또한 실행 중인 애플리케이션에서 작업을 완료하지 못할 수도 있습니다. [sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) 동적 관리 뷰를 사용하여 `tempdb` 파일에서 사용되는 디스크 공간을 모니터링할 수 있습니다.

```sql
 -- Determining the amount of free space in tempdb
SELECT SUM(unallocated_extent_page_count) AS [free pages],
  (SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the amount of space used by the version store
SELECT SUM(version_store_reserved_page_count) AS [version store pages used],
  (SUM(version_store_reserved_page_count)*1.0/128) AS [version store space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the amount of space used by internal objects
SELECT SUM(internal_object_reserved_page_count) AS [internal object pages used],
  (SUM(internal_object_reserved_page_count)*1.0/128) AS [internal object space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the amount of space used by user objects
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],
  (SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]
FROM sys.dm_db_file_space_usage;
 ```

[sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) 및 [sys.dm_db_task_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md) 동적 관리 뷰를 사용하면 세션이나 태스크 수준에서 `tempdb`의 페이지 할당 또는 할당 해제 작업을 모니터링할 수 있습니다. 이러한 보기를 사용하면 `tempdb` 디스크 공간을 많이 사용하는 큰 쿼리, 임시 테이블 또는 테이블 변수를 식별할 수 있습니다. 또한 여러 가지 카운터를 사용하여 `tempdb`에서 사용 가능한 여유 공간과 `tempdb`를 사용 중인 리소스를 모니터링할 수도 있습니다.

```sql
-- Obtaining the space consumed by internal objects in all currently running tasks in each session
SELECT session_id,
  SUM(internal_objects_alloc_page_count) AS task_internal_objects_alloc_page_count,
  SUM(internal_objects_dealloc_page_count) AS task_internal_objects_dealloc_page_count
FROM sys.dm_db_task_space_usage
GROUP BY session_id;

-- Obtaining the space consumed by internal objects in the current session for both running and completed tasks
SELECT R2.session_id,
  R1.internal_objects_alloc_page_count
  + SUM(R2.internal_objects_alloc_page_count) AS session_internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count
  + SUM(R2.internal_objects_dealloc_page_count) AS session_internal_objects_dealloc_page_count
FROM sys.dm_db_session_space_usage AS R1
INNER JOIN sys.dm_db_task_space_usage AS R2 ON R1.session_id = R2.session_id
GROUP BY R2.session_id, R1.internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count;;
```

## <a name="related-content"></a>관련 콘텐츠
[인덱스에 대한 SORT_IN_TEMPDB 옵션](../../relational-databases/indexes/sort-in-TempDB-option-for-indexes.md)    
[시스템 데이터베이스](../../relational-databases/databases/system-databases.md)    
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)    
[sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)    
[데이터베이스 파일 이동](../../relational-databases/databases/move-database-files.md)    
