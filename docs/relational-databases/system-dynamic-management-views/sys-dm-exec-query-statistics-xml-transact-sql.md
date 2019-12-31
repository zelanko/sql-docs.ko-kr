---
title: sys. dm_exec_query_statistics_xml (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_statistics_xml
- sys.dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml
helpviewer_keywords:
- sys.dm_exec_query_statistics_xml management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfecb
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 35f9cdfcc40d417a6aed19a3abe0e590061b2eb7
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75256010"
---
# <a name="sysdm_exec_query_statistics_xml-transact-sql"></a>sys. dm_exec_query_statistics_xml (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

진행 중인 요청에 대 한 쿼리 실행 계획을 반환 합니다. 이 DMV를 사용 하 여 임시 통계를 사용 하 여 실행 계획 XML을 검색 합니다. 

## <a name="syntax"></a>구문

```
sys.dm_exec_query_statistics_xml(session_id)  
``` 

## <a name="arguments"></a>인수 
*session_id*  
 조회할 일괄 처리를 실행 하는 세션 id입니다. *session_id* 은 **smallint**입니다. *session_id* 는 다음과 같은 동적 관리 개체에서 가져올 수 있습니다.  
  
-   [sys. dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys. dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys. dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  

## <a name="table-returned"></a>반환된 테이블

|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|세션의 ID입니다. Null을 허용하지 않습니다.|
|request_id|**int**|요청의 ID입니다. Null을 허용하지 않습니다.|
|sql_handle|**varbinary (64)**|쿼리가 속하는 일괄 처리 또는 저장 프로시저를 고유 하 게 식별 하는 토큰입니다. Null을 허용합니다.|
|plan_handle|**varbinary (64)**|현재 실행 중인 일괄 처리에 대 한 쿼리 실행 계획을 고유 하 게 식별 하는 토큰입니다. Null을 허용합니다.|
|query_plan|**Xml**|부분 통계를 포함 하 *plan_handle* 로 지정 된 쿼리 실행 계획의 런타임 실행 계획 표현을 포함 합니다. 실행 계획은 XML 형식입니다. 임시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 저장 프로시저 호출, 사용자 정의 함수 호출 등이 포함된 각 일괄 처리에 대해 계획 하나가 생성됩니다. Null을 허용합니다.|

## <a name="remarks"></a>설명
이 시스템 함수는 s p 1 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 사용할 수 있습니다. KB [3190871](https://support.microsoft.com/help/3190871) 을 참조 하세요.

이 시스템 함수는 **표준** 및 **경량** 쿼리 실행 통계 프로 파일링 인프라에서 작동 합니다. 자세한 내용은 [쿼리 프로 파일링 인프라](../../relational-databases/performance/query-profiling-infrastructure.md)를 참조 하세요.  

다음 조건에서는 **sys. dm_exec_query_statistics_xml**에 대해 반환 된 테이블의 **query_plan** 열에 실행 계획 출력이 반환 되지 않습니다.  
  
-   지정 된 *session_id* 에 해당 하는 쿼리 계획이 더 이상 실행 되지 않는 경우 반환 된 테이블의 **query_plan** 열은 null입니다. 예를 들어 계획 핸들이 캡처 된 시간과 **sys. dm_exec_query_statistics_xml**와 함께 사용 될 때 사이에 지연이 있는 경우이 문제가 발생할 수 있습니다.  
    
**Xml** 데이터 형식에서 허용 되는 중첩 수준 수의 제한으로 인해 **dm_exec_query_statistics_xml** 는 128 수준의 중첩 된 요소를 충족 하거나 초과 하는 쿼리 계획을 반환할 수 없습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 상태로 인해 쿼리 계획을 반환하지 못했으므로 오류 6335가 발생합니다. 서비스 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 팩 2 이상 버전에서 **QUERY_PLAN** 열은 NULL을 반환 합니다.   

## <a name="permissions"></a>권한  
 서버에 대한 `VIEW SERVER STATE` 권한이 필요합니다.  

## <a name="examples"></a>예  
  
### <a name="a-looking-at-live-query-plan-and-execution-statistics-for-a-running-batch"></a>A. 실행 중인 일괄 처리에 대 한 라이브 쿼리 계획 및 실행 통계 보기  
 다음 예에서는 **dm_exec_requests** 를 쿼리하여 흥미로운 쿼리를 찾고 출력에서 해당 `session_id` 쿼리를 복사 합니다.  
  
```sql  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 그런 다음 라이브 쿼리 계획 및 실행 통계를 얻으려면 시스템 함수 `session_id` **sys. dm_exec_query_statistics_xml**로 복사 된를 사용 합니다.  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_query_statistics_xml(< copied session_id >);  
GO  
```   

 또는 모든 실행 중인 요청에 대해 결합 된 것입니다.  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_requests
CROSS APPLY sys.dm_exec_query_statistics_xml(session_id);  
GO  
```   
  
## <a name="see-also"></a>참고 항목
  [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

