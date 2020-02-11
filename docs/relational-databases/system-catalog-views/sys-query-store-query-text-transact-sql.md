---
title: sys. query_store_query_text (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_QUERY_TEXT
- QUERY_STORE_QUERY_TEXT
- SYS.QUERY_STORE_QUERY_TEXT_TSQL
- QUERY_STORE_QUERY_TEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_store_query_text catalog view
- query_store_query_text catalog view
ms.assetid: f7032fa0-7c16-4492-bb82-685806c63a8c
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b90f6641724ed526a9f7b496b792bb6cf786105f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70000792"
---
# <a name="sysquery_store_query_text-transact-sql"></a>sys. query_store_query_text (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  쿼리의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 텍스트와 SQL 핸들을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**query_text_id**|**bigint**|기본 키입니다.|  
|**query_sql_text**|**nvarchar(max)**|사용자가 제공한 쿼리의 SQL 텍스트입니다. 에는 공백, 힌트 및 주석이 포함 됩니다. 쿼리 텍스트 전후의 주석 및 공백은 무시됩니다. 텍스트 내의 주석 및 공백은 무시되지 않습니다.|  
|**statement_sql_handle**|**vabinary (64)**|개별 쿼리의 SQL 핸들입니다.|  
|**is_part_of_encrypted_module**|**bit**|쿼리 텍스트는 암호화 된 모듈의 일부입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**has_restricted_text**|**bit**|쿼리 텍스트에 암호 또는 기타 기타 권한 없는 단어가 포함 되어 있습니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
  
## <a name="permissions"></a>사용 권한  
 **VIEW DATABASE STATE** 권한이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [query_context_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [query_store_wait_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [쿼리 저장소 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [fn_stmt_sql_handle_from_sql_stmt &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
