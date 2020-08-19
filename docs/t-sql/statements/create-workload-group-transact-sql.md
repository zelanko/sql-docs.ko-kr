---
description: CREATE WORKLOAD GROUP(Transact-SQL)
title: CREATE WORKLOAD GROUP(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/27/2020
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
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: 67106682f9302c7849b8f5523e88aa1dd2aa4475
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444747"
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP(Transact-SQL)

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [SQL Database<br />Managed Instance](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](create-workload-group-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server-and-sql-managed-instance"></a>SQL Server 및 SQL Managed Instance

[!INCLUDE [CREATE WORKLOAD GROUP](../../includes/create-workload-group.md)]
  
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](create-workload-group-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        **_\* SQL Database<br />Managed Instance \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](create-workload-group-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server-and-sql-managed-instance"></a>SQL Server 및 SQL Managed Instance

[!INCLUDE [CREATE WORKLOAD GROUP](../../includes/create-workload-group.md)]

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](create-workload-group-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [SQL Database<br />Managed Instance](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        **_\* Azure Synapse<br />Analytics \*_** &nbsp;
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-synapse-analytics"></a>Azure Synapse Analytics

워크로드 그룹을 만듭니다. 워크로드 그룹은 요청 세트에 대한 컨테이너로, 시스템에서 워크로드 관리를 구성하는 방법에 대한 기본 사항에 해당합니다. 워크로드 그룹은 워크로드 격리를 위해 리소스를 예약하고, 리소스를 포함하고, 요청별로 리소스를 정의하고, 실행 규칙을 따르도록 하는 기능을 제공합니다. 문이 완료되면 설정이 적용됩니다.

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

```syntaxsql
CREATE WORKLOAD GROUP group_name
 WITH
 (   MIN_PERCENTAGE_RESOURCE = value 
   , CAP_PERCENTAGE_RESOURCE = value 
   , REQUEST_MIN_RESOURCE_GRANT_PERCENT = value
  [ [ , ] REQUEST_MAX_RESOURCE_GRANT_PERCENT = value ]
  [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH } ]
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
CREATE WORKLOAD GROUP wgSample 
WITH
  ( MIN_PERCENTAGE_RESOURCE = 26                -- integer value
    , REQUEST_MIN_RESOURCE_GRANT_PERCENT = 3.25 -- factor of 26 (guaranteed a minimum of 8 concurrency)
    , CAP_PERCENTAGE_RESOURCE = 100 )
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

*IMPORTANCE* = { LOW \| BELOW_NORMAL \| NORMAL \| ABOVE_NORMAL \| HIGH }</br>        
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

`min_percentage_resource`가 0보다 큰 작업 그룹이 생성되면 `CREATE WORKLOAD GROUP` 문은 작업 그룹을 만들 충분한 리소스가 있을 때까지 큐에 대기합니다.

## <a name="effective-values"></a>유효 값

`min_percentage_resource`, `cap_percentage_resource`, `request_min_resource_grant_percent` 및 `request_max_resource_grant_percent` 매개 변수에는 현재 서비스 수준의 컨텍스트에서 조정된 유효 값과 다른 작업 그룹의 구성이 포함됩니다.

서비스 수준에 따라 쿼리당 최소 리소스가 필요하기 때문에 `request_min_resource_grant_percent` 매개 변수에는 유효한 값이 있습니다.  예를 들어 가장 낮은 서비스 수준인 DW100c에서는 요청당 최소 25% 리소스가 필요합니다.  작업 그룹이 3% `request_min_resource_grant_percent` 및 `request_max_resource_grant_percent`로 구성된 경우 인스턴스가 시작될 때 두 매개 변수의 유효 값이 25%로 조정됩니다.  인스턴스가 DW1000c로 확장되는 경우 두 매개 변수에 구성되는 유효 값은 3%입니다. 해당 서비스 수준에 지원되는 최소 값이 3%이기 때문입니다.  인스턴스가 DW1000c보다 높게 확장되는 경우 두 매개 변수에 대해 구성되는 유효 값은 3%로 유지됩니다.  각 서비스 수준의 유효 값에 대한 자세한 내용은 아래 표를 참조하세요.

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

`min_percentage_resource` 매개 변수는 유효 `request_min_resource_grant_percent`보다 크거나 같아야 합니다. `min_percentage_resource`가 유효 `min_percentage_resource`보다 작게 구성된 작업 그룹은 값이 런타임에 0으로 조정됩니다. 이 경우 `min_percentage_resource`에 대해 구성된 리소스를 모든 작업 그룹에서 공유할 수 있습니다. 예를 들어 DW1000c에서 10%의 `min_percentage_resource`가 실행되는 작업 그룹 `wgAdHoc`은 유효 `min_percentage_resource`가 10%입니다(3%는 DW1000c에서 지원되는 최솟값임). DW100c에서 `wgAdhoc`의 유효 min_percentage_resource는 0%입니다. `wgAdhoc`에 대해 구성된 10%는 모든 작업 그룹에서 공유됩니다.

또한 `cap_percentage_resource` 매개 변수는 유효 값을 가집니다. 작업 그룹 `wgAdhoc`이 100%의 `cap_percentage_resource`로 구성되고 다른 작업 그룹 `wgDashboards`가 25%의 `min_percentage_resource`로 생성된 경우 `wgAdhoc`의 유효 `cap_percentage_resource`는 75%가 됩니다.

워크로드 그룹에 대한 런타임 값을 이해하는 가장 쉬운 방법은 시스템 보기 [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md)를 쿼리하는 것입니다.

## <a name="permissions"></a>사용 권한

`CONTROL DATABASE` 권한이 필요합니다.

## <a name="see-also"></a>참고 항목

- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](drop-workload-group-transact-sql.md)
- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](alter-workload-group-transact-sql.md)
- [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md)
- [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md)
- [빠른 시작: T-SQL을 사용하여 워크로드 격리 구성](/azure/sql-data-warehouse/quickstart-configure-workload-isolation-tsql)

::: moniker-end
