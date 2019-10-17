---
title: SET RESULT_SET_CACHING(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 095680b9ff4fcfd58c1d655acaba7e07f70fcffb
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251993"
---
# <a name="set-result-set-caching-transact-sql"></a>SET RESULT SET CACHING (Transact-SQL) 

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

현재 클라이언트 세션에 대한 결과 집합 동작을 제어합니다.  

적용 대상: Azure SQL Data Warehouse(미리 보기)
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문

```
SET RESULT_SET_CACHING { ON | OFF };
```  
  
## <a name="remarks"></a>Remarks  

result_set_caching 설정을 구성하려는 사용자 데이터베이스에 연결된 상태에서 이 명령을 실행합니다.

**ON**   
현재 클라이언트 세션에 대한 결과 집합 캐싱을 설정합니다.  데이터베이스 수준에서 결과 집합 캐싱이 OFF인 경우 세션에서 ON으로 설정할 수 없습니다.

**OFF**   
현재 클라이언트 세션에 대한 결과 집합 캐싱을 사용하지 않도록 설정합니다.

## <a name="examples"></a>예

쿼리의 request_id로 [sys.dm_pdw_exec_requests](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql)의 result_cache_hit 열을 쿼리하여 이 쿼리가 결과 캐시 적중 또는 결과 캐시 누락 중 어떤 상태로 실행되었는지 확인합니다.

```sql
SELECT result_cache_hit
FROM sys.dm_pdw_exec_requests
WHERE request_id = 'QID58286'
```

## <a name="permissions"></a>사용 권한

public 역할의 멤버 자격이 필요

## <a name="see-also"></a>관련 항목:

[ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-showresultcachespaceused-transact-sql)</br>
[DBCC DROPRESULTSETCACHE (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)