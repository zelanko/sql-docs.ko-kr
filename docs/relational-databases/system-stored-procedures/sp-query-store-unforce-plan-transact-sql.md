---
title: sp_query_store_unforce_plan (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SP_QUERY_STORE_UNFORCE_PLAN_TSQL
- SP_QUERY_STORE_UNFORCE_PLAN
- SYS.SP_QUERY_STORE_UNFORCE_PLAN
- SYS.SP_QUERY_STORE_UNFORCE_PLAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_query_store_unforce_plan
- sp_query_store_unforce_plan
ms.assetid: a52f91d0-ff1e-46ad-ba36-b32d9623c9ab
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9cff3bb0491db53e195a692014b74a08c4fdcdee
ms.sourcegitcommit: 816ff47eeab157c66e0f75f18897a63dc8033502
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71207713"
---
# <a name="sp_query_store_unforce_plan-transact-sql"></a>sp_query_store_unforce_plan (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  특정 쿼리에 대해 이전에 강제 적용 된 계획을 강제 적용할 수 없습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_query_store_unforce_plan [ @query_id = ] query_id , [ @plan_id = ] plan_id [;]  
```  
  
## <a name="arguments"></a>인수  
`[ @query_id = ] query_id`는 쿼리 id입니다. *query_id* 는 **bigint**이며 기본값은 없습니다.  
  
`[ @plan_id = ] plan_id`는 더 이상 적용 되지 않을 쿼리 계획의 id입니다. *plan_id* 는 **bigint**이며 기본값은 없습니다.  
  
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
  
 Query_id를 확인 하 고 적용 하지 않으려는 plan_id 다음 예를 사용 하 여 계획을 강제로 해제 합니다.  
  
```sql  
EXEC sp_query_store_unforce_plan 3, 3;  
```  
  
## <a name="see-also"></a>참고 항목  
 [ &#40;transact-sql&#41;  sp_query_store_force_plan](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)  
 [sp_query_store_remove_plan &#40;transct-sql&-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [ &#40;transact-sql&#41;  sp_query_store_remove_query](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)  
 [ &#40;transact-sql&#41;  sp_query_store_reset_exec_stats](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)  
 [ &#40;transact-sql&#41;  sp_query_store_flush_db](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)  
 [쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [쿼리 저장소   를 사용 하 여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [쿼리 저장소에 대한 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md#CheckForced)     
  
