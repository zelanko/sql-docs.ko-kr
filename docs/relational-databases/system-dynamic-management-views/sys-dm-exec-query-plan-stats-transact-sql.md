---
title: sys.dm_exec_query_plan_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
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
ms.openlocfilehash: 89185976120c15f9d1fcdfef75f2bddb41415c65
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63474282"
---
# <a name="sysdmexecqueryplanstats-transact-sql"></a>sys.dm_exec_query_plan_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

이전에 캐시 된 쿼리 계획에 마지막으로 알려진된 실제 실행 계획에 해당 하는을 반환합니다. 

## <a name="syntax"></a>구문

```
sys.dm_exec_query_plan_stats(plan_handle)  
``` 

## <a name="arguments"></a>인수 
*plan_handle*  
실행 된 일괄 처리에 대 한 쿼리 실행 계획을 고유 하 게 식별 하는 토큰 및 해당 계획은 계획 캐시에 되거나 현재 실행 합니다. *plan_handle* 됩니다 **varbinary(64)** 합니다.   

합니다 *plan_handle* 다음 동적 관리 개체에서 가져올 수 있습니다.  
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests&#40;Transact-SQL&#41](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  

## <a name="table-returned"></a>반환된 테이블

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|
|**dbid**|**smallint**|이 계획에 해당하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 컴파일할 당시 유효했던 컨텍스트 데이터베이스의 ID입니다. 임시 및 준비된 SQL 문의 경우 문이 컴파일된 데이터베이스의 ID입니다.<br /><br /> 열이 Null 값을 허용합니다.|  
|**objectid**|**int**|이 쿼리 계획에 대한 저장 프로시저나 사용자 정의 함수와 같은 개체의 ID입니다. 임시 및 준비 된 일괄 처리에 대 한이 열은 **null**.<br /><br /> 열이 Null 값을 허용합니다.|  
|**number**|**smallint**|번호가 매겨진 저장 프로시저 정수입니다. 등의 절차에 대 한 그룹의 **주문** 응용 프로그램 이름은 **orderproc; 1**, **orderproc; 2**등. 임시 및 준비 된 일괄 처리에 대 한이 열은 **null**.<br /><br /> 열이 Null 값을 허용합니다.|  
|**encrypted**|**bit**|해당 저장 프로시저가 암호화되었는지 여부를 나타냅니다.<br /><br /> 0 = 암호화되지 않음<br /><br /> 1 = 암호화됨<br /><br /> 열은 Null을 허용하지 않습니다.|  
|**query_plan**|**xml**|마지막으로 알려진된 런타임 실행 계획 표현을 사용 하 여 지정 된 실제 쿼리 실행 계획 포함 *plan_handle*합니다. 실행 계획은 XML 형식입니다. 임시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 저장 프로시저 호출, 사용자 정의 함수 호출 등이 포함된 각 일괄 처리에 대해 계획 하나가 생성됩니다.<br /><br /> 열이 Null 값을 허용합니다.| 

## <a name="remarks"></a>Remarks
이 시스템 함수는 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.4.

이는 옵트인 기능이며 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451을 사용하도록 설정해야 합니다. 부터는 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.5 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]을 데이터베이스 수준에서이 작업을 수행 합니다 LAST_QUERY_PLAN_STATS 옵션을 참조 하십시오 [ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

이 시스템 함수에서 작동 합니다 **경량** 쿼리 실행 통계 인프라를 프로 파일링 합니다. 자세한 내용은 [쿼리 프로파일링 인프라](../../relational-databases/performance/query-profiling-infrastructure.md)를 참조하세요.  

실행 계획 출력에서 다음과 같은 경우 **실제 실행 계획에 해당 하는** 반환 되는 **query_plan** 에 대 한 반환된 된 테이블의 열 **sys.dm_exec_query_plan_ 통계**:  

-   계획을 찾을 수 있습니다 [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)합니다.     
    **AND**    
-   실행 중인 쿼리가 복잡 하거나 리소스를 많이 소비입니다.

다음과 같은 경우에 **간소화 된 <sup>1</sup>**  실행 계획 출력에 반환 됩니다는 **query_plan** 에 대 한 반환된 된 테이블의 열 **sys.dm_exec_ query_plan_stats**:  

-   계획을 찾을 수 있습니다 [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)합니다.     
    **AND**    
-   쿼리는 일반적으로 OLTP 워크 로드의 일부로 분류 충분히 간단 합니다.

<sup>1</sup> 부터 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.5만 루트 노드가 연산자 (선택)를 포함 하는 실행 계획을 나타냅니다. 에 대 한 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.4를 통해 사용 가능한 캐시 된 계획을 나타냅니다 `sys.dm_exec_cached_plans`합니다.

다음 조건을 **출력이 반환 됩니다** 에서 **sys.dm_exec_query_plan_stats**:

-   사용 하 여 지정 된 쿼리 계획 *plan_handle* 계획 캐시에서 제거 되었습니다.     
    **OR**    
-   쿼리 계획에서 처음에 캐시할 수 없습니다. 자세한 내용은 [실행 계획 캐싱 및 재사용 ](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)합니다.
  
> [!NOTE] 
> 에 허용 된 중첩된 수준 수가 제한으로 인해 합니다 **xml** 데이터 형식 **sys.dm_exec_query_plan** 중첩 요소의 128 수준을 충족 하거나 초과 하는 쿼리 계획을 반환할 수 없습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],이 조건은 인해 쿼리 계획을 반환 하 고 생성 [오류 6335가 발생](../../relational-databases/errors-events/database-engine-events-and-errors.md#errors-6000-to-6999)합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 서비스 팩 2 및 이후 버전에서는 합니다 **query_plan** 열 NULL을 반환 합니다.  

## <a name="permissions"></a>사용 권한  
 서버에 대한 `VIEW SERVER STATE` 권한이 필요합니다.  

## <a name="examples"></a>예  
  
### <a name="a-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan"></a>1. 특정 캐시 된 계획에 대 한 마지막으로 알려진된 실제 쿼리 실행 계획 검색  
 다음 예제에서는 쿼리 **sys.dm_exec_cached_plans** 흥미로운 계획 및 복사를 찾으려면 해당 `plan_handle` 출력에서 합니다.  
  
```sql  
SELECT * FROM sys.dm_exec_cached_plans;  
GO  
```  
  
그런 다음 마지막으로 알려진된 실제 쿼리 실행 계획을 가져오려면 사용 하 여 복사한 `plan_handle` 시스템 함수를 사용 하 여 **sys.dm_exec_query_plan_stats**합니다.  
  
```sql  
SELECT * FROM sys.dm_exec_query_plan_stats(< copied plan_handle >);  
GO  
```   

### <a name="b-looking-at-last-known-actual-query-execution-plan-for-all-cached-plans"></a>2. 모든 캐시 된 계획에 대 한 마지막으로 알려진된 실제 쿼리 실행 계획 검색
  
```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps;  
GO  
```   

### <a name="c-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan-and-query-text"></a>3. 특정 캐시 된 계획 및 쿼리 텍스트에 대 한 마지막으로 알려진된 실제 쿼리 실행 계획 검색

```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps
WHERE st.text LIKE 'SELECT * FROM Person.Person%';  
GO  
```   

### <a name="d-look-at-cached-events-for-trigger"></a>4. 트리거에 대 한 캐시 된 이벤트

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

## <a name="see-also"></a>관련 항목
  [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  

