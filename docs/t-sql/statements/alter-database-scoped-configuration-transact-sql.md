---
title: ALTER DATABASE SCOPED CONFIGURATION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- ALTER_DATABASE_SCOPED_CONFIGURATION
- ALTER_DATABASE_SCOPED_CONFIGURATION_TSQL
- DATABASE_SCOPED_CONFIGURATION_TSQL
- SCOPED_CONFIGURATION_TSQL
- SCOPED_TSQL
- ALTER_DATABASE_SCOPED_TSQL
- DATABASE_SCOPED_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CONFIGURATION statement
- configuration [SQL Server], ALTER DATABASE SCOPED CONFIGURATION statement
ms.assetid: 63373c2f-9a0b-431b-b9d2-6fa35641571a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cdd652c18af72c73566afac978c4dc00e2867a8a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065855"
---
# <a name="alter-database-scoped-configuration-transact-sql"></a>ALTER DATABASE SCOPED CONFIGURATION(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

이 명령문은 **개별 데이터베이스** 수준에서 다양한 데이터베이스 구성 설정을 활성화합니다. 이 명령문은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 수 있습니다. 해당 설정은 다음과 같습니다.

- 프로시저 캐시를 지웁니다.
- 주 데이터베이스의 경우 MAXDOP 매개 변수를 해당 데이터베이스에 가장 적합한 임의 값(1,2, ...)으로 설정하고 사용되는 보조 데이터베이스(예: 보고 쿼리용)에는 다른 값(예: 0)을 설정합니다.
- 데이터베이스와 관계없이 쿼리 최적화 프로그램 카디널리티 추정 모델을 호환성 수준으로 설정합니다.
- 데이터베이스 수준에서 매개 변수 스니핑을 사용하거나 사용하지 않도록 설정합니다.
- 데이터베이스 수준에서 쿼리 최적화 프로그램 핫픽스를 사용하거나 사용하지 않도록 설정합니다.
- 데이터베이스 수준에서 ID 캐시를 사용하거나 사용하지 않도록 설정합니다.
- 일괄 처리가 처음으로 컴파일될 때 캐시에 저장될 컴파일된 계획 스텁을 사용하거나 사용하지 않도록 설정합니다.
- 고유하게 컴파일된 T-SQL 모듈에 대한 실행 통계의 수집을 활성화하거나 비활성화합니다.
- `ONLINE =` 구문을 지원하는 DDL 문에 기본적으로 온라인 옵션을 활성화 또는 비활성화합니다.
- `RESUMABLE =` 구문을 지원하는 DDL 문에 기본적으로 다시 시작 가능 옵션을 활성화 또는 비활성화합니다.
- 글로벌 임시 테이블의 자동 삭제 기능을 활성화하거나 비활성화합니다.
- [지능형 쿼리 처리](../../relational-databases/performance/intelligent-query-processing.md) 기능을 활성화하거나 비활성화합니다.
- [간단한 쿼리 프로파일링 인프라](../../relational-databases/performance/query-profiling-infrastructure.md)를 활성화하거나 비활성화합니다.
- 새 `String or binary data would be truncated` 오류 메시지를 활성화하거나 비활성화합니다.
- [sys.dm_exec_query_plan_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md)에서 마지막 실제 실행 계획의 수집을 활성화하거나 비활성화합니다.

![링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```
ALTER DATABASE SCOPED CONFIGURATION
{
     {  [ FOR SECONDARY] SET <set_options>}
}
| CLEAR PROCEDURE_CACHE  [plan_handle]
| SET < set_options >
[;]

< set_options > ::=
{
    MAXDOP = { <value> | PRIMARY}
    | LEGACY_CARDINALITY_ESTIMATION = { ON | OFF | PRIMARY}
    | PARAMETER_SNIFFING = { ON | OFF | PRIMARY}
    | QUERY_OPTIMIZER_HOTFIXES = { ON | OFF | PRIMARY}
    | IDENTITY_CACHE = { ON | OFF }
    | INTERLEAVED_EXECUTION_TVF = { ON | OFF }
    | BATCH_MODE_MEMORY_GRANT_FEEDBACK = { ON | OFF }
    | BATCH_MODE_ADAPTIVE_JOINS = { ON | OFF }
    | TSQL_SCALAR_UDF_INLINING = { ON | OFF }
    | ELEVATE_ONLINE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }
    | ELEVATE_RESUMABLE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }
    | OPTIMIZE_FOR_AD_HOC_WORKLOADS = { ON | OFF }
    | XTP_PROCEDURE_EXECUTION_STATISTICS = { ON | OFF }
    | XTP_QUERY_EXECUTION_STATISTICS = { ON | OFF }
    | ROW_MODE_MEMORY_GRANT_FEEDBACK = { ON | OFF }
    | BATCH_MODE_ON_ROWSTORE = { ON | OFF }
    | DEFERRED_COMPILATION_TV = { ON | OFF }
    | GLOBAL_TEMPORARY_TABLE_AUTODROP = { ON | OFF }
    | LIGHTWEIGHT_QUERY_PROFILING = { ON | OFF }
    | VERBOSE_TRUNCATION_WARNINGS = { ON | OFF }
    | LAST_QUERY_PLAN_STATS = { ON | OFF }
}
```

## <a name="arguments"></a>인수

보조용

보조 데이터베이스에 대한 설정을 지정합니다(모든 보조 데이터베이스가 동일한 값을 가져야 함).

CLEAR PROCEDURE_CACHE [plan_handle]

데이터베이스에 대한 프로시저(플랜) 캐시를 지우고 기본 및 보조에서 둘 다 실행할 수 있습니다.  

쿼리 계획 핸들을 지정하여 계획 캐시에서 단일 쿼리 계획을 지웁니다.

> [!NOTE]
> 쿼리 계획 핸들을 지정하는 작업은 Azure SQL Database 및 SQL Server 2019 이상에서 수행할 수 있습니다.

MAXDOP **=** {\<value> | PRIMARY } **\<value>**

명령문에 사용해야 하는 기본 MAXDOP 설정을 지정합니다. 0은 기본값이며 서버 구성이 대신 사용됨을 나타냅니다. 데이터베이스 범위에서 MAXDOP는 sp_configure로 서버 수준에서 **max degree of parallelism** 설정을 재정의합니다(0으로 설정되지 않은 한). 쿼리 힌트는 다른 설정을 필요로 하는 특정 쿼리를 조정하기 위해 DB 범위 MAXDOP를 여전히 재정의할 수 있습니다. 이러한 모든 설정은 작업 그룹에 대한 MAXDOP 설정으로 제한됩니다.

max degree of parallelism 옵션을 사용하여 병렬 계획 실행에 사용할 프로세서 수를 제한할 수 있습니다. SQL Server는 쿼리에 대한 병렬 실행 계획, 인덱스 DDL(데이터 정의 언어) 작업, 병렬 삽입, 온라인 열 변경, 병렬 통계 수집 및 정적 커서와 키 집합 커서 채우기를 고려합니다.

인스턴스 수준에서 이 옵션을 설정하려면 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요.

> [!TIP]
> 쿼리 수준에서 이를 수행하기 위해 **MAXDOP** [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md)를 추가합니다.

PRIMARY

데이터베이스가 기본에 있는 동안 보조에 대해서만 설정될 수 있으며 구성이 기본에 대해 설정된 것임을 나타냅니다. 기본에 대한 구성이 변경되는 경우 보조에 있는 값은 보조 값을 명시적으로 설정할 필요 없이 적절하게 변경됩니다. **기본**은 보조에 대한 기본 설정입니다.

LEGACY_CARDINALITY_ESTIMATION **=** { ON | **OFF** | PRIMARY }

데이터베이스의 호환성 수준에 관계없이 SQL Server 2012 및 이전 버전에 대한 쿼리 최적화 프로그램 카디널리티 추정 모델을 설정할 수 있습니다. 기본값은 **OFF**이며, 데이터베이스의 호환성 수준에 따라 쿼리 최적화 프로그램 카디널리티 추정 모델을 설정합니다. LEGACY_CARDINALITY_ESTIMATION을 **ON**으로 설정하는 것은 [추적 플래그 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)을 활성화하는 것과 동일합니다.

> [!TIP]
> 쿼리 수준에서 이를 수행하기 위해 **QUERYTRACEON** [쿼리 힌트](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 추가합니다.
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1부터 쿼리 수준에서 이를 수행하기 위해 추적 플래그를 사용하는 대신 **USE HINT** [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md#use_hint)를 추가합니다.

PRIMARY

이 값은 데이터베이스가 기본에 있는 동안 보조에서만 유효하며, 모든 보조의 쿼리 최적화 프로그램 카디널리티 추정 모델 설정이 기본에 대해 설정된 값이 되도록 지정합니다. 쿼리 최적화 프로그램 카디널리티 추정 모델에 대한 기본의 구성이 변경되는 경우 보조의 값도 그에 따라 변경됩니다. **기본**은 보조에 대한 기본 설정입니다.

PARAMETER_SNIFFING **=** { **ON** | OFF | PRIMARY}

[매개 변수 검색](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)을 사용하거나 사용하지 않도록 설정합니다. 기본값은 ON입니다. PARAMETER_SNIFFING를 OFF로 설정하는 것은 [추적 플래그 4136](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)을 활성화하는 것과 동일합니다.

> [!TIP]
> 쿼리 수준에서 이를 수행하기 위해 **OPTIMIZE FOR UNKNOWN** [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1부터 쿼리 수준에서 이를 수행하기 위해 **USE HINT** [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md#use_hint)를 사용할 수도 있습니다.

PRIMARY

이 값은 데이터베이스가 기본에 있는 동안 보조에서만 유효하며, 모든 보조에서 이 설정에 대한 값이 기본에 대해 설정된 값이 되도록 지정합니다. [매개 변수 검색](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)을 사용하기 위해 기본에 대한 구성이 변경되는 경우 보조에 있는 값은 보조 값을 명시적으로 설정할 필요 없이 적절하게 변경됩니다. PRIMARY는 보조에 대한 기본 설정입니다.

<a name="qo_hotfixes"></a> QUERY_OPTIMIZER_HOTFIXES **=** { ON | **OFF** | PRIMARY }

데이터베이스의 호환성 수준에 관계없이 쿼리 최적화 프로그램 핫픽스를 사용하거나 사용하지 않도록 설정합니다. 기본값은 **OFF**이며 가장 높은 호환성 수준이 특정 버전(RTM 이후)에 대해 도입된 후에 릴리스된 쿼리 최적화 프로그램 핫픽스를 비활성화합니다. 이 값을 **ON**으로 설정하면 [추적 플래그 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 활성화하는 것과 동일합니다.

> [!TIP]
> 쿼리 수준에서 이를 수행하기 위해 **QUERYTRACEON** [쿼리 힌트](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 추가합니다.
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1부터 쿼리 수준에서 이를 수행하기 위해 추적 플래그를 사용하는 대신 USE HINT [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md#use_hint)를 추가합니다.

PRIMARY

이 값은 데이터베이스가 기본에 있는 동안 보조에서만 유효하며, 모든 보조에서 이 설정에 대한 값이 기본에 대해 설정된 값이 되도록 지정합니다. 기본에 대한 구성이 변경되는 경우 보조에 있는 값은 보조 값을 명시적으로 설정할 필요 없이 적절하게 변경됩니다. PRIMARY는 보조에 대한 기본 설정입니다.

IDENTITY_CACHE **=** { **ON** | OFF }      

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

데이터베이스 수준에서 ID 캐시를 사용하거나 사용하지 않도록 설정합니다. 기본값은 **ON**입니다. ID 캐싱은 ID 열이 있는 테이블에서 INSERT 성능을 개선하기 위해 사용됩니다. 서버가 예기치 않게 다시 시작하거나 보조 서버로 장애 조치(failover)되는 경우에 ID 열의 값이 차이 나지 않도록 IDENTITY_CACHE 옵션을 비활성화합니다. 이 옵션은 서버 수준에서만이 아니라 데이터베이스 수준에서 설정될 수 있다는 점을 제외하고 기존 [추적 플래그 272](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)와 비슷합니다.

> [!NOTE]
> 이 옵션은 기본에 대해서만 설정될 수 있습니다. 자세한 내용은 [ID 열](create-table-transact-sql-identity-property.md)을 참조하세요.

INTERLEAVED_EXECUTION_TVF **=** { **ON** | OFF }   

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

데이터베이스 호환성 수준 140 이상을 유지하면서 데이터베이스 또는 명령문 범위에서 다중 명령문 테이블 값 함수에 대해 인터리브된 실행을 사용하거나 사용하지 않도록 설정할 수 있습니다. 인터리브된 실행은 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]의 적응 쿼리 처리의 일부인 기능입니다. 자세한 내용은 [지능형 쿼리 처리](../../relational-databases/performance/intelligent-query-processing.md)를 참조하세요.

> [!NOTE]
> 데이터베이스 호환성 수준 130 이하의 경우, 이 데이터베이스 범위 구성에 아무런 영향이 없습니다.
>
> SQL Server 2017(14.x)에서만 INTERLEAVED_EXECUTION_TVF 옵션에 **DISABLE**_INTERLEAVED_EXECUTION_TVF의 이전 이름이 있었습니다.

BATCH_MODE_MEMORY_GRANT_FEEDBACK **=** { **ON** | OFF}    

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

데이터베이스 호환성 수준 140 이상을 유지하면서 데이터베이스 범위에서 일괄 처리 모드 메모리 부여 피드백을 사용하거나 사용하지 않도록 설정할 수 있습니다. 일괄 처리 모드 메모리 부여 피드백은 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]에 도입된 [지능형 쿼리 처리](../../relational-databases/performance/intelligent-query-processing.md)의 일부 기능입니다.

> [!NOTE]
> 데이터베이스 호환성 수준 130 이하의 경우, 이 데이터베이스 범위 구성에 아무런 영향이 없습니다.

BATCH_MODE_ADAPTIVE_JOINS **=** { **ON** | OFF}   

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

데이터베이스 호환성 수준 140 이상을 유지하면서 데이터베이스 범위에서 일괄 처리 모드 적응형 조인을 사용하거나 사용하지 않도록 설정할 수 있습니다. 일괄 처리 모드 적응형 조인은 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]에 도입된 [지능형 쿼리 처리](../../relational-databases/performance/intelligent-query-processing.md)의 일부 기능입니다.

> [!NOTE]
> 데이터베이스 호환성 수준 130 이하의 경우, 이 데이터베이스 범위 구성에 아무런 영향이 없습니다.

TSQL_SCALAR_UDF_INLINING **=** { **ON** | OFF }

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)](기능은 공개 미리 보기 상태)

데이터베이스 호환성 수준 150 이상을 유지하면서 데이터베이스 범위에서 T-SQL Scalar UDF 인라인을 활성화하거나 비활성화할 수 있습니다. T-SQL Scalar UDF 인라인은 [인텔리전트 쿼리 처리](../../relational-databases/performance/intelligent-query-processing.md) 기능 제품군의 일부입니다.

> [!NOTE]
> 데이터베이스 호환성 수준 140 이하의 경우, 이 데이터베이스 범위 구성에 아무런 영향이 없습니다.

ELEVATE_ONLINE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }

**적용 대상**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)](기능은 공개 미리 보기 상태)

엔진이 지원되는 작업의 권한을 online으로 자동 상승시키도록 하는 옵션을 선택할 수 있습니다. 기본값은 OFF, 즉 명령문에 지정되지 않은 경우 작업의 권한이 online으로 상승하지 않는 것입니다. [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)는 ELEVATE_ONLINE의 현재 값을 나타냅니다. 이러한 옵션은 online에 지원되는 작업에만 적용됩니다.

FAIL_UNSUPPORTED

이 값은 지원되는 모든 DDL 작업의 권한을 ONLINE으로 상승시킵니다. 온라인 실행을 지원하지 않는 작업은 실패하고 경고를 throw합니다.

WHEN_SUPPORTED

이 값은 ONLINE을 지원하는 작업의 권한을 상승시킵니다. 온라인을 지원하지 않는 작업은 오프라인으로 실행됩니다.

> [!NOTE]
> ONLINE 옵션이 지정된 명령문을 제출하여 기본 설정을 재정의할 수 있습니다.

ELEVATE_RESUMABLE= { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)](기능은 공개 미리 보기 상태)

엔진이 지원되는 작업의 권한을 resumable로 자동 상승시키도록 하는 옵션을 선택할 수 있습니다. 기본값은 OFF, 즉 명령문에 지정되지 않은 경우 작업의 권한이 resumable로 상승되지 않는 것입니다. [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)는 ELEVATE_ELEVATE_RESUMABLE의 현재 값을 나타냅니다. 이러한 옵션은 resumable에 지원되는 작업에만 적용됩니다.

FAIL_UNSUPPORTED

이 값은 지원되는 모든 DDL 작업의 권한을 RESUMABLE로 상승시킵니다. 다시 시작 가능한 실행을 지원하지 않는 작업은 실패하고 경고를 throw합니다.

WHEN_SUPPORTED

이 값은 RESUMABLE을 지원하는 작업의 권한을 상승시킵니다. resumable을 지원하지 않는 작업은 다시 시작 가능하지 않은 방식으로 실행됩니다.

> [!NOTE]
> RESUMABLE 옵션이 지정된 명령문을 제출하여 기본 설정을 재정의할 수 있습니다.

OPTIMIZE_FOR_AD_HOC_WORKLOADS **=** { ON | **OFF** }

**적용 대상**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]

일괄 처리가 처음으로 컴파일될 때 캐시에 저장될 컴파일된 계획 스텁을 사용하거나 사용하지 않도록 설정합니다. 기본값은 OFF입니다. 데이터베이스 범위 구성 OPTIMIZE_FOR_AD_HOC_WORKLOADS가 데이터베이스에 대해 활성화되면 컴파일된 계획 스텁은 일괄 처리가 처음으로 컴파일될 때 캐시에 저장됩니다. 계획 스텁은 전체 컴파일된 계획의 크기에 비해 작은 메모리 사용 공간을 갖습니다. 일괄 처리가 컴파일되거나 다시 실행되는 경우 컴파일된 계획 스텁은 제거되고 전체 컴파일된 계획으로 대체됩니다.

XTP_PROCEDURE_EXECUTION_STATISTICS **=** { ON | **OFF** }

**적용 대상**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]

현재 데이터베이스에 있는 고유하게 컴파일된 T-SQL 모듈에 대한 모듈 수준 실행 통계 수집을 활성화하거나 비활성화합니다. 기본값은 OFF입니다. 실행 통계는 [sys.dm_exec_procedure_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)에 반영됩니다.

고유하게 컴파일된 T-SQL 모듈에 대한 모듈 수준 실행 통계는 이 옵션이 켜져 있거나 통계 수집이 [sp_xtp_control_proc_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md)를 통해 활성화된 경우 수집됩니다.

XTP_QUERY_EXECUTION_STATISTICS **=** { ON | **OFF** }

**적용 대상**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]

현재 데이터베이스에 있는 고유하게 컴파일된 T-SQL 모듈에 대한 명령문 수준 실행 통계 수집을 활성화하거나 비활성화합니다. 기본값은 OFF입니다. 실행 통계는 [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) 및 [쿼리 저장소](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)에 반영됩니다.

고유하게 컴파일된 T-SQL 모듈에 대한 명령문 수준 실행 통계는 이 옵션이 켜져 있거나 통계 수집이 [sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md)를 통해 활성화된 경우 수집됩니다.

고유하게 컴파일된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈의 성능 모니터링에 대한 자세한 내용은 [고유하게 컴파일된 저장 프로시저의 성능 모니터링](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md)을 참조하세요.

ROW_MODE_MEMORY_GRANT_FEEDBACK **=** { **ON** | OFF}

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)](기능은 공개 미리 보기 상태)

데이터베이스 호환성 수준 150 이상을 유지하면서 데이터베이스 범위에서 행 모드 메모리 부여 피드백을 사용하거나 사용하지 않도록 설정할 수 있습니다. 행 모드 메모리 부여 피드백은 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]에 도입된 [지능형 쿼리 처리](../../relational-databases/performance/intelligent-query-processing.md)의 일부 기능입니다(행 모드는 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 지원됨).

> [!NOTE]
> 데이터베이스 호환성 수준 140 이하의 경우, 이 데이터베이스 범위 구성에 아무런 영향이 없습니다.

BATCH_MODE_ON_ROWSTORE **=** { **ON** | OFF}

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)](기능은 공개 미리 보기 상태)

데이터베이스 호환성 수준 150 이상을 유지하면서 데이터베이스 범위에서 행 저장소의 일괄 처리 모드를 사용하거나 사용하지 않도록 설정할 수 있습니다. 행 저장소의 일괄 처리 모드는 [인텔리전트 쿼리 처리](../../relational-databases/performance/intelligent-query-processing.md) 기능 제품군의 일부 기능입니다.

> [!NOTE]
> 데이터베이스 호환성 수준 140 이하의 경우, 이 데이터베이스 범위 구성에 아무런 영향이 없습니다.

DEFERRED_COMPILATION_TV **=** { **ON** | OFF}

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)](기능은 공개 미리 보기 상태)

데이터베이스 호환성 수준 150 이상을 유지하면서 데이터베이스 범위에서 테이블 변수 지연 컴파일을 사용하거나 사용하지 않도록 설정할 수 있습니다. 테이블 변수 지연 컴파일은 [인텔리전트 쿼리 처리](../../relational-databases/performance/intelligent-query-processing.md) 기능 제품군의 일부 기능입니다.

> [!NOTE]
> 데이터베이스 호환성 수준 140 이하의 경우, 이 데이터베이스 범위 구성에 아무런 영향이 없습니다.

GLOBAL_TEMPORARY_TABLE_AUTODROP **=** { **ON** | OFF }

**적용 대상**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)](기능은 공개 미리 보기 상태)

[전역 임시 테이블](create-table-transact-sql.md)에 대한 자동 삭제 기능을 설정할 수 있습니다. 기본값은 ON입니다. 이는 전역 임시 테이블이 세션에서 사용되지 않을 때 자동으로 삭제됨을 의미합니다. OFF로 설정하면 DROP TABLE 문을 사용하여 전역 임시 테이블을 명시적으로 삭제하거나 서버를 다시 시작할 때 자동으로 삭제됩니다.

- [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 단일 데이터베이스와 탄력적 풀을 사용하면 SQL Database 서버의 개별 사용자 데이터베이스에서 이 옵션을 설정할 수 있습니다.
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 관리되는 인스턴스에서 이 옵션은 `TempDB`에 설정되며 개별 사용자 데이터베이스의 설정은 영향을 미치지 않습니다.

<a name="lqp"></a>

LIGHTWEIGHT_QUERY_PROFILING **=** { **ON** | OFF}

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

[간단한 쿼리 프로파일링 인프라](../../relational-databases/performance/query-profiling-infrastructure.md)를 활성화하거나 비활성화할 수 있습니다. LWP(간단한 쿼리 프로파일링 인프라)는 표준 프로파일링 매커니즘보다 쿼리 성능 데이터를 더 효율적으로 제공하며 기본적으로 활성화되어 있습니다.

<a name="verbose-truncation"></a>

VERBOSE_TRUNCATION_WARNINGS **=** { **ON** | OFF}

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  

새 `String or binary data would be truncated` 오류 메시지를 사용하거나 사용하지 않도록 설정할 수 있습니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에서는 이 시나리오에 대해 보다 구체적인 새 오류 메시지(2628)를 제공합니다.  

`String or binary data would be truncated in table '%.*ls', column '%.*ls'. Truncated value: '%.*ls'.`

데이터베이스 호환성 수준 150에서 ON으로 설정하면 잘림 오류로 인해 더 많은 컨텍스트를 제공하고 문제 해결 프로세스를 간소화하기 위해 오류 메시지 2628이 발생합니다.

데이터베이스 호환성 수준 150 OFF로 설정하면 잘림 오류로 인해 이전 오류 메시지 8152가 발생합니다.

데이터베이스 호환성 수준 140 이하의 경우 오류 메시지 2628은 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460을 사용하도록 설정해야 하는 옵트인 오류 메지시로 남아 있으며, 이 데이터베이스 범위 구성에 영향을 주지 않습니다.

LAST_QUERY_PLAN_STATS **=** { ON | **OFF**}

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작)(기능은 공개 미리 보기 상태임)

[sys.dm_exec_query_plan_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md)에서 마지막 쿼리 계획 통계(실제 실행 계획과 동일)의 수집을 활성화하거나 비활성화할 수 있습니다.

## <a name="Permissions"></a> 사용 권한

데이터베이스에 `ALTER ANY DATABASE SCOPE CONFIGURATION`이 필요합니다. 이 사용 권한은 데이터베이스에서 CONTROL 권한이 있는 사용자에 의해 부여될 수 있습니다.

## <a name="general-remarks"></a>일반적인 주의 사항
보조 데이터베이스가 해당 기본 데이터베이스와 서로 다른 범위 구성 설정을 갖도록 구성할 수도 있지만 모든 보조 데이터베이스는 동일한 구성을 사용합니다. 개별 보조에 대해 서로 다른 설정을 구성할 수 없습니다.

이 명령문을 실행하면 현재 데이터베이스에서 프로시저 캐시를 지웁니다. 즉, 모든 쿼리를 다시 컴파일해야 합니다.

3부분으로 된 이름 쿼리의 경우 현재 데이터베이스 컨텍스트에서 컴파일되는 SQL 모듈(예: 프로시저, 함수, 트리거)이 아닌 쿼리의 현재 데이터베이스 연결에 대한 설정이 적용되므로 존재하는 데이터베이스의 옵션을 사용합니다.

`ALTER_DATABASE_SCOPED_CONFIGURATION` 이벤트는 DDL 트리거를 시작하는 데 사용할 수 있는 DDL 이벤트로 추가되며 `ALTER_DATABASE_EVENTS` 트리거 그룹의 자식입니다.

데이터베이스 범위 구성 설정은 데이터베이스와 함께 전달됩니다. 이는 지정된 데이터베이스가 복원되거나 첨부될 때 기존 구성 설정이 그대로 유지됨을 의미합니다.

## <a name="limitations-and-restrictions"></a>제한 사항

### <a name="maxdop"></a>MAXDOP
세부적인 설정은 전역 설정을 재정의하고 해당 리소스 관리자(resource governor)는 다른 모든 MAXDOP 설정을 제한할 수 있습니다. MAXDOP 설정에 대한 논리는 다음과 같습니다.

- 쿼리 힌트는 `sp_configure`와 데이터베이스 범위 구성 모두를 재정의합니다. 리소스 그룹 MAXDOP가 작업 그룹에 대해 설정된 경우:

  - 쿼리 힌트가 제로(0)로 설정된 경우 리소스 관리자(resource governor) 설정에 의해 재정의됩니다.

  - 쿼리 힌트가 제로(0)가 아닌 경우 리소스 관리자(resource governor) 설정에 의해 제한됩니다.

- 데이터베이스 범위 구성(0이 아닌 경우)은 쿼리 힌트가 있고 리소스 관리자(resource governor) 설정에 의해 제한되지 않는 한 `sp_configure` 설정을 재정의합니다.

- `sp_configure` 설정은 리소스 관리자(resource governor) 설정에 의해 재정의됩니다.

### <a name="queryoptimizerhotfixes"></a>QUERY_OPTIMIZER_HOTFIXES

`QUERYTRACEON` 힌트가 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 버전 또는 쿼리 최적화 프로그램 또는 쿼리 SQL Server 7.0의 기본 쿼리 프로그램을 활성화하는 데 사용되는 경우 쿼리 힌트와 데이터베이스 범위 구성 설정 간의 OR 조건이 됩니다. 즉, 둘 중 하나가 활성화되면 데이터베이스 범위 구성이 적용됩니다.

### <a name="geo-dr"></a>Geo DR

읽기 가능한 보조 데이터베이스(Always On 가용성 그룹 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 지역 복제 데이터베이스)는 데이터베이스의 상태를 확인하여 보조 값을 사용합니다. 재컴파일이 장애 조치(failover)에서 발생하지 않고 기술적으로 새로운 기본에 보조 설정을 사용하는 쿼리가 있더라도 기본 및 보조 간의 설정은 워크로드가 다른 경우에만 다르기 때문에 캐시된 쿼리는 최적의 설정을 사용하는 반면 새로운 쿼리는 적절한 새 설정을 선택합니다.

### <a name="dacfx"></a>DacFx

`ALTER DATABASE SCOPED CONFIGURATION`은 데이터베이스 스키마에 영향을 주는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 시작)의 새 기능이므로 스키마(데이터 유무에 상관없이)를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이전 버전(예: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 또는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])으로 내보낼 수 없습니다. 예를 들어 이 새로운 기능이 사용되는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 또는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 데이터베이스에서 [DACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) 또는 [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4)로 내보내기를 하위 수준 서버로 가져올 수 없게 됩니다.

### <a name="elevateonline"></a>ELEVATE_ONLINE

이 옵션은 `WITH (ONLINE = <syntax>)`를 지원하는 DDL 문에만 적용됩니다. XML 인덱스는 영향을 받지 않습니다.

### <a name="elevateresumable"></a>ELEVATE_RESUMABLE

이 옵션은 `WITH (RESUMABLE = <syntax>)`를 지원하는 DDL 문에만 적용됩니다. XML 인덱스는 영향을 받지 않습니다.

## <a name="metadata"></a>메타데이터

[sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 시스템 뷰는 데이터베이스 내에서 범위 구성에 대한 정보를 제공합니다. 데이터베이스 범위 구성 옵션은 서버 차원의 기본 설정으로 재정의되면 sys.database_scoped_configurations에 나타납니다. [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 시스템 뷰는 서버 차원의 설정을 표시합니다.

## <a name="examples"></a>예
이 예제에서는 ALTER DATABASE SCOPED CONFIGURATION의 사용을 보여 줍니다.

### <a name="a-grant-permission"></a>1\. 사용 권한 부여
이 예제에서는 ALTER DATABASE SCOPED CONFIGURATION을 실행하는 데 필요한 사용 권한을 사용자 Joe에게 부여합니다.

```sql
GRANT ALTER ANY DATABASE SCOPED CONFIGURATION to [Joe] ;
```

### <a name="b-set-maxdop"></a>2\. MAXDOP 설정
이 예제는 지역에서 복제 시나리오에서 기본 데이터베이스에 대해 MAXDOP = 1을 설정하고 보조 데이터베이스에 대해 MAXDOP = 4를 설정합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 1 ;
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP = 4 ;
```

이 예제는 지역에서 복제 시나리오에서 해당 기본 데이터베이스에 대해 설정된 것과 동일하도록 보조 데이터베이스에 대한 MAXDOP를 설정합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP = PRIMARY ;
```

### <a name="c-set-legacycardinalityestimation"></a>C. LEGACY_CARDINALITY_ESTIMATION 설정
이 예제는 지역에서 복제 시나리오에서 보조 데이터베이스에 대해 LEGACY_CARDINALITY_ESTIMATION을 ON으로 설정합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION = ON ;
```

이 예제는 지역에서 복제 시나리오에서 해당 기본 데이터베이스에 대해 설정된 것으로 보조 데이터베이스에 대해 LEGACY_CARDINALITY_ESTIMATION을 설정합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION = PRIMARY ;
```

### <a name="d-set-parametersniffing"></a>D. PARAMETER_SNIFFING 설정
이 예제는 지역에서 복제 시나리오에서 기본 데이터베이스에 대해 PARAMETER_SNIFFING을 OFF로 설정합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET PARAMETER_SNIFFING = OFF ;
```

이 예제는 지역에서 복제 시나리오에서 보조 데이터베이스에 대해 PARAMETER_SNIFFING을 OFF로 설정합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING = OFF ;
```

이 예제는 지역에서 복제 시나리오에서 보조 데이터베이스에 대한 PARAMETER_SNIFFING을 기본 데이터베이스에 대한 것으로 설정합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING = PRIMARY ;
```

### <a name="e-set-queryoptimizerhotfixes"></a>E. QUERY_OPTIMIZER_HOTFIXES 설정
지역에서 복제 시나리오에서 기본 데이터베이스에 대해 QUERY_OPTIMIZER_HOTFIXES를 ON으로 설정합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET QUERY_OPTIMIZER_HOTFIXES = ON ;
```

### <a name="f-clear-procedure-cache"></a>F. 프로시저 캐시 지우기
이 예제에서는 프로시저 캐시를 지웁니다(기본 데이터베이스에 대해서만 사용 가능).

```sql
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
```

### <a name="g-set-identitycache"></a>G. IDENTITY_CACHE 설정
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)](기능은 공개 미리 보기 상태)

이 예제는 ID 캐시를 비활성화합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET IDENTITY_CACHE = OFF ;
```

### <a name="h-set-optimizeforadhocworkloads"></a>H. OPTIMIZE_FOR_AD_HOC_WORKLOADS 설정
**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

이 예제는 일괄 처리가 처음으로 컴파일될 때 캐시에 저장될 컴파일된 계획 스텁을 활성화합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET OPTIMIZE_FOR_AD_HOC_WORKLOADS = ON;
```

### <a name="i-set-elevateonline"></a>9\. ELEVATE_ONLINE 설정
**적용 대상**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)](기능은 공개 미리 보기 상태)

이 예에서는 ELEVATE_ONLINE을 FAIL_UNSUPPORTED로 설정합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ELEVATE_ONLINE = FAIL_UNSUPPORTED ;
```

### <a name="j-set-elevateresumable"></a>J. ELEVATE_RESUMABLE 설정
**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/sssqlv15-md.md)](기능은 공개 미리 보기 상태)

이 예에서는 ELEVATE_RESUMABLE을 WHEN_SUPPORTED로 설정합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ELEVATE_RESUMABLE = WHEN_SUPPORTED ;
```

### <a name="k-clear-a-query-plan-from-the-plan-cache"></a>11. 계획 캐시에서 쿼리 계획 지우기
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

이 예에서는 프로시저 캐시에서 특정 계획을 지웁니다. 

```sql
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE 0x06000500F443610F003B7CD12C02000001000000000000000000000000000000000000000000000000000000;
```

## <a name="additional-resources"></a>추가 리소스

### <a name="maxdop-resources"></a>MAXDOP 리소스

- [병렬 처리 수준](../../relational-databases/query-processing-architecture-guide.md#DOP)
- [SQL Server의 "max degree of parallelism" 구성 옵션에 대한 권장 사항 및 지침(영문)](https://support.microsoft.com/kb/2806535)

### <a name="legacycardinalityestimation-resources"></a>LEGACY_CARDINALITY_ESTIMATION 리소스

- [카디널리티 추정(SQL Server)](../../relational-databases/performance/cardinality-estimation-sql-server.md)
- [SQL Server 2014 카디널리티 추정기로 쿼리 계획 최적화](https://msdn.microsoft.com/library/dn673537.aspx)

### <a name="parametersniffing-resources"></a>PARAMETER_SNIFFING 리소스

- [매개 변수 검색](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)
- ["매개 변수를 찾았습니다!"](https://blogs.msdn.microsoft.com/queryoptteam/2006/03/31/i-smell-a-parameter/)

### <a name="queryoptimizerhotfixes-resources"></a>QUERY_OPTIMIZER_HOTFIXES 리소스

- [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
- [SQL Server 쿼리 최적화 프로그램 핫픽스 추적 플래그 4199 서비스 모델](https://support.microsoft.com/kb/974006)

### <a name="elevateonline-resources"></a>ELEVATE_ONLINE 리소스

[온라인 인덱스 작업에 대한 지침](../../relational-databases/indexes/guidelines-for-online-index-operations.md)

### <a name="elevateresumable-resources"></a>ELEVATE_RESUMABLE 리소스

[온라인 인덱스 작업에 대한 지침](../../relational-databases/indexes/guidelines-for-online-index-operations.md)

## <a name="more-information"></a>자세한 정보

- [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)
- [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)
- [데이터베이스 및 파일 카탈로그 뷰](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)
- [서버 구성 옵션](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [온라인 인덱스 작업 작동 방식](../../relational-databases/indexes/how-online-index-operations-work.md)
- [온라인으로 인덱스 작업 수행](../../relational-databases/indexes/perform-index-operations-online.md)
- [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)
- [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)
