---
description: 임시 테이블
title: Temporal 테이블 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: e442303d-4de1-494e-94e4-4f66c29b5fb9
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d45c26459b43fecaedf401bf98d0a5346da34dbb
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243562"
---
# <a name="temporal-tables"></a>임시 테이블


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]


SQL Server 2016에서는 현재 시점에서 정확한 데이터만이 아니라 임의 시점에서 테이블에 저장된 데이터에 대한 정보를 제공하기 위해 기본적으로 지원을 제공하는 데이터베이스 기능으로 임시 테이블(시스템 버전 임시 테이블이라고도 함)에 대한 지원을 도입했습니다. 임시 테이블은 ANSI SQL 2011에서 도입된 데이터베이스 기능입니다.

**빠른 시작**

- **시작하기:**

  - [시스템 버전 관리 임시 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
  - [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
  - [임시 테이블 사용 시나리오](../../relational-databases/tables/temporal-table-usage-scenarios.md)

  - [Azure SQL Database의 임시 테이블 시작](/azure/azure-sql/temporal-tables)

- **예:**

  - [시스템 버전 임시 테이블 만들기](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
  - [메모리 액세스에 최적화된 시스템 버전 임시 테이블로 작업](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)
  - [시스템 버전 임시 테이블의 데이터 수정](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
  - [시스템 버전 임시 테이블의 데이터 쿼리](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
  - **Adventure Works 샘플 데이터베이스 다운로드:** 임시 테이블을 시작하려면 샘플 스크립트가 포함된 [SQL Server용 AdventureWorks 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016_EXT.bak)를 다운로드하고 ‘Temporal’ 폴더의 지침을 따르세요.

- **구문:**

  - [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)
  - [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
  - [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)
- **비디오:** 임시 테이블에 대한 20분간의 논의는 [SQL Server 2016의 임시 테이블](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016)을 참조하세요.

## <a name="what-is-a-system-versioned-temporal-table"></a>시스템 버전 관리 temporal 테이블이란?

시스템 버전 temporal 테이블은 데이터 변경 내용의 전체 기록을 유지하여 간편한 지정 시간 분석을 허용하도록 설계된 사용자 테이블의 종류입니다. 이 유형의 temporal 테이블은 각 행의 유효 기간이 시스템(예: 데이터베이스 엔진)에 의해 관리되기 때문에 시스템 버전 temporal 테이블이라고 합니다.

모든 temporal 테이블에는 명시적으로 정의된 두 개의 열이 있으며, 각 열의 데이터 형식은 **datetime2** 입니다. 이러한 열을 기간 열이라고 합니다. 이러한 기간 열은 행이 수정될 때마다 시스템에서 각 행의 유효 기간을 기록하는 데에만 사용됩니다.

이러한 기간 열 외에도 temporal 테이블은 미러된 스키마를 사용하는 다른 테이블에 대한 참조를 포함합니다. 시스템에서는 이 테이블을 사용하여 temporal 테이블의 행이 업데이트되거나 삭제될 때마다 이전 버전의 행을 자동으로 저장합니다. 이 추가 테이블을 기록 테이블이라고 하며, 현재(실제) 행 버전을 저장하는 주 테이블을 현재 테이블 또는 temporal 테이블이라고 합니다. temporal 테이블을 만드는 동안 사용자가 기존 기록 테이블(스키마를 준수해야 함)를 지정하거나 시스템에서 기본 기록 테이블을 만들도록 할 수 있습니다.

## <a name="why-temporal"></a>Temporal 테이블을 사용하는 이유

실제 데이터 원본은 동적이며, 비즈니스 의사 결정은 분석가가 데이터 진화에서 얻을 수 있는 통찰력에 의존하는 경우가 많습니다. temporal 테이블에 대한 사용 사례는 다음과 같습니다.

- 모든 데이터 변경 내용을 감사하고 필요한 경우 데이터 범죄 분석 수행
- 과거 시점을 기준으로 데이터 상태 재구성
- 시간에 따른 추세 계산
- 의사 결정 지원 애플리케이션에 대한 느린 변경 차원 유지 관리
- 실수로 인한 데이터 변경 및 애플리케이션 오류로부터 복구

## <a name="how-does-temporal-work"></a>Temporal 테이블의 작동 방식

 테이블에 대한 시스템 버전은 현재 테이블과 기록 테이블의 테이블 쌍으로 구현됩니다. 이러한 각 테이블 내에서 다음 두 개의 추가 **datetime2** 열은 각 행의 유효 기간을 정의하는 데 사용됩니다.

- 기간 시작 열: 시스템에서 이 열의 행에 대한 시작 시간을 기록합니다(일반적으로 **SysStartTime** 열로 표시됨).
- 기간 종료 열: 시스템에서 이 열의 행에 대한 종료 시간을 기록합니다(일반적으로 **SysEndTime** 열로 표시됨).

현재 테이블에는 각 행에 대한 현재 값이 포함됩니다. 기록 테이블에는 각 행에 대한 각각의 이전 값(있는 경우)과 유효 기간의 시작 시간 및 종료 시간이 포함됩니다.

![Temporal 테이블의 작동 방식을 보여 주는 다이어그램](../../relational-databases/tables/media/temporal-howworks.PNG "Temporal-HowWorks")

다음의 간단한 예제에서는 가상 HR 데이터베이스에서 직원 정보를 사용하는 시나리오를 보여 줍니다.

```sql
CREATE TABLE dbo.Employee
(
  [EmployeeID] int NOT NULL PRIMARY KEY CLUSTERED
  , [Name] nvarchar(100) NOT NULL
  , [Position] varchar(100) NOT NULL
  , [Department] varchar(100) NOT NULL
  , [Address] nvarchar(1024) NOT NULL
  , [AnnualSalary] decimal (10,2) NOT NULL
  , [ValidFrom] datetime2 GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.EmployeeHistory));
```

- **INSERTS:** **INSERT** 에서 시스템은 시스템 클록을 기준으로 **SysStartTime** 열의 값을 현재 트랜잭션의 시작 시간(UTC 표준 시간대)으로 설정하고, **SysEndTime** 열의 값을 최댓값 9999-12-31에 할당합니다. 그러면 행이 열린 것으로 표시됩니다.
- **UPDATES:** **UPDATE** 에서 시스템은 기록 테이블에 있는 행의 이전 값을 저장하고, 시스템 클록을 기준으로 **SysEndTime** 열의 값을 현재 트랜잭션의 시작 시간(UTC 표준 시간대)으로 설정합니다. 그러면 행이 닫힌 것으로 표시되고 행이 유효 상태로 유지된 기간이 기록됩니다. 현재 테이블에서는 행이 새 값으로 업데이트되고 시스템에서 시스템 클록을 기준으로 **SysStartTime** 열의 값을 트랜잭션의 시작 시간(UTC 표준 시간대)으로 설정합니다. 현재 테이블에서 **SysEndTime** 열에 대해 업데이트된 행의 값은 최대값 9999-12-31로 그대로 유지됩니다.
- **DELETES:** **DELETE** 에서 시스템은 기록 테이블에 있는 행의 이전 값을 저장하고, 시스템 클록을 기준으로 **SysEndTime** 열의 값을 현재 트랜잭션의 시작 시간(UTC 표준 시간대)으로 설정합니다. 그러면 행이 닫힌 것으로 표시되고 이전 행이 유효 상태로 유지된 기간이 기록됩니다. 현재 테이블에서는 행이 제거됩니다. 현재 테이블의 쿼리는 이 행을 반환하지 않습니다. 기록 데이터를 처리하는 쿼리만 행이 닫힌 데이터를 반환합니다.
- **MERGE:** **MERGE** 에서는 작업이 **MERGE** 문에 동작으로 지정된 항목에 따라 정확히 최대 세 개의 문( **INSERT** , **UPDATE** 및/또는 **DELETE** )이 실행된 것처럼 동작합니다.

> [!IMPORTANT]
> 시스템 datetime2 열에 기록되는 시작 시간은 트랜잭션 자체의 시간을 기반으로 합니다. 예를 들어 단일 트랜잭션 내에 삽입된 모든 행은 **SYSTEM_TIME** 기간의 시작에 해당하는 열에 기록된 것과 UTC 시간이 동일합니다.

## <a name="how-do-i-query-temporal-data"></a>Temporal 데이터를 쿼리하는 방법

**SELECT** 문의 **FROM** _\<table\>_ 절에는 5개의 임시 하위 절과 함께 새로운 **FOR SYSTEM_TIME** 절을 사용하여 현재 및 기록 테이블에서 데이터를 쿼리합니다. 이 새로운 **SELECT** 문의 구문은 단일 테이블에서 직접 지원되며, 여러 조인 및 여러 temporal 테이블 위의 뷰를 통해 전파됩니다.

![임시 쿼리의 작동 방식을 보여 주는 다이어그램](../../relational-databases/tables/media/temporal-querying.PNG "Temporal-Querying")

다음 쿼리는 2014년 1월 1일부터 2015년 1월 1일(포함) 사이에 활성 상태로 있었던 EmployeeID가 1000인 Employee 행에 대한 행 버전을 검색합니다.

```sql
SELECT * FROM Employee
  FOR SYSTEM_TIME
    BETWEEN '2014-01-01 00:00:00.0000000' AND '2015-01-01 00:00:00.0000000'
      WHERE EmployeeID = 1000 ORDER BY ValidFrom;
```

> [!NOTE]
> **FOR SYSTEM_TIME** 은 유효 기간( **SysStartTime** = **SysEndTime** )이 0인 행을 필터링합니다.
> 이러한 행은 동일한 트랜잭션 내의 동일한 기본 키에서 여러 업데이트를 수행하는 경우에 생성됩니다.
> 이 경우 임시 쿼리는 트랜잭션 이전의 행 버전과 트랜잭션 이후에 실제가 된 행 버전만 표시합니다.
> 이러한 행을 분석에 포함해야 하는 경우 기록 테이블을 직접 쿼리합니다.

아래 표에서 행 한정의 SysStartTime 열은 쿼리 중인 테이블의 **SysStartTime** 열 값을 나타내고, **SysEndTime** 은 쿼리 중인 테이블의 **SysEndTime** 열 값을 나타냅니다. 전체 구문 및 예제는 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md) 및 [시스템 버전 임시 테이블의 데이터 쿼리](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)에서 지원되는 데이터베이스 기능입니다.

|식|행 한정|Description|
|----------------|---------------------|-----------------|
|**AS OF** <date_time>|SysStartTime \<= date_time AND SysEndTime > date_time|과거의 지정된 시간에 실제(현재)였던 값이 포함된 행이 있는 테이블을 반환합니다. 내부적으로 temporal 테이블과 기록 테이블 간에 합집합이 계산되며, 지정된 시간에 유효했던 행의 값을 반환하도록 결과가 *<date_time>* 매개 변수로 필터링됩니다. 행 값은 *system_start_time_column_name* 값이 *<date_time>* 매개 변수 값보다 작거나 같고 *system_end_time_column_name* 값이 *<date_time>* 매개 변수 값보다 큰 경우에 유효한 것으로 간주됩니다.|
|**FROM** <start_date_time> **TO** <end_date_time>|SysStartTime < end_date_time AND SysEndTime > start_date_time|FROM 인수에 대한 *<start_date_time>* 매개 변수 값 이전에 활성 상태가 시작되었든 아니면 TO 인수에 대한 *<end_date_time>* 매개 변수 값 이후에 활성 상태가 중단되었든 상관없이 지정된 시간 범위 내에 활성 상태였던 모든 행 버전의 값을 포함하는 테이블을 반환합니다. 내부적으로 temporal 테이블과 기록 테이블 간에 합집합이 계산되며, 지정된 시간 범위 중 임의의 시점에 활성 상태였던 모든 행 버전을 반환하도록 결과가 필터링됩니다. FROM 엔드포인트로 정의된 하위 경계에서 정확히 활동이 중지된 행은 포함되지 않고 TO 엔드포인트로 정의된 상위 경계에서 정확히 활성화된 레코드도 포함되지 않습니다.|
|**BETWEEN** <start_date_time> **AND** <end_date_time>|SysStartTime \<= end_date_time AND SysEndTime > start_date_time|&lt;end_date_time&gt; 엔드포인트로 정의된 상위 경계에서 활성화된 행이 반환되는 행 테이블에 포함된다는 점을 제외하고는 위의 **FOR SYSTEM_TIME FROM** &lt;start_date_time&gt; **TO** 설명과 같습니다.|
|**CONTAINED IN** (<start_date_time> , <end_date_time>)|SysStartTime >= start_date_time AND SysEndTime \<= end_date_time|CONTAINED IN 인수에 대한 두 개의 datetime 값으로 정의된 지정된 시간 범위 내에 열리고 닫힌 모든 행 버전의 값을 포함하는 테이블을 반환합니다. 정확히 하위 경계에서 활성화되거나 상위 경계에서 활성 상태가 중단된 행이 포함됩니다.|
|**ALL**|모든 행|현재 테이블 및 기록 테이블에 속하는 행의 합집합을 반환합니다.|

> [!NOTE]
> 필요한 경우 이러한 기간 열을 명시적으로 참조하지 않는 쿼리에서 이러한 열이 반환되지 않도록 이러한 기간 열을 숨길 수 있습니다( **SELECT \* FROM** _\<table\>_ 시나리오). 숨겨진 열을 반환하려면 쿼리에서 숨겨진 열을 명시적으로 참조하기만 하면 됩니다. 마찬가지로 **INSERT** 및 **BULK INSERT** 문은 이러한 새 기간 열이 존재하지 않은 것처럼 계속되며, 열 값이 자동으로 채워집니다. **HIDDEN** 절 사용에 대한 자세한 내용은 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) 및 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

- [시스템 버전 관리 임시 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [임시 테이블 사용 시나리오](../../relational-databases/tables/temporal-table-usage-scenarios.md)
- [임시 테이블 고려 사항 및 제한 사항](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [임시 테이블을 사용하여 분할](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [임시 테이블 시스템 일관성 검사](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [임시 테이블 보안](../../relational-databases/tables/temporal-table-security.md)
- [임시 테이블 메타데이터 뷰 및 함수](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)