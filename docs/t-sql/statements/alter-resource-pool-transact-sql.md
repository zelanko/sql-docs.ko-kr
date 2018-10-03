---
title: ALTER RESOURCE POOL(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_RESOURCE_POOL_TSQL
- ALTER RESOURCE POOL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER RESOURCE POOL
ms.assetid: 9c1c4cfb-0e3b-4f01-bf57-3fce94c7d1d4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b8d936e14cf2492ae9b9529996e9d28d40d02a9f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47856471"
---
# <a name="alter-resource-pool-transact-sql"></a>ALTER RESOURCE POOL(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기존 리소스 관리자 리소스 풀 구성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER RESOURCE POOL { pool_name | "default" }  
[WITH  
    ( [ MIN_CPU_PERCENT = value ]  
    [ [ , ] MAX_CPU_PERCENT = value ]   
    [ [ , ] CAP_CPU_PERCENT = value ]   
    [ [ , ] AFFINITY {
                        SCHEDULER = AUTO 
                      | ( <scheduler_range_spec> ) 
                      | NUMANODE = ( <NUMA_node_range_spec> )
                      }]   
    [ [ , ] MIN_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_MEMORY_PERCENT = value ]   
    [ [ , ] MIN_IOPS_PER_VOLUME = value ]  
    [ [ , ] MAX_IOPS_PER_VOLUME = value ]  
)]   
[;]  
  
<scheduler_range_spec> ::=  
{SCHED_ID | SCHED_ID TO SCHED_ID}[,…n]  
  
<NUMA_node_range_spec> ::=  
{NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID}[,…n]  
```  
  
## <a name="arguments"></a>인수  
 { *pool_name* | **"default"** }  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치될 때 만들어지는 기본 리소스 풀이나 기존 사용자 정의 리소스 풀의 이름입니다.  
  
 "default"는 시스템 예약어인 DEFAULT와의 충돌을 피하기 위해 ALTER RESOURCE POOL과 함께 사용될 경우 따옴표("") 또는 대괄호([])로 묶어야 합니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
> [!NOTE]  
>  미리 정의된 작업 그룹과 리소스 풀의 이름은 "default"와 같이 소문자를 사용합니다. 대/소문자 구분 데이터 정렬을 사용하는 서버의 경우 이러한 사항을 고려해야 합니다. 대/소문자 구분 데이터 정렬(예: SQL_Latin1_General_CP1_CI_AS)을 사용하는 서버는 "default"와 "Default"를 똑같이 처리합니다.  
  
 MIN_CPU_PERCENT =*value*  
 CPU 경합이 있을 때 리소스 풀의 모든 요청에 대해 보장되는 평균 CPU 대역폭을 지정합니다. *value*는 기본 설정이 0인 정수입니다. 허용되는 *value*의 범위는 0에서 100까지입니다.  
  
 MAX_CPU_PERCENT =*value*  
 CPU 경합이 있을 때 이 리소스 풀의 모든 요청이 받는 최대 평균 CPU 대역폭을 지정합니다. *value*는 기본 설정이 100인 정수입니다. 허용되는 *value*의 범위는 1에서 100까지입니다.  
  
 CAP_CPU_PERCENT =*value*  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 리소스 풀의 요청에 대한 대상 CPU의 최대 용량을 지정합니다. *value*는 기본 설정이 100인 정수입니다. 허용되는 *value*의 범위는 1에서 100까지입니다.  
  
> [!NOTE]  
>  CPU 거버넌스의 통계 특성으로 인해 CAP_CPU_PERCENT에 지정된 값을 초과하는 급격한 변동을 알릴 수 있습니다.  
  
 AFFINITY {SCHEDULER = AUTO | (Scheduler_range_spec) | NUMANODE = (NUMA_node_range_spec)}  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 리소스 풀을 특정 스케줄러에 연결합니다. 기본값은 AUTO입니다.  
  
 AFFINITY SCHEDULER = (Scheduler_range_spec)은 리소스 풀을 지정된 ID로 식별된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 일정으로 매핑합니다. 이러한 ID는 [sys.dm_os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)의 scheduler_id 열에 있는 값에 매핑됩니다.  
  
 AFFINITY NAMANODE = (NUMA_node_range_spec)을 사용하면 리소스 풀의 선호도가 지정된 NUMA 노드 또는 노드 범위에 해당하는 물리적 CPU에 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스케줄러로 설정됩니다. 다음 Transact-SQL 쿼리를 사용하여 물리적 NUMA 구성과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스케줄러 ID 간의 매핑을 검색할 수 있습니다.  
  
```  
SELECT osn.memory_node_id AS [numa_node_id], sc.cpu_id, sc.scheduler_id  
FROM sys.dm_os_nodes AS osn  
INNER JOIN sys.dm_os_schedulers AS sc 
   ON osn.node_id = sc.parent_node_id 
      AND sc.scheduler_id < 1048576;  
```  
  
 MIN_MEMORY_PERCENT =*value*  
 다른 리소스 풀과 공유할 수 없으며 이 리소스 풀에 예약된 최소 메모리 양을 지정합니다. *value*는 기본 설정이 0인 정수입니다. 허용되는 *value*의 범위는 0에서 100까지입니다.  
  
 MAX_MEMORY_PERCENT =*value*  
 이 리소스 풀의 요청에서 사용할 수 있는 총 서버 메모리를 지정합니다. *value*는 기본 설정이 100인 정수입니다. 허용되는 *value*의 범위는 1에서 100까지입니다.  
  
 MIN_IOPS_PER_VOLUME =*value*  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 리소스 풀에 예약할 디스크 볼륨당 최소 IOPS(초당 IO 작업)를 지정합니다. 허용되는 *value*의 범위는 0에서 2^31-1(2,147,483,647)까지입니다. 풀에 대한 최소 임계값이 없음을 나타내려면 0을 지정합니다.  
  
 MAX_IOPS_PER_VOLUME =*value*  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 리소스 풀에 대해 허용할 디스크 볼륨당 최대 IOPS(초당 IO 작업)를 지정합니다. 허용되는 *value*의 범위는 0에서 2^31-1(2,147,483,647)까지입니다. 풀에 대한 무제한 임계값을 설정하려면 0을 지정합니다. 기본값은 0입니다.  
  
 풀에 대한 MAX_IOPS_PER_VOLUME이 0으로 설정된 경우 풀이 전혀 제어되지 않으며, 다른 풀에 MIN_IOPS_PER_VOLUME 집합이 설정되었더라도 시스템에서 모든 IOPS를 사용할 수 있습니다. 이 경우에는 이 풀의 IO를 제어하려는 경우 이 풀에 대한 MAX_IOPS_PER_VOLUME 값을 높은 값(예를 들어, 최대값 2^31-1)으로 설정하는 것이 좋습니다.  
  
## <a name="remarks"></a>Remarks  
 MAX_CPU_PERCENT 및 MAX_MEMORY_PERCENT는 MIN_CPU_PERCENT 및 MIN_MEMORY_PERCENT 각각보다 크거나 같아야 합니다.  
  
 MAX_CPU_PERCENT는 가능하면 MAX_CPU_PERCENT 값 보다 큰 CPU 용량을 사용할 수 있습니다. CAP_CPU_PERCENT를 초과하는 정기적인 급격한 증가가 있을 수 있지만 추가 CPU 용량을 사용할 수 있다 해도 워크로드는 오랜 시간 동안 CAP_CPU_PERCENT를 초과해서는 안 됩니다.  
  
 선호도가 설정된 각 구성 요소(스케줄러 또는 NUMA 모드)에 대한 총 CPU 비율은 100%를 초과하면 안 됩니다.  
  
 DDL 문을 실행할 경우 리소스 관리자 상태에 대해 잘 알고 있는 것이 좋습니다. 자세한 내용은 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)를 참조하세요.  
  
 설정에 영향을 주는 계획을 변경할 경우 *pool_name*이 Resource Governor 리소스 풀의 이름인 DBCC FREEPROCCACHE(*pool_name*)를 실행 한 후 새 설정이 이전에 캐시된 계획에 적용됩니다.  
  
-   여러 스케줄러에서 단일 스케줄러로 AFFINITY를 변경 하는 경우 DBCC FREEPROCCACHE의 실행은 병렬 계획이 직렬 모드에서 실행될 수 있기 때문에 필요하지 않습니다. 그러나 직렬 계획으로 컴파일된 계획만큼 효율적이지 않을 수 있습니다.  
  
-   단일 스케줄러에서 여러 스케줄러로 AFFINITY를 변경 하는 경우 DBCC FREEPROCCACHE의 실행은 필요하지 않습니다. 그러나 직렬 계획이 병렬로 실행될 수 없으므로 해당 캐시의 제거로 새 계획이 잠재적으로 병렬 처리를 사용하여 컴파일될 수 있습니다.  
  
> [!CAUTION]  
>  하나 이상의 작업 그룹에 연결된 리소스 풀에서 캐시된 계획을 삭제하면 *pool_name*에 의해 식별된 사용자 정의 리소스 풀과 함께 모든 작업 그룹에 영향을 미칩니다.  
  
## <a name="permissions"></a>Permissions  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `default`로 변경되는 `MAX_CPU_PERCENT`를 제외한 `25` 풀의 모든 기본 리소스 풀 설정을 유지합니다.  
  
```  
ALTER RESOURCE POOL "default"  
WITH  
     ( MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 다음 예에서는 `CAP_CPU_PERCENT`가 하드 캡을 80%로 설정하고 `AFFINITY SCHEDULER`가 개별 값 8과 12-16 범위로 설정됩니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
ALTER RESOURCE POOL Pool25  
WITH(   
     MIN_CPU_PERCENT = 5,  
     MAX_CPU_PERCENT = 10,       
     CAP_CPU_PERCENT = 80,  
     AFFINITY SCHEDULER = (8, 12 TO 16),   
     MIN_MEMORY_PERCENT = 5,  
     MAX_MEMORY_PERCENT = 15  
);  
  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [관리](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
