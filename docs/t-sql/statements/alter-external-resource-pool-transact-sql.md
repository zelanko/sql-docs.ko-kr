---
title: ALTER EXTERNAL RESOURCE POOL(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- ALTER_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL RESOURCE POOL statement
ms.assetid: 634c327d-971b-49ba-b8a2-e243a04040db
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: ebab091b0e674339141c4ee2ea6d7c7993ccbabf
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68893678"
---
# <a name="alter-external-resource-pool-transact-sql"></a>ALTER EXTERNAL RESOURCE POOL(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

외부 프로세스에서 사용할 수 있는 리소스를 지정하는 Resource Governor 외부 풀을 변경합니다. 

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]에서 [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]의 경우 외부 풀은 `rterm.exe`, `BxlServer.exe`, 이들에 의해 생성된 기타 프로세스를 제어합니다.
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]의 경우 외부 풀은 `rterm.exe`, `python.exe`, `BxlServer.exe` 및 이들에 의해 생성된 기타 프로세스를 제어합니다.
::: moniker-end

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>구문

```
ALTER EXTERNAL RESOURCE POOL { pool_name | "default" }
[ WITH (
    [ MAX_CPU_PERCENT = value ]
    [ [ , ] AFFINITY CPU =
            {
                AUTO
              | ( <cpu_range_spec> )
              | NUMANODE = (( <NUMA_node_id> )
            } ]   
    [ [ , ] MAX_MEMORY_PERCENT = value ]
    [ [ , ] MAX_PROCESSES = value ]
    )
]
[ ; ]
  
<CPU_range_spec> ::=
{ CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]
```  
  
## <a name="arguments"></a>인수

{ *pool_name* | "기본값" }  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이 설치될 때 만들어지는 기본 외부 리소스 풀이나 기존 사용자 정의 외부 리소스 풀의 이름입니다.
"default"는 시스템 예약어인 `DEFAULT`와의 충돌을 피하기 위해 `ALTER EXTERNAL RESOURCE POOL`과 함께 사용될 경우 따옴표("") 또는 대괄호([])로 묶어야 합니다.

MAX_CPU_PERCENT =*value*  
CPU 경합이 있을 때 이 외부 리소스 풀의 모든 요청이 받을 수 있는 최대 평균 CPU 대역폭을 지정합니다. *값*은 정수입니다. 허용되는 *value*의 범위는 1에서 100까지입니다.

AFFINITY {CPU = AUTO | ( \<CPU_range_spec> ) | NUMANODE = (\<NUMA_node_range_spec>)}  
외부 리소스 풀을 특정 UPU에 연결합니다.

AFFINITY CPU = **(** \<CPU_range_spec> **)** 는 외부 리소스 풀을 지정된 CPU_ID로 확인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU에 매핑합니다. AFFINITY NUMANODE = **(** \<NUMA_node_range_spec> **)** 를 사용하는 경우 외부 리소스 풀의 선호도가 지정된 NUMA 노드 또는 노드 범위에 해당하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 물리적 CPU로 설정됩니다.

MAX_MEMORY_PERCENT =*value*  
이 외부 리소스 풀의 요청에서 사용할 수 있는 총 서버 메모리를 지정합니다. *값*은 정수입니다. 허용되는 *value*의 범위는 1에서 100까지입니다.

MAX_PROCESSES =*value*  
이 외부 리소스 풀에 허용되는 프로세스의 최대 수를 지정합니다. 이후에 컴퓨터 리소스에 의해서만 바인딩되는 풀에 대 한 무제한 임계값을 설정하려면 0을 지정합니다.

## <a name="remarks"></a>설명

[!INCLUDE[ssDE](../../includes/ssde-md.md)]은 [ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md) 문을 실행하면 리소스 풀을 구현합니다.

리소스 풀에 대한 일반 정보는 [Resource Governor 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md), [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) 및 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)을 참조합니다.  

컴퓨터 학습 작업을 제어하는 외부 리소스 풀의 사용 관련 정보는 [SQL Server에서의 기계 학습에 대한 리소스 관리](../../advanced-analytics/r/resource-governance-for-r-services.md)를 참조 하십시오...
## <a name="permissions"></a>사용 권한

`CONTROL SERVER` 권한이 필요합니다.

## <a name="examples"></a>예

다음 명령문은 CPU 사용량을 50% 및 최대 메모리를 컴퓨터에서 사용 가능한 메모리의 25%로 제한하는 외부 풀을 변경합니다.
  
```sql
ALTER EXTERNAL RESOURCE POOL ep_1
WITH (
    MAX_CPU_PERCENT = 50
    , AFFINITY CPU = AUTO
    , MAX_MEMORY_PERCENT = 25
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```

## <a name="see-also"></a>참고 항목

+ [SQL Server에서 머신 러닝을 위한 리소스 거버넌스](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [외부 스크립트 설정 서버 구성 옵션](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)
+ [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)
+ [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)
+ [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)
+ [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)
+ [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
+ [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md) 
