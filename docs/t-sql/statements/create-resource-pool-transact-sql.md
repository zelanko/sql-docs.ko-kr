---
title: CREATE RESOURCE POOL (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE RESOURCE POOL
- RESOURCE POOL
- CREATE_RESOURCE_POOL_TSQL
- RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE RESOURCE POOL
ms.assetid: 82712505-c6f9-4a65-a469-f029b5a2d6cd
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c6f9a6ae8f0f869eb5ddd32c0189fcbaab198d3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-resource-pool-transact-sql"></a>CREATE RESOURCE POOL(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 리소스 관리자 리소스 풀을 만듭니다. 리소스 풀은 데이터베이스 엔진 인스턴스의 물리적 리소스(메모리, CPU 및 IO)의 하위 집합을 나타냅니다. 데이터베이스 관리자는 리소스 관리자를 사용하여 서버 리소스를 최대 64개의 리소스 풀에 배치할 수 있습니다. 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서는 리소스 관리자를 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
CREATE RESOURCE POOL pool_name  
[ WITH  
    (  
        [ MIN_CPU_PERCENT = value ]  
        [ [ , ] MAX_CPU_PERCENT = value ]   
        [ [ , ] CAP_CPU_PERCENT = value ]   
        [ [ , ] AFFINITY {SCHEDULER =  
                  AUTO 
                | ( <scheduler_range_spec> )   
                | NUMANODE = ( <NUMA_node_range_spec> )
                } ]   
        [ [ , ] MIN_MEMORY_PERCENT = value ]  
        [ [ , ] MAX_MEMORY_PERCENT = value ]  
        [ [ , ] MIN_IOPS_PER_VOLUME = value ]  
        [ [ , ] MAX_IOPS_PER_VOLUME = value ]  
    )   
]  
[;]  
  
<scheduler_range_spec> ::=  
{ SCHED_ID | SCHED_ID TO SCHED_ID }[,…n]  
  
<NUMA_node_range_spec> ::=  
{ NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID }[,…n]  
```  
  
## <a name="arguments"></a>인수  
 *pool_name 이라*  
 리소스 풀에 대한 사용자 정의 이름입니다. *pool_name 이라는* 은 영숫자로 최대 128 자를 사용할 수의 인스턴스 내에서 고유 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대 한 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다.  
  
 MIN_CPU_PERCENT =*값*  
 CPU 경합이 있을 때 리소스 풀의 모든 요청에 대해 보장되는 평균 CPU 대역폭을 지정합니다. *값* 는 정수 이며 기본 설정은 0입니다. 허용된 범위 *값* 은 0에서 100 까지입니다.  
  
 MAX_CPU_PERCENT =*값*  
 CPU 경합이 있을 때 이 리소스 풀의 모든 요청이 받는 최대 평균 CPU 대역폭을 지정합니다. *값* 는 정수 이며 기본 설정은 100입니다. 허용된 범위 *값* 는 1에서 100 까지입니다.  
  
 CAP_CPU_PERCENT =*값*  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 리소스 풀의 모든 요청에서 받을 CPU 대역폭의 하드 캡을 지정합니다. 최대 CPU 대역폭 수준을 지정된 값과 동일하게 제한합니다. *값* 는 정수 이며 기본 설정은 100입니다. 허용된 범위 *값* 는 1에서 100 까지입니다.  
  
 선호도 {스케줄러 = AUTO | ( \<scheduler_range_spec >) | NUMANODE = (\<NUMA_node_range_spec >)} **적용할**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다.  
  
 리소스 풀을 특정 스케줄러에 연결합니다. 기본값은 AUTO입니다.  
  
 AFFINITY SCHEDULER = **(** \<scheduler_range_spec > **)** 자원 그룹에 매핑하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정된 된 Id로 식별 되는 일정입니다. 이러한 Id의 scheduler_id 열에 있는 값에 매핑할 [sys.dm_os_schedulers &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md). 
  
 AFFINITY NUMANODE를 사용 하는 경우 = **(** \<NUMA_node_range_spec > **)**, 리소스 풀 설정 되 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스케줄러에 해당 하는 물리적 Cpu에 매핑되는 지정 된 NUMA 노드 또는 노드 범위에 있습니다. 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 사용하여 물리적 NUMA 구성과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스케줄러 ID 간의 매핑을 검색할 수 있습니다. 
  
```  
SELECT osn.memory_node_id AS [numa_node_id], sc.cpu_id, sc.scheduler_id  
FROM sys.dm_os_nodes AS osn  
INNER JOIN sys.dm_os_schedulers AS sc   
    ON osn.node_id = sc.parent_node_id   
    AND sc.scheduler_id < 1048576;  
```  
  
 MIN_MEMORY_PERCENT =*값*  
 다른 리소스 풀과 공유할 수 없으며 이 리소스 풀에 예약된 최소 메모리 양을 지정합니다. *값* 는 정수 기본 설정은 0 이며 허용 되는 범위에 대 한 *값* 는 0에서 100입니다.  
  
 MAX_MEMORY_PERCENT =*값*  
 이 리소스 풀의 요청에서 사용할 수 있는 총 서버 메모리를 지정합니다. *값* 는 정수 이며 기본 설정은 100입니다. 허용된 범위 *값* 는 1에서 100 까지입니다.  
  
 MIN_IOPS_PER_VOLUME =*값*  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 리소스 풀에 예약할 디스크 볼륨당 최소 IOPS(초당 IO 작업)를 지정합니다. 허용된 범위 *값* 은 0에서 2 ^31-1 (2147483647). 풀에 대한 최소 임계값이 없음을 나타내려면 0을 지정합니다. 기본값은 0입니다.  
  
 MAX_IOPS_PER_VOLUME =*값*  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 리소스 풀에 대해 허용할 디스크 볼륨당 최대 IOPS(초당 IO 작업)를 지정합니다. 허용된 범위 *값* 은 0에서 2 ^31-1 (2147483647). 풀에 대한 무제한 임계값을 설정하려면 0을 지정합니다. 기본값은 0입니다.  
  
 풀에 대한 MAX_IOPS_PER_VOLUME이 0으로 설정된 경우 풀이 전혀 제어되지 않으며, 다른 풀에 MIN_IOPS_PER_VOLUME 집합이 설정되었더라도 시스템에서 모든 IOPS를 사용할 수 있습니다. 이 경우에는 이 풀의 IO를 제어하려는 경우 이 풀에 대한 MAX_IOPS_PER_VOLUME 값을 높은 값(예를 들어, 최대값 2^31-1)으로 설정하는 것이 좋습니다.  
  
## <a name="remarks"></a>주의  
 MIN_IOPS_PER_VOLUME과 MAX_IOPS_PER_VOLUME은 초당 최소 및 최대 읽기 또는 쓰기를 지정합니다. 이러한 읽기 또는 쓰기는 크기 제한이 없으며 최소 또는 최대 처리량을 나타내지 않습니다.  
  
 MAX_CPU_PERCENT 및 MAX_MEMORY_PERCENT의 값은 MIN_CPU_PERCENT 및 MIN_MEMORY_PERCENT의 각 값보다 크거나 같아야 합니다.  
  
 CAP_CPU_PERCENT는 풀에 연결된 작업이 CAP_CPU_PERCENT 값보다 큰 값이 아닌 MAX_CPU_PERCENT 값보다 큰 CPU 용량(사용 가능한 경우)을 사용할 수 있다는 점에서 MAX_CPU_PERCENT와 다릅니다.  
  
 선호도가 설정된 각 구성 요소(스케줄러 또는 NUMA 모드)에 대한 총 CPU 비율은 100%를 초과하면 안 됩니다.  
  
## <a name="permissions"></a>Permissions  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `bigPool`라는 리소스 풀을 만드는 방법을 보여 줍니다. 이 풀은 기본 리소스 관리자 설정을 사용합니다.  
  
```  
CREATE RESOURCE POOL bigPool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 다음 예에서는 `CAP_CPU_PERCENT`를 하드 캡 30%로 설정하고 `AFFINITY SCHEDULER`를 0-63과 128-191 범위로 설정합니다. 
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
CREATE RESOURCE POOL PoolAdmin  
WITH (  
     MIN_CPU_PERCENT = 10,  
     MAX_CPU_PERCENT = 20,  
     CAP_CPU_PERCENT = 30,  
     AFFINITY SCHEDULER = (0 TO 63, 128 TO 191),  
     MIN_MEMORY_PERCENT = 5,  
     MAX_MEMORY_PERCENT = 15  
      );  
  
```  
  
 다음 예제에서는 `MIN_IOPS_PER_VOLUME` 를 \<일부 값 > 및 `MAX_IOPS_PER_VOLUME` 를 \<일부 값 >입니다. 이러한 값은 리소스 풀에 대해 제공되는 물리적 I/O 읽기 및 쓰기 작업을 제어합니다.  
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
CREATE RESOURCE POOL PoolAdmin  
WITH (  
    MIN_IOPS_PER_VOLUME = 20,  
    MAX_IOPS_PER_VOLUME = 100  
      );  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [리소스 풀 만들기](../../relational-databases/resource-governor/create-a-resource-pool.md)  
  
  


