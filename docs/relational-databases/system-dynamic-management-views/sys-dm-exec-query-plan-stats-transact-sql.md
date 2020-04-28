---
title: sys. dm_exec_query_plan_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_plan_stats
- sys.dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats
helpviewer_keywords:
- sys.dm_exec_query_plan_stats management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfacb
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 279f1a8fbe3ec78dc0cae30d9879615b169075bf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75656995"
---
# <a name="sysdm_exec_query_plan_stats-transact-sql"></a>sys. dm_exec_query_plan_stats (Transact-sql)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

이전에 캐시 된 쿼리 계획에 대해 마지막으로 알려진 실제 실행 계획에 해당 하는를 반환 합니다.

## <a name="syntax"></a>구문

```
sys.dm_exec_query_plan_stats(plan_handle)  
``` 

## <a name="arguments"></a>인수 
*plan_handle*  
실행 된 일괄 처리에 대 한 쿼리 실행 계획을 고유 하 게 식별 하는 토큰 이며 계획 캐시에 있거나 현재 실행 중인 일괄 처리에 대 한 쿼리 실행 계획을 고유 하 게 식별 합니다. *plan_handle* 은 **varbinary (64)** 입니다.   

*Plan_handle* 는 다음과 같은 동적 관리 개체에서 가져올 수 있습니다.  
  
-   [sys.dm_exec_cached_plans&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests&#40;Transact-SQL&#41](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [dm_exec_procedure_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [dm_exec_trigger_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  

## <a name="table-returned"></a>반환된 테이블

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|
|**dbid**|**smallint**|이 계획에 해당하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 컴파일할 당시 유효했던 컨텍스트 데이터베이스의 ID입니다. 임시 및 준비된 SQL 문의 경우 문이 컴파일된 데이터베이스의 ID입니다.<br /><br /> 열이 Null 값을 허용합니다.|  
|**objectid**|**int**|이 쿼리 계획에 대한 저장 프로시저나 사용자 정의 함수와 같은 개체의 ID입니다. 임시 및 준비된 일괄 처리의 경우 이 열은 **Null**입니다.<br /><br /> 열이 Null 값을 허용합니다.|  
|**number**|**smallint**|번호가 매겨진 저장 프로시저 정수입니다. 예를 들어 **orders** 응용 프로그램에 대한 프로시저 그룹에 **orderproc;1**, **orderproc;2** 등의 이름을 지정할 수 있습니다. 임시 및 준비된 일괄 처리의 경우 이 열은 **Null**입니다.<br /><br /> 열이 Null 값을 허용합니다.|  
|**됨**|**bit**|해당 저장 프로시저가 암호화되었는지 여부를 나타냅니다.<br /><br /> 0 = 암호화되지 않음<br /><br /> 1 = 암호화됨<br /><br /> 열은 Null을 허용하지 않습니다.|  
|**query_plan**|**xml**|*Plan_handle*로 지정 된 실제 쿼리 실행 계획의 마지막으로 알려진 런타임 실행 계획 표현을 포함 합니다. 실행 계획은 XML 형식입니다. 임시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 저장 프로시저 호출, 사용자 정의 함수 호출 등이 포함된 각 일괄 처리에 대해 계획 하나가 생성됩니다.<br /><br /> 열이 Null 값을 허용합니다.| 

## <a name="remarks"></a>설명
이 시스템 함수는 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.4부터 사용할 수 있습니다.

이는 옵트인 기능이며 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451을 사용하도록 설정해야 합니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.5부터 데이터베이스 수준에서 이를 수행하려면 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)의 LAST_QUERY_PLAN_STATS 옵션을 참조하세요.

이 시스템 함수는 **경량** 쿼리 실행 통계 프로 파일링 인프라에서 작동 합니다. 자세한 내용은 [쿼리 프로파일링 인프라](../../relational-databases/performance/query-profiling-infrastructure.md)를 참조하세요.  

Sys. dm_exec_query_plan_stats의 실행 계획 출력은 다음 정보를 포함 합니다.
-  캐시 된 계획에 있는 모든 컴파일 시간 정보
-  초당 실제 행 수, 총 쿼리 CPU 시간 및 실행 시간, 분산 경고, 실제 DOP, 사용 되는 최대 메모리 및 부여 된 메모리와 같은 런타임 정보

다음 조건에서 **실제 실행 계획에 해당** 하는 실행 계획 출력은 **sys. dm_exec_query_plan_stats**에 대해 반환 된 테이블의 **query_plan** 열에 반환 됩니다.  

-   이 계획은 [dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)에서 찾을 수 있습니다.     
    **하거나**    
-   실행 되는 쿼리는 복잡 하거나 리소스를 사용 합니다.

다음 조건에서는 dm_exec_query_plan_stats에 대해 반환 된 테이블의 **query_plan** 열에서 **간소화 된 <sup>1</sup> ** 실행 계획 출력이 반환 됩니다 **.**  

-   이 계획은 [dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)에서 찾을 수 있습니다.     
    **하거나**    
-   이 쿼리는 일반적으로 OLTP 워크 로드의 일부로 분류 되어 충분히 간단 합니다.

<sup>1</sup> [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.5부터이는 루트 노드 연산자 (SELECT)만 포함 하는 실행 계획을 나타냅니다. CTP [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 2.4의 경우이는를 통해 `sys.dm_exec_cached_plans`사용 가능한 캐시 된 계획을 나타냅니다.

다음 조건에서는 **sys. dm_exec_query_plan_stats**에서 **출력이 반환 되지 않습니다** .

-   *Plan_handle* 를 사용 하 여 지정한 쿼리 계획이 계획 캐시에서 제거 되었습니다.     
    **디스크나**    
-   첫 번째 장소에서 쿼리 계획을 캐시할 수 없습니다. 자세한 내용은 [실행 계획 캐싱 및 다시 사용 ](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)을 참조 하세요.
  
> [!NOTE] 
> **Xml** 데이터 형식에서 허용 되는 중첩 수준 수의 제한으로 인해 **dm_exec_query_plan** 는 128 수준의 중첩 된 요소를 충족 하거나 초과 하는 쿼리 계획을 반환할 수 없습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는이 조건으로 인해 쿼리 계획에서 반환 하는 [오류 6335이 발생 했습니다](../../relational-databases/errors-events/database-engine-events-and-errors.md#errors-6000-to-6999). 서비스 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 팩 2 이상 버전에서 **QUERY_PLAN** 열은 NULL을 반환 합니다.  

## <a name="permissions"></a>사용 권한  
 서버에 대한 `VIEW SERVER STATE` 권한이 필요합니다.  

## <a name="examples"></a>예  
  
### <a name="a-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan"></a>A. 특정 캐시 된 계획에 대 한 마지막으로 알려진 실제 쿼리 실행 계획 보기  
 다음 예에서는 **dm_exec_cached_plans** 를 쿼리하여 흥미로운 요금제를 찾고 출력 `plan_handle` 에서 복사 합니다.  
  
```sql  
SELECT * FROM sys.dm_exec_cached_plans;  
GO  
```  
  
그런 다음 마지막으로 알려진 실제 쿼리 실행 계획을 가져오려면 시스템 함수 `plan_handle` **sys. dm_exec_query_plan_stats**로 복사 된를 사용 합니다.  
  
```sql  
SELECT * FROM sys.dm_exec_query_plan_stats(< copied plan_handle >);  
GO  
```   

### <a name="b-looking-at-last-known-actual-query-execution-plan-for-all-cached-plans"></a>B. 모든 캐시 된 계획에 대 한 마지막으로 알려진 실제 쿼리 실행 계획 보기
  
```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps;  
GO  
```   

### <a name="c-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan-and-query-text"></a>C. 특정 캐시 된 계획 및 쿼리 텍스트에 대 한 마지막으로 알려진 실제 쿼리 실행 계획 보기

```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps
WHERE st.text LIKE 'SELECT * FROM Person.Person%';  
GO  
```   

### <a name="d-look-at-cached-events-for-trigger"></a>D. 트리거의 캐시 된 이벤트 살펴보기

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

## <a name="see-also"></a>참고 항목
  [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;실행 관련 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  

