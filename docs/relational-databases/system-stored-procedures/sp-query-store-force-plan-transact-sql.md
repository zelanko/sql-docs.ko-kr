---
description: sp_query_store_force_plan (Transact-sql)
title: sp_query_store_force_plan (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.SP_QUERY_STORE_FORCE_PLAN
- SP_QUERY_STORE_FORCE_PLAN
- SYS.SP_QUERY_STORE_FORCE_PLAN_TSQL
- SP_QUERY_STORE_FORCE_PLAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_query_store_force_plan
- sp_query_store_force_plan
ms.assetid: 0068f258-b998-4e4e-b47b-e375157c8213
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 14bf8a5f4e8ca74a7419c62200f87bc7fb4ce052
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97427354"
---
# <a name="sp_query_store_force_plan-transact-sql"></a>sp_query_store_force_plan (Transact-sql)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

특정 쿼리에 대해 특정 계획을 강제로 적용할 수 있습니다.  
  
 특정 쿼리에 대해 계획을 강제 적용 하는 경우 쿼리를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 발견할 때마다 쿼리 최적화 프로그램에서 계획을 강제로 적용 하려고 시도 합니다. 계획 강제 적용에 실패 하는 경우 확장 이벤트가 발생 하 고 쿼리 최적화 프로그램은 일반적인 방식으로 최적화 하도록 지시 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_query_store_force_plan [ @query_id = ] query_id , [ @plan_id = ] plan_id [;]  
```  
  
## <a name="arguments"></a>인수  
`[ @query_id = ] query_id` 쿼리 id입니다. *query_id* 는 **bigint** 이며 기본값은 없습니다.  
  
`[ @plan_id = ] plan_id` 강제 적용할 쿼리 계획의 id입니다. *plan_id* 는 **bigint** 이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대 한 **ALTER** 권한이 필요 합니다.
  
## <a name="examples"></a>예  
 다음 예에서는 쿼리 저장소의 쿼리에 대 한 정보를 반환 합니다.  
  
```sql  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
  
 Query_id를 확인 하 고 강제로 적용 하려는 plan_id 다음 예를 사용 하 여 쿼리에서 계획을 사용 하도록 강제 합니다.  
  
```sql  
EXEC sp_query_store_force_plan 3, 3;  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_query_store_remove_plan &#40;Transct-sql&-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [Transact-sql&#41;sp_query_store_remove_query &#40;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [Transact-sql&#41;sp_query_store_unforce_plan &#40;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [Transact-sql&#41;&#40;카탈로그 뷰 쿼리 저장소 ](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [쿼리 저장소를 사용 하 여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Transact-sql&#41;sp_query_store_reset_exec_stats &#40;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [Transact-sql&#41;sp_query_store_flush_db &#40;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)       
 [쿼리 저장소에 대한 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md#CheckForced)    
  
  
