---
description: sp_query_store_reset_exec_stats (Transact-sql)
title: sp_query_store_reset_exec_stats (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fcfdd367937cb00d98ed79edf6758b74c96ad330
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547875"
---
# <a name="sp_query_store_reset_exec_stats-transact-sql"></a>sp_query_store_reset_exec_stats (Transact-sql)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  쿼리 저장소에서 특정 쿼리 계획에 대 한 런타임 통계를 지웁니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_query_store_reset_exec_stats [ @plan_id = ] plan_id [;]  
```  
  
## <a name="arguments"></a>인수  
`[ @plan_id = ] plan_id` 지워지는 쿼리 계획의 id입니다. *plan_id* 는 **bigint**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대 한 **ALTER** 권한이 필요 합니다. 
  
## <a name="examples"></a>예제  
 다음 예에서는 쿼리 저장소의 쿼리에 대 한 정보를 반환 합니다.  
  
```  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
  
 통계를 지울 plan_id를 확인 한 후 다음 예를 사용 하 여 특정 쿼리 계획에 대 한 실행 통계를 삭제 합니다. 이 예에서는 계획 번호 3에 대 한 실행 통계를 삭제 합니다.  
  
```  
EXEC sp_query_store_reset_exec_stats 3;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_query_store_force_plan &#40;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
 [Transact-sql&#41;sp_query_store_remove_query &#40;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [Transact-sql&#41;sp_query_store_unforce_plan &#40;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [sp_query_store_remove_plan &#40;Transct-sql&-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [Transact-sql&#41;sp_query_store_flush_db &#40;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)   
 [Transact-sql&#41;&#40;카탈로그 뷰 쿼리 저장소 ](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  
