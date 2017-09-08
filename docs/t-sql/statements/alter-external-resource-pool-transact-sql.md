---
title: "외부 리소스 풀 (Transact SQL) ALTER | Microsoft Docs"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL RESOURCE POOL statement
ms.assetid: 634c327d-971b-49ba-b8a2-e243a04040db
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d85123a34de6dea6b76c1dd4ad8dc6af3117764d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-external-resource-pool-transact-sql"></a>ALTER 외부 리소스 풀 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  된 변경 내용을 리소스 관리자 외부 풀 외부 프로세스에 대 한 리소스를 정의 합니다. R 서비스에 대 한 외부 풀 제어 `rterm.exe`, `BxlServer.exe`, 및 생성 된 다른 프로세스입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)합니다.  
  
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
 { *pool_name 이라는* | "default"을 (를)  
 기존 사용자 정의 외부 리소스 풀 또는 때 만들어지는 기본 외부 리소스 풀의 이름인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치 되어 있습니다.  
"default"는 따옴표로 묶어야 합니다 ("") 또는 대괄호 ()와 함께 사용할 경우 `ALTER EXTERNAL RESOURCE POOL` 충돌을 피하기 위해 `DEFAULT`, 시스템인 예약어입니다.  
  
 MAX_CPU_PERCENT =*값*  
 CPU 충돌이 있을 때 외부 리소스 풀의 모든 요청에서 받을 최대 평균 CPU 대역폭을 지정 합니다. *값* 는 정수 이며 기본 설정은 100입니다. 허용된 범위 *값* 는 1에서 100 까지입니다.  
  
선호도 {CPU = AUTO | ( \<CPU_range_spec >) | NUMANODE = (\<NUMA_node_range_spec >)} 특정 Cpu에 외부 리소스 풀을 연결 합니다. 기본값은 AUTO입니다.  
  
CPU 선호도 = **(** \<CPU_range_spec > **)** 외부 리소스 풀에 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 주어진된 CPU_IDs로 식별 되는 Cpu.
  
AFFINITY NUMANODE를 사용 하는 경우 = **(** \<NUMA_node_range_spec > **)**, 외부 리소스 풀 설정 되 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정 된 NUMA에 해당 하는 물리적 Cpu 노드 또는 노드 범위입니다.
  
 MAX_MEMORY_PERCENT =*값*  
 이 외부 리소스 풀의 요청에서 사용할 수 있는 총 서버 메모리를 지정 합니다. *값* 는 정수 이며 기본 설정은 100입니다. 허용된 범위 *값* 는 1에서 100 까지입니다.  
  
 MAX_PROCESSES =*값*  
 외부 리소스 풀에 허용 되는 프로세스의 최대 수를 지정 합니다. 가 있는 풀에만 컴퓨터 리소스 수에 대 한 무제한 임계값을 설정 하려면 0을 지정 합니다. 기본값은 0입니다.  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 실행할 때 리소스 풀을 구현 하는 [ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md) 문.  
  
 리소스 풀에 대 한 자세한 내용은 참조 하십시오. [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md), [sys.resource_governor_external_resource_pools&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), 및 [sys.dm_resource_governor_external_resource_pool_affinity&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 `CONTROL SERVER` 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 문은 50% 및 컴퓨터에서 사용 가능한 메모리의 25%로 최대 메모리를 CPU 사용량을 제한 하는 외부 풀을 변경 합니다.  
  
```  
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
  
## <a name="see-also"></a>관련 항목:  
 [external scripts enabled 서버 구성 옵션](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [SQL Server R Services에 대 한 알려진된 문제](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  

