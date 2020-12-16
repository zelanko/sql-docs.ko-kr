---
description: CREATE EXTERNAL RESOURCE POOL(Transact-SQL)
title: CREATE EXTERNAL RESOURCE POOL(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning-services
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL RESOURCE POOL
- CREATE EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE POOL
- EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE
- EXTERNAL_RESOURCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL RESOURCE POOL statement
ms.assetid: 8cc798ad-c395-461c-b7ff-8c561c098808
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 2b4cd2af87ec181766ab98c9d1483ee6425e51e6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438998"
---
# <a name="create-external-resource-pool-transact-sql"></a>CREATE EXTERNAL RESOURCE POOL(Transact-SQL)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

외부 프로세스에 대한 리소스를 정의하는 외부 풀을 만듭니다. 리소스 풀은 데이터베이스 엔진 인스턴스의 물리적 리소스(메모리 및 CPU)의 하위 집합을 나타냅니다. Resource Governor는 최대 64개의 리소스 풀에서 서버 리소스를 배포할 수 있습니다.

::: moniker range="=sql-server-2016"
[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]에서 [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]의 경우 외부 풀은 `rterm.exe`, `BxlServer.exe`, 이들에 의해 생성된 기타 프로세스를 제어합니다.
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15"
[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]의 경우 외부 풀은 `rterm.exe`, `python.exe`, `BxlServer.exe` 및 이들에 의해 생성된 기타 프로세스를 제어합니다.
::: moniker-end
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
 

## <a name="syntax"></a>구문  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"

```syntaxsql
CREATE EXTERNAL RESOURCE POOL pool_name  
[ WITH (  
    [ MAX_CPU_PERCENT = value ]  
    [ [ , ] MAX_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_PROCESSES = value ]   
    )   
]  
[ ; ]  
  
<CPU_range_spec> ::=    
{ CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]  
```  
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017"
```syntaxsql
CREATE EXTERNAL RESOURCE POOL pool_name  
[ WITH (  
    [ MAX_CPU_PERCENT = value ]  
    [ [ , ] AFFINITY CPU =    
            {  
                AUTO   
              | ( <cpu_range_spec> )   
              | NUMANODE = ( <NUMA_node_id> )   
            } ]   
    [ [ , ] MAX_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_PROCESSES = value ]   
    )   
]  
[ ; ]  
  
<CPU_range_spec> ::=    
{ CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]  
```  
::: moniker-end

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수

*pool_name*  
외부 리소스 풀에 대한 사용자 정의 이름입니다. *pool_name* 은 영숫자이며 최대 128자를 포함할 수 있습니다. 이 인수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 고유해야 하며 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
MAX_CPU_PERCENT =*value*  
CPU 경합이 있을 때 외부 리소스 풀의 받을 수 있는 모든 요청의 최대 평균 CPU 대역폭입니다. *값* 은 정수입니다. 허용되는 *value* 의 범위는 1에서 100까지입니다.


MAX_MEMORY_PERCENT =*value*  
이 외부 리소스 풀의 요청에서 사용할 수 있는 총 서버 메모리를 지정합니다. *값* 은 정수입니다. 허용되는 *value* 의 범위는 1에서 100까지입니다.

MAX_PROCESSES =*value*  
외부 리소스 풀에 허용되는 프로세스의 최대 수입니다. 이후에 컴퓨터 리소스에 의해서만 바인딩되는 풀에 대한 무제한 임계값은 0입니다.
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017"
MAX_CPU_PERCENT =*value*  
CPU 경합이 있을 때 외부 리소스 풀의 받을 수 있는 모든 요청의 최대 평균 CPU 대역폭입니다. *값* 은 정수입니다. 허용되는 *value* 의 범위는 1에서 100까지입니다.

AFFINITY {CPU = AUTO | ( <CPU_range_spec>) | NUMANODE = (\<NUMA_node_range_spec>)} 외부 리소스 풀을 특정 CPU에 연결합니다.

AFFINITY CPU = **(** <CPU_range_spec> **)** 는 외부 리소스 풀을 지정된 CPU_ID로 식별된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU에 매핑합니다.

AFFINITY NUMANODE = **(\<NUMA_node_range_spec> **)** 를 사용하는 경우 지정된 NUMA 노드 또는 노드 범위에 해당하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 물리적 CPU로 외부 리소스 풀의 선호도가 설정됩니다. 

MAX_MEMORY_PERCENT =*value*  
이 외부 리소스 풀의 요청에서 사용할 수 있는 총 서버 메모리를 지정합니다. *값* 은 정수입니다. 허용되는 *value* 의 범위는 1에서 100까지입니다.

MAX_PROCESSES =*value*  
외부 리소스 풀에 허용되는 프로세스의 최대 수입니다. 이후에 컴퓨터 리소스에 의해서만 바인딩되는 풀에 대한 무제한 임계값은 0입니다.
::: moniker-end

## <a name="remarks"></a>설명

[!INCLUDE[ssDE](../../includes/ssde-md.md)]은 [ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md) 문을 실행하면 리소스 풀을 구현합니다.

리소스 풀에 대한 일반 정보는 [Resource Governor 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md), [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) 및 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)을 참조합니다.

기계 학습에 사용된 외부 리소스 풀 관리 관련 정보는 [SQL Server에서 기계 학습을 위한 리소스 거버넌스](../../machine-learning/administration/resource-governor.md)를 참조하세요. 

## <a name="permissions"></a>사용 권한

`CONTROL SERVER` 권한이 필요합니다.

## <a name="examples"></a>예제

외부 풀에서는 CPU 사용량을 75%로 제한했습니다. 최대 메모리는 컴퓨터에서 사용 가능한 메모리의 30%입니다.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
```sql
CREATE EXTERNAL RESOURCE POOL ep_1
WITH (  
    MAX_CPU_PERCENT = 75
    , MAX_MEMORY_PERCENT = 30
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017"
```sql
CREATE EXTERNAL RESOURCE POOL ep_1
WITH (  
    MAX_CPU_PERCENT = 75
    , AFFINITY CPU = AUTO
    , MAX_MEMORY_PERCENT = 30
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```
::: moniker-end

## <a name="see-also"></a>참고 항목

+ [외부 스크립트 설정 서버 구성 옵션](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)
+ [sp_execute_external_script&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [ALTER EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
+ [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)
+ [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
+ [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)
+ [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
+ [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)
+ [sys.dm_resource_governor_external_resource_pool_affinity&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)
+ [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)
