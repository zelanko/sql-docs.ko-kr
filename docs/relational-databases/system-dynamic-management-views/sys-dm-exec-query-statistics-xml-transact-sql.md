---
title: sys.dm_exec_query_statistics_xml (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 8bb66c5bb9b4f69b32efd7761ae08677ee243fee
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044629"
---
# <a name="sysdmexecquerystatisticsxml-transact-sql"></a>sys.dm_exec_query_statistics_xml (Transact-SQL)
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

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|세션의 ID입니다. Null을 허용하지 않습니다.|
|request_id|**int**|요청의 ID입니다. Null을 허용하지 않습니다.|
|sql_handle|**varbinary(64)**|요청의 SQL 텍스트의 해시 맵입니다. Null을 허용합니다.|
|plan_handle|**varbinary(64)**|쿼리 계획의 해시 맵입니다. Null을 허용합니다.|
|query_plan|**xml**|일부 통계를 사용 하 여 Showplan XML입니다. Null을 허용합니다.|

## <a name="remarks"></a>Remarks
이 시스템 함수는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1. 기술 자료를 참조 하세요. [3190871](https://support.microsoft.com/en-us/help/3190871)

이 시스템 함수 둘 다에서 작동 **표준** 하 고 **경량** 쿼리 실행 통계 인프라를 프로 파일링 합니다.  
  
**표준** 인프라를 프로 파일링 통계를 사용 하 여 사용할 수 있습니다.
  -  [SET STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md)
  -  [SET STATISTICS PROFILE](../../t-sql/statements/set-statistics-profile-transact-sql.md)
  -  `query_post_execution_showplan` 확장된 이벤트입니다.  
  
**경량** 에서 사용할 수 있는 통계 인프라를 프로 파일링은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 사용 하도록 설정할 수 있습니다.
  -  전역적으로 추적을 사용 하 여 플래그 7412입니다.
  -  사용 하 여 [ *query_thread_profile* ](https://support.microsoft.com/kb/3170113) 확장된 이벤트입니다.
  
> [!NOTE]
> 대신 표준 프로 파일링, DMV와 같은 인프라를 프로 파일링 하는 쿼리 실행 통계의 모든 소비자에 게 경량 프로 파일링 됩니다 사용 하 여 추적 플래그 7412 사용 하도록 설정 하면 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)합니다.
> 그러나 표준 프로 파일링가 여전히 사용 SET STATISTICS XML *실제 계획 포함* 에서 작업 [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)], 및 `query_post_execution_showplan` xEvent입니다.

> [!IMPORTANT]
> Tpc-c 워크 로드 테스트와 마찬가지로, 프로 파일링 경량 통계 인프라를 사용 하도록 설정 하면 1.5 ~ 2% 오버 헤드를 추가 합니다. 반면, 표준 통계 프로 파일링 인프라는 동일한 워크 로드 시나리오를 위한 오버 헤드가 최대 90%를 추가할 수 있습니다.

## <a name="permissions"></a>사용 권한  
 서버에 대한 `VIEW SERVER STATE` 권한이 필요합니다.  

## <a name="examples"></a>예  
  
### <a name="a-looking-at-live-query-plan-and-execution-statistics-for-a-running-batch"></a>1. 실행 중인 일괄 처리에 대 한 활성 쿼리 계획 및 실행 통계를 살펴보면  
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

