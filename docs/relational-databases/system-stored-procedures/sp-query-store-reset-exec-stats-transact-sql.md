---
title: sp_query_store_reset_exec_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_query_store_reset_exec_stats_TSQL
- sys.sp_query_store_reset_exec_stats_TSQL
- sys.sp_query_store_reset_exec_stats
- sp_query_store_reset_exec_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_query_store_reset_exec_stats
- sys.sp_query_store_reset_exec_stats
ms.assetid: 899df1ff-e871-44df-9361-f3b87ac3ea31
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5ab75a58c9e6181a06849e67f7a63417a2b58e89
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58525995"
---
# <a name="spquerystoreresetexecstats-transact-sql"></a>sp_query_store_reset_exec_stats (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  쿼리 저장소에서 특정 쿼리 계획에 대 한 런타임 통계를 지웁니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_query_store_reset_exec_stats [ @plan_id = ] plan_id [;]  
```  
  
## <a name="arguments"></a>인수  
`[ @plan_id = ] plan_id` 지워지는 쿼리 계획의 id가입니다. *plan_id* 되는 **bigint**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
  
## <a name="permissions"></a>사용 권한  
 필요 합니다 **EXECUTE** 데이터베이스에 대 한 권한 및 **삭제** 의 쿼리 저장소 카탈로그 뷰 사용 권한.  
  
## <a name="examples"></a>예  
 다음 예제에서는 쿼리 저장소에서 쿼리에 대 한 정보를 반환합니다.  
  
```  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
  
 통계의 선택을 취소 하려는 plan_id를 확인 한 후 특정 쿼리 계획에 대 한 실행 통계를 삭제 하려면 다음 예제를 사용 합니다. 계획 번호 3에 대 한 실행 통계를 삭제 하는이 예제입니다.  
  
```  
EXEC sp_query_store_reset_exec_stats 3;  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_query_store_force_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
 [sp_query_store_remove_query &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [sp_query_store_unforce_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [sp_query_store_remove_plan &#40;TRANSCT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [sp_query_store_flush_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)   
 [쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  
