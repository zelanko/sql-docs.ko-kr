---
title: sys.dm_exec_query_statistics_xml (TRANSACT-SQL) | Microsoft Docs
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
ms.openlocfilehash: 06091ffc26ea036a4a0bd7e30196545bcaca60d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936943"
---
# <a name="sysdmexecquerystatisticsxml-transact-sql"></a>sys.dm_exec_query_statistics_xml (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

반환 진행 중인 요청에 대 한 실행 계획을 쿼리 합니다. 이 DMV를 사용 하 여 실행 계획 XML 임시 통계를 사용 하 여 검색 합니다. 

## <a name="syntax"></a>구문

```
sys.dm_exec_query_statistics_xml(session_id)  
``` 

## <a name="arguments"></a>인수 
*session_id*  
 세션 id가 조회 일괄 처리를 실행 합니다. *session_id* 됩니다 **smallint**합니다. *session_id* 다음 동적 관리 개체에서 가져올 수 있습니다.  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  

## <a name="table-returned"></a>반환된 테이블

|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|세션의 ID입니다. Null을 허용하지 않습니다.|
|request_id|**int**|요청의 ID입니다. Null을 허용하지 않습니다.|
|sql_handle|**varbinary(64)**|일괄 처리를 고유 하 게 식별 하는 토큰 또는 쿼리가 포함 된 저장된 프로시저입니다. Null을 허용합니다.|
|plan_handle|**varbinary(64)**|현재 실행 중인 일괄 처리에 대 한 쿼리 실행 계획을 고유 하 게 식별 하는 토큰이입니다. Null을 허용합니다.|
|query_plan|**xml**|런타임 실행 계획 표현을 사용 하 여 지정 된 쿼리 실행 계획 포함 *plan_handle* 부분 통계를 포함 합니다. 실행 계획은 XML 형식입니다. 임시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 저장 프로시저 호출, 사용자 정의 함수 호출 등이 포함된 각 일괄 처리에 대해 계획 하나가 생성됩니다. Null을 허용합니다.|

## <a name="remarks"></a>설명
이 시스템 함수는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1. 기술 자료를 참조 하세요. [3190871](https://support.microsoft.com/en-us/help/3190871)

이 시스템 함수 둘 다에서 작동 **표준** 하 고 **경량** 쿼리 실행 통계 인프라를 프로 파일링 합니다. 자세한 내용은 [쿼리 프로파일링 인프라](../../relational-databases/performance/query-profiling-infrastructure.md)를 참조하세요.  

다음과 같은 경우 실행 계획 출력이 반환 된 **query_plan** 에 대 한 반환된 된 테이블의 열 **sys.dm_exec_query_statistics_xml**:  
  
-   지정 된 쿼리 계획이 있는 경우 해당 *session_id* 더 이상 실행 되는 **query_plan** 반환된 된 테이블의 열은 null입니다. 계획 핸들을 캡처한 경우 사용 된 경우 사이의 시간 지연이 있는 경우이 상황이 발생할 수 있습니다 예를 들어 **sys.dm_exec_query_statistics_xml**합니다.  
    
에 허용 된 중첩된 수준 수가 제한으로 인해 합니다 **xml** 데이터 형식 **sys.dm_exec_query_statistics_xml** 중첩 요소의 128 수준을 충족 하거나 초과 하는 쿼리 계획을 반환할 수 없습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 상태로 인해 쿼리 계획을 반환하지 못했으므로 오류 6335가 발생합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 서비스 팩 2 및 이후 버전에서는 합니다 **query_plan** 열 NULL을 반환 합니다.   

## <a name="permissions"></a>사용 권한  
 서버에 대한 `VIEW SERVER STATE` 권한이 필요합니다.  

## <a name="examples"></a>예  
  
### <a name="a-looking-at-live-query-plan-and-execution-statistics-for-a-running-batch"></a>A. 실행 중인 일괄 처리에 대 한 활성 쿼리 계획 및 실행 통계를 살펴보면  
 다음 예제에서는 쿼리 **sys.dm_exec_requests** 흥미로운 쿼리 및 복사를 찾으려면 해당 `session_id` 출력에서 합니다.  
  
```sql  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 활성 쿼리 계획 및 실행 통계를 얻으려면 사용 하 여 복사한 `session_id` 시스템 함수를 사용 하 여 **sys.dm_exec_query_statistics_xml**합니다.  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_query_statistics_xml(< copied session_id >);  
GO  
```   

 또는 실행 중인 모든 요청에 대 한 결합 합니다.  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_requests
CROSS APPLY sys.dm_exec_query_statistics_xml(session_id);  
GO  
```   
  
## <a name="see-also"></a>관련 항목
  [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

