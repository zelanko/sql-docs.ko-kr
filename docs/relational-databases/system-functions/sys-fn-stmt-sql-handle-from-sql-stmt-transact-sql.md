---
title: sys. fn_stmt_sql_handle_from_sql_stmt (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 6794e073-0895-4507-aba3-c3545acc843f
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9ffc1ca0ec2e44377012f4149255bca80bce6af7
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002994"
---
# <a name="sysfn_stmt_sql_handle_from_sql_stmt-transact-sql"></a>sys. fn_stmt_sql_handle_from_sql_stmt (Transact-sql)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  **stmt_sql_handle** [!INCLUDE[tsql](../../includes/tsql-md.md)] 지정 된 매개 변수화 형식 (simple 또는 강제) 아래에 있는 문의 stmt_sql_handle를 가져옵니다. 이렇게 하면 텍스트를 알고 있을 때 **stmt_sql_handle** 를 사용 하 여 쿼리 저장소에 저장 된 쿼리를 참조할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 핸들을 원하는 쿼리 저장소의 쿼리 텍스트입니다. *query_sql_text* 은 **nvarchar (max)** 이며 기본값은 없습니다.  
  
 *query_param_type*  
 쿼리의 매개 변수 형식입니다. *query_param_type* 는 **tinyint**입니다. 가능한 값은  
  
-   NULL-기본값은 0입니다.  
  
-   0 - 없음  
  
-   1-사용자  
  
-   2-단순  
  
-   3-강제  
  
## <a name="columns-returned"></a>반환되는 열  
 다음 표에서는 fn_stmt_sql_handle_from_sql_stmt에서 반환 하는 열을 나열 합니다.  
  
|열 이름|Type|Description|  
|-----------------|----------|-----------------|  
|**statement_sql_handle**|**varbinary(64)**|SQL 핸들입니다.|  
|**query_sql_text**|**nvarchar(max)**|[!INCLUDE[tsql](../../includes/tsql-md.md)]문의 텍스트입니다.|  
|**query_parameterization_type**|**tinyint**|쿼리 매개 변수화 형식입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
  
## <a name="permissions"></a>권한  
 데이터베이스에 대 한 **EXECUTE** 권한과 쿼리 저장소 카탈로그 뷰에 대 한 **삭제** 권한이 필요 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 문을 실행 한 다음를 사용 하 여 `sys.fn_stmt_sql_handle_from_sql_stmt` 해당 문의 SQL 핸들을 반환 합니다.  
  
```  
SELECT * FROM sys.databases;   
SELECT * FROM sys.fn_stmt_sql_handle_from_sql_stmt('SELECT * FROM sys.databases', NULL);  
```  
  
 함수를 사용 하 여 쿼리 저장소 데이터와 기타 동적 관리 뷰 간의 상관 관계를 바꿉니다. 다음 예제가 하는 일:  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_query_store_force_plan &#40;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
 [sp_query_store_remove_plan &#40;Transct-sql&-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [Transact-sql&#41;sp_query_store_unforce_plan &#40;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [Transact-sql&#41;sp_query_store_reset_exec_stats &#40;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [Transact-sql&#41;sp_query_store_flush_db &#40;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)   
 [Transact-sql&#41;sp_query_store_remove_query &#40;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [Transact-sql&#41;&#40;카탈로그 뷰 쿼리 저장소](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  
