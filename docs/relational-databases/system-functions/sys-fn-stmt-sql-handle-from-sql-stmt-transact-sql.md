---
title: sys.fn_stmt_sql_handle_from_sql_stmt (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 6794e073-0895-4507-aba3-c3545acc843f
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c3ee062aeadaec0c79af0b822b50442d4c575902
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="sysfnstmtsqlhandlefromsqlstmt-transact-sql"></a>sys.fn_stmt_sql_handle_from_sql_stmt (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  가져옵니다는 **stmt_sql_handle** 에 대 한 한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 문을 매개 변수화 유형 (단순 또는 강제)를 제공 합니다. 사용 하 여 쿼리 저장소에 저장 된 쿼리를 참조할 수 있습니다 자신의 **stmt_sql_handle** 해당 텍스트를 알고 있는 경우.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sys.fn_stmt_sql_handle_from_sql_stmt   
(  
    'query_sql_text',   
    [ query_param_type   
) [;]  
```  
  
## <a name="arguments"></a>인수  
 *query_sql_text*  
 핸들을 원하는 쿼리 저장소에 있는 쿼리의 텍스트가입니다. *query_sql_text* 는 **nvarchar (max)**, 기본값은 없습니다.  
  
 *query_param_type*  
 쿼리 매개 변수 유형이입니다. *query_param_type* 는 **tinyint**합니다. 가능한 값은  
  
-   기본값은 0-NULL  
  
-   0-없음  
  
-   1-사용자  
  
-   2 – 단순  
  
-   3 – 강제  
  
## <a name="columns-returned"></a>반환되는 열  
 다음 표에서 열이 나열 되어 해당 sys.fn_stmt_sql_handle_from_sql_stmt 반환 합니다.  
  
|열 이름|유형|Description|  
|-----------------|----------|-----------------|  
|**statement_sql_handle**|**varbinary(64)**|SQL 핸들입니다.|  
|**query_sql_text**|**nvarchar(max)**|텍스트는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문.|  
|**query_parameterization_type**|**tinyint**|쿼리 매개 변수화 유형입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
  
## <a name="permissions"></a>Permissions  
 필요는 **EXECUTE** 데이터베이스에 대 한 권한 및 **삭제** 쿼리 저장소 카탈로그 뷰에 대 한 권한이 있습니다.  
  
## <a name="examples"></a>예  
 다음 예제는 문을 실행 하 고 다음 사용 하 여 `sys.fn_stmt_sql_handle_from_sql_stmt` 를 해당 문의 SQL 핸들을 반환 합니다.  
  
```  
SELECT * FROM sys.databases;   
SELECT * FROM sys.fn_stmt_sql_handle_from_sql_stmt('SELECT * FROM sys.databases', NULL);  
```  
  
 다른 동적 관리 뷰와 쿼리 저장소 데이터를 상호 연결 하는 함수를 사용 합니다. 다음 예제:  
  
```  
SELECT qt.query_text_id, q.query_id, qt.query_sql_text, qt.statement_sql_handle,  
q.context_settings_id, qs.statement_context_id   
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_id  
CROSS APPLY sys.fn_stmt_sql_handle_from_sql_stmt (qt.query_sql_text, null) AS fn_handle_from_stmt  
JOIN sys.dm_exec_query_stats AS qs   
    ON fn_handle_from_stmt.statement_sql_handle = qs.statement_sql_handle;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_query_store_force_plan&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
 [sp_query_store_remove_plan&#40; Transct-sql&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [sp_query_store_unforce_plan&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [sp_query_store_reset_exec_stats&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [sp_query_store_flush_db&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)   
 [sp_query_store_remove_query&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  
