---
title: Dmv를 사용 하 여 Python 및 R 스크립트 실행 모니터링
description: Dmv (동적 관리 뷰)를 사용 하 여 SQL Server Machine Learning Services에서 Python 및 R 외부 스크립트 실행을 모니터링할 수 있습니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0e541e1d0eb2a8bb1ac512276fa395f8d8c6379f
ms.sourcegitcommit: 1c3f56deaa4c1ffbe5d7f75752ebe10447c3e7af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "70978400"
---
# <a name="monitor-sql-server-machine-learning-services-using-dynamic-management-views-dmvs"></a>Dmv (동적 관리 뷰)를 사용 하 여 SQL Server Machine Learning Services 모니터링
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Dmv (동적 관리 뷰)를 사용 하 여 외부 스크립트 (Python 및 R)의 실행을 모니터링 하 고, 사용 되는 리소스를 모니터링 하 고, 문제를 진단 하 고, SQL Server Machine Learning Services에서 성능을 조정 합니다.

이 문서에서는 SQL Server Machine Learning Services와 관련 된 Dmv를 찾을 수 있습니다. 또한 다음을 보여 주는 예제 쿼리를 찾을 수 있습니다.

+ 기계 학습에 대 한 설정 및 구성 옵션
+ 외부 Python 또는 스크립트를 실행 하는 활성 세션
+ Python 및 R에 대 한 외부 런타임에 대 한 실행 통계
+ 외부 스크립트에 대 한 성능 카운터
+ OS, SQL Server 및 외부 리소스 풀의 메모리 사용량
+ SQL Server 및 외부 리소스 풀에 대 한 메모리 구성
+ 외부 리소스 풀을 포함 하 여 리소스 풀 Resource Governor
+ Python 및 R에 대 한 설치 된 패키지

Dmv에 대 한 일반적인 정보는 [시스템 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)를 참조 하세요.

> [!TIP]
> 사용자 지정 보고서를 사용 하 여 SQL Server Machine Learning Services을 모니터링할 수도 있습니다. 자세한 내용은 [Management Studio에서 사용자 지정 보고서를 사용 하 여 기계 학습 모니터링](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)을 참조 하세요.

## <a name="dynamic-management-views"></a>동적 관리 뷰

SQL Server에서 기계 학습 워크 로드를 모니터링 하는 경우 다음과 같은 동적 관리 뷰를 사용할 수 있습니다. Dmv를 쿼리하려면 인스턴스에 대 한 사용 `VIEW SERVER STATE` 권한이 필요 합니다.

| 동적 관리 뷰 | type | 설명 |
|-------------------------|------|-------------|
| [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | 실행 | 외부 스크립트를 실행 중인 각 활성 작업자 계정 행을 반환합니다. |
| [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) | 실행 | 외부 스크립트 요청의 각 유형에 대해 하나의 행을 반환합니다. |
| [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) | 실행 | 서버에서 유지되는 각 성능 카운터에 대해 행을 반환합니다. 검색 조건을 `WHERE object_name LIKE '%External Scripts%'`사용 하는 경우이 정보를 사용 하 여 실행 된 스크립트 수, 인증 모드를 사용 하 여 실행 된 스크립트 또는 전체 인스턴스에서 실행 된 R 또는 Python 호출 수를 확인할 수 있습니다. |
| [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) | 리소스 관리자 | Resource Governor의 현재 외부 리소스 풀 상태, 리소스 풀의 현재 구성 및 리소스 풀 통계에 대 한 정보를 반환 합니다. |
| [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md) | 리소스 관리자 | Resource Governor의 현재 외부 리소스 풀 구성에 대 한 CPU 선호도 정보를 반환 합니다. 각 스케줄러가 개별 프로세서에 매핑되는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]의 스케줄러당 하나의 행을 반환합니다. 이 뷰를 사용하여 스케줄러 상태를 모니터링하거나 런어웨이 태스크를 식별할 수 있습니다. |

인스턴스를 모니터링 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 하는 방법에 대 한 자세한 내용은 [카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) 및 [Resource Governor 관련 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)를 참조 하세요.

## <a name="settings-and-configuration"></a>설정 및 구성

Machine Learning Services 설치 설정 및 구성 옵션을 확인 합니다.

![설정 및 구성 쿼리의 출력](media/dmv-settings-and-configuration.png "설정 및 구성 쿼리의 출력")

이 출력을 가져오려면 아래 쿼리를 실행 합니다. 사용 되는 뷰 및 함수에 대 한 자세한 내용은 [sys.dm_server_registry](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md), [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md)및를 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)참조 하세요.

```sql
SELECT CAST(SERVERPROPERTY('IsAdvancedAnalyticsInstalled') AS INT) AS IsMLServicesInstalled
    , CAST(value_in_use AS INT) AS ExternalScriptsEnabled
    , COALESCE(SIGN(SUSER_ID(CONCAT (
                    CAST(SERVERPROPERTY('MachineName') AS NVARCHAR(128))
                    , '\SQLRUserGroup'
                    , CAST(serverproperty('InstanceName') AS NVARCHAR(128))
                    ))), 0) AS ImpliedAuthenticationEnabled
    , COALESCE((
            SELECT CAST(r.value_data AS INT)
            FROM sys.dm_server_registry AS r
            WHERE r.registry_key LIKE 'HKLM\Software\Microsoft\Microsoft SQL Server\%\SuperSocketNetLib\Tcp'
            AND r.value_name = 'Enabled'
            ), - 1) AS IsTcpEnabled
FROM sys.configurations
WHERE name = 'external scripts enabled';
```

쿼리에서 반환 되는 열은 다음과 같습니다.

| Column | 설명 |
|--------|-------------|
| IsMLServicesInstalled | 인스턴스에 대해 Machine Learning Services SQL Server 설치 된 경우 1을 반환 합니다. 그렇지 않으면 0을 반환 합니다. |
| ExternalScriptsEnabled | 인스턴스에 대해 외부 스크립트를 사용 하는 경우 1을 반환 합니다. 그렇지 않으면 0을 반환 합니다. |
| ImpliedAuthenticationEnabled | 묵시적 인증을 사용 하는 경우 1을 반환 합니다. 그렇지 않으면 0을 반환 합니다. SQLRUserGroup에 대 한 로그인이 있는지 확인 하 여 묵시적 인증에 대 한 구성을 확인 합니다. |
| IsTcpEnabled | 인스턴스에 대해 TCP/IP 프로토콜을 사용 하는 경우 1을 반환 합니다. 그렇지 않으면 0을 반환 합니다. 자세한 내용은 [기본 SQL Server 네트워크 프로토콜 구성](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md)을 참조 하세요. |

## <a name="active-sessions"></a>Active sessions

외부 스크립트를 실행 중인 활성 세션을 확인 합니다.

![활성 설정 쿼리의 출력](media/dmv-active-sessions.png "활성 설정 쿼리의 출력")

이 출력을 가져오려면 아래 쿼리를 실행 합니다. 사용 되는 동적 관리 뷰에 대 한 자세한 내용은 [_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md), [_exec_sessions 및 sys. dm](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) [를 참조](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)하세요.

```sql
SELECT r.session_id, r.blocking_session_id, r.status, DB_NAME(s.database_id) AS database_name
    , s.login_name, r.wait_time, r.wait_type, r.last_wait_type, r.total_elapsed_time, r.cpu_time
    , r.reads, r.logical_reads, r.writes, er.language, er.degree_of_parallelism, er.external_user_name
FROM sys.dm_exec_requests AS r
INNER JOIN sys.dm_external_script_requests AS er
ON r.external_script_request_id = er.external_script_request_id
INNER JOIN sys.dm_exec_sessions AS s
ON s.session_id = r.session_id;
```

쿼리에서 반환 되는 열은 다음과 같습니다.

| Column | 설명 |
|--------|-------------|
| session_id | 각각의 기본 활성 연결과 연결된 세션을 식별합니다. |
| blocking_session_id | 요청을 차단하고 있는 세션의 ID입니다. 이 열이 NULL이면 요청이 차단되지 않거나 차단 세션의 세션 정보를 사용할 수 없습니다(또는 식별할 수 없음). |
| 상태 | 요청의 상태입니다. |
| database_name | 각 세션에 대 한 현재 데이터베이스의 이름입니다. |
| login_name | 세션이 현재 실행 되 고 있는 SQL Server 로그인 이름입니다. |
| wait_time | 요청이 현재 차단된 경우 이 열은 현재 대기의 기간(밀리초)을 반환합니다. Null을 허용하지 않습니다. |
| wait_type | 요청이 현재 차단된 경우 이 열은 대기 유형을 반환합니다. 대기 유형에 대 한 자세한 내용은 [_os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)를 참조 하세요. |
| last_wait_type | 이 요청이 이전에 차단된 경우 이 열은 마지막 대기의 유형을 반환합니다. |
| total_elapsed_time | 요청이 도착한 이후 경과한 총 시간(밀리초)입니다. |
| cpu_time | 요청에 사용된 CPU 시간(밀리초)입니다. |
| reads | 이 요청에서 수행된 읽기 수입니다. |
| logical_reads | 요청에서 수행된 논리적 읽기 수입니다. |
| writes | 이 요청에서 수행된 쓰기 수입니다. |
| language | 지원되는 스크립트 언어를 나타내는 키워드입니다. |
| degree_of_parallelism | 생성된 병렬 프로세스의 수를 나타내는 숫자입니다. 이 값은 요청된 병렬 프로세스의 수와 다를 수 있습니다. |
| external_user_name | 스크립트가 실행된 Windows 작업자 계정입니다. |

## <a name="execution-statistics"></a>실행 통계

R 및 Python에 대 한 외부 런타임에 대 한 실행 통계를 확인 합니다. RevoScaleR, revoscalepy 또는 microsoftml package 함수의 통계만 현재 사용할 수 있습니다.

![실행 통계 쿼리의 출력](media/dmv-execution-statistics.png "실행 통계 쿼리의 출력")

이 출력을 가져오려면 아래 쿼리를 실행 합니다. 사용 되는 동적 관리 뷰에 대 한 자세한 [내용은 참조 하십시오.](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 이 쿼리는 두 번 이상 실행 된 함수만 반환 합니다.

```sql
SELECT language, counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE counter_value > 0
ORDER BY language, counter_name;
```

쿼리에서 반환 되는 열은 다음과 같습니다.

| Column | 설명 |
|--------|-------------|
| language | 등록된 외부 스크립트 언어의 이름입니다. |
| counter_name | 등록된 외부 스크립트 함수의 이름입니다. |
| counter_value | 서버에서 등록된 외부 스크립트 함수를 호출한 총 인스턴스 수입니다. 이 값은 누적되며, 인스턴스에 기능이 설치된 시간부터 시작되어 다시 설정할 수 없습니다. |

## <a name="performance-counters"></a>성능 카운터

외부 스크립트 실행과 관련 된 성능 카운터를 확인 합니다.

![성능 카운터 쿼리의 출력](media/dmv-performance-counters.png "성능 카운터 쿼리의 출력")

이 출력을 가져오려면 아래 쿼리를 실행 합니다. 사용 되는 동적 관리 뷰에 대 한 자세한 내용은 [_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)를 참조 하세요.

```sql
SELECT counter_name, cntr_value
FROM sys.dm_os_performance_counters 
WHERE object_name LIKE '%External Scripts%'
```

**_os_performance_counters** 는 외부 스크립트에 대해 다음과 같은 성능 카운터를 출력 합니다.

| 카운터 | 설명 |
|---------|-------------|
| 모든 실행 | 로컬 또는 원격 호출로 시작 되는 외부 프로세스의 수입니다. |
| 병렬 실행 | 스크립트가  _\@병렬_ 쿼리 계획을 생성 하 고 사용할 수 있는 병렬 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 사양을 포함 하는 횟수입니다. |
| 스트림 실행 | 스트리밍 기능이 호출 된 횟수입니다. |
| SQL CC 실행 | 호출이 원격으로 인스턴스화되어 SQL Server 계산 컨텍스트로 사용 된 외부 스크립트 실행 수입니다. |
| 묵시적 인증 로그인 | 암시적 인증을 사용 하 여 ODBC 루프백 호출을 수행한 횟수 즉,는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 스크립트 요청을 보내는 사용자를 대신 하 여 호출을 실행 했습니다. |
| 총 실행 시간(ms) | 호출 및 호출 완료 사이에 경과 된 시간입니다. |
| 실행 오류 | 스크립트에서 오류를 보고 한 횟수입니다. 이 수에는 R 또는 Python 오류가 포함 되지 않습니다. |

## <a name="memory-usage"></a>메모리 사용

OS, SQL Server 및 외부 풀에서 사용 하는 메모리에 대 한 정보를 확인 합니다.

![메모리 사용량 쿼리의 출력](media/dmv-memory-usage.png "메모리 사용량 쿼리의 출력")

이 출력을 가져오려면 아래 쿼리를 실행 합니다. 사용 되는 동적 관리 뷰에 대 한 자세한 내용은 [_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) 및 [_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)를 참조 하세요.

```sql
SELECT physical_memory_kb, committed_kb
    , (SELECT SUM(peak_memory_kb)
        FROM sys.dm_resource_governor_external_resource_pools AS ep
        ) AS external_pool_peak_memory_kb
FROM sys.dm_os_sys_info;
```

쿼리에서 반환 되는 열은 다음과 같습니다.

| Column | 설명 |
|--------|-------------|
| physical_memory_kb | 컴퓨터에 있는 실제 메모리의 총 크기입니다. |
| committed_kb | 메모리 관리자에서 커밋된 메모리 (KB)입니다. 메모리 관리자의 예약된 메모리는 포함하지 않습니다. |
| external_pool_peak_memory_kb | 모든 외부 리소스 풀에 사용 되는 최대 메모리 양 (kb)의 합계입니다. |

## <a name="memory-configuration"></a>메모리 구성

SQL Server 및 외부 리소스 풀의 최대 메모리 구성에 대 한 정보를 표시 합니다. SQL Server 기본값 `max server memory (MB)`을 사용 하 여 실행 되는 경우 OS 메모리의 100%로 간주 됩니다.

![메모리 구성 쿼리의 출력](media/dmv-memory-configuration.png "메모리 구성 쿼리의 출력")

이 출력을 가져오려면 아래 쿼리를 실행 합니다. 사용 되는 보기에 대 한 자세한 내용은 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 및 [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)을 참조 하십시오.

```sql
SELECT 'SQL Server' AS name
    , CASE CAST(c.value AS BIGINT)
        WHEN 2147483647 THEN 100
        ELSE (SELECT CAST(c.value AS BIGINT) / (physical_memory_kb / 1024.0) * 100 FROM sys.dm_os_sys_info)
        END AS max_memory_percent
FROM sys.configurations AS c
WHERE c.name LIKE 'max server memory (MB)'
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name, ep.max_memory_percent
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

쿼리에서 반환 되는 열은 다음과 같습니다.

| Column | 설명 |
|--------|-------------|
| name | 외부 리소스 풀 또는 SQL Server의 이름입니다. |
| max_memory_percent | SQL Server 또는 외부 리소스 풀에서 사용할 수 있는 최대 메모리입니다. |

## <a name="resource-pools"></a>리소스 풀

[SQL Server Resource Governor](../../relational-databases/resource-governor/resource-governor.md)에서 [리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md) 은 인스턴스의 물리적 리소스의 하위 집합을 나타냅니다. 외부 스크립트 실행을 포함 하 여 들어오는 응용 프로그램 요청이 리소스 풀 내에서 사용할 수 있는 CPU, 물리적 IO 및 메모리 양에 대 한 제한을 지정할 수 있습니다. SQL Server 및 외부 스크립트에 사용 되는 리소스 풀을 확인 합니다.

![리소스 풀 쿼리의 출력](media/dmv-resource-pools.png "리소스 풀 쿼리의 출력")

이 출력을 가져오려면 아래 쿼리를 실행 합니다. 사용 되는 동적 관리 뷰에 대 한 자세한 내용은 [_resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md) 및 [_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)를 참조 하세요.

```sql
SELECT CONCAT ('SQL Server - ', p.name) AS pool_name
    , p.total_cpu_usage_ms, p.read_io_completed_total, p.write_io_completed_total
FROM sys.dm_resource_governor_resource_pools AS p
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name
    , ep.total_cpu_user_ms, ep.read_io_count, ep.write_io_count
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

쿼리에서 반환 되는 열은 다음과 같습니다.

| Column | 설명 |
|--------|-------------|
| pool_name | 리소스 풀의 이름입니다. SQL Server 리소스 풀에는 접두사가 `SQL Server` 있고 외부 리소스 풀에는 `External Pool`접두사가 붙습니다.
| total_cpu_usage_hours | 리소스 Govenor 통계가 다시 설정 된 이후의 누적 CPU 사용량 (밀리초)입니다. |
| read_io_completed_total | 리소스 관리자 통계를 다시 설정한 후 완료된 총 읽기 IO입니다. |
| write_io_completed_total | 리소스 관리자 통계를 다시 설정한 후 완료된 총 쓰기 IO입니다. |

## <a name="installed-packages"></a>설치 된 패키지

이러한를 출력 하는 R 또는 Python 스크립트를 실행 하 여 SQL Server Machine Learning Services에 설치 된 R 및 Python 패키지를 볼 수 있습니다.

### <a name="installed-packages-for-r"></a>R에 대 한 설치 된 패키지

SQL Server Machine Learning Services에 설치 된 R 패키지를 확인 합니다.

![R 쿼리에 대해 설치 된 패키지의 출력](media/dmv-installed-packages-r.png "R 쿼리에 대해 설치 된 패키지의 출력")

이 출력을 가져오려면 아래 쿼리를 실행 합니다. 이 쿼리는 R 스크립트를 사용 하 여 SQL Server와 함께 설치 된 R 패키지를 확인 합니다.

```sql
EXEC sp_execute_external_script @language = N'R'
, @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
    , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
```

반환 되는 열은 다음과 같습니다.

| Column | 설명 |
|--------|-------------|
| 패키지 | 설치 된 패키지의 이름입니다. |
| 버전 | 패키지의 버전입니다. |
| 종속 | 설치 된 패키지가 종속 된 패키지를 나열 합니다. |
| 라이선스 | 설치 된 패키지에 대 한 라이선스. |
| LibPath | 패키지를 찾을 수 있는 디렉터리입니다. |

### <a name="installed-packages-for-python"></a>Python 용 설치 된 패키지

SQL Server Machine Learning Services에 설치 된 Python 패키지를 확인 합니다.

![설치 된 Python 용 패키지 쿼리 출력](media/dmv-installed-packages-python.png "설치 된 Python 용 패키지 쿼리 출력")

이 출력을 가져오려면 아래 쿼리를 실행 합니다. 이 쿼리는 Python 스크립트를 사용 하 여 SQL Server와 함께 설치 되는 Python 패키지를 확인 합니다.

```sql
EXEC sp_execute_external_script @language = N'Python'
, @script = N'
import pip
OutputDataSet = pandas.DataFrame([(i.key, i.version, i.location) for i in pip.get_installed_distributions()])'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128), Location NVARCHAR(1000)));
```

반환 되는 열은 다음과 같습니다.

| Column | 설명 |
|--------|-------------|
| 패키지 | 설치 된 패키지의 이름입니다. |
| 버전 | 패키지의 버전입니다. |
| 위치 | 패키지를 찾을 수 있는 디렉터리입니다. |

## <a name="next-steps"></a>다음 단계

+ [기계 학습 솔루션 관리 및 모니터링](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
+ [기계 학습에 대 한 확장 이벤트](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)
+ [Resource Governor 관련 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)
+ [시스템 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [Management Studio에서 사용자 지정 보고서를 사용 하 여 기계 학습 모니터링](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)
