---
description: sys.dm_exec_query_plan(Transact-SQL)
title: sys. dm_exec_query_plan (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_plan_TSQL
- sys.dm_exec_query_plan
- dm_exec_query_plan
- sys.dm_exec_query_plan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_plan dynamic management function
ms.assetid: e26f0867-9be3-4b2e-969e-7f2840230770
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 741cfebb7eb50e37512a5778691ab61700f9d98e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548561"
---
# <a name="sysdm_exec_query_plan-transact-sql"></a>sys.dm_exec_query_plan(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

계획 핸들로 지정한 일괄 처리에 대한 XML 형식의 실행 계획을 반환합니다. 계획 핸들로 지정된 계획은 캐시되거나 현재 실행 중일 수 있습니다.  
  
실행 계획에 대 한 XML 스키마가 게시 되며 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)에서 사용할 수 있습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이 설치된 디렉터리에서도 사용할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sys.dm_exec_query_plan(plan_handle)  
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
|**query_plan**|**xml**|*Plan_handle*지정 된 쿼리 실행 계획의 컴파일 시간 실행 계획 표현을 포함 합니다. 실행 계획은 XML 형식입니다. 임시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 저장 프로시저 호출, 사용자 정의 함수 호출 등이 포함된 각 일괄 처리에 대해 계획 하나가 생성됩니다.<br /><br /> 열이 Null 값을 허용합니다.|  
  
## <a name="remarks"></a>설명  
 다음과 같은 경우 **sys.dm_exec_query_plan**에 대해 반환된 테이블의 **query_plan** 열에 실행 계획 출력이 반환되지 않습니다.  
  
-   *Plan_handle* 를 사용 하 여 지정한 쿼리 계획이 계획 캐시에서 제거 된 경우 반환 된 테이블의 **query_plan** 열은 null입니다. 예를 들어 계획 핸들을 캡처한 시간과 **sys.dm_exec_query_plan**에 사용한 시간 사이에 지연이 있을 경우 이러한 상황이 발생할 수 있습니다.  
  
-   대량 작업 문이나 8KB를 넘는 문자열 리터럴이 포함된 문과 같은 일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 캐시되지 않습니다. 이러한 문의 XML 실행 계획은 캐시에 없기 때문에 일괄 처리가 현재 실행되고 있지 않으면 **sys.dm_exec_query_plan**을 사용하여 검색할 수 없습니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]EXEC (*string*)를 사용 하는 경우와 같이 일괄 처리 또는 저장 프로시저가 사용자 정의 함수에 대 한 호출을 포함 하거나 동적 SQL에 대 한 호출을 포함 하는 경우 사용자 정의 함수에 대 한 컴파일된 XML 실행 계획은 일괄 처리 또는 저장 프로시저에 대 한 **dm_exec_query_plan** 에서 반환 된 테이블에 포함 되지 않습니다. 대신 사용자 정의 함수에 해당 하는 계획 핸들에 대해 **dm_exec_query_plan** 에 대 한 별도의 호출을 수행 해야 합니다.  
  
 임시 쿼리에서 간단한 매개 변수화 또는 강제 매개 변수화를 사용하는 경우 **query_plan** 열에는 문 텍스트만 포함되고 실제 쿼리 계획은 포함되지 않습니다. 쿼리 계획을 반환하려면 매개 변수가 있는 준비된 쿼리의 계획 핸들에 대한 **sys.dm_exec_query_plan**을 호출합니다. [sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) 뷰의 **sql** 열 또는 [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) 동적 관리 뷰의 텍스트 열을 참조하여 쿼리가 매개 변수화되었는지 여부를 확인할 수 있습니다.  
  
> [!NOTE] 
> **Xml** 데이터 형식에서 허용 되는 중첩 수준 수의 제한으로 인해 **dm_exec_query_plan** 는 128 수준의 중첩 된 요소를 충족 하거나 초과 하는 쿼리 계획을 반환할 수 없습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 상태로 인해 쿼리 계획을 반환하지 못했으므로 오류 6335가 발생합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]서비스 팩 2 이상 버전에서 **query_plan** 열은 NULL을 반환 합니다.   
> [Dm_exec_text_query_plan &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md) 동적 관리 함수를 사용 하 여 쿼리 계획의 출력을 텍스트 형식으로 반환할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Dm_exec_query_plan**를 실행 하려면 사용자가 **sysadmin** 고정 서버 역할의 멤버 이거나 `VIEW SERVER STATE` 서버에 대 한 권한이 있어야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 **sys.dm_exec_query_plan** 동적 관리 뷰를 사용하는 방법을 보여줍니다.  
  
 XML 실행 계획을 보려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 쿼리 편집기에서 다음 쿼리를 실행하고 **sys.dm_exec_query_plan**에 의해 반환된 테이블의 **query_plan** 열에서 **ShowPlanXML**을 클릭합니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 보고서 요약 창에 XML 실행 계획이 표시됩니다. XML 실행 계획을 파일에 저장 하려면 **query_plan** 열에서 **showplan XML** 을 마우스 오른쪽 단추로 클릭 하 고 다른 이름 **으로 결과 저장**을 클릭 하 고 파일 이름을. sqlplan로 지정 합니다 ( \<*file_name*> 예: myxmlshowplan. sqlplan).  
  
### <a name="a-retrieve-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>A. 실행 속도가 느린 Transact-SQL 쿼리 또는 일괄 처리에 대한 캐시된 쿼리 계획 검색  
 임시 일괄 처리, 저장 프로시저, 사용자 정의 함수 등 다양한 유형의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리에 대한 쿼리 계획은 계획 캐시라는 메모리 영역에서 캐시됩니다. 캐시된 쿼리 계획 각각은 계획 핸들이라는 고유 식별자로 식별됩니다. **sys.dm_exec_query_plan** 동적 관리 뷰에 이 계획 핸들을 지정하여 특정 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 또는 일괄 처리에 대한 실행 계획을 검색할 수 있습니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]에 대한 특정 연결에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 또는 일괄 처리가 오랫동안 실행되는 경우 이 쿼리나 일괄 처리에 대한 실행 계획을 검색하여 지연 원인을 알아낼 수 있습니다. 다음 예에서는 실행 속도가 느린 쿼리나 일괄 처리에 대한 XML 실행 계획을 검색하는 방법을 보여 줍니다.  
  
> [!NOTE]  
>  이 예를 실행 하려면 *session_id* 의 값과 *plan_handle* 를 서버에 특정 한 값으로 바꿉니다.  
  
 먼저 `sp_who` 저장 프로시저를 사용하여 쿼리 또는 일괄 처리를 실행 중인 프로세스의 SPID(서버 프로세스 ID)를 검색합니다.  
  
```sql  
USE master;  
GO  
exec sp_who;  
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
  
 **Dm_exec_requests** 에서 반환 하는 테이블은 실행 속도가 느려지는 쿼리 또는 일괄 처리에 대 한 계획 핸들이 `0x06000100A27E7C1FA821B10600` *plan_handle* `sys.dm_exec_query_plan` 다음과 같이 XML 형식의 실행 계획을 검색 하는 데 사용 하는 plan_handle 인수로 지정할 수 있음을 나타냅니다. 실행 속도가 느린 쿼리나 일괄 처리에 대한 XML 형식의 실행 계획은 `sys.dm_exec_query_plan`에 의해 반환되는 테이블의 **query_plan** 열에 포함됩니다.  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_query_plan (0x06000100A27E7C1FA821B10600);  
GO  
```  
  
### <a name="b-retrieve-every-query-plan-from-the-plan-cache"></a>B. 계획 캐시에서 모든 쿼리 계획 검색  
 계획 캐시에 있는 모든 쿼리 계획의 스냅샷을 검색하려면 `sys.dm_exec_cached_plans` 동적 관리 뷰를 쿼리하여 캐시에 있는 모든 쿼리 계획의 계획 핸들을 검색합니다. 계획 핸들은 `plan_handle`의 `sys.dm_exec_cached_plans` 열에 저장됩니다. 그런 다음 CROSS APPLY 연산자를 사용하여 다음과 같이 계획 핸들을 `sys.dm_exec_query_plan`으로 전달합니다. 계획 캐시에 있는 각 계획의 XML 실행 계획 출력은 현재 반환된 테이블의 `query_plan` 열에 있습니다.  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_cached_plans AS cp 
CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
GO  
```  
  
### <a name="c-retrieve-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. 서버가 계획 캐시에서 쿼리 통계를 수집한 모든 쿼리 계획 검색  
 서버가 통계를 수집한 현재 계획 캐시에 있는 모든 쿼리 계획의 스냅샷을 검색하려면 `sys.dm_exec_query_stats` 동적 관리 뷰를 쿼리하여 캐시에서 이 계획의 계획 핸들을 검색합니다. 계획 핸들은 `plan_handle`의 `sys.dm_exec_query_stats` 열에 저장됩니다. 그런 다음 CROSS APPLY 연산자를 사용하여 다음과 같이 계획 핸들을 `sys.dm_exec_query_plan`으로 전달합니다. 서버가 통계를 수집한 현재 계획 캐시에 있는 각 계획의 XML 실행 계획 출력은 반환된 테이블의 `query_plan` 열에 있습니다.  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_query_stats AS qs 
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle);  
GO  
```  
  
### <a name="d-retrieve-information-about-the-top-five-queries-by-average-cpu-time"></a>D. 평균 CPU 시간별 상위 5개 쿼리에 대한 정보 검색  
 다음 예에서는 상위 5개 쿼리에 대한 계획과 평균 CPU 시간을 반환합니다.  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
   plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_exec_cached_plans&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [dm_exec_query_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sp_who&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [실행 계획 논리 및 물리 연산자 참조](../../relational-databases/showplan-logical-and-physical-operators-reference.md)   
 [dm_exec_text_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)  
  
  
