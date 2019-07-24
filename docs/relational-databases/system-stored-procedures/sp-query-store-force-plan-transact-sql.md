---
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
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 07d2e8032bb596faaac577194273760c59006645
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68418857"
---
# <a name="spquerystoreforceplan-transact-sql"></a>sp_query_store_force_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  특정 쿼리에 대해 특정 계획을 강제로 적용할 수 있습니다.  
  
 특정 쿼리에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대해 계획을 강제 적용 하는 경우 쿼리를 발견할 때마다 최적화 프로그램에서 계획을 강제로 적용 하려고 시도 합니다. 계획 강제 적용에 실패 하는 경우 XEvent가 실행 되 고 최적화 프로그램이 일반적인 방법으로 최적화 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_query_store_force_plan [ @query_id = ] query_id , [ @plan_id = ] plan_id [;]  
```  
  
## <a name="arguments"></a>인수  
`[ @query_id = ] query_id`쿼리 id입니다. *query_id* 는 **bigint**이며 기본값은 없습니다.  
  
`[ @plan_id = ] plan_id`강제 적용할 쿼리 계획의 id입니다. *plan_id* 는 **bigint**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대 한 **ALTER** 권한이 필요 합니다.
  
## <a name="examples"></a>예  
 다음 예에서는 쿼리 저장소의 쿼리에 대 한 정보를 반환 합니다.  
  
```  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
  
 강제로 적용 하려는 query_id 및 plan_id를 확인 한 후 다음 예를 사용 하 여 쿼리에서 계획을 사용 하도록 강제 합니다.  
  
```  
EXEC sp_query_store_force_plan 3, 3;  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_query_store_remove_plan &#40;TRANSCT-SQL&AMP;-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [sp_query_store_remove_query &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [sp_query_store_unforce_plan &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [sp_query_store_reset_exec_stats &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [sp_query_store_flush_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)  
  
  
