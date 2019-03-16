---
title: sys.dm_exec_sql_text (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_sql_text
- sys.dm_exec_sql_text
- sys.dm_exec_sql_text_TSQL
- dm_exec_sql_text_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_sql_text dynamic management function
ms.assetid: 61b8ad6a-bf80-490c-92db-58dfdff22a24
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 48554e48d09822b23320d36080084d4947882736
ms.sourcegitcommit: d92ad400799d8b74d5c601170167b86221f68afb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2019
ms.locfileid: "58080285"
---
# <a name="sysdmexecsqltext-transact-sql"></a>sys.dm_exec_sql_text(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  즉에 일괄 처리 sql 텍스트를 반환 합니다. 지정 된 식별 *sql_handle*합니다. 시스템 함수를 대체 하는이 테이블 반환 함수 **fn_get_sql**합니다.  
  
 
## <a name="syntax"></a>구문  
  
```  
sys.dm_exec_sql_text(sql_handle | plan_handle)  
```  
  
## <a name="arguments"></a>인수  
*sql_handle*  
실행 되거나 현재 실행 하는 일괄 처리를 고유 하 게 식별 하는 토큰이입니다. *sql_handle* 됩니다 **varbinary(64)** 합니다. 

합니다 *sql_handle* 다음 동적 관리 개체에서 가져올 수 있습니다.  
  
-   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)  
  
-   [sys.dm_exec_xml_handles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)  
  
-   [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  
  
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
|**dbid**|**smallint**|데이터베이스의 ID입니다.<br /><br /> 임시 및 준비된 SQL 문의 경우 문이 컴파일된 데이터베이스의 ID입니다.|  
|**objectid**|**int**|개체의 ID입니다.<br /><br /> 임시 및 준비된 SQL 문의 경우 NULL입니다.|  
|**number**|**smallint**|번호가 있는 저장 프로시저의 경우 저장 프로시저의 번호가 이 열에 반환됩니다. 자세한 내용은 [sys.numbered_procedures &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md)합니다.<br /><br /> 임시 및 준비된 SQL 문의 경우 NULL입니다.|  
|**encrypted**|**bit**|1 = SQL 텍스트가 암호화됩니다.<br /><br /> 0 = SQL 텍스트가 암호화되지 않습니다.|  
|**text**|**nvarchar(max** **)**|SQL 쿼리의 텍스트입니다.<br /><br /> 암호화된 개체의 경우 NULL입니다.|  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 `VIEW SERVER STATE` 권한이 필요합니다.  
  
## <a name="remarks"></a>Remarks  
임시 쿼리를 SQL 핸들 서버로 전송 되는 SQL 텍스트 기반의 해시 값 이며 데이터베이스에서 발생할 수 있습니다. 

저장 프로시저, 트리거, 함수 등의 데이터베이스 개체용 SQL 핸들은 데이터베이스 ID, 개체 ID 및 개체 번호에서 파생됩니다. 

계획 핸들에는 전체 일괄 처리의 컴파일된 계획에서 파생 된 해시 값입니다. 

> [!NOTE]
> **dbid** 에서 확인할 수 없으므로 *sql_handle* 임시 쿼리에 대 한 합니다. 결정할 **dbid** 임시 쿼리를 사용 하 여 *plan_handle* 대신 합니다.
  
## <a name="examples"></a>예 

### <a name="a-conceptual-example"></a>1. 개념적 예제
다음은 전달 설명 하기 위해 기본 예제는 **sql_handle** 직접적으로 또는 사용 하 여 **CROSS APPLY**합니다.
  1.  활동을 만듭니다.  
새 쿼리 창에서 다음 T-SQL을 실행 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.   
      ```sql
      -- Identify current spid (session_id)
      SELECT @@SPID;
      GO
  
      -- Create activity
        WAITFOR DELAY '00:02:00';
      ```
      
    2.  사용 하 여 **CROSS APPLY**합니다.  
    sql_handle **sys.dm_exec_requests** 전달할 **sys.dm_exec_sql_text** 사용 하 여 **CROSS APPLY**합니다. 새 쿼리 창을 열고 1 단계에서 식별 된 spid를 전달 합니다. Spid가 이런 경우에이 예에서 `59`합니다.

        ```sql
        SELECT t.*
        FROM sys.dm_exec_requests AS r
        CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t
        WHERE session_id = 59 -- modify this value with your actual spid
         ```      
 
    2.  전달 **sql_handle** 직접.  
획득 합니다 **sql_handle** 에서 **sys.dm_exec_requests**합니다. 그런 다음 전달 된 **sql_handle** 에 직접 **sys.dm_exec_sql_text**합니다. 새 쿼리 창을 열고 1 단계에서 식별 된 spid 전달 **sys.dm_exec_requests**합니다. Spid가 이런 경우에이 예에서 `59`합니다. 그런 다음 반환 된 **sql_handle** 인수로 **sys.dm_exec_sql_text**합니다.

        ```sql
        -- acquire sql_handle
        SELECT sql_handle FROM sys.dm_exec_requests WHERE session_id = 59  -- modify this value with your actual spid
        
        -- pass sql_handle to sys.dm_exec_sql_text
        SELECT * FROM sys.dm_exec_sql_text(0x01000600B74C2A1300D2582A2100000000000000000000000000000000000000000000000000000000000000) -- modify this value with your actual sql_handle
         ```      
    
  
### <a name="b-obtain-information-about-the-top-five-queries-by-average-cpu-time"></a>2. 평균 CPU 시간별 상위 5 개 쿼리에 대 한 정보  
 다음 예에서는 상위 5개 쿼리에 대한 SQL 문 텍스트와 평균 CPU 시간을 반환합니다.  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
    SUBSTRING(st.text, (qs.statement_start_offset/2)+1,   
        ((CASE qs.statement_end_offset  
          WHEN -1 THEN DATALENGTH(st.text)  
         ELSE qs.statement_end_offset  
         END - qs.statement_start_offset)/2) + 1) AS statement_text  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
ORDER BY total_worker_time/execution_count DESC;  
```  
  
### <a name="c-provide-batch-execution-statistics"></a>3. 일괄 처리 실행 통계 제공  
 다음 예에서는 일괄 처리에서 실행되는 SQL 쿼리 텍스트를 반환하고 이에 대한 통계 정보를 제공합니다.  
  
```sql  
SELECT s2.dbid,   
    s1.sql_handle,    
    (SELECT TOP 1 SUBSTRING(s2.text,statement_start_offset / 2+1 ,   
      ( (CASE WHEN statement_end_offset = -1   
         THEN (LEN(CONVERT(nvarchar(max),s2.text)) * 2)   
         ELSE statement_end_offset END)  - statement_start_offset) / 2+1))  AS sql_statement,  
    execution_count,   
    plan_generation_num,   
    last_execution_time,     
    total_worker_time,   
    last_worker_time,   
    min_worker_time,   
    max_worker_time,  
    total_physical_reads,   
    last_physical_reads,   
    min_physical_reads,    
    max_physical_reads,    
    total_logical_writes,   
    last_logical_writes,   
    min_logical_writes,   
    max_logical_writes    
FROM sys.dm_exec_query_stats AS s1   
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS s2    
WHERE s2.objectid is null   
ORDER BY s1.sql_handle, s1.statement_start_offset, s1.statement_end_offset;  
```  
  
## <a name="see-also"></a>참고자료  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_cursors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)   
 [sys.dm_exec_xml_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [적용을 사용 하 여](../../t-sql/queries/from-transact-sql.md#using-apply)   [sys.dm_exec_text_query_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)  

