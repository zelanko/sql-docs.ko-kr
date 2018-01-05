---
title: ALTER WORKLOAD GROUP (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_WORKLOAD_GROUP_TSQL
- ALTER WORKLOAD GROUP
dev_langs: TSQL
helpviewer_keywords: ALTER WORKLOAD GROUP statement
ms.assetid: 957addce-feb0-4e54-893e-5faca3cd184c
caps.latest.revision: "56"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0103b63c883e1d3f9a263cf5fdb4e4ef4ca9521f
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="alter-workload-group-transact-sql"></a>ALTER WORKLOAD GROUP(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 리소스 관리자 작업 그룹 구성을 변경하고 선택적으로 리소스 관리자 리소스 풀에 할당합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
ALTER WORKLOAD GROUP { group_name | "default" }  
[ WITH  
    ([ IMPORTANCE = { LOW | MEDIUM | HIGH } ]  
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]  
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]  
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]   
      [ [ , ] MAX_DOP = value ]  
      [ [ , ] GROUP_MAX_REQUESTS = value ] )  
 ]  
[ USING { pool_name | "default" } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *group_name* | "**기본**"  
 기존의 사용자 정의 작업 그룹 또는 리소스 관리자 기본 작업 그룹의 이름입니다.  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치되면 리소스 관리자가 "default" 그룹과 내부 그룹을 만듭니다.  
  
 "default" 옵션은 시스템 예약어인 DEFAULT와의 충돌을 피하기 위해 ALTER WORKLOAD GROUP과 함께 사용될 경우 따옴표("") 또는 대괄호([])로 묶어야 합니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
> [!NOTE]  
> 미리 정의된 작업 그룹과 리소스 풀의 이름은 "default"와 같이 소문자를 사용합니다. 대/소문자 구분 데이터 정렬을 사용하는 서버의 경우 이러한 사항을 고려해야 합니다. 대/소문자 구분 데이터 정렬(예: SQL_Latin1_General_CP1_CI_AS)을 사용하는 서버는 "default"와 "Default"를 똑같이 처리합니다.  
  
 IMPORTANCE = { LOW | MEDIUM | HIGH }  
 작업 그룹에 있는 요청의 상대적 중요도를 지정합니다. 중요도는 다음 값 중 하나입니다.  
  
-   LOW  
-   MEDIUM(기본값)  
-   HIGH  
  
> [!NOTE]  
> 내부적으로 각 중요도 설정은 계산에 사용된 멤버로 저장됩니다.  
  
 IMPORTANCE는 리소스 풀에 대해 로컬입니다. 같은 리소스 풀 내에 있는 다른 중요도의 작업 그룹은 서로 영향을 주지만 다른 리소스 풀의 작업 그룹에는 영향을 주지 않습니다.  
  
 REQUEST_MAX_MEMORY_GRANT_PERCENT =*값*  
 단일 요청이 풀에서 사용할 수 있는 최대 메모리 양을 지정합니다. 이 비율은 MAX_MEMORY_PERCENT에서 지정한 리소스 풀 크기에 따라 바뀝니다.  
  
> [!NOTE]  
> 지정된 양은 쿼리 실행 부여 메모리만 참조합니다.  
  
 *값* 0 또는 양의 정수 여야 합니다. 허용된 범위 *값* 은 0에서 100 까지입니다. 에 대 한 기본 설정은 *값* 은 25입니다.  
  
 다음에 유의하세요.  
  
-   설정 *값* 0은 차단 쿼리와 사용자 정의 작업 그룹에 SORT 및 HASH JOIN 연산 함께 실행에서 합니다.  
  
-   설정을 권장 하지는 않습니다 *값* 서버 수 다른 동시 쿼리를 실행 중인 경우 가능한 메모리를 충분히 따로 설정 수 없기 때문에 70 보다 큽니다. 71 이상의 값으로 설정하면 쿼리 시간 초과 오류 8645가 발생할 수 있습니다.  
  
> [!NOTE]  
>  쿼리 메모리 요구 사항이 이 매개 변수에 지정된 제한을 초과하는 경우 서버는 다음을 수행합니다.  
>   
>  사용자 정의 작업 그룹의 경우 서버는 메모리 요구 사항이 제한 수준 아래로 낮아지거나 병렬 처리 수준이 1이 될 때까지 쿼리 병렬 처리 수준을 줄이려고 합니다. 그래도 쿼리 메모리 요구 사항이 제한보다 클 경우 오류 8657이 발생합니다.  
>   
>  내부 및 기본 작업 그룹의 경우 서버는 쿼리가 필요한 메모리를 가져오도록 허용합니다.  
>   
>  두 경우 모두 서버에 실제 메모리가 부족하면 시간 초과 오류 8645가 발생할 수 있습니다.  
  
 REQUEST_MAX_CPU_TIME_SEC =*값*  
 요청이 사용할 수 있는 최대 CPU 시간(초)을 지정합니다. *값* 0 또는 양의 정수 여야 합니다. 에 대 한 기본 설정은 *값* 0은 무제한을 의미 합니다.  
  
> [!NOTE]  
> 기본적으로 리소스 관리자를 최대 시간을 초과 하는 경우 계속할 요청을 해도 됩니다. 이벤트가 생성됩니다. 자세한 내용은 참조 [CPU 임계값을 초과 이벤트 클래스](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)합니다. 

> [!IMPORTANT]
> 부터는 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3, 및를 사용 하 여 [추적 플래그 2422](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md), 최대 시간을 초과 하는 경우 리소스 관리자 요청을 중단 됩니다.
  
 REQUEST_MEMORY_GRANT_TIMEOUT_SEC =*값*  
 메모리(작업 버퍼 메모리)가 부여될 때까지 쿼리가 대기할 수 있는 최대 시간(초)을 지정합니다.  
  
> [!NOTE]  
>  메모리 부여 제한 시간에 도달할 때마다 쿼리가 실패하지는 않습니다. 쿼리는 너무 많은 쿼리가 동시에 실행되는 경우에만 실패합니다. 그렇지 않을 경우 쿼리에 최소한의 메모리만 부여되어 쿼리 성능이 떨어질 수 있습니다.  
  
 *값* 양의 정수 여야 합니다. 에 대 한 기본 설정은 *값*, 0, 쿼리 비용에 따른 내부 계산을 사용 하 여 최대 시간을 결정 합니다.  
  
 MAX_DOP =*값*  
 병렬 요청의 최대 DOP(병렬 처리 수준)를 지정합니다. *값* 0 또는 양의 정수 1 ~ 255 여야 합니다. 때 *값* 가 0 이면 서버는 최대 병렬 처리 수준을 선택 합니다. 이 값은 기본값이며 권장 설정입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 MAX_DOP에 설정하는 실제 값은 지정된 값보다 작을 수 있습니다. 최종 값 수식 min에 의해 결정 됩니다 (255, *Cpu 수)*합니다.  
  
> [!CAUTION]  
>  MAX_DOP를 변경하면 서버 성능이 저하될 수 있습니다. MAX_DOP를 변경해야 할 경우에는 단일 NUMA 노드에 있는 하드웨어 스케줄러의 최대 수보다 작거나 같은 값으로 설정하는 것이 좋습니다. MAX_DOP를 8보다 큰 값으로 설정하면 성능에 영향을 줄 수 있습니다.  
  
 MAX_DOP는 다음과 같이 처리합니다.  
  
-   MAX_DOP는 작업 그룹 MAX_DOP를 초과하지 않는 한 쿼리 힌트 역할을 합니다.  
  
-   MAX_DOP는 쿼리 힌트로서 항상 sp_configure 'max degree of parallelism'을 무시합니다.  
  
-   작업 그룹 MAX_DOP는 sp_configure 'max degree of parallelism'을 무시합니다.  
  
-   컴파일할 때 쿼리가 직렬(MAX_DOP = 1 )로 표시되면 작업 그룹이나 sp_configure 설정에 관계없이 런타임에서 병렬로 다시 변경할 수 없습니다.  
  
 DOP가 구성된 후에는 부여 메모리가 부족할 때만 낮아질 수 있습니다. 작업 그룹 재구성은 부여 메모리 큐에서 대기하는 동안 표시되지 않습니다.  
  
 GROUP_MAX_REQUESTS =*값*  
 작업 그룹에서 실행할 수 있는 최대 동시 요청 수를 지정합니다. *값* 0 또는 양의 정수 여야 합니다. 에 대 한 기본 설정은 *값*, 0, 무제한 요청을 허용 합니다. 최대 동시 요청에 도달한 경우 해당 그룹의 사용자가 로그인할 수 있지만 지정된 값 아래로 동시 요청 수가 떨어질 때까지 사용자가 대기 상태에 배치됩니다.  
  
 사용 하 여 { *pool_name 이라는* | "**기본**"을 (를)  
 로 식별 되는 사용자 정의 리소스 풀과 작업 그룹을 연결 *pool_name 이라는*, 리소스 풀의 작업 그룹을 넣습니다 사실입니다. 경우 *pool_name 이라는* 제공 하지 않으면 또는 USING 인수가 사용 되지 않으면 작업 그룹 미리 정의 된 리소스 관리자 기본 풀에 저장 됩니다.  
  
 "default" 옵션은 시스템 예약어인 DEFAULT와의 충돌을 피하기 위해 ALTER WORKLOAD GROUP과 함께 사용될 경우 따옴표("") 또는 대괄호([])로 묶어야 합니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
> [!NOTE]  
>  "default" 옵션은 대/소문자를 구분합니다.  
  
## <a name="remarks"></a>주의  
 ALTER WORKLOAD GROUP은 기본 그룹에서 허용됩니다.  
  
 작업 그룹 구성의 변경 내용은 ALTER RESOURCE GOVERNOR RECONFIGURE가 실행된 후에 적용됩니다. 설정에 영향을 주는 계획을 변경할 경우 새 설정이 적용 됩니다 이전에 캐시 된 계획에 DBCC FREEPROCCACHE를 실행 한 후 (*pool_name 이라는*) 여기서 *pool_name 이라는* 리소스의 이름 작업 그룹은 연결 된 관리자 리소스 풀.  
  
-   1로 MAX_DOP를 변경 하는 경우 DBCC FREEPROCCACHE 실행 필요 하지 않은 직렬 모드에서 병렬 계획 실행 수 있습니다. 그러나 그 수 없습니다 효율적으로 직렬 계획에서 컴파일된 계획으로.  
  
-   1에서 MAX_DOP를 0으로 변경 경우 DBCC FREEPROCCACHE를 실행 하는 1 보다 큰 값이 필요 하지 않습니다. 그러나 직렬 계획을 병렬로 실행할 수 없습니다, 그리고 되므로 해당 캐시를 지워야 하면 새 계획을 잠재적으로 병렬 처리를 사용 하 여 컴파일할 수 있습니다.  
  
> [!CAUTION]  
>  둘 이상의 작업 그룹에 연관 된 리소스 풀에서 캐시 된 계획 삭제에 영향이 모든 작업 그룹으로 식별 하는 사용자 정의 리소스 풀과 *pool_name 이라는*합니다.  
  
 DDL 문을 실행할 경우 리소스 관리자 상태에 대해 잘 알고 있는 것이 좋습니다. 자세한 내용은 참조 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)합니다.  
  
 REQUEST_MEMORY_GRANT_PERCENT: [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 인덱스 생성은 향상된 성능을 위해 초기에 부여된 메모리보다 많은 작업 메모리를 사용할 수 있습니다. 이 특수 처리는 이후 버전의 리소스 관리자에서 지원되지만 초기 부여 및 추가 메모리 부여는 리소스 풀 및 작업 그룹 설정에 따라 제한됩니다.  
  
 **분할된 된 테이블에서 인덱스 생성**  
  
 정렬되지 않은 분할된 테이블에서 인덱스 생성에 사용되는 메모리는 관련된 파티션 수에 비례합니다.  필요한 총 메모리가 리소스 관리자 작업 그룹 설정에서 지정한 쿼리당 제한(REQUEST_MAX_MEMORY_GRANT_PERCENT)을 초과하면 이 인덱스 생성이 실행되지 않을 수 있습니다. "default" 작업 그룹에서는 쿼리가 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 호환성을 위해 시작하는 데 필요한 최소 메모리를 포함하는 쿼리당 제한을 초과하게 되므로 "default" 리소스 풀에 이러한 쿼리를 실행할 수 있는 총 메모리가 구성되어 있는 경우 사용자가 "default" 작업 그룹에서 같은 인덱스 생성을 실행할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 기본 그룹에 있는 요청의 중요도를 `MEDIUM`에서 `LOW`로 변경하는 방법을 보여 줍니다.  
  
```  
ALTER WORKLOAD GROUP "default"  
WITH (IMPORTANCE = LOW);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 다음 예에서는 작업 그룹을 현재 속해 있는 풀에서 기본 풀로 이동하는 방법을 보여 줍니다.  
  
```  
ALTER WORKLOAD GROUP adHoc  
USING [default];  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [관리](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
