---
title: sys. dm_exec_text_query_plan (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_text_query_plan
- sys.dm_exec_text_query_plan_TSQL
- dm_exec_text_query_plan_TSQL
- sys.dm_exec_text_query_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_text_query_plan dynamic management function
ms.assetid: 9d5e5f59-6973-4df9-9eb2-9372f354ca57
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 082de052d40cc41a81ea7a0963b2e3174338b8a5
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824588"
---
# <a name="sysdm_exec_text_query_plan-transact-sql"></a>sys.dm_exec_text_query_plan(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

[!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 또는 일괄 처리 내 특정 문에 대한 텍스트 형식의 실행 계획을 반환합니다. 계획 핸들로 지정된 쿼리 계획은 캐시되거나 현재 실행 중일 수 있습니다. 이 테이블 반환 함수는 [dm_exec_query_plan &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)와 유사 하지만 다음과 같은 차이점이 있습니다.  
  
-   쿼리 계획의 출력은 텍스트 형식으로 반환됩니다.  
-   쿼리 계획의 출력 크기는 제한되지 않습니다.  
-   일괄 처리 내 개별 문을 지정할 수 있습니다.  
  
**적용**대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] .
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sys.dm_exec_text_query_plan   
(   
    plan_handle   
    , { statement_start_offset | 0 | DEFAULT }  
        , { statement_end_offset | -1 | DEFAULT }  
)  
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
  
*statement_start_offset* | 0 | 기본  
일괄 처리 또는 지속형 개체의 텍스트 내에서 행이 설명하는 쿼리의 시작 위치(바이트)를 나타냅니다. *statement_start_offset* 은 **int**입니다. 값 0은 일괄 처리의 시작을 나타냅니다. 기본값은 0입니다.  
  
다음 동적 관리 개체에서 문 시작 오프셋을 얻을 수 있습니다.  
  
-  [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-  [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
*statement_end_offset* | -1 | 기본  
일괄 처리 또는 지속형 개체의 텍스트 내에서 행이 설명하는 쿼리의 끝 위치(바이트)를 나타냅니다.  
  
*statement_start_offset* 은 **int**입니다.  
  
값이 -1인 경우 일괄 처리의 끝을 나타냅니다. 기본값은 -1입니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|이 계획에 해당하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 컴파일할 당시 유효했던 컨텍스트 데이터베이스의 ID입니다. 임시 및 준비된 SQL 문의 경우 문이 컴파일된 데이터베이스의 ID입니다.<br /><br /> 열이 Null 값을 허용합니다.|  
|**objectid**|**int**|이 쿼리 계획에 대한 저장 프로시저나 사용자 정의 함수와 같은 개체의 ID입니다. 임시 및 준비된 일괄 처리의 경우 이 열은 **Null**입니다.<br /><br /> 열이 Null 값을 허용합니다.|  
|**number**|**smallint**|번호가 매겨진 저장 프로시저 정수입니다. 예를 들어 **orders** 응용 프로그램에 대한 프로시저 그룹에 **orderproc;1**, **orderproc;2** 등의 이름을 지정할 수 있습니다. 임시 및 준비된 일괄 처리의 경우 이 열은 **Null**입니다.<br /><br /> 열이 Null 값을 허용합니다.|  
|**됨**|**bit**|해당 저장 프로시저가 암호화되었는지 여부를 나타냅니다.<br /><br /> 0 = 암호화되지 않음<br /><br /> 1 = 암호화됨<br /><br /> 열은 Null을 허용하지 않습니다.|  
|**query_plan**|**nvarchar(max)**|*Plan_handle*지정 된 쿼리 실행 계획의 컴파일 시간 실행 계획 표현을 포함 합니다. 실행 계획은 텍스트 형식입니다. 임시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 저장 프로시저 호출, 사용자 정의 함수 호출 등이 포함된 각 일괄 처리에 대해 계획 하나가 생성됩니다.<br /><br /> 열이 Null 값을 허용합니다.|  
  
## <a name="remarks"></a>설명  
 다음과 같은 경우 **sys.dm_exec_text_query_plan**에 대해 반환된 테이블의 **plan** 열에 실행 계획 출력이 반환되지 않습니다.  
  
-   *Plan_handle* 를 사용 하 여 지정한 쿼리 계획이 계획 캐시에서 제거 된 경우 반환 된 테이블의 **query_plan** 열은 null입니다. 예를 들어 계획 핸들을 캡처한 시간과 **sys.dm_exec_text_query_plan**에 사용한 시간 사이에 지연이 있을 경우 이러한 상황이 발생할 수 있습니다.  
  
-   대량 작업 문이나 8KB를 넘는 문자열 리터럴이 포함된 문과 같은 일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 캐시되지 않습니다. 이러한 문의 실행 계획은 캐시에 없기 때문에 **sys.dm_exec_text_query_plan**을 사용하여 검색할 수 없습니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]EXEC (*string*)를 사용 하는 경우와 같이 일괄 처리 또는 저장 프로시저가 사용자 정의 함수에 대 한 호출을 포함 하거나 동적 SQL에 대 한 호출을 포함 하는 경우 사용자 정의 함수에 대 한 컴파일된 XML 실행 계획은 일괄 처리 또는 저장 프로시저에 대 한 **dm_exec_text_query_plan** 에서 반환 된 테이블에 포함 되지 않습니다. 대신 사용자 정의 함수에 해당 하는 *plan_handle* 에 대해 **dm_exec_text_query_plan** 에 대 한 별도의 호출을 수행 해야 합니다.  
  
임시 쿼리가 [단순](../../relational-databases/query-processing-architecture-guide.md#SimpleParam) [매개 변수화 또는 강제 매개 변수화](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)를 사용 하는 경우 **query_plan** 열에는 문 텍스트만 포함 되 고 실제 쿼리 계획은 포함 되지 않습니다. 쿼리 계획을 반환하려면 매개 변수가 있는 준비된 쿼리의 계획 핸들에 대한 **sys.dm_exec_text_query_plan**을 호출합니다. [sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) 뷰의 **sql** 열 또는 [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) 동적 관리 뷰의 텍스트 열을 참조하여 쿼리가 매개 변수화되었는지 여부를 확인할 수 있습니다.  
  
## <a name="permissions"></a>권한  
 **sys.dm_exec_text_query_plan**을 실행하려면 **sysadmin** 고정 서버 역할의 멤버이거나 해당 서버에서 VIEW SERVER STATE 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-retrieving-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>A. 실행 속도가 느린 Transact-SQL 쿼리 또는 일괄 처리에 대한 캐시된 쿼리 계획 검색  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]에 대한 특정 연결에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 또는 일괄 처리가 오랫동안 실행되는 경우 이 쿼리나 일괄 처리에 대한 실행 계획을 검색하여 지연 원인을 알아낼 수 있습니다. 다음 예에서는 실행 속도가 느린 쿼리나 일괄 처리에 대한 실행 계획을 검색하는 방법을 보여 줍니다.  
  
> [!NOTE]  
> 이 예를 실행 하려면 *session_id* 의 값과 *plan_handle* 를 서버에 특정 한 값으로 바꿉니다.  
  
 먼저 `sp_who` 저장 프로시저를 사용하여 쿼리 또는 일괄 처리를 실행 중인 프로세스의 SPID(서버 프로세스 ID)를 검색합니다.  
  
```sql  
USE master;  
GO  
EXEC sp_who;  
GO  
```  
  
 `sp_who`에 의해 반환되는 결과 집합은 SPID가 `54`임을 나타냅니다. `sys.dm_exec_requests` 동적 관리 뷰에 이 SPID를 사용하여 다음 쿼리를 통해 계획 핸들을 검색할 수 있습니다.  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_requests  
WHERE session_id = 54;  
GO  
```  
  
 **sys.dm_exec_requests**가 반환하는 테이블은 실행 속도가 느린 쿼리나 일괄 처리에 대한 계획 핸들이 `0x06000100A27E7C1FA821B10600`임을 나타냅니다. 다음 예에서는 지정 계획 핸들에 대한 쿼리 계획을 반환하고 쿼리 또는 일괄 처리의 모든 문을 반환하도록 기본값 0 및 -1을 사용합니다.  
  
```sql  
USE master;  
GO  
SELECT query_plan   
FROM sys.dm_exec_text_query_plan (0x06000100A27E7C1FA821B10600,0,-1);  
GO  
```  
  
### <a name="b-retrieving-every-query-plan-from-the-plan-cache"></a>B. 계획 캐시에서 모든 쿼리 계획 검색  
 계획 캐시에 있는 모든 쿼리 계획의 스냅샷을 검색하려면 `sys.dm_exec_cached_plans` 동적 관리 뷰를 쿼리하여 캐시에 있는 모든 쿼리 계획의 계획 핸들을 검색합니다. 계획 핸들은 `plan_handle`의 `sys.dm_exec_cached_plans` 열에 저장됩니다. 그런 다음 CROSS APPLY 연산자를 사용하여 다음과 같이 계획 핸들을 `sys.dm_exec_text_query_plan`으로 전달합니다. 현재 계획 캐시에 있는 각 계획의 실행 계획 출력은 반환 되는 `query_plan` 테이블의 열에 있습니다.  
  
```sql  
USE master;  
GO  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_text_query_plan(cp.plan_handle, DEFAULT, DEFAULT);  
GO  
```  
  
### <a name="c-retrieving-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. 서버가 계획 캐시에서 쿼리 통계를 수집한 모든 쿼리 계획 검색  
 서버가 통계를 수집한 현재 계획 캐시에 있는 모든 쿼리 계획의 스냅샷을 검색하려면 `sys.dm_exec_query_stats` 동적 관리 뷰를 쿼리하여 캐시에서 이 계획의 계획 핸들을 검색합니다. 계획 핸들은 `plan_handle`의 `sys.dm_exec_query_stats` 열에 저장됩니다. 그런 다음 CROSS APPLY 연산자를 사용하여 다음과 같이 계획 핸들을 `sys.dm_exec_text_query_plan`으로 전달합니다. 각 계획의 실행 계획 출력은 반환된 테이블의 `query_plan` 열에 있습니다.  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset);  
GO  
```  
  
### <a name="d-retrieving-information-about-the-top-five-queries-by-average-cpu-time"></a>D. 평균 CPU 시간별 상위 5개 쿼리에 대한 정보 검색  
 다음 예에서는 상위 5개 쿼리에 대한 쿼리 계획과 평균 CPU 시간을 반환합니다. **sys.dm_exec_text_query_plan** 함수는 쿼리 계획에서 일괄 처리의 모든 문을 반환하도록 기본값 0 및 -1을 지정합니다.  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
Plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, 0, -1)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [dm_exec_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
