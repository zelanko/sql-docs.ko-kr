---
title: DBCC FREEPROCCACHE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FREEPROCCACHE_TSQL
- FREEPROCCACHE
- DBCC_FREEPROCCACHE_TSQL
- DBCC FREEPROCCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- freeing procedure cache
- removing procedure cache elements
- deleting procedure cache elements
- DBCC FREEPROCCACHE statement
- procedure cache [SQL Server]
- clearing procedure cache
ms.assetid: 0e09d210-6f23-4129-aedb-3d56b2980683
caps.latest.revision: 61
author: uc-msft
ms.author: umajay
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a6d9b899fa1bfd606b30c1759da3cb1052643d7b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33262976"
---
# <a name="dbcc-freeproccache-transact-sql"></a>DBCC FREEPROCCACHE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

계획 캐시에서 모든 요소를 제거하거나, 계획 핸들이나 SQL 핸들을 지정하여 계획 캐시에서 특정 계획을 제거하거나, 지정한 리소스 풀에 연결된 모든 캐시 항목을 제거합니다.

>[!NOTE]
>DBCC FREEPROCCACHE는 고유하게 컴파일된 저장 프로시저에 대한 실행 통계를 지우지 않습니다. 프로시저 캐시는 고유하게 컴파일된 저장 프로시저에 대한 정보를 포함하지 않습니다. 프로시저 실행에서 수집된 모든 실행 통계는 실행 통계 DMV([sys.dm_exec_procedure_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) 및 [sys.dm_exec_query_plan&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md))에 표시됩니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
SQL Server용 구문:

```sql
DBCC FREEPROCCACHE [ ( { plan_handle | sql_handle | pool_name } ) ] [ WITH NO_INFOMSGS ]  
```  

Azure SQL Data Warehouse 및 병렬 데이터 웨어하우스용 구문:
  
```sql
DBCC FREEPROCCACHE [ ( COMPUTE | ALL ) ] 
     [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>인수  
 ( { *plan_handle* | *sql_handle* | *pool_name* } )  
*plan_handle*은 실행된 일괄 처리에 대한 쿼리 계획을 고유하게 식별하며, 해당 계획은 계획 캐시에 있습니다. *plan_handle*은 **varbinary(64)** 이며, 다음 동적 관리 개체에서 가져올 수 있습니다.  
 -   [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
 -   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
 -   [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
 -   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  

*sql_handle*은 지우려는 일괄 처리의 SQL 핸들입니다. *sql_handle*은 **varbinary(64)** 이며, 다음 동적 관리 개체에서 가져올 수 있습니다.  
 -   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
 -   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
 -   [sys.dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)  
 -   [sys.dm_exec_xml_handles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)  
 -   [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  

*pool_name*은 Resource Governor 리소스 풀의 이름입니다. *pool_name*은 **sysname**이며, [sys.dm_resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md) 동적 관리 뷰를 쿼리하여 가져올 수 있습니다.  
 Resource Governor 작업 그룹을 리소스 풀에 연결하려면 [sys.dm_resource_governor_workload_groups](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md) 동적 관리 뷰를 쿼리합니다. 세션의 작업 그룹에 대한 자세한 내용은 [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) 동적 관리 뷰를 쿼리하세요.  

  
 WITH NO_INFOMSGS  
 모든 정보 메시지를 표시하지 않습니다.  
  
 COMPUTE  
 각 계산 노드에서 쿼리 계획 캐시를 제거합니다. 이것은 기본값입니다.  
  
 ALL  
 각 계산 노드와 제어 노드에서 쿼리 계획 캐시를 제거합니다.  

> [!NOTE]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE`를 사용하여 범위에 있는 데이터베이스의 프로시저(계획) 캐시를 지웁니다.

## <a name="remarks"></a>Remarks  
계획 캐시를 신중하게 지우려면 DBCC FREEPROCCACHE를 사용합니다. 프로시저(계획) 캐시를 지우면 모든 계획이 제거되고, 이전에 캐시된 계획을 다시 사용하지 않고 들어오는 쿼리를 실행하면 새 계획이 컴파일됩니다. 

이로 인해 새 컴파일 횟수가 증가함에 따라 쿼리 성능이 갑자기 일시적으로 저하될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 "'DBCC FREEPROCCACHE' 또는 'DBCC FREESYSTEMCACHE' 작업으로 인해 '%s' 캐시스토어(계획 캐시의 일부)에 대한 캐시스토어 플러시가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 %d번 발견되었습니다"라는 계획 캐시의 삭제된 각 캐시스토어에 대한 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.

다음과 같은 다시 구성 작업은 프로시저 캐시도 지웁니다.
-   access check cache bucket count  
-   access check cache quota  
-   clr enabled  
-   cost threshold for parallelism  
-   cross db ownership chaining  
-   index create memory  
-   max degree of parallelism  
-   max server memory  
-   max text repl size  
-   max worker threads  
-   min memory per query  
-   min server memory  
-   query governor cost limit  
-   query wait  
-   remote query timeout  
-   user options  
  
## <a name="result-sets"></a>결과 집합  
WITH NO_INFOMSGS 절이 지정되지 않으면 DBCC FREEPROCCACHE에서 "DBCC 실행이 완료되었습니다. DBCC에서 오류 메시지를 출력하면 시스템 관리자에게 문의하세요."
  
## <a name="permissions"></a>사용 권한  
적용 대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 
- 서버에 대한 ALTER SERVER STATE 권한이 필요합니다.  

적용 대상: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
- DB_OWNER 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  

## <a name="general-remarks-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 대한 일반적인 주의 사항  
여러 DBCC FREEPROCCACHE 명령을 동시에 실행할 수 있습니다.
[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 계획 캐시를 지우면 들어오는 쿼리에서 이전에 캐시된 계획을 다시 사용하지 않고 새 계획을 컴파일하므로 쿼리 성능이 일시적으로 저하될 수 있습니다. 

DBCC FREEPROCCACHE (COMPUTE)만 사용하면 계산 노드에서 쿼리를 실행할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 해당 쿼리를 다시 컴파일합니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서는 제어 노드에 생성된 병렬 쿼리 계획을 다시 컴파일하지 않습니다.
DBCC FREEPROCCACHE는 실행 중에 취소할 수 있습니다.
  
## <a name="limitations-and-restrictions-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 대한 제한 사항  
DBCC FREEPROCCACHE는 트랜잭션 내에서 실행할 수 없습니다.
DBCC FREEPROCCAHCE는 EXPLAIN 문에서 지원되지 않습니다.
  
## <a name="metadata-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 대한 메타데이터  
DBCC FREEPROCCACHE가 실행되면 새 행이 sys.pdw_exec_requests 시스템 뷰에 추가됩니다.

## <a name="examples-includessnoversionincludesssnoversion-mdmd"></a>예제: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]   
  
### <a name="a-clearing-a-query-plan-from-the-plan-cache"></a>1. 계획 캐시에서 쿼리 계획 만들기  
다음 예에서는 쿼리 계획 핸들을 지정하여 계획 캐시에서 계획 지침을 삭제합니다. 예제 쿼리가 계획 캐시에 놓이도록 쿼리가 먼저 실행됩니다. `sys.dm_exec_cached_plans` 및 `sys.dm_exec_sql_text` 동적 관리 뷰를 쿼리하여 쿼리에 대한 계획 핸들을 반환합니다. 

그러면 계획 캐시에서 해당 계획만 제거하도록 결과 집합의 계획 핸들 값이 `DBCC FREEPROCACHE` 문에 삽입됩니다.
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT * FROM Person.Address;  
GO  
SELECT plan_handle, st.text  
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st  
WHERE text LIKE N'SELECT * FROM Person.Address%';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
plan_handle                                         text  
--------------------------------------------------  -----------------------------  
0x060006001ECA270EC0215D05000000000000000000000000  SELECT * FROM Person.Address;  
  
(1 row(s) affected)
 ```
 
```sql  
-- Remove the specific plan from the cache.  
DBCC FREEPROCCACHE (0x060006001ECA270EC0215D05000000000000000000000000);  
GO  
```  
  
### <a name="b-clearing-all-plans-from-the-plan-cache"></a>2. 계획 캐시에서 모든 계획 삭제  
다음 예에서는 계획 캐시에서 모든 요소를 삭제합니다. WITH `NO_INFOMSGS`절은 정보 메시지가 표시되지 않도록 지정됩니다.
  
```sql  
DBCC FREEPROCCACHE WITH NO_INFOMSGS;  
```  
  
### <a name="c-clearing-all-cache-entries-associated-with-a-resource-pool"></a>3. 리소스 풀에 연결된 모든 캐시 항목 지우기  
다음 예에서는 지정된 리소스 풀에 연결된 모든 캐시 항목을 지웁니다. `sys.dm_resource_governor_resource_pools` 뷰를 먼저 쿼리하여 *pool_name* 값을 가져옵니다.
  
```sql  
SELECT * FROM sys.dm_resource_governor_resource_pools;  
GO  
DBCC FREEPROCCACHE ('default');  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-dbcc-freeproccache-basic-syntax-examples"></a>4. DBCC FREEPROCCACHE 기본 구문 예제  
다음 예제에서는 계산 노드에서 기존 쿼리 계획 캐시를 모두 제거합니다. 컨텍스트가 UserDbSales로 설정되어 있지만 모든 데이터베이스에 대한 계산 노드 쿼리 계획 캐시가 제거됩니다. WITH NO_INFOMSGS 절은 정보 메시지가 결과에 표시되지 않도록 합니다.  
  
```sql
USE UserDbSales;  
DBCC FREEPROCCACHE (COMPUTE) WITH NO_INFOMSGS;
```  
  
 다음 예제에서는 정보 메시지가 결과에 표시된다는 점을 제외하고 이전 예제와 동일한 결과를 보여 줍니다.  
  
```sql
USE UserDbSales;  
DBCC FREEPROCCACHE (COMPUTE);  
```  
  
정보 메시지가 요청되고 실행이 성공하면 쿼리 결과에는 계산 노드당 한 줄씩 표시됩니다.
  
### <a name="e-granting-permission-to-run-dbcc-freeproccache"></a>5. DBCC FREEPROCCACHE 실행 권한 부여  
다음 예제에서는 DBCC FREEPROCCACHE를 실행할 수 있는 David 로그인 권한을 제공합니다.  
  
```sql
GRANT ALTER SERVER STATE TO David; 
GO
```  
  
## <a name="see-also"></a>참고 항목  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)  
[데이터베이스 범위 구성 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
  
  
