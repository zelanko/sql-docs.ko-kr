---
title: sp_query_store_force_plan (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f479710b8916fae3b315981663f97bac8488fb19
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38036121"
---
# <a name="spquerystoreforceplan-transact-sql"></a>sp_query_store_force_plan (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  특정 쿼리에 대해 특정 계획을 강제로 적용 하는 데 사용 하도록 설정 합니다.  
  
 경우 계획을 강제 적용에서 특정 쿼리에 대해 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리를 발견 하면 최적화 프로그램의 계획 강제 적용 하려고 합니다. 계획 강제 적용 실패 하면 한 XEvent 발생 하 고 최적화 프로그램은 일반적인 방법으로 최적화 하도록 지시 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_query_store_force_plan [ @query_id = ] query_id , [ @plan_id = ] plan_id [;]  
```  
  
## <a name="arguments"></a>인수  
 [  **@query_id =** ] *query_id*  
 쿼리의 id가입니다. *query_id* 되는 **bigint**, 기본값은 없습니다.  
  
 [  **@plan_id =** ] *plan_id*  
 강제 실행 해야 하는 쿼리 계획의 id가입니다. *plan_id* 되는 **bigint**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
  
## <a name="permissions"></a>사용 권한  
 필요 합니다 **EXECUTE** 데이터베이스에 대 한 권한 및 **삽입**, **업데이트**, 및 **삭제** 쿼리 저장소 카탈로그에 대 한 권한 레이아웃.  
  
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
  
 Query_id 및 강제 적용 하려는 plan_id를 확인 한 후 쿼리 계획을 사용 하도록 강제 하려면 다음 예제를 사용 합니다.  
  
```  
EXEC sp_query_store_force_plan 3, 3;  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_query_store_remove_plan &#40;TRANSCT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [sp_query_store_remove_query &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [sp_query_store_unforce_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [sp_query_store_reset_exec_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [sp_query_store_flush_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)  
  
  
