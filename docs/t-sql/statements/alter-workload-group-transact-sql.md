---
description: ALTER WORKLOAD GROUP(Transact-SQL)
title: ALTER WORKLOAD GROUP(Transact-SQL)
ms.custom: ''
ms.date: 05/05/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_WORKLOAD_GROUP_TSQL
- ALTER WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER WORKLOAD GROUP statement
ms.assetid: 957addce-feb0-4e54-893e-5faca3cd184c
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: acbd75ed614f6f7a2c018fb537b01528fe166e80
ms.sourcegitcommit: d35d0901296580bfceda6e0ab2e14cf2b7e99a0f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92496964"
---
# <a name="alter-workload-group-transact-sql"></a>ALTER WORKLOAD GROUP(Transact-SQL)

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [SQL Managed Instance](alter-workload-group-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-workload-group-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server-and-sql-managed-instance"></a>SQL Server 및 SQL Managed Instance

[!INCLUDE [ALTER WORKLOAD GROUP](../../includes/alter-workload-group.md)]
  
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-workload-group-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        **_\* SQL Managed Instance \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-workload-group-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server-and-sql-managed-instance"></a>SQL Server 및 SQL Managed Instance

[!INCLUDE [ALTER WORKLOAD GROUP](../../includes/alter-workload-group.md)]

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-workload-group-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [SQL Managed Instance](alter-workload-group-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        **_\* Azure Synapse<br />Analytics \*_** &nbsp;
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-synapse-analytics"></a>Azure Synapse Analytics

기존 작업 그룹을 변경합니다.

실행 중이거나 대기 중인 요청이 있는 시스템에서 `ALTER WORKLOAD GROUP`이 동작하는 방법에 대한 자세한 내용은 아래의 `ALTER WORKLOAD GROUP` 동작 섹션을 참조하세요. 

[작업 그룹 만들기](create-workload-group-transact-sql.md)에 대한 제한 사항은 `ALTER WORKLOAD GROUP`에도 적용됩니다.  매개 변수를 수정하기 전에 [workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md)를 쿼리하여 값이 허용 범위 내에 있는지 확인합니다.

## <a name="syntax"></a>구문

```syntaxsql
ALTER WORKLOAD GROUP group_name
 WITH
 ([       MIN_PERCENTAGE_RESOURCE = value ]
  [ [ , ] CAP_PERCENTAGE_RESOURCE = value ]
  [ [ , ] REQUEST_MIN_RESOURCE_GRANT_PERCENT = value ]
  [ [ , ] REQUEST_MAX_RESOURCE_GRANT_PERCENT = value ] 
  [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }]
  [ [ , ] QUERY_EXECUTION_TIMEOUT_SEC = value ] )
  [ ; ]
  ```

## <a name="arguments"></a>인수

group_name  
변경되는 기존 사용자 정의 작업 그룹의 이름입니다.  group_name은 변경할 수 없습니다. 

MIN_PERCENTAGE_RESOURCE = value  
value는 0에서 100 사이의 정수 범위입니다.  min_percentage_resource를 변경하는 경우 모든 작업 그룹의 min_percentage_resource 합계는 100을 초과할 수 없습니다.  min_percentage_resource를 변경하려면 명령이 완료되기 전에 실행 중인 모든 쿼리가 작업 그룹에서 완료되어야 합니다.  자세한 내용은 이 문서의 ALTER WORKLOAD GROUP 동작 섹션을 참조하세요.

CAP_PERCENTAGE_RESOURCE = value  
value는 1에서 100 사이의 정수 범위입니다.  cap_percentage_resource 값은 min_percentage_resource보다 커야 합니다.  cap_percentage_resource를 변경하려면 명령이 완료되기 전에 실행 중인 모든 쿼리가 작업 그룹에서 완료되어야 합니다.  자세한 내용은 이 문서의 ALTER WORKLOAD GROUP 동작 섹션을 참조하세요. 

REQUEST_MIN_RESOURCE_GRANT_PERCENT = value  
value는 0.75에서 100.00 사이의 범위에 해당하는 10진수입니다.  request_min_resource_grant_percent 값은 min_percentage_resource의 요소여야 하며, cap_percentage_resource보다 작아야 합니다. 
  
REQUEST_MAX_RESOURCE_GRANT_PERCENT = value  
value는 10진수이며 request_min_resource_grant_percent보다 커야 합니다.

IMPORTANCE = { LOW \|  BELOW_NORMAL \| NORMAL \| ABOVE_NORMAL \| HIGH }  
워크로드 그룹에 대한 요청의 기본 중요도를 변경합니다.

QUERY_EXECUTION_TIMEOUT_SEC = value  
쿼리가 취소되기 전에 실행될 수 있는 최대 시간(초)을 변경합니다. value는 0 또는 양의 정수여야 합니다. value의 기본 설정인 0은 무제한을 의미합니다.   

## <a name="permissions"></a>사용 권한

CONTROL DATABASE 권한이 필요합니다.

## <a name="example"></a>예제

아래 예제에서는 wgDataLoads에 대한 카탈로그 뷰의 값을 확인하고 값을 변경합니다.

```sql
SELECT *
FROM sys.workload_management_workload_groups  
WHERE [name] = 'wgDataLoads'

ALTER WORKLOAD GROUP wgDataLoads WITH
( MIN_PERCENTAGE_RESOURCE            = 40
 ,CAP_PERCENTAGE_RESOURCE            = 80
 ,REQUEST_MIN_RESOURCE_GRANT_PERCENT = 10 )
 ```

## <a name="alter-workload-group-behavior"></a>ALTER WORKLOAD GROUP 동작

특정 시점에 시스템에는 3가지 형식의 요청이 있습니다.
- 아직 분류되지 않은 요청
- 개체 잠금이나 시스템 리소스에 대해 분류되고 대기 중인 요청
- 분류되고 실행 중인 요청

변경 중인 작업 그룹의 속성을 기반으로 설정이 적용되는 타이밍은 다릅니다.

**중요도 또는 query_execution_timeout** 중요도 및 query_execution_timeout 속성의 경우 분류되지 않은 요청은 새 구성 값을 선택합니다.  대기 및 실행 중인 요청은 이전 구성으로 실행됩니다.  작업 그룹에서 실행 중인 쿼리가 있는지에 관계없이 `ALTER WORKLOAD GROUP` 요청이 즉시 실행됩니다.

**Request_min_resource_grant_percent or request_max_resource_grant_percent** request_min_resource_grant_percent 및 request_max_resource_grant_percent의 경우 실행 중인 요청은 이전 구성으로 실행됩니다.  대기 중인 요청 및 분류되지 않은 요청은 새 구성 값을 선택합니다.  작업 그룹에서 실행 중인 쿼리가 있는지에 관계없이 `ALTER WORKLOAD GROUP` 요청이 즉시 실행됩니다.

**Min_percentage_resource or cap_percentage_resource** min_percentage_resource 및 cap_percentage_resource의 경우 실행 중인 요청은 이전 구성으로 실행됩니다.  대기 중인 요청 및 분류되지 않은 요청은 새 구성 값을 선택합니다. 

Min_percentage_resource 및 cap_percentage_resource를 변경하려면 변경 중인 작업 그룹에서 실행 중인 요청을 드레이닝해야 합니다.  Min_percentage_resource를 줄이면 다른 작업 그룹의 요청에서 활용할 수 있도록 해제된 리소스가 공유 풀로 반환됩니다.  반대로 min_percentage_resource를 늘리면 공유 풀에서 필요한 리소스만 활용하여 요청이 완료될 때까지 대기합니다.  Alter 작업 그룹 작업은 공유 풀에서 실행 대기 중인 다른 요청보다 공유 리소스로 액세스하도록 우선 순위를 지정합니다.  Min_percentage_resource 합계가 100%를 초과하면 ALTER WORKLOAD GROUP 요청이 즉시 실패합니다. 

**잠금 동작** 작업 그룹을 변경하려면 모든 작업 그룹에 대해 전역 잠금이 필요합니다.  작업 그룹 변경 요청은 큐에서 이미 제출된 작업 그룹 요청 만들기 또는 삭제 요청 뒤에 위치합니다.  변경 문의 일괄 처리가 한 번에 제출되는 경우 전송된 순서대로 처리됩니다.  

## <a name="see-also"></a>참고 항목

- [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](create-workload-group-transact-sql.md)
- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](drop-workload-group-transact-sql.md)
- [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md)
- [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md)
- [빠른 시작: T-SQL을 사용하여 워크로드 격리 구성](/azure/sql-data-warehouse/quickstart-configure-workload-isolation-tsql)

::: moniker-end
