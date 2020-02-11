---
title: CREATE WORKLOAD GROUP(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/14/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD GROUP
- WORKLOAD_GROUP_TSQL
- CREATE WORKLOAD GROUP
- CREATE_WORKLOAD_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD GROUP statement
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: ca80b2f95ee049d763d22f35e4ff6d35e344a8c0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75956506"
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP(Transact-SQL)

## <a name="click-a-product"></a>제품을 클릭하세요.

다음 행에서 관심이 있는 제품 이름을 클릭합니다. 클릭하면 웹페이지의 여기에서 클릭한 제품에 적절한 다른 콘텐츠를 표시합니다.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**_\* SQL Server \*_** &nbsp;|[SQL Database<br />관리되는 인스턴스](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](create-workload-group-transact-sql.md?view=azure-sqldw-latest)|

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server 및 SQL Database Managed Instance

리소스 관리자 작업 그룹을 만든 후 이 작업 그룹을 리소스 관리자 리소스 풀에 연결합니다. 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서는 Resource Governor를 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>구문

```
CREATE WORKLOAD GROUP group_name
[ WITH
    ( [ IMPORTANCE = { LOW | MEDIUM | HIGH } ]
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]
      [ [ , ] MAX_DOP = value ]
      [ [ , ] GROUP_MAX_REQUESTS = value ] )
 ]
[ USING {
    [ pool_name | "default" ]
    [ [ , ] EXTERNAL external_pool_name | "default" ] ]
    } ]
[ ; ]
```

## <a name="arguments"></a>인수

*group_name*은 작업 그룹에 대한 사용자 정의 이름입니다. *group_name*은 영숫자로 최대 128자를 사용할 수 있으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스 내에서 고유해야 하고 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다.

IMPORTANCE = { LOW | **MEDIUM** | HIGH } 작업 그룹에 있는 요청의 상대적 중요도를 지정합니다. 중요도는 다음 중 하나이며 MEDIUM이 기본값이 됩니다.

- LOW
- MEDIUM(기본값)
- HIGH

> [!NOTE]
> 내부적으로 각 중요도 설정은 계산에 사용된 멤버로 저장됩니다.

IMPORTANCE는 리소스 풀에 대해 로컬입니다. 같은 리소스 풀 내에 있는 다른 중요도의 작업 그룹은 서로 영향을 주지만 다른 리소스 풀의 작업 그룹에는 영향을 주지 않습니다.

REQUEST_MAX_MEMORY_GRANT_PERCENT = *값* 단일 요청이 풀에서 사용할 수 있는 최대 메모리 양을 지정합니다. *값*은 MAX_MEMORY_PERCENT에서 지정한 리소스 풀 크기와 관련된 백분율입니다.

‘값’은 최대 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]까지의 정수이며, 부동 소수점 수는 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]로 시작합니다.  기본값은 25입니다. 허용되는 *value*의 범위는 1에서 100까지입니다.

> [!IMPORTANT]  
> 지정된 양은 쿼리 실행 부여 메모리만 참조합니다.
>
> *value*를 0으로 설정하면 사용자 정의 작업 그룹에 SORT 및 HASH JOIN 작업이 있는 쿼리가 실행되지 않습니다.
>
> 다른 동시 쿼리를 실행 중인 경우 서버가 사용 가능한 메모리를 충분히 따로 설정해 놓지 못할 수 있으므로 ‘값’을 70을 초과하는 값으로 설정하지 않는 것이 좋습니다.  71 이상의 값으로 설정하면 쿼리 시간 초과 오류 8645가 발생할 수 있습니다.
>
> 쿼리 메모리 요구 사항이 이 매개 변수에 지정된 제한을 초과하는 경우 서버는 다음을 수행합니다.
>
> - 사용자 정의 작업 그룹의 경우 서버는 메모리 요구 사항이 제한 수준 아래로 낮아지거나 병렬 처리 수준이 1이 될 때까지 쿼리 병렬 처리 수준을 줄이려고 합니다. 그래도 쿼리 메모리 요구 사항이 제한보다 클 경우 오류 8657이 발생합니다.
>
> - 내부 및 기본 작업 그룹의 경우 서버는 쿼리가 필요한 메모리를 가져오도록 허용합니다.
>
> 두 경우 모두 서버에 실제 메모리가 부족하면 시간 초과 오류 8645가 발생할 수 있습니다.

REQUEST_MAX_CPU_TIME_SEC = *값* 요청이 사용할 수 있는 최대 CPU 시간(초)을 지정합니다. *value*는 0 또는 양의 정수여야 합니다. *value*의 기본 설정인 0은 무제한을 의미합니다.

> [!NOTE]
> 기본적으로 최대 시간이 초과하는 경우 Resource Governor가 요청을 종료하지는 않지만 이벤트가 생성됩니다. 자세한 내용은 [CPU Threshold Exceeded 이벤트 클래스](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)를 참조하세요.
> [!IMPORTANT]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 [2422 추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 사용하여 최대 시간이 초과되면 Resource Governor에서 요청을 중단합니다.

REQUEST_MEMORY_GRANT_TIMEOUT_SEC = *값* 메모리(작업 버퍼 메모리)가 부여될 때까지 쿼리가 대기할 수 있는 최대 시간(초)을 지정합니다. *value*는 0 또는 양의 정수여야 합니다. *value*의 기본 설정인 0은 쿼리 비용에 따른 내부 계산을 사용하여 최대 시간을 결정합니다.

> [!NOTE]
> 메모리 부여 제한 시간에 도달할 때마다 쿼리가 실패하지는 않습니다. 쿼리는 너무 많은 쿼리가 동시에 실행되는 경우에만 실패합니다. 그렇지 않을 경우 쿼리에 최소한의 메모리만 부여되어 쿼리 성능이 떨어질 수 있습니다.

MAX_DOP = *value*는 병렬 쿼리 실행에 대한 **MAXDOP(최대 병렬 처리 수준)** 를 지정합니다. *value*는 0 또는 양의 정수여야 합니다. 허용되는 *value*의 범위는 0에서 64까지입니다. *value*의 기본 설정 0은 전역 설정을 사용합니다. MAX_DOP는 다음과 같이 처리합니다.

> [!NOTE]
> 워크로드 그룹 MAX_DOP는 [최대 병렬 처리 수준 서버 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 및 **MAXDOP** [데이터베이스 범위 구성](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 재정의합니다.
> [!TIP]
> 쿼리 수준에서 이 작업을 수행하려면 **MAXDOP** [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md)를 사용합니다. 쿼리 힌트로 설정된 최대 병렬 처리 수준은 작업 그룹 MAX_DOP를 초과하지 않는 한 유효합니다. MAXDOP 쿼리 힌트 값이 리소스 관리자를 사용하여 구성된 값을 초과하는 경우 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]는 Resource Governor `MAX_DOP` 값을 사용합니다. MAXDOP [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md)는 항상 [최대 병렬 처리 수준 서버 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 재정의합니다.
>
> 데이터베이스 수준에서 이 작업을 수행하려면 **MAXDOP** [데이터베이스 범위 구성](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 사용합니다.
>
> 서버 수준에서 이 작업을 수행하려면 **MAXDOP(최대 병렬 처리 수준)** [서버 구성 옵션](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 사용합니다.

GROUP_MAX_REQUESTS = *값* 작업 그룹에서 실행할 수 있는 최대 동시 요청 수를 지정합니다. *value*는 0이거나 양의 정수여야 합니다. *값*의 기본 설정은 0이며, 무제한 요청을 허용합니다. 최대 동시 요청에 도달한 경우 해당 그룹의 사용자가 로그인할 수 있지만 지정된 값 아래로 동시 요청 수가 떨어질 때까지 사용자가 대기 상태에 배치됩니다.

USING { *pool_name* |  **"default"** } *pool_name*으로 식별된 사용자 정의 리소스 풀에 작업 그룹을 연결합니다. 그러면 실제로 리소스 풀에 작업 그룹을 넣습니다. *pool_name*이 제공되지 않거나 USING 인수가 사용되지 않으면 작업 그룹은 미리 정의된 Resource Governor 기본 풀에 배치됩니다.

"default"는 예약어이며 USING으로 사용될 경우 따옴표("") 또는 대괄호([])로 묶여야 합니다.

> [!NOTE]
> 미리 정의된 작업 그룹과 리소스 풀은 모두 "default"와 같은 소문자 이름을 사용합니다. 대/소문자 구분 데이터 정렬을 사용하는 서버의 경우 이러한 사항을 고려해야 합니다. 대/소문자 구분 데이터 정렬(예: SQL_Latin1_General_CP1_CI_AS)을 사용하는 서버는 "default"와 "Default"를 똑같이 처리합니다.

EXTERNAL external_pool_name | “기본값” **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이후).

작업 그룹은 외부 리소스 풀을 지정할 수 있습니다. 작업 그룹을 정의하고 다음 2개의 풀과 연결할 수 있습니다.

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 워크로드 및 쿼리에 대한 리소스 풀
- 외부 프로세스에 대한 외부 리소스 풀. 자세한 내용은 [sp_execute_external_script&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 참조하세요.

## <a name="remarks"></a>설명

`REQUEST_MEMORY_GRANT_PERCENT`를 사용할 경우 인덱스 생성은 성능 향상을 위해 초기에 부여된 메모리보다 많은 작업 영역 메모리를 사용할 수 있습니다. 이러한 특별 처리는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 리소스 관리자에서 지원됩니다. 그러나 초기 부여 및 추가 메모리 부여는 리소스 풀 및 작업 그룹 설정으로 제한됩니다.

`MAX_DOP` 제한은 [작업별](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)로 설정됩니다. [요청](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)별 또는 쿼리 제한별로 수행되지 않습니다. 즉, 병렬 쿼리 실행 중에 단일 요청은 [스케줄러](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)에 할당되는 여러 작업을 생성할 수 있습니다. 자세한 내용은 [스레드 및 태스크 아키텍처 가이드](../../relational-databases/thread-and-task-architecture-guide.md)를 참조하세요.

`MAX_DOP`가 사용되고 컴파일할 때 쿼리가 직렬로 표시되면 작업 그룹이나 서버 구성 설정에 관계없이 런타임에서 병렬로 다시 변경할 수 없습니다. `MAX_DOP`가 구성된 후에는 메모리 압력으로 인해서만 낮아질 수 있습니다. 작업 그룹 재구성은 부여 메모리 큐에서 대기하는 동안 표시되지 않습니다.

### <a name="index-creation-on-a-partitioned-table"></a>분할된 테이블에서 인덱스 생성

정렬되지 않은 분할된 테이블에서 인덱스 생성에 사용되는 메모리는 관련된 파티션 수에 비례합니다. 필요한 총 메모리가 Resource Governor 작업 그룹 설정에서 지정한 쿼리당 제한 `REQUEST_MAX_MEMORY_GRANT_PERCENT`를 초과하면 이 인덱스 생성이 실행되지 않을 수 있습니다. *"default"* 작업 그룹에서는 쿼리가 필요한 최소 메모리를 포함하는 쿼리당 제한을 초과하게 되므로 *"default"* 리소스 풀에 이러한 쿼리를 실행할 수 있는 총 메모리가 구성되어 있는 경우 사용자가 *"default"* 작업 그룹에서 같은 인덱스 생성을 실행할 수 있습니다.

## <a name="permissions"></a>사용 권한

`CONTROL SERVER` 권한이 필요합니다.

## <a name="example"></a>예제

Resource Governor 기본 설정을 사용하고 리소스 관리자 기본 풀에 있는 `newReports`라는 작업 그룹을 만듭니다. 예에서는 `default` 풀을 지정하지만 이 작업을 반드시 수행할 필요는 없습니다.

```sql
CREATE WORKLOAD GROUP newReports
    USING "default" ;
GO
```

## <a name="see-also"></a>참고 항목

- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)
- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](create-workload-group-transact-sql.md?view=sql-server-2017)||[SQL Database<br />관리되는 인스턴스](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)||**_\* Azure Synapse<br />분석 \*_** &nbsp;||||

&nbsp;

## <a name="azure-synapse-analytics-preview"></a>Azure Synapse Analytics(미리 보기)

워크로드 그룹을 만듭니다. 워크로드 그룹은 요청 세트에 대한 컨테이너로, 시스템에서 워크로드 관리를 구성하는 방법에 대한 기본 사항에 해당합니다. 워크로드 그룹은 워크로드 격리를 위해 리소스를 예약하고, 리소스를 포함하고, 요청별로 리소스를 정의하고, 실행 규칙을 따르도록 하는 기능을 제공합니다. 문이 완료되면 설정이 적용됩니다.

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

```
CREATE WORKLOAD GROUP group_name
 WITH
 (        MIN_PERCENTAGE_RESOURCE = value
      ,   CAP_PERCENTAGE_RESOURCE = value
      ,   REQUEST_MIN_RESOURCE_GRANT_PERCENT = value
  [ [ , ] REQUEST_MAX_RESOURCE_GRANT_PERCENT = value ]
  [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }]
  [ [ , ] QUERY_EXECUTION_TIMEOUT_SEC = value ] )
  [ ; ]
```

*group_name*</br>
워크로드 그룹을 식별하는 이름을 지정합니다. *group_name*은 sysname입니다. 최대 128자까지 가능하며 인스턴스 내에서 고유해야 합니다.

*MIN_PERCENTAGE_RESOURCE* = value</br>
이 워크로드 그룹에 대해 다른 작업 그룹과 공유되지 않도록 보장된 최소 리소스 할당을 지정합니다. *value*는 0에서 100 사이의 정수 범위입니다. 모든 워크로드 그룹에서 min_percentage_resource의 합계는 100을 초과할 수 없습니다. min_percentage_resource 값은 cap_percentage_resource보다 클 수 없습니다. 서비스 수준에 따라 허용되는 최소 유효 값이 있습니다. 자세한 내용은 [유효 값](#effective-values)을 참조하세요.

*CAP_PERCENTAGE_RESOURCE* = value</br>
워크로드 그룹의 모든 요청에 대한 최대 리소스 사용률을 지정합니다. 허용되는 정수 값의 범위는 1에서 100까지입니다. cap_percentage_resource 값은 min_percentage_resource보다 커야 합니다. 다른 워크로드 그룹에서 min_percentage_resource가 0보다 크게 구성된 경우 cap_percentage_resource의 유효 값이 줄어들 수 있습니다.

*REQUEST_MIN_RESOURCE_GRANT_PERCENT* = value</br>
요청별로 할당된 최소 리소스 크기를 설정합니다. *value*는 0.75에서 100.00 사이의 10 진수 범위에 속하는 필수 매개 변수입니다. request_min_resource_grant_percent 값은 0.25의 배수여야 하고 min_percentage_resource의 요소여야 하며, cap_percentage_resource보다 작아야 합니다. 서비스 수준에 따라 허용되는 최소 유효 값이 있습니다. 자세한 내용은 [유효 값](#effective-values)을 참조하세요.

다음은 그 예입니다.

```sql
CREATE WORKLOAD GROUP wgSample WITH
( MIN_PERCENTAGE_RESOURCE = 26              -- integer value
 ,REQUEST_MIN_RESOURCE_GRANT_PERCENT = 3.25 -- factor of 26 (guaranteed a minimum of 8 concurrency)
 ,CAP_PERCENTAGE_RESOURCE = 100 )
```

리소스 클래스에 사용되는 값을 request_min_resource_grant_percent에 대한 지침으로 간주합니다.  다음 표에서는 Gen2에 대한 리소스 할당을 포함합니다.

|리소스 클래스|리소스 비율|
|---|---|
|Smallrc|3%|
|Mediumrc|10%|
|Largerc|22%|
|Xlargerc|70%|
|||

*REQUEST_MAX_RESOURCE_GRANT_PERCENT* = value</br>
요청별로 할당된 최대 리소스 크기를 설정합니다. *value*는 기본값이 request_min_resource_grant_percent와 같은 선택적 10진수 매개 변수입니다. *value*는 request_min_resource_grant_percent보다 크거나 같아야 합니다. request_max_resource_grant_percent 값이 request_min_resource_grant_percent보다 크고, 시스템 리소스를 사용할 수 있는 경우 추가 리소스가 요청에 할당됩니다.

*IMPORTANCE* = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }</br>
워크로드 그룹에 대한 요청의 기본 중요도를 지정합니다. 중요도는 다음 중 하나이며 NORMAL이 기본값입니다.

- LOW
- BELOW_NORMAL
- NORMAL(기본값)
- ABOVE_NORMAL
- HIGH

워크로드 그룹에 설정된 중요도는 워크로드 그룹의 모든 요청에 대한 기본 중요도입니다. 또한 사용자는 분류자 수준에서 중요도를 설정할 수 있으며 이 중요도로 워크로드 그룹 중요도 설정을 재정의할 수 있습니다. 이렇게 하면 워크로드 그룹 내에서 요청의 중요도를 차별화하여 예약되지 않은 리소스에 더 빠르게 액세스할 수 있습니다. 워크로드 그룹의 min_percentage_resource 합계가 100보다 작으면 예약되지 않은 리소스가 중요도를 기준으로 할당됩니다.

*QUERY_EXECUTION_TIMEOUT_SEC* = value</br>
쿼리가 취소되기 전에 실행될 수 있는 최대 시간(초)을 지정합니다. *value*는 0 또는 양의 정수여야 합니다. value의 기본 설정인 0은 쿼리 시간이 제한되지 않음을 의미합니다. QUERY_EXECUTION_TIMEOUT_SEC는 쿼리가 큐에 대기할 때가 아니라 실행 중 상태로 전환된 후 계산됩니다.

## <a name="remarks"></a>설명

리소스 클래스에 해당하는 워크로드 그룹은 이전 버전과의 호환성을 위해 자동으로 만들어집니다. 이러한 시스템 정의 워크로드 그룹은 삭제할 수 없습니다. 추가로 8개의 사용자 정의 워크로드 그룹을 만들 수 있습니다.

min_percentage_resource가 0보다 큰 워크로드 그룹이 생성되면 `CREATE WORKLOAD GROUP` 문은 워크로드 그룹을 만들 충분한 리소스가 있을 때까지 큐에 대기합니다.

## <a name="effective-values"></a>유효 값

min_percentage_resource, cap_percentage_resource, request_min_resource_grant_percent 및 request_max_resource_grant_percent 매개 변수에는 현재 서비스 수준의 컨텍스트 및 다른 워크로드 그룹의 구성에서 조정되는 유효 값이 있습니다.

서비스 수준별로 지원되는 동시성은 리소스 클래스를 사용하여 쿼리당 리소스 허용을 정의할 때와 동일하게 유지됩니다. 따라서 request_min_resource_grant_percent에 대해 지원되는 값은 인스턴스가 설정된 서비스 수준에 따라 달라집니다. 가장 낮은 서비스 수준인 DW100c에서는 요청당 최소 25% 리소스가 필요합니다. DW100c에서 구성된 워크로드 그룹의 유효 request_min_resource_grant_percent는 25% 이상일 수 있습니다. 유효 값이 파생되는 방법에 대한 자세한 내용은 아래 표를 참조하세요.

|서비스 수준|REQUEST_MIN_RESOURCE_GRANT_PERCENT에 대한 가장 낮은 유효 값|최대 동시 쿼리 수|
|---|---|---|
|DW100c|25%|4|
|DW200c|12.5%|8|
|DW300c|8%|12|
|DW400c|6.25%|16|
|DW500c|5%|20|
|DW1000c|3%|32|
|DW1500c|3%|32|
|DW2000c|2%|48|
|DW2500c|2%|48|
|DW3000c|1.5%|64|
|DW5000c|1.5%|64|
|DW6000c|0.75%|128|
|DW7500c|0.75%|128|
|DW10000c|0.75%|128|
|DW15000c|0.75%|128|
|DW30000c|0.75%|128|
||||

마찬가지로 request_min_resource_grant_percent, min_percentage_resource는 유효 request_min_resource_grant_percent보다 크거나 같아야 합니다. 유효 min_percentage_resource보다 작게 min_percentage_resource가 구성된 워크로드 그룹은 값이 런타임에 0으로 조정됩니다. 이 경우 min_percentage_resource에 대해 구성된 리소스를 모든 워크로드 그룹에서 공유할 수 있습니다. 예를 들어, DW1000c에서 10%의 min_percentage_resource가 실행되는 워크로드 그룹 wgAdHoc은 유효 min_percentage_resource가 10%입니다(3.25%는 DW1000c에서 지원되는 최솟값임). DW100c에서 wgAdhoc의 유효 min_percentage_resource는 0%입니다. wgAdhoc에 대해 구성된 10%는 모든 워크로드 그룹에서 공유됩니다.

Cap_percentage_resource에도 유효 값이 있습니다. 워크로드 그룹 wgAdhoc이 100%의 cap_percentage_resource로 구성되고 다른 워크로드 그룹 wgDashboards가 25%의 min_percentage_resource로 생성되면 wgAdhoc의 유효 cap_percentage_resource는 75%가 됩니다.

워크로드 그룹에 대한 런타임 값을 이해하는 가장 쉬운 방법은 시스템 보기 [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md)를 쿼리하는 것입니다.

## <a name="permissions"></a>사용 권한

CONTROL DATABASE 권한이 필요합니다.

## <a name="see-also"></a>참고 항목

- [DROP WORKLOAD GROUP(Transact-SQL)](drop-workload-group-transact-sql.md)
- [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md)
- [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md)
- [워크로드 그룹](https://docs.microsoft.com/azure/sql-data-warehouse/quickstart-configure-workload-isolation-tsql)을 만들고 사용하는 방법에 대한 빠른 시작

::: moniker-end
