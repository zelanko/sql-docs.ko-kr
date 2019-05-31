---
title: SET RESULT SET CACHING  (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 0b932c1fa3aa8575f8f12ef5f164841788f74c1a
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65948750"
---
# <a name="set-result-set-caching-transact-sql"></a>SET RESULT SET CACHING (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Azure SQL Data Warehouse가 쿼리 결과 집합을 캐시하도록 합니다.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문

```
SET RESULT_SET_CACHING { ON | OFF };
```  
  
## <a name="remarks"></a>Remarks  

> [!Note]
> 이 기능이 모든 지역에 롤아웃되는 동안 인스턴스에 배포된 버전과 최신 [Azure SQL DW 릴리스 정보](/azure/sql-data-warehouse/release-notes-10-0-10106-0)에서 기능 가용성을 확인합니다.
  
이 명령은 master 데이터베이스에 연결되어 있는 동안 실행되어야 합니다.  이 데이터베이스 설정 변경이 즉시 적용됩니다.  쿼리 집합 캐싱으로 스토리지 비용이 발생합니다. 데이터베이스의 결과 캐싱을 사용하지 않도록 설정하면 영구 결과 캐시가 즉시 Microsoft Azure SQL Data Warehouse 스토리지에서 삭제됩니다. 데이터베이스의 결과 캐싱을 표시하기 위해 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql?view=azure-sqldw-latest)에 새 called is_result_set_caching_on 열이 추가되었습니다.  

**ON**은 이 데이터베이스에서 반환된 쿼리 결과 집합이 Azure SQL Data Warehouse 스토리지에서 캐시되도록 지정합니다.

**OFF**은 이 데이터베이스에서 반환된 쿼리 결과 집합이 Azure SQL Data Warehouse 스토리지에서 캐시되지 않도록 지정합니다.

사용자는 specific request_id로 [sys.pdw_request_steps](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql?view=azure-sqldw-latest)를 쿼리하여 결과 캐시 적중 또는 누락을 통해 쿼리가 실행되었는지 알 수 있습니다. 캐시가 적중된 경우 쿼리 결과에는 다음 세부 정보와 함께 단일 단계가 포함됩니다.

|**열 이름**|**같음**|**Value**|
|----|----|----|
|operation_type|=|ReturnOperation|
|step_index|=|0|
|location_type|=|Control|
|command|Like|%DWResultCacheDb%|
||||
  
## <a name="permissions"></a>사용 권한

다음과 같은 사용 권한이 필요합니다.

- 서버 수준 보안 주체 로그인(프로비저닝 프로세스에 의해 생성됨) 또는
- dbmanager 데이터베이스 역할의 구성원.

데이터베이스의 소유자가 dbmanager 역할의 구성원이 아니면 데이터베이스를 변경할 수 있습니다.
  
## <a name="examples"></a>예

### <a name="enable-result-set-caching-for-a-database"></a>데이터베이스의 결과 집합 캐싱 사용 설정

```sql
ALTER DATABASE myTestDW  
SET RESULT_SET_CACHING ON;
```

### <a name="disable-result-set-caching-for-a-database"></a>데이터베이스의 결과 집합 캐싱 사용 설정 안 함

```sql
ALTER DATABASE myTestDW  
SET RESULT_SET_CACHING OFF;
```

### <a name="check-result-set-caching-setting-for-a-database"></a>데이터베이스의 결과 집합 캐싱 설정 확인

```sql
SELECT name, is_result_set_caching  
FROM sys.databases
```

### <a name="check-for-number-of-queries-with-result-set-cache-hit-and-cache-miss"></a>결과 집합 캐시 적중 및 캐시 누락으로 쿼리 수 확인

```sql
SELECT  
Queries=CacheHits+CacheMisses,
CacheHits,
CacheMisses,
CacheHitPct=CacheHits*1.0/(CacheHits+CacheMisses)
FROM  
(SELECT  
CacheHits=count(distinct case when s.command like '%DWResultCacheDb%' and
r.resource_class IS NULL and s.operation_type = 'ReturnOperation' and  
s.step_index = 0 then s.request_id else null end) ,
CacheMisses=count(distinct case when r.resource_class IS NOT NULL then  
s.request_id else null end)
     FROM sys.dm_pdw_request_steps s  
     JOIN sys.dm_pdw_exec_requests r  
     ON s.request_id = r.request_id) A
```

### <a name="check-for-result-set-cache-hit-or-cache-miss-for-a-query"></a>쿼리의 결과 집합 캐시 적중 또는 캐시 누락 확인

```sql
If
(SELECT step_index  
FROM sys.dm_pdw_request_steps  
WHERE request_id = 'QID58286'
      and operation_type = 'ReturnOperation'
      and command like '%DWResultCacheDb%') = 0
SELECT 1 as is_cache_hit  
ELSE
SELECT 0 as is_cache_hit
```

### <a name="check-for-all-queries-with-result-set-cache-hits"></a>결과 집합 캐시 적중으로 모든 쿼리 확인

```sql
SELECT *  
FROM sys.dm_pdw_request_steps  
WHERE command like '%DWResultCacheDb%' and step_index = 0
```

## <a name="see-also"></a>참고 항목

[SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)</br>
[ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)